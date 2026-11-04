# 내 컴퓨터에 개발자용 '작업실' 꾸미기 (E1-1)

터미널(Linux CLI), Docker, Git/GitHub를 직접 세팅하고 "같은 서비스를 여러 번 실행해도 재현되는 환경"을 만든 수행 결과 보고서입니다.

- 작업 계획과 단계별 체크 상태: [check_list.md](check_list.md)
- 웹 서버 소스: [`site/`](site/) · Dockerfile: [`Dockerfile`](Dockerfile) · 증거: [`docs/evidence/`](docs/evidence/)

---

## 1. 프로젝트 개요

| 항목 | 내용 |
|---|---|
| 목표 | 코드가 "내 컴퓨터에서만" 돌아가는 문제를 줄이고, 누구나 같은 방식으로 실행·배포·디버깅할 수 있는 개발 워크스테이션 구축 |
| 핵심 도구 | 리눅스 CLI(터미널), Docker(컨테이너), Git/GitHub(버전 관리·협업) |
| 수행 흐름 | 디렉토리·권한 정리 → Docker 설치/점검 → 컨테이너 실행/관리 → Dockerfile 웹 서버 → 포트 매핑 → 바인드 마운트/볼륨 → Git/GitHub 연동 |
| 적용 원칙 | 이미지와 컨테이너의 분리 · 격리된 실행 환경 · 포트/스토리지 연결 방식 |

---

## 2. 실행 환경

> 상태: 미수행 (T01에서 실제 출력으로 기록)

| 항목 | 값 |
|---|---|
| OS | |
| Shell / Terminal | |
| Docker | |
| Git | |
| VSCode | |
| 저장소 | https://github.com/yong05610/e1-1 |

---

## 3. 수행 체크리스트

체크 상태의 기준은 [check_list.md](check_list.md)입니다. 아래는 결과 위치 링크입니다.

- [ ] 터미널 기본 조작 및 폴더 구성 → [T02 결과](#t02)
- [ ] 권한 변경 실습 → [T03 결과](#t03)
- [ ] Docker 설치/점검 → [T04 결과](#t04)
- [ ] Docker 기본 운영 명령 → [T05 결과](#t05)
- [ ] hello-world 실행 → [T06 결과](#t06)
- [ ] Dockerfile 빌드/실행 → [T07 결과](#t07)
- [ ] 포트 매핑 접속(2회) → [T08 결과](#t08)
- [ ] 바인드 마운트 반영 → [T09 결과](#t09)
- [ ] 볼륨 영속성 → [T10 결과](#t10)
- [ ] Git 설정 → [T11 결과](#t11)
- [ ] GitHub/VSCode 연동 → [T12 결과](#t12)
- [ ] 트러블슈팅 2건 이상 → [T13 결과](#t13)
- [ ] 회고 → [T14 결과](#t14)
- [ ] 보안 점검 → [T15 결과](#t15)
- [ ] 최종 제출 점검(클린 클론 재현) → [T16 결과](#t16)

---

## 4. 단계별 수행 로그

각 단계는 실제 수행 후 `명령 + 출력`을 코드블록으로 기록합니다. 상태 표기는 "미수행"인 단계가 아직 실행되지 않은 단계입니다.

<a id="t01"></a>
### T01. 실행 환경

미수행

<a id="t02"></a>
### T02. 터미널 기본 조작

미수행

<a id="t03"></a>
### T03. 권한 실습

미수행

<a id="t04"></a>
### T04. Docker 설치 및 점검

미수행 (현재 PC에 Docker 미설치: `docker: command not found`)

<a id="t05"></a>
### T05. Docker 기본 운영 명령

미수행

<a id="t06"></a>
### T06. 컨테이너 실행 실습

미수행

<a id="t07"></a>
### T07. 기존 Dockerfile 기반 커스텀 이미지

미수행

<a id="t08"></a>
### T08. 포트 매핑 접속 증거

미수행

<a id="t09"></a>
### T09. 바인드 마운트 반영

미수행

<a id="t10"></a>
### T10. Docker 볼륨 영속성

미수행

<a id="t11"></a>
### T11. Git 설정

미수행

<a id="t12"></a>
### T12. GitHub 연동 + VSCode 연동

미수행

---

<a id="t13"></a>
## 5. 트러블슈팅

미수행 (실제로 겪은 문제 2건 이상을 기록)

---

<a id="t14"></a>
## 6. 미션 회고

미수행

---

<a id="t15"></a>
## 7. 보안 점검

미수행

---

<a id="t16"></a>
## 8. 최종 점검

미수행

---

## 9. 검증 방법 요약

| 단계 | 확인 명령 | 확인 내용 | 결과 위치 |
|---|---|---|---|
| T02 | `pwd`, `ls -la`, `cat`, `cp`, `mv`, `rm` | 터미널 조작 | [T02](#t02) |
| T03 | `ls -l`, `chmod` | 권한 전/후 | [T03](#t03) |
| T04 | `docker --version`, `docker info` | 설치·데몬 동작 | [T04](#t04) |
| T05 | `docker images`, `ps -a`, `logs`, `stats` | 운영 명령 | [T05](#t05) |
| T06 | `docker run hello-world`, `exec`, `attach` | 컨테이너 실습 | [T06](#t06) |
| T07 | `docker build`, `docker run`, `docker inspect` | 커스텀 이미지 | [T07](#t07) |
| T08 | `curl`, 브라우저 | 포트 매핑 접속 | [T08](#t08) |
| T09 | `curl`, `diff` | 바인드 마운트 반영 | [T09](#t09) |
| T10 | `docker exec cat` 전/후 | 볼륨 영속성 | [T10](#t10) |
| T11 | `git config --list` | Git 설정 | [T11](#t11) |
| T12 | `git push`, 스크린샷 | GitHub/VSCode 연동 | [T12](#t12) |
| T13 | 각 사례의 확인 명령 | 트러블슈팅 | [T13](#t13) |
| T14 | - | 회고 | [T14](#t14) |
| T15 | `grep`, `git log -p` | 민감정보 검사 | [T15](#t15) |
| T16 | `git clone` 후 T07~T10 재현 | 재현성 | [T16](#t16) |

---

## 10. 재현성

- 저장소를 `git clone` 한 뒤 [check_list.md](check_list.md)의 T07~T10 명령으로 동일 결과를 확인할 수 있습니다.
- 이미지 태그는 `nginx:1.27-alpine`, `ubuntu:22.04`, `redis:7.4-alpine`으로 고정합니다.
- 개인 PC 종속 사항(Windows Git Bash 경로 변환, `winpty`, NTFS `chmod` 제한 등)과 대체 방법은 [check_list.md의 재현성 노트](check_list.md#재현성-노트)에 있습니다.
