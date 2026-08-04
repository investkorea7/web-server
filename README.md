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
# 폴더 생성 및 확인
$ mkdir -p ~/codyssey/practice
$cd ~/codyssey/practice$ ls -la

# 권한 변경 실험
$ mkdir test_dir
$chmod 700 test_dir$ ls -l