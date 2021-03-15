
```
docker run busybox echo "Hello LSW"
```
busybox 이미지가 없으면, 도커허브에서 pull을 받아서 이미지를 실행시키게 된다.


출처 ::  https://blog.naver.com/adamdoha/222243824999

#### 나의 docker 만들기
```
vi app.js
```

```
const http = require('http');
const os = require('os');

console.log("test server starting...");

var handler = function(req, res){
        console.log("Received request from "+ req.connection.remoteAddress);
        res.writeHead(200);
        res.end("You've hit "+ os.hostname() + "\n");
};

var www = http.createServer(handler);
www.listen(8080);
```

```
vi Dockerfile
```

```
FROM node:7
ADD app.js /app.js
ENTRYPOINT ["node", "app.js"]
```

#### docker 빌드
```
docker build -t test .
```

#### docker 확인
```
docker images
```

#### docker 실행
```
docker run --name test-container -p 8080:8080 -d test
```

#### docker 테스트
```
curl localhost:8080
```

#### 실행 중인 모든 컨테이너 조회
```
docker ps
```

#### 컨테이너에 대한 자세한 정보 얻기
```
docker inspect test-container
```

#### 실행 중인 컨테이너 내부 탐색하기
```
docker exec -it test-container bash
ps aux
ls
```


* 각 컨테이너는 격리된 파일 시스템을 가짐.
* 컨테이너는 고유의 프로세스 번호를 가지고, 완전히 분리된 프로세스 트리를 가짐.
* 컨테이너 내부에서는 호스트 운영체제에 있는 프로세스는 볼 수 없음.








