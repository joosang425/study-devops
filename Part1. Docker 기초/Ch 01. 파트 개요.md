# Docker 기초
## 컨테이너 기술의 발전
![컨테이너_기술의_발전](https://github.com/joosang425/study-devops/assets/68217970/6d3aa45c-9e3b-45bc-80dc-af48df005bac)
- 전통적인 배포 운영 방식
  - Hardware 위에 Operating System(ex. 리눅스, 윈도우)를 두고 그 위에 Application을 둔 뒤 운영하는 방식
  - 이 운영 방식의 문제점은 추후에 다양한 서비스들이 추가가 되면 비용 효율성이 떨어진다.
- 가상 환경 배포 운영 방식
  - 전통적인 배포 운영 방식의 형태에서 가상 머신(Hypervisor)이 추가된 형태
  - 가상 머신이 호스트 운영체제 위에서 게스트 OS 구동 -> 물리적 자원을(ex. CPU, RAM 등)을 에뮬레이팅
    - 고유한 라이브러리와 프레임워크만 의존성을 가짐
    - 성능 효율성이 떨어지고 자원의 오버헤드가 증가될 수 있는 단점이 존재
- 컨테이너 배포 운영 방식
  - 전통적인 배포 운영 방식의 형태에서 docker가 추가된 형태
  - Host 운영체제를 사용하지만 공통 커널을 사용해서 격리가 된 것처럼 느껴진다.
    - Host 운영체제를 사용해서 가상 환경 배포 운영 방식의 단점을 줄인다.
- 쿠버네티스 배포 운영 방식
  - Container Orchestration System으로 현재 가장 널리 사용
  - 관리 소프트웨어, 여러 서버로 구성된 클러스터 환경에서 컨테이너를 효율적으로 관리하는 시스템
## Docker의 개념 및 핵심 설명
### Docker
![Docker](https://github.com/joosang425/study-devops/assets/68217970/2e60a3ff-890e-4773-b872-88f2f706551f)
- Go 언어로 작성된 리눅스 컨테이너 기반으로 하는 오픈소스 가상화 플랫폼
### Docker 설치
```bash
# docker repository에 접근하기 위한 키 생성 설정
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# 패키지 매니저가 docker 설치 시, 설치 위치를 알기 위한 repository 추가
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# 위에서 추가한 repository를 위해서 업데이트
$ sudo apt update

# docker 설치
$ sudo apt install docker-ce

# Active: active (running) 이 문구가 보이면 올바르게 설치된 것
$ sudo systemctl status docker
```
# docker-compose
## docker-compose를 쓰는 이유
- docker-compose는 컨테이너 여럿을 띄우는 도커 애플리케이션을 정의하고 실행하는 도구 (Tool for defining and running multi-container Docker applications) 이다.
- 컨테이너 실행에 필요한 옵션을 docker-compose.yml 이라는 파일에 적어둘 수 있고, 컨테이너 간 의존성도 관리할 수 있다.
## docker-compose 설치
```bash
# curl 명령어를 통해 docker-compose를 설치
$ sudo curl -L "https://github.com/docker/compose/releases/download/[설치할 docker-compose 버전]/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# 다운로드한 docker-compose 파일을 실행할 수 있도록 권한 부여
$ sudo chmod +x /usr/local/bin/docker-compose

# 정상적으로 설치되었는지 확인
$ docker-compose -v
```
### docker-compose 속성
- version
  - docker-compose의 파일 포맷 버전을 지정
- services
  - 서비스의 이름
- image
  - docker container의 이름을 정의
  - DockerHub에 있는 이미지를 사용하여 docker container를 작성할 경우 image를 설정할 수 있다.
- restart
  - docker container가 다운되었을 경우, 항상 재시작하라는 설정
- volumes
  - docker run 명령의 -v 옵션과 동일한 역할
- environment
  - Dockerfile의 ENV 옵션과 동일한 역할
- ports
  - docker run 명령의 -p 옵션과 동일한 역할
- build
  - docker image를 Dockerfile 기반으로 작성 시 사용
# kubectl
## kubectl 사용 목적
- kubectl은 kubernetes의 상태를 확인하고 원하는 상태를 요청하는 걸 주 목적으로 사용
- kubectl은 그 밖에도 컨테이너 로그 확인 및 원격 접속도 가능
## kubectl 명령어 
- apply : 원하는 상태 적용 -> 주로 -f 옵션과 함께 사용
- get : 리소스 리스트 조회
- describe : 리소스 상태 상세 조회
- delete : 리소스 제거
- logs : 컨테이너 로그 조회
- exec : 컨테이너에 명령어 전달 (주로 컨테이너 접근 시 사용)
- config : kubectl 설정 관리
