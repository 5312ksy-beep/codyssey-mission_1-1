# codyssey-mission_1-1
# Mission 1-1: 개발 워크스테이션 구축

## 작업 로그

# 🖥️ Mission 1-1: 개발 워크스테이션 구축

## 1. 프로젝트 개요

터미널, Docker, Git을 활용하여 개발 환경을 직접 구축하는 미션입니다.

**미션 목표**
- 터미널 기본 명령어를 익히고 파일/디렉토리를 자유롭게 다룬다
- Docker를 설치하고 컨테이너를 직접 실행·관리한다
- Git과 GitHub를 연동하여 작업 결과를 버전 관리한다

---

## 2. 실행 환경

| 항목 | 내용 |
|------|------|
| OS | macOS |
| Shell / Terminal | zsh / VSCode 통합 터미널 |
| Docker 버전 | 추후 기입 |
| Git 버전 | 추후 기입 |

---

## 3. 수행 항목 체크리스트

| 항목 | 완료 여부 |
|------|----------|
| 터미널 기본 명령 수행 | ✅ |
| 파일/디렉토리 권한 변경 | ⬜ |
| Docker 설치 및 버전 확인 | ⬜ |
| Docker 기본 운영 명령 | ⬜ |
| hello-world 컨테이너 실행 | ⬜ |
| ubuntu 컨테이너 진입 및 명령 수행 | ⬜ |
| Dockerfile 커스텀 이미지 제작 | ⬜ |
| 포트 매핑 및 접속 확인 | ⬜ |
| Docker 볼륨 영속성 검증 | ⬜ |
| Git 설정 및 GitHub 연동 | ✅ |

---

## 4. 터미널 조작 로그

### 4-1. 현재 위치 확인

현재 작업 중인 디렉토리를 확인합니다.  
`pwd`는 **Print Working Directory**의 약자로, 내가 지금 어느 폴더에 있는지 절대경로로 보여줍니다.

```bash
pwd

/Users/c5312ksy5312/codyssey-mission_1-1
```

---

### 4-2. 목록 확인 (숨김 파일 포함)

`-a` 옵션을 붙이면 `.git`처럼 `.`으로 시작하는 숨김 파일도 함께 볼 수 있습니다.

```bash
ls -a

.               ..              .git            README.md
``` 

---

### 4-3. 디렉토리 이동

`cd`는 **Change Directory**의 약자입니다.  
`..`은 상위 폴더를 의미하고, 폴더 이름을 직접 입력하면 해당 폴더로 이동합니다.

```bash
# 상위 디렉토리로 이동
cd ..          

# 다시 프로젝트 폴더로 이동
cd codyssey-mission_1-1   
```

---

### 4-4. 디렉토리 생성

`mkdir`로 새 폴더를 만들 수 있습니다.

```bash
mkdir test-dir
ls

README.md       test-dir
```

---

### 4-5. 빈 파일 생성

`touch`는 빈 파일을 만드는 명령어입니다.  
파일이 이미 있으면 수정 시간만 갱신됩니다.

```bash
touch hello.txt
ls

hello.txt       README.md       test-dir
```

---

### 4-6. 파일 내용 입력 및 확인

`echo`로 파일에 내용을 쓰고, `cat`으로 내용을 확인합니다.

```bash
echo 'Hello, World!' > hello.txt
cat hello.txt

Hello, World!
```

---

### 4-7. 파일 복사

`cp`는 **Copy**의 약자입니다.  
원본 파일은 그대로 유지되고 새 파일이 생성됩니다.

```bash
cp hello.txt hello-copy.txt
ls

hello-copy.txt  hello.txt       README.md       test-dir
```

---

### 4-8. 파일 이름 변경 / 이동

`mv`는 **Move**의 약자입니다.  
같은 폴더 안에서 쓰면 이름 변경, 다른 경로를 지정하면 이동이 됩니다.

```bash
# 이름 변경
mv hello-copy.txt hello-renamed.txt 
ls

hello-renamed.txt       hello.txt               README.md               test-dir

# 파일이동 
mv hello-renamed.txt test-dir/  
ls

hello.txt    README.md    test-dir
```

---

### 4-9. 파일 삭제

`rm`은 **Remove**의 약자입니다.  
⚠️ 삭제한 파일은 휴지통 없이 바로 사라지므로 주의가 필요합니다.

```bash
rm hello-renamed.txt
cd test-dir
ls

# 안에 파일이 없어져서 빈 디렉토리라 아무것도 출력되지 않음
```

---

## 5. 권한 실습

### 5-1. 권한이란?

리눅스/macOS에서 모든 파일과 폴더는 **읽기(r)/쓰기(w)/실행(x)** 권한을 가집니다.  
숫자로 표현할 때는 r=4, w=2, x=1을 더해서 나타냅니다.

| 숫자 | 권한 | 의미 |
|------|------|------|
| 7 | rwx | 읽기 + 쓰기 + 실행 |
| 6 | rw- | 읽기 + 쓰기 |
| 5 | r-x | 읽기 + 실행 |
| 4 | r-- | 읽기만 |

---

### 5-2. 파일 권한 변경

`chmod`은 **change mode**의 약자입니다.  
변경 전 권한을 먼저 확인하고, `chmod`로 변경한 뒤 다시 확인합니다.

```bash
# 변경 전 확인 (-l은 상세정보 확인)
ls -l hello.txt          

-rw-r--r--  1 c5312ksy5312  c5312ksy5312  14  8  3 21:27 hello.txt # 644

# 권한 변경
chmod 755 hello.txt    
# 변경 후 확인  
ls -l hello.txt   

-rwxr-xr-x  1 c5312ksy5312  c5312ksy5312  14  8  3 21:27 hello.txt # 755
```

755는 **소유자(rwx) / 그룹(r-x) / 기타(r-x)** 를 의미합니다.  
실행 가능한 스크립트 파일에 주로 사용합니다.

---

### 5-3. 디렉토리 권한 변경

```bash
# 변경 전 확인 (-ld는 디렉토리의 상세정보 확인)
ls -ld test-dir      

drwxr-xr-x  2 c5312ksy5312  c5312ksy5312  64  8  3 21:48 test-dir # 755

 # 권한 변경
chmod 644 test-dir     
# 변경 후 확인 
ls -ld test-dir          

drw-r--r--  2 c5312ksy5312  c5312ksy5312  64  8  3 21:48 test-dir # 644
```

644는 **소유자(rw-) / 그룹(r--) / 기타(r--)** 를 의미합니다.  
일반 문서 파일에 주로 사용합니다.

---

## 6. Docker 설치 및 기본 점검

### 6-1. Docker란?

Docker는 애플리케이션을 **컨테이너**라는 독립된 환경에서 실행할 수 있게 해주는 도구입니다.  
"내 컴퓨터에서는 되는데 서버에서는 안 돼요" 문제를 해결해줍니다.

---

### 6-2. Docker 버전 확인

```bash
docker --version

Docker version 28.5.2, build ecc6942
```

---

### 6-3. Docker 데몬 동작 확인

`docker info`는 Docker 엔진이 정상적으로 실행 중인지 확인합니다.

```bash
docker info
```

<details> 

<summary>📋 docker info 전체 출력 결과</summary>

 ```bash

Client:
 Version:    28.5.2
 Context:    orbstack
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.29.1
    Path:     /Users/c5312ksy5312/.docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
    Version:  v2.40.3
    Path:     /Users/c5312ksy5312/.docker/cli-plugins/docker-compose

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 28.5.2
 Storage Driver: overlay2
  Backing Filesystem: btrfs
  Supports d_type: true
  Using metacopy: false
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 CDI spec directories:
  /etc/cdi
  /var/run/cdi
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 1c4457e00facac03ce1d75f7b6777a7a851e5c41
 runc version: d842d7719497cc3b774fd71620278ac9e17710e0
 init version: de40ad0
 Security Options:
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 6.17.8-orbstack-00308-g8f9c941121b1
 Operating System: OrbStack
 OSType: linux
 Architecture: x86_64
 CPUs: 6
 Total Memory: 15.67GiB
 Name: orbstack
 ID: 75e2897f-3f33-4bf4-a5fc-92ed031b3001
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Experimental: false
 Insecure Registries:
  ::1/128
  127.0.0.0/8
 Live Restore Enabled: false
 Product License: Community Engine
 Default Address Pools:
   Base: 192.168.97.0/24, Size: 24
   Base: 192.168.107.0/24, Size: 24
   Base: 192.168.117.0/24, Size: 24
   Base: 192.168.147.0/24, Size: 24
   Base: 192.168.148.0/24, Size: 24
   Base: 192.168.155.0/24, Size: 24
   Base: 192.168.156.0/24, Size: 24
   Base: 192.168.158.0/24, Size: 24
   Base: 192.168.163.0/24, Size: 24
   Base: 192.168.164.0/24, Size: 24
   Base: 192.168.165.0/24, Size: 24
   Base: 192.168.166.0/24, Size: 24
   Base: 192.168.167.0/24, Size: 24
   Base: 192.168.171.0/24, Size: 24
   Base: 192.168.172.0/24, Size: 24
   Base: 192.168.181.0/24, Size: 24
   Base: 192.168.183.0/24, Size: 24
   Base: 192.168.186.0/24, Size: 24
   Base: 192.168.207.0/24, Size: 24
   Base: 192.168.214.0/24, Size: 24
   Base: 192.168.215.0/24, Size: 24
   Base: 192.168.216.0/24, Size: 24
   Base: 192.168.223.0/24, Size: 24
   Base: 192.168.227.0/24, Size: 24
   Base: 192.168.228.0/24, Size: 24
   Base: 192.168.229.0/24, Size: 24
   Base: 192.168.237.0/24, Size: 24
   Base: 192.168.239.0/24, Size: 24
   Base: 192.168.242.0/24, Size: 24
   Base: 192.168.247.0/24, Size: 24
   Base: fd07:b51a:cc66:d000::/56, Size: 64

WARNING: DOCKER_INSECURE_NO_IPTABLES_RAW is set

```
</details>

✅ Docker 정상 작동!

---

## 7. Docker 기본 운영 명령

### 7-1. 이미지 다운로드

이미지는 컨테이너를 만들기 위한 **설계도**입니다.

```bash
# ubuntu 이미지를 Docker Hub에서 다운로드
docker pull ubuntu 

Using default tag: latest
latest: Pulling from library/ubuntu
ed819469700f: Pull complete 
a3679419df18: Pull complete 
Digest: sha256:3131b4cc82a783df6c9df078f86e01819a13594b865c2cad47bd1bca2b7063bb
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:lates

# nginx 이미지를 Docker Hub에서 다운로드
docker pull nginx 

Using default tag: latest
latest: Pulling from library/nginx
062e450697fa: Pull complete 
82454cdbf456: Pull complete 
3c7ab7949321: Pull complete 
cacfcdd01f30: Pull complete 
b6698f04e005: Pull complete 
2bedaf25031a: Pull complete 
d26f27cc8c41: Pull complete 
Digest: sha256:5a88c9c45479443d7be2eadc894b4ed0a9801bae03d97a5760ae13b5c2005942
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest

```

---

### 7-2. 이미지 목록 확인

```bash
# 다운로드된 이미지 목록 확인
docker images    

REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
nginx        latest    5253dc86cc93   30 hours ago   161MB
ubuntu       latest    86a1a31fdd84   12 days ago    100MB
```

---

### 7-3. 컨테이너 실행

`docker run` 명령어로 이미지를 기반으로 컨테이너를 실행합니다.

- `-d` : 백그라운드 실행 (detached mode)
- `--name` : 컨테이너 이름 지정
- `sleep 1000` : 컨테이너가 종료되지 않도록 대기 명령 실행

```bash
# my-ubuntu라는 이름으로 백그라운드 실행
docker run -d --name my-ubuntu ubuntu:20.04 sleep 1000    

Unable to find image 'ubuntu:20.04' locally
20.04: Pulling from library/ubuntu
13b7e930469f: Pull complete 
Digest: sha256:8feb4d8ca5354def3d8fce243717141ce31e2c428701f6682bd2fafe15388214
Status: Downloaded newer image for ubuntu:20.04
af5cbe0965ba1378db48ffd6e5a7b4eddd2bd5cbd26917afa5cdfcb3f76dfb6f
```

---

### 7-4. 컨테이너 중지

```bash
# my-ubuntu 컨테이너 중지
docker stop my-ubuntu    

my-ubuntu
```

---

### 7-5. 컨테이너 목록 확인

`docker ps`는 실행 중인 컨테이너만, `docker ps -a`는 중지된 컨테이너까지 모두 확인합니다.

```bash
# 실행 중인 컨테이너 목록 확인
docker ps    

CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

```bash
# 중지된 컨테이너 포함 전체 목록 확인
docker ps -a    

ONTAINER ID   IMAGE          COMMAND        CREATED         STATUS                        PORTS     NAMES
af5cbe0965ba   ubuntu:20.04   "sleep 1000"   4 minutes ago   Exited (137) 50 seconds ago             my-ubuntu
```

---

### 7-6. 로그 및 리소스 확인

```bash
# 로그/리소스 확인을 위해 컨테이너 재시작
docker start my-ubuntu    

my-ubuntu
```

```bash
# 컨테이너 로그 확인
docker logs my-ubuntu    

(sleep 명령은 출력이 없어 로그가 비어있음)
```

```bash
# 리소스 사용량 1회 확인 (--no-stream: 실시간 모니터링 종료)
docker stats --no-stream my-ubuntu    

CONTAINER ID   NAME        CPU %     MEM USAGE / LIMIT   MEM %     NET I/O         BLOCK I/O     PIDS
af5cbe0965ba   my-ubuntu   0.00%     692KiB / 15.67GiB   0.00%     1.13kB / 126B   2.45MB / 0B   1
```

---

## 8. 컨테이너 실행 실습

### 8-1. hello-world 실행

Docker가 정상 설치되었는지 확인하는 가장 기본적인 테스트입니다.

```bash
docker run hello-world

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
4f55086f7dd0: Pull complete 
Digest: sha256:7f4da0fc94bcece205a8c0b6f4d11c8196924654ffe5c4d1aa439b7f632048b2
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

---

### 8-2. ubuntu 컨테이너 진입

`-it` 옵션은 **인터랙티브 터미널** 모드로 컨테이너 내부에 직접 접속합니다.

```bash
docker run -it ubuntu /bin/bash

root@72e874efc7c5:/#

# 컨테이너 내부에서 실행
ls

bin   dev  home  lib64  mnt  proc  run   srv  tmp  var
boot  etc  lib   media  opt  root  sbin  sys  usr
---
echo 'Hello from inside container!'

Hello from inside container!

# 컨테이너 종료
exit 
```

---

### 8-3. attach vs exec 차이

컨테이너에 접속하는 방법은 두 가지가 있습니다.

| 방식 | 명령어 | 특징 |
|------|--------|------|
| attach | `docker attach [ID]` | 메인 프로세스에 연결. `exit` 시 컨테이너 종료됨 |
| exec | `docker exec -it [ID] bash` | 새 프로세스 추가. `exit` 해도 컨테이너 유지됨 |

> 💡 실무에서는 컨테이너를 종료시키지 않기 위해 `exec`를 주로 사용합니다.

---
## 9. 커스텀 이미지 제작 (Dockerfile)

### 9-1. 선택 방식

**(A) NGINX 베이스 이미지 + 정적 콘텐츠 교체** 방식을 선택했습니다.

- **기존 베이스 이미지**: `nginx:latest`
- **선택 이유**: 
  - NGINX는 가장 널리 사용되는 웹 서버로 학습 가치가 높음
  - 웹 서버 기능이 이미 포함되어 있어 추가 설정이 최소화됨
  - 정적 웹 페이지 배포에 최적화되어 있음

---

### 9-2. 커스텀 콘텐츠 준비

컨테이너에 넣을 정적 HTML 파일을 먼저 준비합니다.

```bash
# 프로젝트 디렉토리 생성 및 이동
mkdir custom-nginx && cd custom-nginx

# 사용자 정의 HTML 파일 생성
cat > index.html << 'EOF'
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>My Custom NGINX</title>
</head>
<body>
    <h1>🚀 커스텀 NGINX 서버에 오신 것을 환영합니다!</h1>
    <p>이 페이지는 Docker 커스텀 이미지에서 제공됩니다.</p>
</body>
</html>
EOF
```

```bash
# 파일 생성 확인
ls

index.html
```

---

### 9-3. Dockerfile 생성

NGINX 베이스 이미지에 커스텀 HTML을 복사하는 Dockerfile을 작성합니다.

```dockerfile
# Dockerfile 생성
cat > Dockerfile << 'EOF'

# 베이스 이미지: 공식 NGINX 이미지 사용
FROM nginx:latest

# 이미지 메타데이터 설정 (작성자 정보)
LABEL maintainer="5312ksy@gmail.com"
LABEL description="Custom NGINX with static content"

# NGINX 기본 페이지를 커스텀 HTML로 교체
# /usr/share/nginx/html/ 은 NGINX의 기본 웹 루트 디렉토리
COPY index.html /usr/share/nginx/html/index.html

# 80번 포트를 사용할 것임을 명시
EXPOSE 80

# 헬스체크: 30초마다 웹 서버 정상 동작 여부 확인
HEALTHCHECK --interval=30s --timeout=3s \
  CMD curl -f http://localhost/ || exit 1

# 컨테이너 시작 시 NGINX를 포그라운드로 실행하여 컨테이너 유지
CMD ["nginx", "-g", "daemon off;"]

#생성완료
EOF
```

---

### 9-4. 커스텀 포인트 설명

| 항목 | 목적 |
|------|------|
| `FROM nginx:latest` | 공식 NGINX 이미지 사용으로 안정성과 신뢰성 확보 |
| `LABEL` | 이미지 메타데이터 추가로 관리 편의성 확보 |
| `COPY index.html` | 기본 페이지를 커스텀 콘텐츠로 교체 |
| `EXPOSE 80` | 컨테이너가 사용할 포트 명시 (문서화 목적) |
| `HEALTHCHECK` | 컨테이너 상태 자동 모니터링으로 안정성 확보 |
| `daemon off` | 포그라운드 실행으로 컨테이너 정상 유지 |

---

### 9-5. 이미지 빌드

작성한 Dockerfile로 커스텀 이미지를 빌드합니다.

```bash
# -t: 이미지 이름과 태그 지정
# .: 현재 디렉토리의 Dockerfile 사용
docker build -t my-custom-nginx:1.0 .

[+] Building 1.7s (7/7) FINISHED                                      docker:orbstack
 => [internal] load build definition from Dockerfile                             0.1s
 => => transferring dockerfile: 325B                                             0.0s
 => [internal] load metadata for docker.io/library/nginx:latest                  0.0s
 => [internal] load .dockerignore                                                0.1s
 => => transferring context: 2B                                                  0.0s
 => [1/2] FROM docker.io/library/nginx:latest                                    0.8s
 => [internal] load build context                                                0.4s
 => => transferring context: 325B                                                0.0s
 => [2/2] COPY index.html /usr/share/nginx/html/index.html                       0.1s
 => exporting to image                                                           0.2s
 => => exporting layers                                                          0.1s
 => => writing image sha256:620f4e451ccba191c8544411dfc169e7d672ae4584712eb903b  0.0s
 => => naming to docker.io/library/my-custom-nginx:1.0                           0.0s

**이미지 확인:**

# 빌드된 이미지 목록 확인
docker images | grep my-custom-nginx

my-custom-nginx   1.0       620f4e451ccb   53 seconds ago   161MB
```

---

### 9-6. 컨테이너 실행 및 포트 매핑

호스트의 8080 포트를 컨테이너의 80 포트에 연결합니다.  
브라우저에서 `localhost:8080`으로 접속할 수 있습니다.

```bash
# -d: 백그라운드 실행
# -p 8080:80: 호스트 8080 포트 → 컨테이너 80 포트 매핑
# --name: 컨테이너 이름 지정
docker run -d -p 8080:80 --name my-nginx my-custom-nginx:1.0

24c25ed68664e0d9f054a0eb21c491f0b20bd7712e4033b783edffd073fad757

**컨테이너 상태 확인:**
docker ps

CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS                    PORTS                                     NAMES
24c25ed68664   my-custom-nginx:1.0   "/docker-entrypoint.…"   18 minutes ago   Up 18 minutes (healthy)   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   my-nginx:8080->80/tcp   my-nginx
```

---

### 9-7. 접속 증거

#### curl로 응답 확인

```bash
# 로컬 8080 포트로 HTTP 요청
curl http://localhost:8080

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>My Custom NGINX</title>
</head>
<body>
    <h1>🚀 커스텀 NGINX 서버에 오신 것을 환영합니다!</h1>
    <p>이 페이지는 Docker 커스텀 이미지에서 제공됩니다.</p>
</body>
</html>
```

#### 브라우저 접속 화면

브라우저에서 `http://localhost:8080` 접속 결과:

![커스텀 NGINX 브라우저 접속](./screenshots/nginx-browser.png)

---

### 9-8. 정리 (컨테이너 종료)

실습 완료 후 컨테이너를 정리합니다.

```bash
# 컨테이너 중지
docker stop my-nginx

my-nginx

# 컨테이너 삭제
docker rm my-nginx

my-nginx
```
---

## 10. Docker 볼륨 영속성 검증

### 10-1. 볼륨이란?

컨테이너는 삭제되면 내부 데이터도 함께 사라집니다.  
**볼륨**을 사용하면 컨테이너 외부에 데이터를 저장하여 컨테이너가 삭제되어도 데이터가 유지됩니다.

---

### 10-2. 볼륨 생성 및 연결

```bash
# 볼륨 생성
docker volume create my-volume       

my-volume

# 볼륨 연결 후 컨테이너 실행 
docker run -it -v my-volume:/data ubuntu bash  

# 컨테이너 내부에서 파일 생성 
echo 'volume test' > /data/test.txt  
exit

exit
```

---

### 10-3. 컨테이너 삭제 후 데이터 확인 (검증)

```bash
# 컨테이너 삭제 (컨테이너 ID 확인후 진행, docker ps -a)
docker rm f89b1a4f6b96              

f89b1a4f6b96

# 데이터 유지 확인
docker run -v my-volume:/data ubuntu cat /data/test.txt 

volume test    # 데이터가 그대로 남아있음       
```

컨테이너를 삭제했음에도 볼륨에 저장된 데이터는 유지되는 것을 확인했습니다. ✅

---

## 11. Git 설정 및 GitHub 연동

### 11-1. Git 사용자 설정

커밋할 때 작성자 정보로 사용됩니다.

```bash
git config --global user.name "강서연"
git config --global user.email "5312ksy@gmail.com"
```

---

### 11-2. 설정 확인

```bash
git config --list

credential.helper=osxkeychain
user.email=5312ksy@gmail.com
user.name=강서연
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true
submodule.active=.
remote.origin.url=https://github.com/5312ksy-beep/codyssey-mission_1-1.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
branch.main.remote=origin
:
```

---

### 11-3. GitHub 연동 증거

> 스크린샷 첨부 예정

---

## 12. 검증 방법 요약

| 항목 | 검증 명령 | 결과 위치 |
|------|----------|----------|
| 터미널 명령 | pwd, ls, touch, cp, mv, rm | 4장 |
| 파일 권한 | ls -l, chmod | 5장 |
| Docker 설치 | docker --version, docker info | 6장 |
| Docker 운영 | docker images, docker ps | 7장 |
| 컨테이너 실행 | docker run | 8장 |
| 이미지 빌드 | docker build | 9장 |
| 볼륨 영속성 | docker volume create | 10장 |
| Git 연동 | git config --list | 11장 |