# Dockerfile
- [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/#shell)
## Dockerfile 문법
- '#'을 이용해서 주석으로 사용
- Dockerfile에서 지시어는 대문자로 구성
- WORKDIR ${Foo}
  - FOO는 환경변수
  - 호스트의 환경변수가 아닌 컨테이너 내에 정의된 환경변수
- ARG [변수값]
  - ARG를 통해 변수로 만들어 Dockerfile 내에서 사용이 가능
  - 정의 방식이 총 두 가지가 존재
  ```bash
  # key-value 형식으로 정의
  ARG user1=joosang

  # Dockerfile을 빌드하는 시점에 인자값으로 정의
  $ docker build --build-arg CONT_IMG_VER=v2.0.1
  ```
  ```bash
  # 동일한 값이 정의가 된 경우 ENV로 정의된 값이 ARG로 정의한 값을 덮어쓴다.
  ARG CONT_IMG_VER
  ENV CONT_IMG_VER=v1.0.0

  # user를 따로 넘겨주지 않으면 기본값이 -some_user 값을 사용
  USER ${user:-some_user}
  ```
```bash
FROM node:16      # 베이스 이미지 사용
LABEL maintance="FastCampus"      # 이미지의 메타데이터

WORKDIR /app      # Set Working Directory => cd와 같은 역할

COPY package*.jsom ./      # COPY SRC DEST로 정의
                           # SRC : 호스트 OS
                           # DEST : 이미지 상에서 경로

RUN npm install      # Dockerfile에서 실행할 명령어

COPY . .      # 현 디렉토리에서 모든 파일 복제
EXPOSE 8080      # Port Number
CMD [ "node", "server.js" ]
```

# 이미지 압축파일로 저장 및 불러오기
- 인터넷이 되지 않는 상황에서 사용할 수 있는 방법(폐쇄망)
## 이미지 압축파일로 저장
- 이미지를 tar 압축파일로 저장
```bash
# docker save -o [OUTPUT-FILE] IMAGE
# ubuntu:focal 이미지를 ubuntu_focal.tar 압축 파일로 저장
$ docker save -o ubuntu_focal.tar ubuntu:focal
```
## 이미지 압축에서 불러오기
- 이미지를 tar 압축파일로부터 불러옵니다.
```bash
# docker load -i [INPUT-FILE]
# ubuntu_focal.tar 압축 파일에서 ubuntu:focal 이미지 불러오기
$ docker load -i ubuntu_focal.tar
```
