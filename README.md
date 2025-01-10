# pinpoint-docker

# pinpoint 서버 실행

1. 우리팀 orga 레포에 pinpoint-docker 레포 있음 
   ( [pinpoint-docker GitHub Repository](https://github.com/pinpoint-apm/pinpoint-docker) 에서 다운 받아도 됨 )
```
git clone https://github.com/strong2team/pinpoint-docker.git
cd pinpoint-docker
```

2. docker-compopse 로 컨테이너들 실행
```
docker-compose up 
```
- 잘 실행되는지 로그 보기
```
docker-compose logs -f
```

3. 컨테이너들 정상 작동하면 pinpoint-web 접속 - localhost:9090

# pinpoint 에이전트 실행
- 우리팀 orga shoppingMall 프로젝트
feature/pinpoint 브랜치로 이동

```
cd shopingMall
```

1. build 
```
./gradlew clean build -Dspring.profiles.active=dev -x test
```
2. jar 파일 agent 실행에 필요한 값들로 실행

```
java -javaagent:$(pwd)/pinpoint-agent-2.5.4/pinpoint-bootstrap-2.5.4.jar \
     -Dpinpoint.agentId=my-agent \
     -Dpinpoint.applicationName=my-spring-boot-app \
     -Dprofiler.collector.ip=172.24.0.30 \
     -Dprofiler.collector.tcp.port=9994 \
     -Dprofiler.collector.stat.port=9995 \
     -Dprofiler.collector.span.port=9996 \
     -Dspring.data.redis.host=localhost \
     -Dspring.data.redis.port=6379 \
     -jar build/libs/timedeal-0.0.1-SNAPSHOT.jar --spring.profiles.active=dev

```