# workstation-develop


## 1. 프로젝트 개요 

docker를 사용해 웹 서버를 컨테이너화 하기. 과정을 git으로 관리하여 github에 저장하기.

---

## 2. 실행 환경 (Execution Environment)

이 프로젝트를 수행하고 검증한 환경 정보입니다.

### OS : MacOS 26.4 (Tahoe)
### shell : bash
### docker : 4.67.0
### git : 2.50.1
---

## 3. 프로젝트 수행 체크리스트 (Task Checklist)

- [x] 터미널 기본 조작 및 폴더 구성
- [x] 권한 변경 실습
- [x] Docker 설치/점검
- [x] hello-world 실행
- [x] Dockerfile 빌드/실행
- [x] 포트 매핑 접속
- [x] 바인드 마운트 반영
- [x] 볼륨 영속성
- [x] Git 설정

---

## 4. 수행 로그 (Work Log)
### 1. 환경준비
ryusungeun@SungEuns-MacBook-Pro Codyssey % git clone https://github.com/loader1017/workstation-develop.git
Cloning into 'workstation-develop'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (3/3), done.
ryusungeun@SungEuns-MacBook-Pro Codyssey % cd workstation-develop
ryusungeun@SungEuns-MacBook-Pro workstation-develop % pwd
/Users/ryusungeun/Desktop/2026/Codyssey/workstation-develop
ryusungeun@SungEuns-MacBook-Pro workstation-develop % ls -la
total 8
drwxr-xr-x   4 ryusungeun  staff  128 Apr  1 15:07 .
drwxr-xr-x@  4 ryusungeun  staff  128 Apr  1 15:07 ..
drwxr-xr-x  12 ryusungeun  staff  384 Apr  1 15:07 .git
-rw-r--r--   1 ryusungeun  staff   21 Apr  1 15:07 README.md

### 2. 터미널 조작, 파일권한 변경
ryusungeun@SungEuns-MacBook-Pro workstation-develop % mkdir practice 
ryusungeun@SungEuns-MacBook-Pro workstation-develop % cd practice 
ryusungeun@SungEuns-MacBook-Pro practice % touch test.txt
ryusungeun@SungEuns-MacBook-Pro practice % cat test.txt
ryusungeun@SungEuns-MacBook-Pro practice % cd ..
ryusungeun@SungEuns-MacBook-Pro workstation-develop % ls -ld practice practice/test.txt
drwxr-xr-x  3 ryusungeun  staff  96 Apr  1 15:07 practice
-rw-r--r--  1 ryusungeun  staff   0 Apr  1 15:07 practice/test.txt
ryusungeun@SungEuns-MacBook-Pro workstation-develop % chmod 755 practice/test.txt 
ryusungeun@SungEuns-MacBook-Pro workstation-develop % chmod 700 practice
ryusungeun@SungEuns-MacBook-Pro workstation-develop % ls -ld practice practice/test.txt
drwx------  3 ryusungeun  staff  96 Apr  1 15:07 practice
-rwxr-xr-x  1 ryusungeun  staff   0 Apr  1 15:07 practice/test.txt

### 3. git, docker 버전확인
ryusungeun@SungEuns-MacBook-Pro workstation-develop % git --version
git version 2.50.1 (Apple Git-155)

ryusungeun@SungEuns-MacBook-Pro workstation-develop % docker --version
Docker version 29.3.1, build c2be9cc

### 4. docker 설치 및 연결확인
ryusungeun@SungEuns-MacBook-Pro workstation-develop % docker info
Client:
 Version:    29.3.1
 Context:    desktop-linux
 Debug Mode: false
 Plugins:
  agent: Docker AI Agent Runner (Docker Inc.)
    Version:  v1.34.0
    Path:     /Users/ryusungeun/.docker/cli-plugins/docker-agent
  ai: Docker AI Agent - Ask Gordon (Docker Inc.)
    Version:  v1.20.1
    Path:     /Users/ryusungeun/.docker/cli-plugins/docker-ai
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.32.1-desktop.1
    Path:     /Users/ryusungeun/.docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
    Version:  v5.1.1
    Path:     /Users/ryusungeun/.docker/cli-plugins/docker-compose
  debug: Get a shell into any image or container (Docker Inc.)
    Version:  0.0.47
    Path:     /Users/ryusungeun/.docker/cli-plugins/docker-debug
  desktop: Docker Desktop commands (Docker Inc.)
    Version:  v0.3.0
    Path:     /Users/ryusungeun/.docker/cli-plugins/docker-desktop
  dhi: CLI for managing Docker Hardened Images (Docker Inc.)
    Version:  v0.0.2
    Path:     /Users/ryusungeun/.docker/cli-plugins/docker-dhi
  extension: Manages Docker extensions (Docker Inc.)
    Version:  v0.2.31
    Path:     /Users/ryusungeun/.docker/cli-plugins/docker-extension
  init: Creates Docker-related starter files for your project (Docker Inc.)
    Version:  v1.4.0
    Path:     /Users/ryusungeun/.docker/cli-plugins/docker-init
  mcp: Docker MCP Plugin (Docker Inc.)
    Version:  v0.40.3
    Path:     /Users/ryusungeun/.docker/cli-plugins/docker-mcp
  model: Docker Model Runner (Docker Inc.)
    Version:  v1.1.28
    Path:     /Users/ryusungeun/.docker/cli-plugins/docker-model
  offload: Docker Offload (Docker Inc.)
    Version:  v0.5.77
    Path:     /Users/ryusungeun/.docker/cli-plugins/docker-offload
  pass: Docker Pass Secrets Manager Plugin (beta) (Docker Inc.)
    Version:  v0.0.24
    Path:     /Users/ryusungeun/.docker/cli-plugins/docker-pass
  sandbox: Docker Sandbox (Docker Inc.)
    Version:  v0.12.0
    Path:     /Users/ryusungeun/.docker/cli-plugins/docker-sandbox
  sbom: View the packaged-based Software Bill Of Materials (SBOM) for an image (Anchore Inc.)
    Version:  0.6.0
    Path:     /Users/ryusungeun/.docker/cli-plugins/docker-sbom
  scout: Docker Scout (Docker Inc.)
    Version:  v1.20.3
    Path:     /Users/ryusungeun/.docker/cli-plugins/docker-scout

Server:
 Containers: 4
  Running: 0
  Paused: 0
  Stopped: 4
 Images: 2
 Server Version: 29.3.1
 Storage Driver: overlayfs
  driver-type: io.containerd.snapshotter.v1
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
 containerd version: dea7da592f5d1d2b7755e3a161be07f43fad8f75
 runc version: v1.3.4-0-gd6d73eb8
 init version: de40ad0
 Security Options:
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 6.12.76-linuxkit
 Operating System: Docker Desktop
 OSType: linux
 Architecture: aarch64
 CPUs: 11
 Total Memory: 7.653GiB
 Name: docker-desktop
 ID: 0b2c0127-e74d-41ee-9eae-88a8cd6aab54
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 HTTP Proxy: http.docker.internal:3128
 HTTPS Proxy: http.docker.internal:3128
 No Proxy: hubproxy.docker.internal
 Labels:
  com.docker.desktop.address=unix:///Users/ryusungeun/Library/Containers/com.docker.docker/Data/docker-cli.sock
 Experimental: false
 Insecure Registries:
  hubproxy.docker.internal:5555
  ::1/128
  127.0.0.0/8
 Live Restore Enabled: false

ryusungeun@SungEuns-MacBook-Pro workstation-develop % docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (arm64v8)
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

ryusungeun@SungEuns-MacBook-Pro workstation-develop % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
ryusungeun@SungEuns-MacBook-Pro workstation-develop % docker ps -a
CONTAINER ID   IMAGE                             COMMAND                  CREATED          STATUS                      PORTS     NAMES
5a6f774519e6   hello-world                       "/hello"                 16 seconds ago   Exited (0) 16 seconds ago             blissful_murdock
d87c22a1a3bf   hello-world                       "/hello"                 8 minutes ago    Exited (0) 8 minutes ago              quirky_ardinghelli
95f80fe08dfe   hello-world                       "/hello"                 29 minutes ago   Exited (0) 29 minutes ago             admiring_noether
b1cd193f5ea6   hello-world                       "/hello"                 23 hours ago     Exited (0) 23 hours ago               awesome_ritchie
2fc4f7c96042   docker/welcome-to-docker:latest   "/docker-entrypoint.…"   23 hours ago     Exited (0) 23 hours ago               welcome-to-docker


### 5. 웹 서버 소스코드, dockerfile 작성.
ryusungeun@SungEuns-MacBook-Pro workstation-develop % mkdir app
ryusungeun@SungEuns-MacBook-Pro workstation-develop % cd app
ryusungeun@SungEuns-MacBook-Pro app % touch index.html
ryusungeun@SungEuns-MacBook-Pro app % cat << EOF > index.html
heredoc> <!DOCTYPE html>
<html>
<head>
    <title>My Docker Web Server</title>
</head>
<body>
    <h1>Hello, Docker!</h1>
    <p>This is my first web server.</p> 
</body>
</html>
heredoc> EOF 
ryusungeun@SungEuns-MacBook-Pro app % cd ..
ryusungeun@SungEuns-MacBook-Pro workstation-develop % touch Dockerfile    
ryusungeun@SungEuns-MacBook-Pro workstation-develop % cat << EOF > Dockerfile
heredoc> FROM nginx:alpine
heredoc> COPY ./app /usr/share/nginx/html
heredoc> EXPOSE 80
heredoc> EOF
ryusungeun@SungEuns-MacBook-Pro workstation-develop % ls  
Dockerfile    README.md    app        practice

### 6.이미지빌드
ryusungeun@SungEuns-MacBook-Pro workstation-develop % docker build -t my-web-server:1.0 .
[+] Building 8.3s (8/8) FINISHED                           docker:desktop-linux
 => [internal] load build definition from Dockerfile                       0.0s
 => => transferring dockerfile: 98B                                        0.0s
 => [internal] load metadata for docker.io/library/nginx:alpine            5.9s
 => [auth] library/nginx:pull token for registry-1.docker.io               0.0s
 => [internal] load .dockerignore                                          0.0s
 => => transferring context: 2B                                            0.0s
 => [internal] load build context                                          0.0s
 => => transferring context: 239B                                          0.0s
 => [1/2] FROM docker.io/library/nginx:alpine@sha256:e7257f1ef28ba17cf7c2  2.2s
 ... (생략) ...
 => [2/2] COPY ./app /usr/share/nginx/html                                 0.0s
 => exporting to image                                                     0.0s
 ... (생략) ...
 => => naming to docker.io/library/my-web-server:1.0                       0.0s
 => => unpacking to docker.io/library/my-web-server:1.0                    0.0s

ryusungeun@SungEuns-MacBook-Pro workstation-develop % docker images
                                                            i Info →   U  In Use
IMAGE                           ID             DISK USAGE   CONTENT SIZE   EXTRA
docker/welcome-to-docker:latest
                                c4d56c24da4f       22.9MB         6.35MB    U   
hello-world:latest              452a468a4bf9       22.6kB         10.3kB    U   
my-web-server:1.0               f63ed6630e29       91.8MB         25.8MB        

### 7.컨테이너 실행, 확인
ryusungeun@SungEuns-MacBook-Pro workstation-develop % docker run -d -p 8080:80 --name my-first-web my-web-server:1.0
a79f9f472978df29191bb59744bbc49298390742927e38b3ee3e8f9f8105


---


## 6. 바인드 마운트

## 실행 명령어

### 기존 컨테이너 정리
$ docker stop my-first-web
my-first-web
$ docker rm my-first-web
my-first-web

### -v 옵션으로 바인드 마운트 설정 후 실행
$ docker run -d -p 8080:80 \
  --name my-web-mounted \
  -v $(pwd)/app:/usr/share/nginx/html \
  my-web-server:1.0
4b4d4fab1deabccdcc20cf645820107e9a7a88ea09e69c62876cdf73262442a1

## 결과
호스트에서 `app/index.html` 파일을 수정한 후, 웹 브라우저를 새로고침하자 즉시 변경사항이 반영되는 것을 확인했습니다.
### 변경 전
<img width="1004" height="569" alt="screenshot" src="https://github.com/user-attachments/assets/29d3303e-91db-4f6e-9d64-67c3cb336693" />

### 변경 후
<img width="1512" height="982" alt="screenshot2" src="https://github.com/user-attachments/assets/1aa09026-6ff1-47cd-aba0-3574ba256d73" />

다른 조작 없이 app/index.html 에 있는 파일이 수정시 즉각 반영됩니다.
