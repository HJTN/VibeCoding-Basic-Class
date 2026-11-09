# 7차시 "Vibe Coding 기초" 강의 슬라이드 설계

- 대상 Canva 디자인: `DAHWd29xxbw` ([VibeCoding] 7차시 강의 자료, 1920×1080, 1차시 덱 사본 45장)
- 참고: `docs/intermediate-products/seventh-course.md`, `docs/references/Google_Cloud_Infrastructure.pdf`, `docs/references/[2-2]Agent_Native_SaaS_Development.pdf`
- 대상: 대부분 IT 전공 1~2학년 → 용어는 정확히(영문 병기), 설명은 비유로 쉽게
- 원칙 (5·6차시와 동일)
  - 글은 최소화, 개조식. 설명글이 필요하면 **2줄 이내**
  - 개념 이미지는 Canva AI 일러스트(글자 없는 플랫 벡터, 파란 톤 `#5170ff`), 기술 스택·서비스는 공식 로고 이미지
  - 모든 슬라이드에 구어체 발표자 노트 (문장마다 빈 줄 1개)
- 제약: Canva MCP는 페이지 복제·삭제 불가 → 기존 45장을 재배치·재구성

## 시간표 (110분)

| 시간 | 내용 |
|---|---|
| 19:00 ~ 19:30 | PART 01 클라우드 플랫폼 개요 |
| 19:30 ~ 19:40 | 휴식 |
| 19:40 ~ 20:10 | PART 02 프론트엔드 · 백엔드 기술 스택과 배포 |
| 20:10 ~ 20:20 | 휴식 |
| 20:20 ~ 20:40 | PART 03 미니 프로젝트 기획 |
| 20:40 ~ 20:50 | 마무리 · Q&A |

## 확장한 교육 내용

### PART 01 클라우드 플랫폼 개요

- 클라우드 컴퓨팅: 인터넷으로 IT 자원(서버·스토리지·DB·네트워크)을 **필요할 때 빌려 쓰고 쓴 만큼 내는** 방식 (NIST 정의)
- 이전/이후: 최대 사용량을 추측해 서버를 사던 시대 → 몇 초 만에 만들고 지우는 "임시 자원"
- On-premise vs Cloud: 초기 비용(큼/거의 없음), 준비 기간(수 주/수 분), 확장(구매/클릭), 관리(직접/공급자)
- 주요 개념 4: 온디맨드(On-demand) · 종량제(Pay-as-you-go) · 탄력성(Auto Scaling) · 리전/영역(Region/Zone)
- 장점: 비용 절감, 확장성·민첩성, 자동화(패치·백업), 어디서나 접속
- 단점: 요금 폭탄(설정 실수), 벤더 종속(Lock-in), 네트워크 의존, 데이터 위치·보안 책임
- 가상화: 물리 서버 1대를 하이퍼바이저로 나눠 여러 VM처럼 사용 → 클라우드의 기반 기술
  - 자원 분할(서버 가상화), 자원 통합(클러스터링), 자원 가상화(가상 메모리)
- 책임 모델 진화: On-premise(전부 내가) → IaaS(OS부터 내가, Compute Engine·EC2) → PaaS(코드만, Cloud Run·App Engine) → SaaS(그냥 사용, Gmail·Notion)
  - 비유: Pizza as a Service (집에서 만들기 → 밀키트 → 배달 → 외식)
- Google Cloud: 구글 검색·YouTube와 같은 인프라, 전 세계 40개 이상 리전, 신규 가입 무료 크레딧($300)
- GCP 서비스 4분류: 컴퓨팅(Compute Engine · GKE · Cloud Run · Cloud Functions) / 스토리지·DB(Cloud Storage · Cloud SQL · Firestore) / 빅데이터(BigQuery · Pub/Sub) / AI(Vertex AI · Gemini API)
- 컴퓨팅 고르기: VM 통째로(Compute Engine) · 컨테이너 여러 개 관리(GKE) · 컨테이너 하나 서버리스(Cloud Run) · 함수 하나(Cloud Functions)
- Cloud Run: 컨테이너만 올리면 끝, 요청 없으면 0개(Scale-to-Zero) → 비용 0, 트래픽 늘면 자동 확장
- GCP vs AWS 대응표: Compute Engine↔EC2, Cloud Run↔App Runner, Cloud Functions↔Lambda, Cloud Storage↔S3
- 거버넌스 뼈대: Organization → Folder → Project → Resource, 권한은 위에서 아래로 상속, Project = 과금·신뢰 경계
- IAM: Who(사용자·그룹·서비스 계정) + Role(권한 묶음) + Where(리소스), 최소 권한 원칙

### PART 02 프론트엔드 · 백엔드 기술 스택과 배포

- 웹 서비스 = 식당: 홀(프론트엔드) · 주방(백엔드) · 창고(데이터베이스)
- 프론트엔드: 브라우저에서 사용자가 보고 누르는 화면, HTML(뼈대) · CSS(옷) · JavaScript(동작)
- FE 스택: React(점유율 1위, 생태계) · Next.js(React + 서버 렌더링, SEO) · Vue(배우기 쉬움) · Svelte(가볍고 빠름)
  - 단점: React(선택지가 너무 많음) · Next.js(개념이 많음) · Vue(채용 시장 작음) · Svelte(자료 적음)
- FE 배포 서비스: Vercel(Next.js 제작사, Git 연동 자동 배포) · Netlify · GitHub Pages(정적) · Cloudflare Pages · Firebase Hosting
- FE 배포 방법: GitHub push → Vercel에서 Import → Deploy → `*.vercel.app` 주소 발급 → push마다 자동 재배포
- 백엔드: 요청을 받아 데이터를 처리·저장하고 결과(JSON)를 돌려주는 보이지 않는 서버, API로 소통
- BE 스택: Node.js(Express·NestJS, JS 하나로 풀스택) · Python(FastAPI·Django, AI·데이터 강함) · Java(Spring Boot, 대규모·안정성)
- BE 배포 서비스: Railway · Render(무료 플랜 슬립 주의) · Google Cloud Run · Fly.io
- BaaS: Supabase(PostgreSQL + 인증) · Firebase(구글, 실시간 DB + 인증) → 백엔드를 빌려 쓰는 지름길
- BE 배포 방법: GitHub push → Railway "Deploy from GitHub repo" → 환경 변수(API 키) 등록 → 도메인 생성
- 배포 전 체크: API 키는 `.env`로 숨기고 GitHub에 올리지 않기, 무료 플랜 한도 확인, 로컬에서 먼저 실행 확인

### PART 03 미니 프로젝트 기획 (7차시 = 서비스 기획 단계)

- 원하는 역할: 프론트엔드 · 백엔드 · 풀스택(기획 포함) 중 하나 고르기
- 주제: **신입 회원의 입장에서 동아리 내 필요한 서비스**
- 세부 주제 예시 6: 동아리 FAQ 챗봇 · 행사 일정 캘린더 · 스터디 매칭 보드 · 장비·도서 대여 관리 · 출석 체크 · 선배 멘토 찾기
- 기획 방법: ① 문제 정의(누가·언제·무엇이 불편?) ② 최소 기능(MVP) 3개만
- [실습] Antigravity에 1페이지 기획서(`PLAN.md`) 작성 요청 프롬프트
- 일정: 7차시 기획 → 8차시 구현 · 발표

### 마무리

- Q&A, 다음 수업(8차시: 미니 프로젝트 구현 · 발표 · 운영진 모집) 안내, 기획서 준비해 오기

## 슬라이드 구성 (45장, 괄호는 원본 페이지 레이아웃)

| # | 내용 | 원본 | 시각 요소 |
|---|---|---|---|
| 1 | 표지 | p1 | |
| 2 | INDEX | p2 | |
| 3 | 오늘의 시간표 | p4 | 표 |
| 4 | PART 01 표지: 클라우드 플랫폼 | p3 | |
| 5 | 클라우드 컴퓨팅이란? | p5 | AI 일러스트 |
| 6 | 클라우드 이전 vs 이후 | p28 | AI 일러스트 2 |
| 7 | On-premise vs Cloud | p6 | 표 |
| 8 | 클라우드 주요 개념 4가지 | p7 | 카드 2×2 |
| 9 | 장점과 단점 | p8 | 카드 2×2 |
| 10 | 가상화 = 클라우드의 기반 | p13 | AI 일러스트 |
| 11 | 가상화 3가지 방식 | p9 | AI 아이콘 3 |
| 12 | 책임 모델의 진화 (IaaS · PaaS · SaaS) | p15 | 표 |
| 13 | 피자로 이해하기 | p16 | AI 일러스트 |
| 14 | Google Cloud 소개 | p30 | AI 일러스트 |
| 15 | GCP 서비스 4분류 | p14 | 카드 2×2 |
| 16 | 컴퓨팅 서비스 고르기 | p19 | 표 |
| 17 | Cloud Run (서버리스 컨테이너) | p33 | AI 일러스트 |
| 18 | GCP vs AWS | p40 | 표 |
| 19 | 거버넌스 뼈대: 리소스 계층 | p17 | 카드 3 |
| 20 | IAM: 누가 · 무엇을 · 어디에 | p10 | 카드 3 |
| 21 | 쉬는 시간 | p11 | |
| 22 | PART 02 표지: 기술 스택 · 배포 | p12 | |
| 23 | 식당으로 이해하는 웹 서비스 | p43 | AI 일러스트 |
| 24 | 프론트엔드란? | p21 | 코드 블록 |
| 25 | 프론트엔드 기술 스택 | p26 | 로고 3 |
| 26 | 프론트엔드 스택 장단점 | p27 | 표 |
| 27 | 프론트엔드 배포 서비스 | p36 | 로고 2 |
| 28 | 프론트엔드 배포 방법 | p29 | AI 일러스트 |
| 29 | 백엔드란? | p22 | 코드 블록 + AI 일러스트 |
| 30 | 백엔드 기술 스택 | p35 | 로고 3 |
| 31 | 백엔드 스택 장단점 | p18 | 카드 3 |
| 32 | 백엔드 배포 서비스 | p38 | 로고 2 |
| 33 | BaaS: 백엔드를 빌려 쓰기 | p39 | 로고 2 |
| 34 | 백엔드 배포 방법 | p20 | AI 일러스트 |
| 35 | 배포 전 체크 3가지 | p41 | 카드 3 |
| 36 | 쉬는 시간 | p24 | |
| 37 | PART 03 표지: 미니 프로젝트 기획 | p25 | |
| 38 | 여러분이 원하는 개발 역할은? | p42 | AI 일러스트 3 |
| 39 | 프로젝트 주제 | p31 | AI 일러스트 |
| 40 | 세부 주제 예시 6 | p34 | AI 일러스트 6 |
| 41 | 기획 2단계 (문제 정의 · MVP) | p32 | AI 일러스트 2 |
| 42 | [실습] 1페이지 기획서 만들기 | p23 | 코드 블록(프롬프트) |
| 43 | 7차시 → 8차시 일정 | p37 | AI 일러스트 2 |
| 44 | Q&A | p44 | |
| 45 | Thank you | p45 | |
