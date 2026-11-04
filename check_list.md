# E1-1 작업 체크리스트 (check_list.md)

> 작업용 문서입니다. **체크 상태의 기준은 이 파일 하나**입니다. 실제 수행 로그와 증거(명령+출력, 스크린샷)는 [README.md](README.md)의 같은 번호 섹션에 기록합니다.
> 명령은 Git Bash(Windows) 또는 Linux/macOS 터미널 기준입니다. 기록하는 로그에는 토큰·비밀번호·개인키·인증 코드·이메일을 남기지 않습니다.

## 진행 방법

1. 단계(`T00`~`T16`, 보너스 `B1`~`B5`)를 순서대로 실행한다.
2. 각 단계의 명령을 실행하고 **명령 + 출력**을 README의 같은 번호 섹션에 코드블록으로 붙인다.
3. 스크린샷은 `docs/evidence/`에 저장하고 README에서 링크한다. (명령 입력과 출력이 함께 보여야 한다.)
4. 단계를 마치면 아래 체크박스를 `[x]`로 바꾸고 **단계별로 커밋**한다. (예: `git commit -m "T05: docker basic ops"`)
5. 보안 점검은 **T15**에서 수행한다.

## 마스터 체크리스트

### 필수

- [ ] **T00** 저장소 구조 생성 (`docs/evidence/`, `site/`, `site-bind/`, `compose/`, `.gitignore`)
- [ ] **T01** 실행 환경 기록 (OS/쉘/터미널, Docker·Git·VSCode 버전)
- [ ] **T02** 터미널 기본 조작
- [ ] **T03** 권한 실습 (파일 1 + 디렉토리 1, 변경 전/후)
- [ ] **T04** Docker 설치 및 기본 점검
- [ ] **T05** Docker 기본 운영 명령
- [ ] **T06** 컨테이너 실행 실습 (hello-world, ubuntu, attach/exec 차이)
- [ ] **T07** 기존 Dockerfile 기반 커스텀 이미지
- [ ] **T08** 포트 매핑 접속 증거 (2회 이상)
- [ ] **T09** 바인드 마운트 반영
- [ ] **T10** Docker 볼륨 영속성
- [ ] **T11** Git 설정
- [ ] **T12** GitHub 연동 + VSCode 연동
- [ ] **T13** 트러블슈팅 2건 이상 (실제 사례)
- [ ] **T14** 미션 회고
- [ ] **T15** 보안 점검
- [ ] **T16** 최종 제출 점검 (클린 클론 재현)

### 보너스

- [ ] **B1** Compose 기초 (단일 서비스)
- [ ] **B2** Compose 멀티 컨테이너
- [ ] **B3** Compose 운영 명령어
- [ ] **B4** 환경 변수 활용
- [ ] **B5** GitHub SSH 키

## 미션 요구사항 ↔ 단계 매핑

| 미션 요구사항 | 단계 |
|---|---|
| 제출 저장소(공개 또는 규칙에 맞는 권한), 링크만으로 산출물 확인 | T00, T12, T16 |
| 기술 문서: 개요 / 실행 환경 / 체크리스트 / 검증 방법 + 결과 링크 / 트러블슈팅 2건+ | README 전체, T13 |
| 터미널 조작 (위치·목록·이동·생성·복사·이동/이름변경·삭제·내용 확인·빈 파일) | T02 |
| 권한 실습 (파일 1 + 디렉토리 1, 전/후) | T03 |
| Docker 버전 / 데몬 확인 | T04 |
| 이미지·컨테이너·로그·리소스 운영 명령 | T05 |
| hello-world / ubuntu / 종료·유지(attach·exec) 차이 | T06 |
| Dockerfile 직접 작성, 커스텀 이미지 (베이스, 커스텀 포인트 목적, 빌드/실행 결과) | T07 |
| 포트 매핑 + 브라우저(주소창 포함)/curl 증거 | T08 |
| 바인드 마운트 반영 (전/후) | T09 |
| 볼륨 생성/연결/검증 + 삭제 전/후 | T10 |
| Git 사용자·기본 브랜치 + `git config --list` | T11 |
| GitHub 로그인·저장소 연동 + VSCode 연동 증거 | T12 |
| 보안·개인정보 마스킹, 노출 시 제거·재발급 | T15 |
| 학습 목표 6개 | T02, T03, T07, T08, T10, T11~T12, T14 |
| 모든 작업 CLI 기반, Dockerfile 직접 작성, 포트/마운트/볼륨 직접 설정·검증 | 전 단계 |
| 재현성 (README만으로 재현, 개인 PC 종속 경로 대체 방법) | T16, 재현성 노트 |
| 보너스 (Compose, 멀티 컨테이너, 운영 명령, 환경 변수, SSH 키) | B1~B5 |

---

## T00. 저장소 구조 생성

```bash
cd ~/Desktop/all-in-one/e1-1      # 본인 저장소 경로 (개인 PC 종속, 재현성 노트 참고)
mkdir -p docs/evidence site site-bind compose

cat > .gitignore <<'EOF'
.env
*.pem
id_rsa*
id_ed25519*
*.key
EOF

git status
```

웹 서버 소스는 정적 콘텐츠 방식이므로 `site/`가 소스 디렉토리다. (`app/`은 만들지 않는다.)

```text
e1-1/
├─ README.md            # 제출용 보고서
├─ check_list.md        # 이 문서
├─ Dockerfile           # T07
├─ site/                # 웹 서버 소스(정적 콘텐츠, T07)
├─ site-bind/           # 바인드 마운트 실습용 (T09)
├─ compose/             # 보너스
└─ docs/evidence/       # 스크린샷
```

## T01. 실행 환경 기록

```bash
uname -a
echo $SHELL
bash --version | head -1
git --version
docker --version          # T04 이후
code --version | head -1
docker info | grep -iE "Operating System|Server Version|Context"   # Docker 백엔드(WSL2) 확인, T04 이후
```

PowerShell: `$PSVersionTable.PSVersion`, `[System.Environment]::OSVersion`
결과를 README "실행 환경" 표에 실제 값으로 채운다.

## T02. 터미널 기본 조작

```bash
pwd
ls
ls -la
mkdir -p ~/codyssey/practice
cd ~/codyssey/practice
pwd
touch empty.txt
echo "hello workstation" > hello.txt
cat hello.txt
cp hello.txt hello_copy.txt
mv hello_copy.txt renamed.txt
mkdir sub && mv renamed.txt sub/
ls -la . sub
cd sub && cd ..                 # 상대 경로 이동
rm sub/renamed.txt
rmdir sub
ls -la
```

절대/상대 경로 예시는 실제 실행 결과를 보고 README 회고(T14)에 쓴다.

## T03. 권한 실습 (파일 1개 + 디렉토리 1개)

### 3-1. 호스트(Git Bash)에서 시도

```bash
cd ~/codyssey/practice
touch perm_test.txt && mkdir perm_dir
ls -l perm_test.txt
ls -ld perm_dir
chmod 600 perm_test.txt && ls -l perm_test.txt
chmod 755 perm_test.txt && ls -l perm_test.txt
chmod 644 perm_test.txt && ls -l perm_test.txt
chmod 700 perm_dir && ls -ld perm_dir
```

Windows(NTFS)에서는 `chmod`가 반영되지 않을 수 있다. 반영되지 않으면 3-2로 수행하고 그 사실을 T13 트러블슈팅 후보로 기록한다.

### 3-2. 컨테이너(Linux)에서 수행 — root는 권한 거부가 일어나지 않으므로 일반 사용자로 실습

```bash
docker run -it --name perm-lab ubuntu:22.04 bash
```

컨테이너 안에서:

```bash
useradd -m dev && su dev
cd ~
touch perm_test.txt && mkdir perm_dir
ls -l perm_test.txt && ls -ld perm_dir                       # 변경 전

chmod 600 perm_test.txt && ls -l perm_test.txt
chmod 755 perm_test.txt && ls -l perm_test.txt
chmod 644 perm_test.txt && ls -l perm_test.txt

echo hi > perm_dir/a.txt
chmod u-x perm_dir && ls -ld perm_dir
cd perm_dir                                                  # x 제거: 진입 거부 확인
ls -l perm_dir                                               # x 제거: 내부 항목 상세 조회 거부 확인
chmod 755 perm_dir && cd perm_dir && ls -l && cd ..          # 복구 확인

chmod u+x,g-r,o-r perm_test.txt && ls -l perm_test.txt       # 기호 모드
exit
exit
```

```bash
docker rm -f perm-lab
```

권한 해석: r=4, w=2, x=1, 숫자는 합산(755=rwx r-x r-x, 644=rw- r-- r--). 디렉토리의 x는 진입(cd) 및 내부 항목 접근 가능 여부다.

## T04. Docker 설치 및 기본 점검

```powershell
# PowerShell, 관리자 권한/재부팅이 필요할 수 있음
winget install -e --id Docker.DockerDesktop
```

설치 후 Docker Desktop을 실행하고 터미널을 새로 연다.

```bash
docker --version
docker info
docker version
docker compose version
```

`docker info`에 `Server:`가 보이면 데몬 동작 중이다. 데몬 연결 오류가 나면 Docker Desktop 실행 여부를 확인하고 T13 트러블슈팅 후보로 기록한다.

## T05. Docker 기본 운영 명령

```bash
docker pull nginx:1.27-alpine
docker pull ubuntu:22.04
docker images

docker run -d --name ops-nginx nginx:1.27-alpine
docker ps
docker stop ops-nginx
docker ps
docker ps -a
docker start ops-nginx

docker logs ops-nginx
docker logs --tail 5 ops-nginx
docker stats --no-stream

docker rm -f ops-nginx
```

## T06. 컨테이너 실행 실습

```bash
# 1) hello-world
docker run hello-world

# 2) ubuntu 진입 (Git Bash에서 TTY 오류가 나면 winpty 접두)
docker run -it --name my-ubuntu ubuntu:22.04 bash
#   (내부) ls ; echo "hello from ubuntu" ; cat /etc/os-release ; exit
docker ps -a

# 3) 종료/유지 차이 관찰: -dit 로 stdin/TTY를 연결해야 attach·detach 가 동작한다
docker run -dit --name keep-alive ubuntu:22.04 sleep infinity
docker exec -it keep-alive bash
#   (내부) echo exec-test ; exit
docker ps                                   # exec 에서 exit 해도 컨테이너 유지 관찰

docker attach keep-alive
#   Ctrl+P, Ctrl+Q 로 detach
docker ps                                   # detach 후에도 컨테이너 유지 관찰

docker attach keep-alive
#   Ctrl+C 입력 → PID 1(sleep)이 Ctrl+C 를 무시하는지 관찰 (종료 안 될 수 있음)
#   다른 터미널에서: docker ps
docker rm -f keep-alive my-ubuntu
```

관찰 결과(실제로 일어난 일)를 README T06에 표로 정리한다. 미리 정한 가설을 그대로 쓰지 않는다.

## T07. 기존 Dockerfile 기반 커스텀 이미지

- 방식: (A) 웹 서버 베이스 이미지 활용 — `nginx:1.27-alpine` (버전 고정) + 정적 콘텐츠/설정 교체
- 커스텀 포인트와 목적:

| 커스텀 포인트 | 목적 |
|---|---|
| `COPY site/ ...` | 기본 페이지를 내 정적 콘텐츠로 교체 |
| `LABEL ...title` | 이미지 메타데이터로 출처/용도 식별 |
| `ENV APP_ENV=dev` | 설정(모드)을 코드와 분리 |
| `HEALTHCHECK` | 컨테이너 정상 여부를 Docker가 판단 |

```bash
cat > site/index.html <<'EOF'
<!doctype html>
<html lang="ko">
<head><meta charset="utf-8"><title>E1-1 작업실</title></head>
<body>
  <h1>Hello, 개발자 작업실!</h1>
  <p>Served by nginx in Docker - v1</p>
</body>
</html>
EOF

cat > Dockerfile <<'EOF'
FROM nginx:1.27-alpine
LABEL org.opencontainers.image.title="my-custom-nginx"
ENV APP_ENV=dev
COPY site/ /usr/share/nginx/html/
HEALTHCHECK --interval=10s --timeout=3s CMD wget -qO- http://localhost/ >/dev/null || exit 1
EOF

docker build -t my-custom-nginx:1.0 .
docker images my-custom-nginx
docker run -d --name my-web-test my-custom-nginx:1.0
docker ps
docker inspect --format '{{json .Config.Labels}} {{.Config.Env}}' my-web-test
docker rm -f my-web-test
```

## T08. 포트 매핑 접속 증거 (2회 이상)

```bash
docker run -d -p 8080:80 --name my-web-8080 my-custom-nginx:1.0
docker run -d -p 8081:80 --name my-web-8081 my-custom-nginx:1.0
docker ps
docker port my-web-8080
curl -i http://localhost:8080
curl -i http://localhost:8081

# 대조군: 포트 매핑 없음
docker run -d --name my-web-nomap my-custom-nginx:1.0
curl -m 3 http://localhost:80 || echo "접속 실패(매핑 없음) - 예상 결과"
docker rm -f my-web-nomap
```

브라우저로 `http://localhost:8080`, `http://localhost:8081`에 접속해 **주소창(포트 포함)과 응답 화면이 한 장에 보이게** 캡처한다.
저장: `docs/evidence/t08-browser-8080.png`, `docs/evidence/t08-browser-8081.png`

## T09. 바인드 마운트 반영

`site/`는 이미지에 들어간 v1과 일치해야 하므로 수정하지 않고 별도 디렉토리 `site-bind/`로 실습한다.

```bash
cp site/index.html site-bind/index.html

MSYS_NO_PATHCONV=1 docker run -d --name my-web-bind -p 8082:80 \
  -v "$(pwd -W 2>/dev/null || pwd)/site-bind":/usr/share/nginx/html:ro my-custom-nginx:1.0

curl http://localhost:8082                                   # 변경 전
cp site-bind/index.html /tmp/before.html
sed -i 's/v1/v2 (bind mount 반영)/' site-bind/index.html
diff /tmp/before.html site-bind/index.html                   # 호스트 변경 전/후 비교
curl http://localhost:8082                                   # 변경 후 (재시작/재빌드 없음)

docker inspect --format '{{json .Mounts}}' my-web-bind
docker rm -f my-web-bind
```

Linux/macOS는 `-v "$(pwd)/site-bind":...`로 충분하다.

## T10. Docker 볼륨 영속성

```bash
docker volume create mydata
docker volume ls
docker volume inspect mydata

docker run -d --name vol-test -v mydata:/data ubuntu:22.04 sleep infinity
docker exec vol-test bash -lc "echo 'persistence test' > /data/hello.txt && cat /data/hello.txt"
docker exec vol-test ls -l /data                              # 삭제 전

docker rm -f vol-test
docker ps -a --filter name=vol-test                           # 비어 있어야 함

docker run -d --name vol-test2 -v mydata:/data ubuntu:22.04 sleep infinity
docker exec vol-test2 bash -lc "cat /data/hello.txt"          # 삭제 후

# 대조군: 볼륨 없이 쓴 데이터는 컨테이너와 함께 사라짐
docker run --rm ubuntu:22.04 bash -lc "echo temp > /tmp/a.txt; cat /tmp/a.txt"
docker run --rm ubuntu:22.04 bash -lc "cat /tmp/a.txt || echo '없음(새 컨테이너)'"

docker rm -f vol-test2
docker volume rm mydata
```

## T11. Git 설정

```bash
git config --global user.name  "<이름>"
git config --global user.email "<GitHub 등록 이메일>"
git config --global init.defaultBranch main
git config --global core.editor "code --wait"
git branch -M main

git config --list
```

README에 `git config --list` 결과를 붙일 때 `user.email` 값은 `user.email=s***@***` 형태로 마스킹한다.

## T12. GitHub 연동 + VSCode 연동

```bash
git remote -v
git status
git add README.md check_list.md .gitignore Dockerfile site site-bind docs      # 파일을 지정해 추가 (git add . 지양)
git commit -m "T12: connect GitHub and push mission log"
git push -u origin main
git log --oneline -5
```

VSCode: 좌하단 계정 아이콘 → *Sign in with GitHub* → 저장소 폴더 열기 → Source Control 패널 확인.
캡처(이메일/토큰 가림): `docs/evidence/t12-vscode-login.png`, `t12-vscode-scm.png`, `t12-github-repo.png`.
GitHub Settings에서 저장소 Visibility를 Public(또는 제출 규칙에 맞는 권한)으로 확인한다.

## T13. 트러블슈팅 (실제 사례 2건 이상)

실제로 겪은 문제만 README T13에 기록한다. 형식: 문제 → 원인 가설 → 확인(명령/출력) → 해결/대안.
이 저장소의 `Merge branch 'main'` 이력(`git log --oneline --graph --all`)에 push 거부/병합의 실제 흔적이 있을 수 있으므로 먼저 확인한다.
후보: Docker 데몬 연결 오류, Git Bash `-it` TTY 오류(`winpty`), 바인드 마운트 경로 오류(`MSYS_NO_PATHCONV`), `port is already allocated`, Windows `chmod` 미반영.

## T14. 미션 회고

README T14에 아래를 **예시를 들어 직접 서술**한다.
절대/상대 경로, 권한 r/w/x와 755/644, 커스텀 이미지(기존 Dockerfile 기반), 포트 매핑 필요성, Docker 볼륨, Git vs GitHub, 이미지와 컨테이너의 분리·격리·포트/스토리지 연결, 재현 가능한 환경.

## T15. 보안 점검

README, 이 문서, 지시서에는 검사 패턴이 적혀 있으므로 자기 매칭이 없게 패턴을 `[]`로 분리하고 안내 문서는 제외한다.

```bash
# 토큰/개인키 패턴 (패턴의 [] 분리로 이 명령 자체는 매칭되지 않음)
grep -rniE "gh[p]_[A-Za-z0-9]{20,}|github_pa[t]_|BEGIN [A-Z ]+PRIVATE KEY" \
  README.md docs Dockerfile site site-bind compose || echo "토큰/키 패턴 없음"

# 이메일 노출 검사
grep -rnE "[A-Za-z0-9._-]+@[A-Za-z0-9.-]+\.[a-z]{2,}" \
  README.md docs Dockerfile site site-bind compose || echo "이메일 없음"

# 히스토리 검사
git log -p -- README.md docs Dockerfile site site-bind compose \
  | grep -nE "gh[p]_[A-Za-z0-9]{20,}|github_pa[t]_|BEGIN [A-Z ]+PRIVATE KEY" || echo "히스토리에도 없음"
```

- [ ] 스크린샷의 이메일/계정/토큰 부분을 가렸다
- [ ] `git config --list` 출력에 자격 증명이 없고 이메일이 마스킹되었다
- [ ] 노출이 의심되면: 문서/히스토리에서 제거 후 토큰/키를 폐기(revoke)하고 재발급

## T16. 최종 제출 점검

- [ ] 저장소가 Public(또는 규칙에 맞는 권한)이다
- [ ] 저장소 링크만으로 README, `Dockerfile`, `site/`, `docs/evidence/`가 모두 열람된다
- [ ] README의 모든 체크리스트 항목에 결과 링크가 있고 깨지지 않는다(이미지 포함)
- [ ] 모든 명령/출력이 코드블록이다
- [ ] 브라우저 증거에 주소창(포트 포함)과 응답 화면이 함께 있다
- [ ] 캡처/로그에 명령 입력과 출력이 함께 있다
- [ ] 클린 클론 재현 테스트 통과

```bash
git clone https://github.com/yong05610/e1-1.git /tmp/e1-1-verify && cd /tmp/e1-1-verify
docker build -t my-custom-nginx:verify . && docker run -d -p 8090:80 --name verify my-custom-nginx:verify
curl http://localhost:8090
docker rm -f verify
# T09: site-bind 로 바인드 마운트 재현, T10: 볼륨 재현은 README 절차대로 수행
```

---

## 보너스

### B1. Compose 기초 (단일 서비스)

`compose/docker-compose.yml`:

```yaml
services:
  web:
    build: ..
    image: my-custom-nginx:compose
    ports:
      - "${HOST_PORT:-8083}:80"
```

```bash
cd compose
docker compose up -d
curl http://localhost:8083
docker compose down        # B2와 같은 8083 포트를 쓰므로 다음 실습 전에 반드시 내린다
```

### B2. Compose 멀티 컨테이너

```yaml
services:
  web:
    build: ..
    ports:
      - "${HOST_PORT:-8083}:80"
    depends_on:
      - cache
  cache:
    image: redis:7.4-alpine
```

```bash
docker compose up -d
docker compose ps
docker compose exec cache redis-cli ping              # PONG
docker compose exec web nslookup cache                # 서비스명 DNS 해석
docker compose exec web ping -c 2 cache               # 서비스명으로 통신
docker network ls
docker compose down
```

### B3. Compose 운영 명령어

```bash
docker compose up -d
docker compose ps
docker compose logs --tail 20
docker compose down
docker compose ps
```

### B4. 환경 변수 활용

```bash
docker run -d --name env-test -e APP_ENV=prod -p 8084:80 my-custom-nginx:1.0
docker exec env-test printenv APP_ENV
docker rm -f env-test

cd compose
HOST_PORT=8085 docker compose up -d                   # B1 yaml의 ${HOST_PORT:-8083} 사용
docker compose ps
curl http://localhost:8085
docker compose down
```

### B5. GitHub SSH 키

```bash
ssh-keygen -t ed25519 -C "<GitHub 이메일>"
cat ~/.ssh/id_ed25519.pub        # 공개키만 등록. 개인키는 절대 출력/공유/기록하지 않는다
# GitHub → Settings → SSH and GPG keys → New SSH key
ssh -T git@github.com
git remote set-url origin git@github.com:yong05610/e1-1.git
git remote -v
git commit --allow-empty -m "B5: ssh push test" && git push
```

---

## 정리(Cleanup) — 실습에서 만든 이름만 개별 삭제

```bash
docker rm -f ops-nginx my-ubuntu keep-alive perm-lab my-web-test my-web-8080 my-web-8081 \
  my-web-nomap my-web-bind vol-test vol-test2 env-test verify 2>/dev/null
docker volume rm mydata 2>/dev/null
docker rmi my-custom-nginx:1.0 my-custom-nginx:compose my-custom-nginx:verify 2>/dev/null
```

`docker volume prune`, `docker ps -aq | xargs docker rm -f`처럼 실습과 무관한 자원까지 지우는 명령은 쓰지 않는다.

## 재현성 노트

| 종속 항목 | 대체 방법 / 주의사항 |
|---|---|
| 저장소 로컬 경로 `C:\Users\<user>\Desktop\all-in-one\e1-1` | 임의 폴더에서 `git clone` 후 진행 |
| Windows Git Bash 경로 변환 | `MSYS_NO_PATHCONV=1`, `pwd -W` |
| Windows `-it` TTY 오류 | `winpty` 접두 |
| NTFS `chmod` 제한 | 컨테이너에서 일반 사용자로 실습(T03-2) |
| 호스트 포트 충돌 | 사용 중이면 다른 포트로 바꾸고 기록 |
| Docker Desktop 필요 | Linux는 Docker Engine으로 대체 |
| 이미지 태그 | `nginx:1.27-alpine`, `ubuntu:22.04`, `redis:7.4-alpine`으로 고정. Docker Desktop 백엔드(WSL2 여부)는 T01에서 기록 |
