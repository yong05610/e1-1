# 🛠️ 내 컴퓨터에 개발자용 '작업실' 꾸미기

## 1. 미션 소개
개발은 코드를 작성하는 순간이 아니라, 환경을 세팅하는 순간부터 시작됩니다. 본 미션은 터미널(Linux CLI), Docker, Git/GitHub라는 현대 개발의 3대 필수 도구를 직접 세팅하며 "어디서나 재현 가능한 개발 환경"을 구축하는 것을 목표로 합니다.

---

## 2. 실행 환경 (Environment)
- **OS**: [작성 예: Windows 11 / macOS]
- **Shell/Terminal**: [작성 예: PowerShell / zsh]
- **Docker 버전**: [작성 필요: docker --version 결과]
- **Git 버전**: [작성 필요: git --version 결과]

---

## 3. 수행 항목 체크리스트
- [ ] 터미널 기본 조작 및 폴더 구성 (ls, cd, mkdir 등)
- [ ] 파일 및 디렉토리 권한 변경 실습 (chmod)
- [ ] Docker 설치 및 기본 점검 (version, info)
- [ ] Docker 기본 운영 명령 수행 (images, ps, logs, stats)
- [ ] 컨테이너 실행 실습 (hello-world, ubuntu)
- [ ] Dockerfile 기반 커스텀 웹 서버 이미지 제작
- [ ] 포트 매핑을 통한 브라우저 접속 확인
- [ ] 바인드 마운트 및 Docker 볼륨 영속성 검증
- [ ] Git 사용자 설정 및 GitHub 연동 완료

---

## 4. 터미널 조작 및 권한 실습 로그

### 4.1 기본 명령어 수행
~~~bash
# 현재 위치 확인
pwd

# 작업 디렉토리 생성 및 이동
mkdir -p ~/workspace/mission1
cd ~/workspace/mission1

# 빈 파일 생성 및 목록 확인
touch testfile.txt
ls -la
~~~

### 4.2 권한 변경 실습
- **대상**: testfile.txt
- **변경 전**: [작성 필요: ls -l 결과]
- **변경 명령**: chmod 644 testfile.txt
- **변경 후**: [작성 필요: ls -l 결과]

---

## 5. Docker 운영 및 검증

### 5.1 기본 점검
~~~bash
docker --version
docker info
~~~

### 5.2 컨테이너 실행 및 관리
~~~bash
# hello-world 실행
docker run hello-world

# ubuntu 컨테이너 진입 및 명령 수행
docker run -it --name my-ubuntu ubuntu bash
# (내부 진입 후) ls, echo "hello" 수행 후 exit
~~~

### 5.3 커스텀 Dockerfile 제작
- **베이스 이미지**: [작성 예: nginx:alpine]
- **커스텀 포인트**: 기본 index.html 파일을 교체함

**[Dockerfile 소스]**
~~~dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/
~~~

### 5.4 포트 매핑 및 접속 확인
- **실행 명령**: docker run -d -p 8080:80 --name my-web my-custom-nginx
- **접속 증거**: [브라우저 주소창이 포함된 스크린샷 또는 curl localhost:8080 결과]

---

## 6. 데이터 영속성 검증 (Volume)

### 6.1 Docker 볼륨 실습
~~~bash
# 볼륨 생성
docker volume create my-data

# 컨테이너 연결 및 데이터 쓰기
docker run -it --name vol-test -v my-data:/app/data ubuntu bash
# (내부) echo "persistence test" > /app/data/test.txt && exit

# 컨테이너 삭제 후 새 컨테이너에서 확인
docker rm -f vol-test
docker run -it --name vol-test2 -v my-data:/app/data ubuntu cat /app/data/test.txt
~~~
- **결과**: 컨테이너를 삭제하고 새로 만들어도 데이터가 유지됨을 확인.

---

## 7. Git & GitHub 연동

### 7.1 Git 설정 확인
~~~bash
git config --list
~~~

### 7.2 연동 증거
- [GitHub 저장소에 파일이 올라간 화면 캡처 또는 push 로그]

---

## 8. 트러블슈팅 (Troubleshooting)

### Case 1: 원격 저장소 충돌 (Rejected)
- **문제**: git push 시 'fetch first' 오류 발생.
- **원인**: GitHub에 이미 파일이 있어 로컬과 히스토리가 다름.
- **해결**: git pull origin main --allow-unrelated-histories로 해결.

### Case 2: Vim 편집기 종료 문제
- **문제**: Merge 메시지 창(Vim)에서 나가지지 않음.
- **원인**: Git 기본 편집기인 Vim의 사용법 미숙.
- **해결**: Esc -> :wq -> Enter 입력으로 저장 및 종료.

---

## 9. 미션 회고
- **절대 경로 vs 상대 경로**: [본인의 설명 작성]
- **파일 권한(755, 644)**: [본인의 설명 작성]
- **포트 매핑의 필요성**: [본인의 설명 작성]
- **Git과 GitHub의 차이**: [본인의 설명 작성]