## 라즈베리파이 도커
라즈베리파이는 Arm 아키텍쳐이기 때문에 기존 PC에서 사용하던 도커 이미지가 돌아가지 않음

따라서 arm 전용 이미지를 구해서 돌려줘야함

## 도커 컨테이너 접속하기
`docker exec -it "컨테이너 이름" bash` - 컨테이너의 bash에 접속

## 리눅스에서 docker 위에 jenkins 올리기
jenkins 볼륨을 설정해주고 리눅스에서 docker-compose를 통해 젠킨스를 실행하면 실행이 안된다.

젠킨스 볼륨 권한이 문제가 되는데 docker-compose 실행하기 전에 미리 볼륨으로 사용할 폴더를 생성해주고 다음 명령어를 통해 권한을 주면 해결된다.
```bash
sudo chown 1000 [디렉터리 이름]
```

### docker.sock permission denied 에러
폴더 접근 권한이 없기 때문

다음 명령어를 통해 실행
```bash
sudo chmod 666 /var/run/docker.sock
```