# [Codyssey] 입학 연수 2기 - 개발 워크스테이션 구축 미션

## 1. 프로젝트 개요
- **목표:** 개발의 기초가 되는 터미널(CLI), Docker(컨테이너), Git/GitHub(버전 관리 및 협업)의 핵심 도구를 직접 다루고, 재현 가능한 개발 워크스테이션 환경을 구축한다.
- **주요 내용:** 
  - Linux CLI를 통한 폴더 구조화 및 권한 제어
  - OrbStack 기반 Docker 환경에서 웹서버 커스텀 이미지 제작 및 포트 매핑
  - Docker 볼륨을 활용한 데이터 영속성 검증
  - Git 및 GitHub를 활용한 소스 코드 버전 관리 및 연동

---

## 2. 실행 환경
- **OS:** macOS (Apple Silicon)
- **Terminal:** Zsh / Terminal
- **Docker:** OrbStack (Docker Engine 호환)
- **Git 버전:** 2.x

---

## 3. 수행 항목 체크리스트
- [x] 터미널 기본 조작 및 폴더 구성
- [x] 파일 및 디렉토리 권한 변경 실습 (755, 700 등)
- [x] Docker 설치 및 데몬 동작 점검 (docker version, info)
- [x] 기본 컨테이너 실행 (`hello-world`, `ubuntu`)[cite: 1]
- [x] Dockerfile 기반 커스텀 웹서버 이미지 제작 및 빌드[cite: 1]
- [x] 포트 매핑 및 브라우저 접속 확인 (`localhost:8080`)[cite: 1]
- [x] Docker 볼륨 생성 및 영속성 검증[cite: 1]
- [x] Git 설정 (`git config`) 및 VSCode-GitHub 연동[cite: 1]

---

## 4. 수행 방법 및 검증 로그
### (1) 터미널 및 권한 실습

```bash
# <현재위치 확인>
$ pwd
/Users/investkorea8007

# <폴더생성>
$ mkdir -p ~/codyssey/practice

# <폴더목록>
$ ls -la
total 48
drwxr-x---+ 22 investkorea8007 investkorea8007 704 8 4 16:06 .
drwxr-xr-x 7 root admin 224 8 3 19:58 ..
-rw------- 1 investkorea8007 investkorea8007 8 8 3 11:43 .CFUserTextEncoding
drwxr-xr-x 5 investkorea8007 investkorea8007 160 8 4 15:29 .docker
-rw-r--r--@ 1 investkorea8007 investkorea8007 8196 8 4 10:45 .DS_Store
drwx------ 10 investkorea8007 investkorea8007 320 8 4 15:29 .orbstack
drwxr-xr-x 3 investkorea8007 investkorea8007 96 8 4 15:29 .ssh
drwx------ 26 investkorea8007 investkorea8007 832 8 4 15:52 .Trash
drwxr-xr-x 3 investkorea8007 investkorea8007 96 8 3 11:46 .vscode
-rw-r--r-- 1 investkorea8007 investkorea8007 154 8 4 15:29 .zprofile
-rw------- 1 investkorea8007 investkorea8007 20 8 4 15:38 .zsh_history
drwx------ 6 investkorea8007 investkorea8007 192 8 4 15:38 .zsh_sessions
drwxr-xr-x 3 investkorea8007 investkorea8007 96 8 4 16:06 codyssey

# <폴더 안으로 이동>
$ cd ~/codyssey/practice

# <텍스트파일 생성>
$ touch 123.txt

# <텍스트파일 확인>
$ ls -la
total 0
drwxr-xr-x 3 investkorea8007 investkorea8007 96 8 4 16:20 .
drwxr-xr-x 3 investkorea8007 investkorea8007 96 8 4 16:06 ..
-rw-r--r-- 1 investkorea8007 investkorea8007 0 8 4 16:20 123.txt

# <123파일 내용 확인>
$ cat 123.txt

# <123파일 복사본 생성>
$cp 123.txt copy_123.txt$ ls -la
total 0
drwxr-xr-x 4 investkorea8007 investkorea8007 128 8 4 16:27 .
drwxr-xr-x 3 investkorea8007 investkorea8007 96 8 4 16:06 ..
-rw-r--r-- 1 investkorea8007 investkorea8007 0 8 4 16:27 copy_123.txt
-rw-r--r-- 1 investkorea8007 investkorea8007 0 8 4 16:20 123.txt

# <복사본 파일 이름 변경>
$ mv copy_123.txt welcome.txt
$ ls -la
total 0
drwxr-xr-x 4 investkorea8007 investkorea8007 128 8 4 17:16 .
drwxr-xr-x 3 investkorea8007 investkorea8007 96 8 4 16:06 ..
-rw-r--r-- 1 investkorea8007 investkorea8007 0 8 4 16:27 welcome.txt
-rw-r--r-- 1 investkorea8007 investkorea8007 0 8 4 16:20 123.txt

# <파일 삭제>
$ rm welcome.txt
$ ls -la
total 0
drwxr-xr-x 3 investkorea8007 investkorea8007 96 8 4 17:20 .
drwxr-xr-x 3 investkorea8007 investkorea8007 96 8 4 16:06 ..
-rw-r--r-- 1 investkorea8007 investkorea8007 0 8 4 16:20 123.txt



## 권한 실습하기

<데스트 디렉토리 234 생성>
nvestcorea8007@c5r1s2 practice % mkdir 234_dir    
investcorea8007@c5r1s2 practice % 

<현재 권한 확인>
investcorea8007@c5r1s2 practice % ls -l
total 0
-rw-r--r--  1 investcorea8007  investcorea8007   0  8  4 16:20 123.txt
drwxr-xr-x  2 investcorea8007  investcorea8007  64  8  4 17:30 234_dir
investcorea8007@c5r1s2 practice % 

<파일권한 변경, 777은 모두에게 읽고 쓰고 실행할 권한을 부여>
investcorea8007@c5r1s2 practice % ls -l
total 0
-rwxrwxrwx  1 investcorea8007  investcorea8007   0  8  4 16:20 123.txt
drwxr-xr-x  2 investcorea8007  investcorea8007  64  8  4 17:30 234_dir
investcorea8007@c5r1s2 practice % 

<디렉토리 권한변경, 700은 나 이외에는 아무도 못보게 디렉토리를 꽉 잠그겠다는 뜻>
investcorea8007@c5r1s2 practice % chmod 700 234_dir    
investcorea8007@c5r1s2 practice % ls -l
total 0
-rwxrwxrwx  1 investcorea8007  investcorea8007   0  8  4 16:20 123.txt
drwx------  2 investcorea8007  investcorea8007  64  8  4 17:30 234_dir
investcorea8007@c5r1s2 practice % 



## Docker 설치 및 기본 점검하기

<도커 버전 확인>
investcorea8007@c5r1s2 practice % docker --version
Docker version 29.4.0, build 9d7ad9f
investcorea8007@c5r1s2 practice % 

<도커 엔진(데몬) 동작 여부 확인하기>
investcorea8007@c5r1s2 practice % docker info
Client:
 Version:    29.4.0
 Context:    orbstack
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.33.0
    Path:     /Users/investcorea8007/.docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
    Version:  v5.1.2
    Path:     /Users/investcorea8007/.docker/cli-plugins/docker-compose

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 29.4.0
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
 containerd version: 301b2dac98f15c27117da5c8af12118a041a31d9
 runc version: c241c0bb5e60a8e8c1b2e53d4eca8d0068d8d57e
 init version: de40ad0
 Security Options:
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 7.0.11-orbstack-00360-gc9bc4d96ac70
 Operating System: OrbStack
 OSType: linux
 Architecture: x86_64
 CPUs: 6
 Total Memory: 15.69GiB
 Name: orbstack
 ID: 26b3b55f-d3da-4981-9474-00895402b8e4
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 HTTP Proxy: http://proxy.orb.internal:8305
 HTTPS Proxy: http://proxy.orb.internal:8305
 No Proxy: localhost,127.0.0.1,127.0.0.0/8,::1,10.0.0.0/8,172.16.0.0/12,192.168.0.0/16,0.250.250.0/24,*.orb.internal,*.local,gateway.docker.internal,host.internal,host.docker.internal,host.lima.internal,docker.for.mac.localhost,docker.for.mac.host.internal
 Experimental: true
 Insecure Registries:
  127.0.0.0/8
  ::1/128
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
 Firewall Backend: iptables

WARNING: DOCKER_INSECURE_NO_IPTABLES_RAW is set
investcorea8007@c5r1s2 practice % 

<가벼운 테스트용 이미지 다운로드 및 실행하기>
investcorea8007@c5r1s2 practice % docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
4f55086f7dd0: Pull complete 
d5e71e642bf5: Download complete 
Digest: sha256:c3cbe1cc1aa588a64951ac6286e0df7b27fe2e6324b1001c619bb358770c0178
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

investcorea8007@c5r1s2 practice % 

<다운로드 된 이미지 목록 확인>
investcorea8007@c5r1s2 practice % docker images
                                                                     i Info →   U  In Use
IMAGE                ID             DISK USAGE   CONTENT SIZE   EXTRA
hello-world:latest   c3cbe1cc1aa5       21.8kB         9.49kB    U   
investcorea8007@c5r1s2 practice % 

<실행 중이거나 종료된 컨테이너 목록 확인>
investcorea8007@c5r1s2 practice % docker ps -a          
CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES
34a44472af3b   hello-world   "/hello"   6 minutes ago   Exited (0) 6 minutes ago             gracious_goldstine
investcorea8007@c5r1s2 practice % 


## 웹서버 소스코드 및 Dockerfile 만들기

<web-server 폴더를 만들어 그안에 들어갔음>
investcorea8007@c5r1s2 practice % cd ~/codyssey/practice
investcorea8007@c5r1s2 practice % mkdir web-server
investcorea8007@c5r1s2 practice % cd web-server
investcorea8007@c5r1s2 web-server % 

<웹서버용 html 만들기>
investcorea8007@c5r1s2 web-server % echo "안녕 반가워 코디세이. 내 이름은 성우라고해!!" > index.html 
echo "안녕 반가워 코디세이. 내 이름은 성우라고해cd web-server" > index.html
investcorea8007@c5r1s2 web-server % 

<Dockerfile(설계도) 만들기>
investcorea8007@c5r1s2 web-server % echo -e "FROM nginx:alpine\nCOPY index.html /usr/share/nginx/html/index.html"
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
investcorea8007@c5r1s2 web-server % echo "FROM nginx:alpine" > Dockerfile
investcorea8007@c5r1s2 web-server % echo "COPY index.html /usr/share/nginx/html/index.html" >> Dockerfile
investcorea8007@c5r1s2 web-server % ls -la
total 16
drwxr-xr-x  4 investcorea8007  investcorea8007  128  8  4 18:31 .
drwxr-xr-x  5 investcorea8007  investcorea8007  160  8  4 18:14 ..
-rw-r--r--  1 investcorea8007  investcorea8007   67  8  4 18:32 Dockerfile
-rw-r--r--  1 investcorea8007  investcorea8007   74  8  4 18:19 index.html
investcorea8007@c5r1s2 web-server %                      

<나만의 커스텀 이미지 빌드하기 (조립하기)>
investcorea8007@c5r1s2 web-server % docker build -t my-web:1.0 .         
[+] Building 7.5s (7/7) FINISHED                                               docker:orbstack
 => [internal] load build definition from Dockerfile                                      0.1s
 => => transferring dockerfile: 104B                                                      0.0s
 => [internal] load metadata for docker.io/library/nginx:alpine                           2.2s
 => [internal] load .dockerignore                                                         0.2s
 => => transferring context: 2B                                                           0.0s
 => [internal] load build context                                                         0.3s
 => => transferring context: 111B                                                         0.0s
 => [1/2] FROM docker.io/library/nginx:alpine@sha256:4a73073bd557c65b759505da037898b61f1  3.3s
 => => resolve docker.io/library/nginx:alpine@sha256:4a73073bd557c65b759505da037898b61f1  0.2s
 => => sha256:46519e7231d2eb5604df229beb44d59719a489eaa7aca52982535a01 20.31MB / 20.31MB  0.5s
 => => sha256:d0008c891db48b5f526d914bce9e8d889fe1a9d1f08291ae03fe97f871 1.21kB / 1.21kB  0.4s
 => => sha256:46f977ee452f4399c208714afa034868d6056864f8a0cf3c643ab143dd802c 404B / 404B  0.6s
 => => sha256:390dc935348d8070e695fbaae2a4bb114fb9e69c59f628e7576036ee9d 1.40kB / 1.40kB  0.6s
 => => sha256:1223f016b4e4a2c21f7c49d4837fbfd47a9da6436b511690ca1e582fc2810d 627B / 627B  0.2s
 => => sha256:62bec68d7c31c4c8a19d812d84da5f7748e54690c037979945b6c5b6c924b1 957B / 957B  0.2s
 => => sha256:3cd534fe98c64d68a1f4f1c83abb8d5cba7ecfd7be88e592389929d12e 1.89MB / 1.89MB  0.3s
 => => sha256:55afa1ecc21d2bb5e5045f32dafee56272ffd89860bac26f6c32123439 3.85MB / 3.85MB  0.3s
 => => extracting sha256:55afa1ecc21d2bb5e5045f32dafee56272ffd89860bac26f6c32123439af26a  0.2s
 => => extracting sha256:3cd534fe98c64d68a1f4f1c83abb8d5cba7ecfd7be88e592389929d12e6253d  0.2s
 => => extracting sha256:1223f016b4e4a2c21f7c49d4837fbfd47a9da6436b511690ca1e582fc2810d5  0.1s
 => => extracting sha256:62bec68d7c31c4c8a19d812d84da5f7748e54690c037979945b6c5b6c924b14  0.1s
 => => extracting sha256:46f977ee452f4399c208714afa034868d6056864f8a0cf3c643ab143dd802c8  0.1s
 => => extracting sha256:d0008c891db48b5f526d914bce9e8d889fe1a9d1f08291ae03fe97f871726f3  0.1s
 => => extracting sha256:390dc935348d8070e695fbaae2a4bb114fb9e69c59f628e7576036ee9d5244c  0.1s
 => => extracting sha256:46519e7231d2eb5604df229beb44d59719a489eaa7aca52982535a010b07a9e  0.5s
 => [2/2] COPY index.html /usr/share/nginx/html/index.html                                0.3s
 => exporting to image                                                                    0.9s
 => => exporting layers                                                                   0.5s
 => => exporting manifest sha256:0ef53b8236e47f6353cd45f9fb2a777dd5aafa5690854de91b9fee4  0.1s
 => => exporting config sha256:382e5087a1984193c9000a4c8a5e54500f48d4cbb886f90139c04ae3a  0.1s
 => => exporting attestation manifest sha256:b0fb816aba14e1de2bc31a20e2455fe4a0dd55beaa0  0.1s
 => => exporting manifest list sha256:241dc03559027eb85feb8a68b2546a2d0ab3ebf94c74f806c0  0.1s
 => => naming to docker.io/library/my-web:1.0                                             0.0s
 => => unpacking to docker.io/library/my-web:1.0                                          0.1s
investcorea8007@c5r1s2 web-server % 

<컨테이너 실행 및 포트 연결하기(포트매핑)>
investcorea8007@c5r1s2 web-server % docker build -t my-web:1.0 .         
[+] Building 7.5s (7/7) FINISHED                                               docker:orbstack
 => [internal] load build definition from Dockerfile                                      0.1s
 => => transferring dockerfile: 104B                                                      0.0s
 => [internal] load metadata for docker.io/library/nginx:alpine                           2.2s
 => [internal] load .dockerignore                                                         0.2s
 => => transferring context: 2B                                                           0.0s
 => [internal] load build context                                                         0.3s
 => => transferring context: 111B                                                         0.0s
 => [1/2] FROM docker.io/library/nginx:alpine@sha256:4a73073bd557c65b759505da037898b61f1  3.3s
 => => resolve docker.io/library/nginx:alpine@sha256:4a73073bd557c65b759505da037898b61f1  0.2s
 => => sha256:46519e7231d2eb5604df229beb44d59719a489eaa7aca52982535a01 20.31MB / 20.31MB  0.5s
 => => sha256:d0008c891db48b5f526d914bce9e8d889fe1a9d1f08291ae03fe97f871 1.21kB / 1.21kB  0.4s
 => => sha256:46f977ee452f4399c208714afa034868d6056864f8a0cf3c643ab143dd802c 404B / 404B  0.6s
 => => sha256:390dc935348d8070e695fbaae2a4bb114fb9e69c59f628e7576036ee9d 1.40kB / 1.40kB  0.6s
 => => sha256:1223f016b4e4a2c21f7c49d4837fbfd47a9da6436b511690ca1e582fc2810d 627B / 627B  0.2s
 => => sha256:62bec68d7c31c4c8a19d812d84da5f7748e54690c037979945b6c5b6c924b1 957B / 957B  0.2s
 => => sha256:3cd534fe98c64d68a1f4f1c83abb8d5cba7ecfd7be88e592389929d12e 1.89MB / 1.89MB  0.3s
 => => sha256:55afa1ecc21d2bb5e5045f32dafee56272ffd89860bac26f6c32123439 3.85MB / 3.85MB  0.3s
 => => extracting sha256:55afa1ecc21d2bb5e5045f32dafee56272ffd89860bac26f6c32123439af26a  0.2s
 => => extracting sha256:3cd534fe98c64d68a1f4f1c83abb8d5cba7ecfd7be88e592389929d12e6253d  0.2s
 => => extracting sha256:1223f016b4e4a2c21f7c49d4837fbfd47a9da6436b511690ca1e582fc2810d5  0.1s
 => => extracting sha256:62bec68d7c31c4c8a19d812d84da5f7748e54690c037979945b6c5b6c924b14  0.1s
 => => extracting sha256:46f977ee452f4399c208714afa034868d6056864f8a0cf3c643ab143dd802c8  0.1s
 => => extracting sha256:d0008c891db48b5f526d914bce9e8d889fe1a9d1f08291ae03fe97f871726f3  0.1s
 => => extracting sha256:390dc935348d8070e695fbaae2a4bb114fb9e69c59f628e7576036ee9d5244c  0.1s
 => => extracting sha256:46519e7231d2eb5604df229beb44d59719a489eaa7aca52982535a010b07a9e  0.5s
 => [2/2] COPY index.html /usr/share/nginx/html/index.html                                0.3s
 => exporting to image                                                                    0.9s
 => => exporting layers                                                                   0.5s
 => => exporting manifest sha256:0ef53b8236e47f6353cd45f9fb2a777dd5aafa5690854de91b9fee4  0.1s
 => => exporting config sha256:382e5087a1984193c9000a4c8a5e54500f48d4cbb886f90139c04ae3a  0.1s
 => => exporting attestation manifest sha256:b0fb816aba14e1de2bc31a20e2455fe4a0dd55beaa0  0.1s
 => => exporting manifest list sha256:241dc03559027eb85feb8a68b2546a2d0ab3ebf94c74f806c0  0.1s
 => => naming to docker.io/library/my-web:1.0                                             0.0s
 => => unpacking to docker.io/library/my-web:1.0                                          0.1s
investcorea8007@c5r1s2 web-server % docker run -d -p 8080:80 --name my-web-8080 my-web:1.0
1bd7401bef448d484b626818ef3c652001ff0dad743980a38f120ce5712e1476
investcorea8007@c5r1s2 web-server % 

<터미널에서 웹 접속 확인>
investcorea8007@c5r1s2 web-server % curl http://localhost:8080                              
안녕 반가워 코디세이. 내 이름은 성우라고해cd web-server
investcorea8007@c5r1s2 web-server % 

<브라우저에서 접속 확인>
/Users/investcorea8007/Library/Group Containers/group.com.apple.notes/Accounts/LocalAccount/Media/0B9D9760-47BE-4B7A-A104-3A8F7F7A2C5C/1_8AFCBF62-69E6-43FD-8E30-A16C3A258F7B/Pasted Graphic.png


## Docker 볼륨 영속성 검증하기

<전용 볼륨(금고) 만들기>
investcorea8007@c5r1s2 web-server % docker volume create mydata
mydata
investcorea8007@c5r1s2 web-server % 

<볼륨을 연결한 테스트용 컨테이너 실행>
investcorea8007@c5r1s2 web-server % docker run -d --name vol-test -v mydata:/data ubuntu sleep infinity
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
617772c7d19b: Pull complete 
a7fb98a8eddd: Pull complete 
cc2ffdbc1bf7: Download complete 
Digest: sha256:678c6550cc43645e08669028bc177f50be4e7c5b8cca677067b1914d4afc7a03
Status: Downloaded newer image for ubuntu:latest
6a89e3be333f1ef86744466940e9ed1c6ff608fd8724a7065d88521a95cc2f51
investcorea8007@c5r1s2 web-server % 

<컨테이너 안의 볼륨 폴더에 파일 만들고 내용 확인>
investcorea8007@c5r1s2 web-server % docker exec -it vol-test bash -c "echo 'Hello Persistence' > /data/test.txt && cat /data/test.txt"
Hello Persistence
investcorea8007@c5r1s2 web-server % 

<컨테이너 통째로 삭제>
investcorea8007@c5r1s2 web-server % docker rm -f vol-test
vol-test
investcorea8007@c5r1s2 web-server % 

<새로운 컨테이너를 띄워서 볼륨 폴더 속 데이터가 살아있는지 증명>
investcorea8007@c5r1s2 web-server % docker run -d --name vol-test2 -v mydata:/data ubuntu sleep infinity

docker exec -it vol-test2 bash -c "cat /data/test.txt"
00310861161d3b6678f44c9cc54e41689fb8fa19908e1f738de6e2e4f0e4c40d
Hello Persistence
investcorea8007@c5r1s2 web-server % 


## Git 사용자 정보 및 기본 브랜치 설정하기

<사용자 이름 등록>
investcorea8007@c5r1s2 web-server % git config --global user.name "Sung-woo Kim"
investcorea8007@c5r1s2 web-server % 

<이메일 등록>
investcorea8007@c5r1s2 web-server % git config --global user.email "investcorea@hanmail.net"
investcorea8007@c5r1s2 web-server %

<기본 브랜치 이름 설정>
investcorea8007@c5r1s2 web-server % git config --global init.defaultBranch main
investcorea8007@c5r1s2 web-server % 

<이름, 이메일, 브렌치가 잘 설정됐는지 확인>
investcorea8007@c5r1s2 web-server % git config --list
credential.helper=osxkeychain
user.name=Sung-woo Kim
user.email=investcorea@hanmail.net
init.defaultbranch=main
investcorea8007@c5r1s2 web-server %



## 📝 최종 과제 보완 및 트러블슈팅 보고서

### [평가 항목 #8, #17] 볼륨 백업 절차 및 바인드 마운트 대안
* **바인드 마운트 대안:** 볼륨 대신 호스트의 특정 폴더를 컨테이너에 직접 연결(Bind Mount)하여 데이터 영속성을 확보할 수 있습니다. (예: `-v ~/practice/data:/usr/share/nginx/html`)
* **볼륨 데이터 백업 및 복원 방법:**
  - **백업:** `docker cp <컨테이너명>:<컨테이너_경로> <호스트_경로>` 명령어를 통해 컨테이너 내부 데이터를 호스트로 백업합니다.
  - **복원:** 반대로 호스트의 백업 파일을 컨테이너 내부로 복사하여 복원할 수 있습니다.

### [평가 항목 #9] 원격 리포지토리 설정 및 Push 출력 로그
* **GitHub 링크:** https://github.com/investkorea7/web-server
* **원격 repo 등록 및 push 기록 (로그):**
  ```bash
  $ git remote add origin [https://github.com/investkorea7/web-server.git](https://github.com/investkorea7/web-server.git)
  $ git push -u origin main
  # [출력 결과]
  # To [https://github.com/investkorea7/web-server.git](https://github.com/investkorea7/web-server.git)
  #  * [new branch]      main -> main
  # Branch 'main' set up to track remote branch 'main' from 'origin'.
  ```

### [평가 항목 #10] 디렉토리 트리, 파일 역할 및 재현 절차
* **디렉토리 구조 및 역할:**
  ```text
  web-server/
  ├── Dockerfile   # 커스텀 웹 서버 이미지를 빌드하기 위한 인프라 환경 명세서 (설계 기준)
  ├── index.html   # Nginx 웹 서버가 구동될 때 화면에 노출될 정적 웹 페이지 소스 코드
  └── README.md    # 프로젝트 실행 방법과 설계 기준을 담은 가이드 문서
  ```
* **재현 절차 (재현성 확보):**
  1. 저장소 복제: `git clone https://github.com/investkorea7/web-server.git`
  2. 디렉토리 이동: `cd web-server`
  3. 이미지 빌드: `docker build -t my-web:1.0 .`
  4. 컨테이너 실행: `docker run -d -p 8080:80 my-web:1.0`

### [평가 항목 #12] 이미지와 컨테이너의 차이점 요약
* **이미지:** 애플리케이션 실행에 필요한 모든 것이 포함된 **불변성(Immutable)**을 가진 정적 파일입니다. (실행 및 변경 불가)
* **컨테이너:** 이미지를 기반으로 메모리에 로드되어 격리된 상태로 **실행** 중인 프로세스 공간입니다. 내부에 읽기/쓰기 레이어가 있어 **변경**이 가능합니다.

### [평가 항목 #13] 컨테이너 포트 노출 이유 및 보안 고려사항
* **포트 노출 이유:** 컨테이너는 호스트와 격리된 **네임스페이스(Namespace)**를 사용하므로, 외부(브라우저)에서 접근하려면 호스트 포트와 컨테이너 포트를 연결해야 합니다.
* **보안 관점:** 모든 포트를 열지 않고, 웹 서비스에 필요한 최소한의 특정 포트(예: 80번)만 제한적으로 개방하여 **보안** 위협을 최소화합니다.

### [평가 항목 #14] 호스트/컨테이너 간 경로 선택 기준
* **권장 경로 사용 기준:** 프로젝트의 **재현성**과 다른 환경에서의 **이식성**을 보장하기 위해, 호스트 경로는 명확한 **절대 경로**(`~/codyssey/practice`)를 기준으로 삼습니다. 컨테이너 경로는 내부 환경이 고정적이므로 리눅스 표준 **절대 경로**(`/usr/share/nginx/html`)를 사용합니다.

### [평가 항목 #15] 리눅스 파일 권한 (755/644 규칙 및 rwx 비트)
* **숫자 의미:** r(읽기=4), w(쓰기=2), x(실행=1) 비트의 합.
* **755 (디렉토리 및 실행파일):** **소유자**는 모든 권한(rwx=7), **그룹**과 기타 사용자는 읽기/실행(r-x=5) 권한을 가집니다.
* **644 (일반 파일):** **소유자**는 읽기/쓰기(rw-=6), **그룹**과 기타 사용자는 읽기(r--=4) 권한만 가져, 타인의 임의 수정을 방지합니다.

### [평가 항목 #16] 포트 충돌 진단 및 해결 순서
1. **포트 점검:** `netstat -tuln | grep 8080` 명령으로 8080 포트 사용 여부 확인
2. **프로세스 확인:** `lsof -i :8080` 또는 `ps aux | grep 8080` 명령으로 충돌 프로세스 식별
3. **해결 순서:** 기존 프로세스 종료(`kill -9 PID`) 또는 도커 실행 시 충돌하지 않는 다른 포트로 변경(`-p 8081:80`)

### [평가 항목 #18] 트러블슈팅 사례 (가설-확인-조치)
* **이슈:** `curl localhost:8080` 접속 실패 및 연결 거부(Connection refused).
* **가설:** 포트 포워딩(`-p 8080:80`) 옵션이 누락되었거나 Nginx 프로세스가 정상 작동하지 않을 것이다.
* **확인(검증):** `docker ps` 명령어로 포트 매핑 상태를 확인하고, `docker logs`로 컨테이너 내부 에러를 점검.
* **조치:** 포트 매핑이 누락된 것을 확인 후, 컨테이너를 삭제하고 `-p 8080:80` 옵션을 추가하여 재실행 후 정상 작동 확인.