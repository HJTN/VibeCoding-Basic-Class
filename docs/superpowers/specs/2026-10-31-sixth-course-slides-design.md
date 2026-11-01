# 6차시 "Vibe Coding 기초" 강의 슬라이드 설계

- 대상 Canva 디자인: `DAHWd1zuqiU` ([VibeCoding] 6차시 강의 자료, 1920×1080, 1차시 덱 사본 45장)
- 참고: `docs/intermediate-products/sixth-course.md` (별도 참고 PDF 없음 → 웹 검색 자료로 구성)
- 대상: 대부분 전공자 → 용어는 정확히(영문 병기), 화면은 이미지 중심
- 원칙 (5차시와 동일)
  - 글은 최소화, 개조식. 설명글이 필요하면 서술형 **2줄 이내**
  - 개념 이미지는 Canva AI 일러스트(글자 없는 플랫 벡터, 파란 톤 `#5170ff`)와 Canva 도형으로 새로 그림
  - 실습은 Antigravity IDE 에이전트에 입력할 **프롬프트 위주**, 어두운 코드 블록으로 표시
  - 모든 슬라이드에 한국어 발표자 노트 작성
- 사용자가 정한 것
  - 수업의 목표 장면: 간단한 주제로 서비스를 개발하면서 SKILL을 활용하는 장면
  - 서비스 주제: 5차시 "미니 리뷰 챗봇"을 이어서 사용
  - MCP: 구현에 필요한 자료와 구성 방식만 소개하고 **실제 실행은 하지 않음**
- 제약: Canva MCP는 페이지 복제·삭제 불가 → 기존 45장을 재배치·재구성
- 작업 중에는 저장하지 않고(keep_open), 사용자 확인 후 저장

## 시간표 (100분)

| 시간 | 내용 |
|---|---|
| 19:00 ~ 19:20 | PART 01 SKILL 개요 |
| 19:20 ~ 19:30 | 휴식 |
| 19:30 ~ 19:50 | PART 02 MCP 개요 · 구성 방법 |
| 19:50 ~ 20:00 | 휴식 |
| 20:00 ~ 20:20 | PART 03 나만의 SKILL 만들기 실습 |
| 20:20 ~ 20:30 | 마무리 · Q&A |

## 조사 내용 (웹 검색)

- SKILL (Agent Skills 표준, agentskills.io)
  - 폴더 + `SKILL.md`(YAML 머리말 `name`·`description` + Markdown 본문), 선택 폴더 `scripts/` `references/` `assets/`
  - `name`: 소문자·숫자·하이픈, 64자 이내, 폴더 이름과 같아야 함 / `description`: 무엇을 + 언제, 1024자 이내
  - 3단계 로딩: 머리말만 먼저(약 100토큰) → 요청과 맞으면 본문 → 필요할 때 부가 파일
  - 위치: Antigravity `.agents/skills/`(프로젝트) · `~/.gemini/config/skills/`(전역), Claude Code `.claude/skills/`, Codex `.agents/skills/`
  - Tips: 구체적인 description, 본문은 목표·단계·예시·제약, 정답 예시, 정해진 검사는 스크립트로, 500줄 이하
- MCP (modelcontextprotocol.io)
  - Host 안의 Client가 Server와 1:1 연결, Server는 Tools · Resources · Prompts 제공
  - 연결 방식: stdio(로컬 실행) · Streamable HTTP(원격)
  - Antigravity: `mcp_config.json` (`mcpServers` → `command` · `args` · `env`, 원격은 `serverUrl`), 설정 화면 "Manage MCP servers → View raw config"
  - 전역 파일 경로는 버전마다 달라 슬라이드에는 "설정 화면에서 열기"를 기준으로 표기

## 슬라이드 구성 (45장, 괄호는 원본 페이지 레이아웃)

| # | 내용 | 원본 | 시각 요소 |
|---|---|---|---|
| 1 | 표지 | p1 | |
| 2 | INDEX | p2 | |
| 3 | 오늘의 시간표 | p4 | 표 |
| 4 | PART 01 표지: SKILL 개요 | p3 | |
| 5 | 오늘의 흐름: 리뷰 챗봇 → SKILL → MCP | p9 | AI 아이콘 3 |
| 6 | Agent의 SKILL = 작업 설명서 | p5 | AI 일러스트 |
| 7 | SKILL 없을 때 vs 있을 때 | p32 | AI 일러스트 2 |
| 8 | 규칙 파일 vs SKILL | p6 | 표 |
| 9 | SKILL 폴더 구조 | p16 | 도형 트리 |
| 10 | SKILL.md 해부 (머리말 + 본문) | p17 | 도형 + 박스 |
| 11 | 3단계 로딩 (Progressive Disclosure) | p34 | 도형 흐름도 |
| 12 | LLM 서비스별 SKILL 파일 구성 | p15 | 표 |
| 13 | Tips ① description 잘 쓰기 | p10 | 카드 (나쁜 예 / 좋은 예) |
| 14 | Tips ② 본문 4요소 (목표·단계·예시·제약) | p14 | 카드 4 |
| 15 | Tips ③ 정답 예시 · 스크립트 · 500줄 | p26 | AI 아이콘 3 |
| 16 | 쉬는 시간 | p11 | |
| 17 | PART 02 표지: MCP | p12 | |
| 18 | MCP = AI의 USB-C 포트 | p13 | AI 일러스트 |
| 19 | MCP 전/후 (N×M 연결 → 표준 1개) | p28 | AI 일러스트 2 |
| 20 | Host · Client · Server 구조 | p19 | 도형 흐름도 |
| 21 | Server의 3가지 기능 (Tools · Resources · Prompts) | p35 | AI 아이콘 3 |
| 22 | 연결 방식: stdio vs Streamable HTTP | p37 | AI 일러스트 2 |
| 23 | 서비스별 MCP 설정 파일 | p27 | 표 |
| 24 | mcp_config.json 해부 | p23 | 코드 블록 |
| 25 | Antigravity에서 MCP 설정하기 (4단계) | p8 | 카드 2×2 |
| 26 | 많이 쓰는 MCP 서버 예시 | p7 | 카드 2×2 |
| 27 | MCP 보안 수칙 | p30 | AI 일러스트 |
| 28 | SKILL vs MCP | p36 | AI 일러스트 2 |
| 29 | 쉬는 시간 | p24 | |
| 30 | PART 03 표지: 나만의 SKILL 만들기 | p25 | |
| 31 | 실습 시나리오: 리뷰 챗봇 + review-answer SKILL | p43 | AI 일러스트 |
| 32 | SKILL 실습 요령 3가지 | p18 | 카드 |
| 33 | [실습 1] 5차시 프로젝트 열고 지금 답변 확인 | p21 | 코드 블록 |
| 34 | [실습 2] SKILL 만들기 프롬프트 | p20 | 코드 블록(도형) |
| 35 | [실습 2] 만들어진 SKILL.md 확인 | p22 | 코드 블록 |
| 36 | [실습 3] SKILL로 에이전트 실행 | p31 | 코드 블록(도형) |
| 37 | [실습 3] 적용 전/후 비교 | p39 | 답변 박스 2 |
| 38 | 자주 겪는 문제 | p41 | 카드 3 |
| 39 | 다른 SKILL 아이디어 | p29 | AI 일러스트 |
| 40 | SKILL + MCP 함께 쓰기 | p33 | AI 일러스트 |
| 41 | 실습 완료 체크리스트 | p40 | 표 |
| 42 | 오늘 배운 것 | p42 | 일러스트 3 |
| 43 | 다음 수업: 7차시 클라우드 배포 | p38 | AI 일러스트 2 |
| 44 | Q&A | p44 | |
| 45 | Thank you | p45 | |

## 실습 흐름 (Antigravity IDE 에이전트)

1. [실습 1] 5차시 `rag.py` 프로젝트를 열고 질문 하나로 현재 답변 형식 확인
2. [실습 2] 에이전트에게 `.agents/skills/review-answer/SKILL.md` 생성 요청
   - 규칙: 답변 3줄 이내, 근거 리뷰 번호 표기, 리뷰에 없으면 "리뷰에서 찾을 수 없어요"
3. [실습 3] "챗봇 답변 형식을 개선해줘" → 에이전트가 SKILL을 불러 `rag.py` 프롬프트를 수정하는지 확인, 적용 전/후 비교
- 토큰 절약: 프롬프트 2~3개, 질문 1~2개로 제한

## 빌더 판단으로 정한 것 (사용자 확인 대상)

- SKILL 이름은 `review-answer`, 저장 위치는 프로젝트용 `.agents/skills/`
- MCP 설정 예시는 로컬 `filesystem` 서버 1개 (실행하지 않고 구조만 설명)
- 다음 수업 예고는 Curriculum.md의 7차시(클라우드 플랫폼 · 배포) 기준
