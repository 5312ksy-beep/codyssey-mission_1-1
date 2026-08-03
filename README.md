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

# 출력 예정
```

---

### 4-3. 디렉토리 이동

`cd`는 **Change Directory**의 약자입니다.  
`..`은 상위 폴더를 의미하고, 폴더 이름을 직접 입력하면 해당 폴더로 이동합니다.

```bash
cd ..          # 상위 디렉토리로 이동
cd codyssey-mission_1-1   # 다시 프로젝트 폴더로 이동
```

---

### 4-4. 디렉토리 생성

`mkdir`로 새 폴더를 만들 수 있습니다.

```bash
mkdir test-dir
ls

hello.txt       README.md       test-dir
```

---

### 4-5. 빈 파일 생성

`touch`는 빈 파일을 만드는 명령어입니다.  
파일이 이미 있으면 수정 시간만 갱신됩니다.

```bash
touch hello.txt
ls
# 출력 예정
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
# 출력 예정
```

---

### 4-8. 파일 이름 변경 / 이동

`mv`는 **Move**의 약자입니다.  
같은 폴더 안에서 쓰면 이름 변경, 다른 경로를 지정하면 이동이 됩니다.

```bash
mv hello-copy.txt hello-renamed.txt
ls
# 출력 예정
```

---

### 4-9. 파일 삭제

`rm`은 **Remove**의 약자입니다.  
⚠️ 삭제한 파일은 휴지통 없이 바로 사라지므로 주의가 필요합니다.

```bash
rm hello-renamed.txt
ls
# 출력 예정
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

변경 전 권한을 먼저 확인하고, `chmod`로 변경한 뒤 다시 확인합니다.

```bash
ls -l hello.txt          # 변경 전 확인
# 출력 예정

chmod 755 hello.txt      # 권한 변경

ls -l hello.txt          # 변경 후 확인
# 출력 예정
```

755는 **소유자(rwx) / 그룹(r-x) / 기타(r-x)** 를 의미합니다.  
실행 가능한 스크립트 파일에 주로 사용합니다.

---

### 5-3. 디렉토리 권한 변경

```bash
ls -ld test-dir          # 변경 전 확인
# 출력 예정

chmod 644 test-dir       # 권한 변경

ls -ld test-dir          # 변경 후 확인
# 출력 예정
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
# 출력 예정
```

---

### 6-3. Docker 데몬 동작 확인

`docker info`는 Docker 엔진이 정상적으로 실행 중인지 확인합니다.

```bash
docker info
```
<details>
 
---
<summary>📋 docker info 전체 출력 결과</summary>

---
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
---
</details>

✅ Docker 정상 작동!

---
---

## 7. Docker 기본 운영 명령

### 7-1. 이미지 목록 확인

이미지는 컨테이너를 만들기 위한 **설계도**입니다.

```bash
docker images
# 출력 예정
```

---

### 7-2. 컨테이너 목록 확인

```bash
docker ps        # 실행 중인 컨테이너만
docker ps -a     # 종료된 컨테이너 포함 전체
# 출력 예정
```

---

### 7-3. 로그 및 리소스 확인

```bash
docker logs [컨테이너ID]    # 컨테이너 로그 확인
docker stats                # CPU/메모리 실시간 확인
# 출력 예정
```

---

## 8. 컨테이너 실행 실습

### 8-1. hello-world 실행

Docker가 정상 설치되었는지 확인하는 가장 기본적인 테스트입니다.

```bash
docker run hello-world
# 출력 예정
```

---

### 8-2. ubuntu 컨테이너 진입

`-it` 옵션은 **인터랙티브 터미널** 모드로 컨테이너 내부에 직접 접속합니다.

```bash
docker run -it ubuntu /bin/bash

# 컨테이너 내부에서 실행
ls
echo 'Hello from inside container!'
# 출력 예정
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

---

### 9-2. Dockerfile

```dockerfile
# 출력 예정
```

---

### 9-3. 커스텀 포인트 설명

| 항목 | 목적 |
|------|------|
| 추후 기입 | 추후 기입 |

---

### 9-4. 이미지 빌드

```bash
docker build -t my-custom-image .
# 출력 예정
```

---

### 9-5. 컨테이너 실행 및 포트 매핑

호스트의 8080 포트를 컨테이너의 80 포트에 연결합니다.  
브라우저에서 `localhost:8080`으로 접속할 수 있습니다.

```bash
docker run -p 8080:80 my-custom-image
# 출력 예정
```

**접속 증거 (스크린샷 또는 curl 결과)**

```bash
curl http://localhost:8080
# 출력 예정
```

---

## 10. Docker 볼륨 영속성 검증

### 10-1. 볼륨이란?

컨테이너는 삭제되면 내부 데이터도 함께 사라집니다.  
**볼륨**을 사용하면 컨테이너 외부에 데이터를 저장하여 컨테이너가 삭제되어도 데이터가 유지됩니다.

---

### 10-2. 볼륨 생성 및 연결

```bash
docker volume create my-volume       # 볼륨 생성
# 출력 예정

docker run -it -v my-volume:/data ubuntu bash   # 볼륨 연결 후 실행
echo 'volume test' > /data/test.txt  # 컨테이너 내부에서 파일 생성
exit
# 출력 예정
```

---

### 10-3. 컨테이너 삭제 후 데이터 확인

```bash
docker rm [컨테이너ID]               # 컨테이너 삭제
# 출력 예정

docker run -v my-volume:/data ubuntu cat /data/test.txt  # 데이터 유지 확인
volume test                          # 데이터가 그대로 남아있음
```

컨테이너를 삭제했음에도 볼륨에 저장된 데이터는 유지되는 것을 확인했습니다. ✅

---

## 11. Git 설정 및 GitHub 연동

### 11-1. Git 사용자 설정

커밋할 때 작성자 정보로 사용됩니다.

```bash
git config --global user.name "이름"
git config --global user.email "이메일"
```

---

### 11-2. 설정 확인

```bash
git config --list
# 출력 예정
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
