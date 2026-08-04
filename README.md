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
<현재위치 확인>
investcorea8007@c5r1s2 ~ % pwd 
/Users/investcorea8007

<폴더생성>
investcorea8007@c5r1s2 ~ % mkdir -p ~/codyssey/practice  
investcorea8007@c5r1s2 ~ %

<폴더목록>
nvestcorea8007@c5r1s2 ~ % ls -la
total 48
drwxr-x---+ 22 investcorea8007  investcorea8007   704  8  4 16:06 .
drwxr-xr-x   7 root             admin             224  8  3 19:58 ..
-r--------   1 investcorea8007  investcorea8007     8  8  3 11:43 .CFUserTextEncoding
drwxr-xr-x   5 investcorea8007  investcorea8007   160  8  4 15:29 .docker
-rw-r--r--@  1 investcorea8007  investcorea8007  8196  8  4 10:45 .DS_Store
drwx------  10 investcorea8007  investcorea8007   320  8  4 15:29 .orbstack
drwxr-xr-x   3 investcorea8007  investcorea8007    96  8  4 15:29 .ssh
drwx------+ 26 investcorea8007  investcorea8007   832  8  4 15:52 .Trash
drwxr-xr-x   3 investcorea8007  investcorea8007    96  8  3 11:46 .vscode
-rw-r--r--   1 investcorea8007  investcorea8007   154  8  4 15:29 .zprofile
-rw-------   1 investcorea8007  investcorea8007    20  8  4 15:38 .zsh_history
drwx------   6 investcorea8007  investcorea8007   192  8  4 15:38 .zsh_sessions
drwxr-xr-x   3 investcorea8007  investcorea8007    96  8  4 16:06 codyssey
drwx------+  7 investcorea8007  investcorea8007   224  8  4 15:52 Desktop
drwx------+  3 investcorea8007  investcorea8007    96  8  3 11:43 Documents
drwx------+  7 investcorea8007  investcorea8007   224  8  4 11:03 Downloads
drwx------@ 81 investcorea8007  investcorea8007  2592  8  4 15:29 Library
drwx------   4 investcorea8007  investcorea8007   128  8  4 09:51 Movies
drwx------+  3 investcorea8007  investcorea8007    96  8  3 11:43 Music
drwx------   4 investcorea8007  investcorea8007   160  8  4 15:29 OrbStack
drwx------+  4 investcorea8007  investcorea8007   128  8  3 11:43 Pictures
drwxr-xr-x+  4 investcorea8007  investcorea8007   128  8  3 11:43 Public
investcorea8007@c5r1s2 ~ % 

<폴더 안으로 이동>
nvestcorea8007@c5r1s2 ~ % cd ~/codyssey/practice
investcorea8007@c5r1s2 practice % 

<텍스트파일을 만듬>
investcorea8007@c5r1s2 practice % touch 123.txt
investcorea8007@c5r1s2 practice % 

<텍스트파일 확인>
investcorea8007@c5r1s2 practice % ls -la 
total 0
drwxr-xr-x  3 investcorea8007  investcorea8007  96  8  4 16:20 .
drwxr-xr-x  3 investcorea8007  investcorea8007  96  8  4 16:06 ..
-rw-r--r--  1 investcorea8007  investcorea8007   0  8  4 16:20 123.txt
investcorea8007@c5r1s2 practice % 

<123파일에 어떤 내용이 있는지 확인>
investcorea8007@c5r1s2 practice % cat 123.txt
investcorea8007@c5r1s2 practice % 

<123파일 카피본 만듬>
investcorea8007@c5r1s2 practice % cp 123.txt copy_123.txt
investcorea8007@c5r1s2 practice % ls -la
total 0
drwxr-xr-x  4 investcorea8007  investcorea8007  128  8  4 16:27 .
drwxr-xr-x  3 investcorea8007  investcorea8007   96  8  4 16:06 ..
-rw-r--r--  1 investcorea8007  investcorea8007    0  8  4 16:27 copy_123.txt
-rw-r--r--  1 investcorea8007  investcorea8007    0  8  4 16:20 123.txt
investcorea8007@c5r1s2 practice %

<카피파일 이름을 welcome로 바꿈>
investcorea8007@c5r1s2 practice % mv copy_123.txt welcome.txt
investcorea8007@c5r1s2 practice % ls -la
total 0
drwxr-xr-x  4 investcorea8007  investcorea8007  128  8  4 17:16 .
drwxr-xr-x  3 investcorea8007  investcorea8007   96  8  4 16:06 ..
-rw-r--r--  1 investcorea8007  investcorea8007    0  8  4 16:27 welcome.txt
-rw-r--r--  1 investcorea8007  investcorea8007    0  8  4 16:20 123.txt
investcorea8007@c5r1s2 practice % 

<123파일 삭제>
investcorea8007@c5r1s2 practice % rm welcome.txt
investcorea8007@c5r1s2 practice % ls -la
total 0
drwxr-xr-x  3 investcorea8007  investcorea8007  96  8  4 17:20 .
drwxr-xr-x  3 investcorea8007  investcorea8007  96  8  4 16:06 ..
-rw-r--r--  1 investcorea8007  investcorea8007   0  8  4 16:20 123.txt
investcorea8007@c5r1s2 practice %






### (1) 터미널 및 권한 실습
```bash
# 폴더 생성 및 확인
$ mkdir -p ~/codyssey/practice
$cd ~/codyssey/practice$ ls -la

# 권한 변경 실험
$ mkdir test_dir
$chmod 700 test_dir$ ls -l