# 개발 환경 설정 가이드라인
---

> 🛠️ 1차시 수업 **전까지** 아래 내용을 따라 개인 노트북에 AI 개발 환경을 구축해 주세요!

본 문서는 바이브코딩 기초반 8차시 과정에서 사용할 AI 툴의 설치 방법을 안내하고 있어요!<br/>
필수 설치 대상은 **Antigravity (2.0 앱 + IDE 앱)** 2가지이고, 나머지는 선택 사항입니다.

- **Antigravity** 2.0 앱 · IDE 앱 (필수)
- Antigravity CLI · SDK (선택)
- **Claude Code** 앱 + CLI (선택)
- **ChatGPT** 앱 + CLI (선택)

Antigravity는 2.0으로 올라오면서 네 가지 도구로 분화되었어요!<br/>
따라서 어떤 도구를 설치할지 먼저 확인한 뒤 진행해 주세요.
<br/>
수업 시간에 아직 환경 설정이 안된 부분을 짚고 넘어가니 걱정하지 마시기 바래요!<br/>
설치 도중 막히는 부분이 있으면 단톡방에 남겨주세요! 1차시에 함께 해결합시다.

---

# 1. 사전 준비 사항

설치를 시작하기 전에 준비물을 먼저 갖춰야 해요.
계정과 기본 도구가 없으면 설치 중간에 진행이 멈출 수 있습니다.
아래 항목을 순서대로 확인해 주세요.

## 가. 하드웨어 및 운영체제

| 구분 | 최소 사양 | 권장 사양 | 비고 |
| :---: | :---: | :---: | :---: |
| 운영체제 | Windows 10(64bit) 이상,<br/>macOS 13 이상 | Windows 11,<br/>macOS 최신 버전 | Apple Silicon · Intel Mac 모두 지원 |
| 메모리 | 8GB | 16GB | AI 연산은 클라우드에서 처리 |
| 저장 공간 | 10GB 이상 여유 | 20GB 이상 여유 | IDE · CLI · 프로젝트 파일 포함 |
| 네트워크 | 인터넷 연결 필수 | 유선 또는 안정적인 Wi-Fi | 모든 AI 기능이 온라인 동작 |
| 그래픽 | 별도 GPU 불필요 | - | 로컬 추론을 하지 않음 |

## 나. 계정 준비

세 가지 툴은 각각 다른 계정을 사용합니다.<br/>
특히 Claude와 Codex는 **유료 구독이 필요**하다는 점에 유의해 주세요.<br/>
무료 계정만으로는 CLI에서 로그인할 수 없어요!

| 구분 | 필요한 계정 | 요금제 | 비고 |
| :---: | :---: | :---: | :---: |
| Antigravity<br/>(2.0·IDE·CLI) | Google 계정 | 무료 요금제로 시작 가능 | 일일 사용량 제한 존재,<br/>Google AI Pro/Ultra로 한도 확장 |
| Antigravity SDK | Gemini API Key<br/>또는 GCP 계정 | 사용량 기반 과금 | 선택 사항 |
| Claude Code CLI | Anthropic 계정 | Pro 이상 유료 구독 | 무료 요금제는 사용 불가 |
| Codex CLI | ChatGPT 계정 | Plus 이상 유료 구독 | API Key 방식도 가능 |

- 구독 결제가 부담되는 경우, **Antigravity만 설치**하셔도 됩니다!
- 유료 구독 여부는 **개인 선택**입니다.

## 다. 기본 도구 설치

CLI 도구를 사용하려면 Git과 Node.js를 먼저 설치하셔야 합니다.<br/>
Git은 코드 버전 관리와 Bash 셸 제공에 사용하고, Node.js는 npm 설치 방식에 사용합니다.

### 1) Git 설치

- Windows: [Git for Windows](https://git-scm.com/downloads/win)에서 설치 파일을 내려받아 실행합니다.
- macOS: 터미널에서 `xcode-select --install`을 실행하거나 Homebrew로 설치합니다.

```bash
git --version
```

- 위 명령을 실행했을 때 버전이 출력되면 설치가 정상입니다.

### 2) Node.js 설치

- [Node.js 공식 사이트](https://nodejs.org/en/download)에서 **LTS 버전(22 이상)** 을 설치합니다.
- npm 설치 방식을 쓰지 않는다면 Node.js는 생략하셔도 됩니다.

```bash
node --version
npm --version
```

- 두 명령 모두 버전이 출력되면 설치가 정상입니다.

---

# 2. Antigravity 설치

Antigravity는 Google이 만든 AI 에이전트 개발 플랫폼입니다.<br/>
수업 전반에 다루므로 **가장 먼저 설치**해 주세요.

## 가. 네 가지 도구(Surface)의 이해

**Antigravity는 2.0부터 하나의 IDE가 아니라 네 개의 도구로 나뉘었습니다.**<br/>
기존 1.x에서는 에디터와 에이전트 관리자가 하나의 앱에 들어 있었습니다.<br/>
그러나 에이전트의 활용 범위가 코딩 밖으로 넓어지면서 역할별로 앱을 분리했습니다.
<br/>
4가지 도구 모두 **동일한 에이전트 하네스(Agent Harness)** 위에서 동작합니다.<br/>
따라서 플러그인, 스킬, 설정을 서로 공유하며 같은 프로젝트 폴더를 함께 사용합니다.<br/>
어떤 도구로 작업하든 결과 파일은 동일한 위치(폴더)에 저장돼요!

| 구분 | 형태 | 주요 용도 | 설치 권장 |
| :---: | :---: | :--- | :---: |
| Antigravity 2.0 | 데스크톱 앱 | 에이전트에게 작업을 맡기고<br/>여러 프로젝트를 동시에 관리 | **필수** |
| Antigravity IDE | 데스크톱 앱 | 코드를 직접 보면서<br/>에이전트의 수정 내용을 한 줄씩 확인 | **필수** |
| Antigravity CLI | 터미널(CLI) | 터미널에서 에이전트 실행,<br/>SSH·원격 환경 작업 | 선택 |
| Antigravity SDK | Python 라이브러리 | 나만의 에이전트를 코드로 직접 구현 | 선택 |

### 1) Antigravity 2.0과 IDE의 차이

| 구분 | Antigravity 2.0 | Antigravity IDE | 비고 |
| :---: | :---: | :---: | :---: |
| 중심 화면 | 에이전트 대화 화면 | 코드 편집기 | - |
| 에디터 | 없음 | 있음 (VS Code 기반) | - |
| 작업 방식 | 여러 작업을 동시에 맡김 | 한 줄씩 확인하며 수정 | - |
| 아이콘 | **흰색** 배경 로고 | **검은색** 격자 배경 로고 | 실행 시 혼동 주의 |
| 적합한 상황 | 반복 작업, 병렬 작업, 예약 작업 | 코드 학습, 세밀한 검토 | - |

### 2) 수업에서의 설치 범위

- 1차시 전까지 **Antigravity 2.0**과 **Antigravity IDE** 모두 설치해 주세요!
- 두 앱은 함께 설치해도 서로 충돌하지 않습니다.
- **CLI**와 **SDK**는 선택 사항이에요!
- 기존에 Antigravity 1.x를 쓰셨다면 자동 업데이트 안내를 통해 2.0을 추가 설치하면 돼요!

## 나. 시스템 요구 사항

| 구분 | 요구 사항 | 비고 |
| :---: | :---: | :---: |
| Windows | Windows 10 (64bit) 이상 | x64 및 ARM64 설치 파일 제공 |
| macOS | macOS 12(Monterey) 이상 | Apple Silicon·Intel 설치 파일 제공 |
| Linux | glibc 2.28 이상,<br/>glibcxx 3.4.25 이상 | x64 및 ARM64 지원 |
| 브라우저 | Chrome 브라우저 | 에이전트 브라우저 연동에 사용 |
| 계정 | Google(Gmail) 계정 | 세 앱이 로그인 정보를 공유 |

## 다. Antigravity 2.0 설치

### 1) 설치 절차

1. [Antigravity 다운로드 페이지](https://antigravity.google/download)에 접속합니다.
2. **Antigravity 2.0** 항목에서 본인의 운영체제와 아키텍처에 맞는 설치 파일을 선택합니다.
3. 내려받은 설치 파일을 실행하여 설치를 완료합니다.
4. 설치가 끝나면 Antigravity 2.0을 실행하세요.

### 2) 최초 실행 설정

최초 실행 시 설정 마법사가 순서대로 나타나는데요.<br/>
아래 순서대로 진행하시면 됩니다.

#### 가) Google 계정 로그인

- `Sign in with Google`을 선택합니다.
- 브라우저가 열리면 사용할 Gmail 계정으로 로그인합니다.
- 인증이 끝나면 앱 화면으로 자동 복귀합니다.

#### 나) 보안 및 데이터 정책 동의

- 보안·데이터 사용 정책 화면을 확인한 뒤 `Next`를 클릭합니다.

#### 다) 테마 및 플러그인 선택

- 원하는 테마를 선택합니다.
- Google 개발자 도구 연동 플러그인은 선택 사항입니다.
- `Finish`를 클릭하여 설정을 마칩니다.

### 3) 첫 프로젝트 생성

1. 노트북 바탕화면에 작업용 폴더를 하나 만듭니다. (예: `C:\Users\사용자명\Desktop\vibe-coding`)
2. `Select Project → New Project`를 선택합니다.
3. `Add Folder`를 클릭하여 앞서 만든 폴더를 지정합니다.
4. 보안 프리셋은 **기본값(default)** 을 그대로 사용합니다.
5. 프로젝트 이름을 입력한 뒤 `Create`를 클릭합니다.
6. 채팅 창에 `이 프로젝트에 대해 설명해줘`를 입력하여 동작을 확인합니다.

## 라. Antigravity IDE 설치

### 1) 설치 절차

1. 같은 [다운로드 페이지](https://antigravity.google/download)에서 **Antigravity IDE** 항목을 찾습니다.
2. 본인의 운영체제와 아키텍처에 맞는 설치 파일을 내려받습니다.
3. 설치 파일을 실행하여 설치를 완료합니다.
4. 실행 시 **검은색 격자 아이콘**이 IDE입니다. 흰색 아이콘과 혼동하지 마세요.

### 2) 기존 VS Code 환경 가져오기

기존에 VS Code나 Cursor를 사용하셨다면 설정을 그대로 가져올 수 있습니다.<br/>
Antigravity IDE가 VS Code 포크이므로 호환성이 높기 때문입니다.

- 설정 마법사에서 `Import from VS Code`(또는 Cursor)를 선택합니다.
- `settings.json`, 확장 프로그램, 단축키 설정을 함께 가져옵니다.
- 새로 시작하고 싶다면 `Start fresh`를 선택합니다.
- 가져오기가 동작하지 않으면 설치 후 설정 화면에서 다시 시도합니다.

### 3) 2.0 앱과 함께 사용하기

두 앱은 별개의 프로그램이지만 같은 폴더를 함께 바라봅니다.<br/>
디스크의 동일한 파일을 읽고 쓰기 때문입니다.

- Antigravity 2.0과 IDE에서 **같은 프로젝트 폴더**를 엽니다.
- 2.0에서 에이전트가 코드를 수정하면 IDE 화면에 즉시 반영돼요!
- 작업은 2.0에 맡기고, 검토는 IDE에서 하는 방식으로 개발할 수 있어요.

### 4) 확장 프로그램 관련 유의 사항

Antigravity IDE는 VS Code 마켓플레이스가 아닌 **OpenVSX 레지스트리**를 사용합니다.<br/>
따라서 일부 VS Code 확장 프로그램은 검색 결과에 나타나지 않아요!

> - 검색되지 않는 확장은 `.vsix` 파일을 내려받아 설치할 수 있어요.
> - 확장 패널에서 `Install from VSIX...`를 선택한 뒤 파일을 지정하면 됩니다.
> - VS Code 전용 API에 의존하는 확장은 정상 동작하지 않을 수도 있어요.

## 마. Antigravity CLI 설치 (선택)

Antigravity CLI는 터미널(검은 창)에서 동작하는 에이전트 도구에요.<br/>
Go 언어로 만들어 실행 속도가 빠르며, 키보드만으로 조작할 수 있어요!<br/>
실행 명령어는 `antigravity`가 아닌 **`agy`** 입니다.

### 1) 설치 절차

Windows는 WSL 없이 PowerShell 5 이상에서 바로 설치할 수 있습니다.

```powershell
# Windows (PowerShell)
irm https://antigravity.google/cli/install.ps1 | iex
```

```bash
# macOS · Linux
curl -fsSL https://antigravity.google/cli/install.sh | bash
```

- 설치 경로는 macOS·Linux가 `~/.local/bin/agy`입니다.
- Windows는 `C:\Users\<사용자명>\AppData\Local\agy\bin`에 설치합니다.
- 설치 후에는 반드시 터미널을 새로 열어야 PATH가 반영됩니다.

### 2) 실행 및 로그인

1. 작업할 프로젝트 폴더에서 터미널을 엽니다.
2. `agy` 명령을 입력하여 실행합니다.
3. 브라우저가 열리면 Google 계정으로 로그인합니다.
4. 색상 테마와 렌더링 모드를 선택합니다.
5. 워크스페이스 신뢰(Workspace Trust) 여부를 승인합니다.

```bash
agy
```

- 로그인 정보는 운영체제의 보안 키링에 저장합니다.
- 계정을 해제하려면 `/logout` 명령을 사용합니다.

## 바. Antigravity SDK 설치 (선택)

Antigravity SDK는 에이전트를 직접 코드로 만드는 Python 라이브러리입니다.<br/>
앞선 세 도구가 완성된 에이전트를 쓰는 방식이라면, SDK는 에이전트를 만드는 방식입니다.

### 1) 설치 절차

```bash
pip install google-antigravity
```

- 반드시 **PyPI에서 설치**해야 합니다. GitHub 저장소만 내려받으면 동작하지 않습니다.
- 실행 바이너리가 플랫폼별 wheel 파일에 포함되어 있기 때문입니다.
- Windows에서 설치가 실패하면 WSL 환경에서 다시 시도해 주세요.

### 2) 인증 설정

SDK는 Google 로그인이 아닌 **API Key 방식**으로 인증합니다.<br/>
[Google AI Studio](https://aistudio.google.com/apikey)에서 API Key를 먼저 발급받으세요.

```powershell
# Windows (PowerShell)
$env:GEMINI_API_KEY = "발급받은_API_KEY"
```

```bash
# macOS · Linux
export GEMINI_API_KEY="발급받은_API_KEY"
```

- Google Cloud(Vertex AI)를 쓰실 경우 `gcloud auth application-default login`을 사용합니다.
- API Key는 절대 GitHub에 올리지 않도록 주의해 주세요.

### 3) 동작 확인

아래 코드를 `test_agent.py`로 저장한 뒤 실행합니다.

```python
import asyncio
from google.antigravity import Agent, LocalAgentConfig

async def main():
    config = LocalAgentConfig()
    async with Agent(config) as agent:
        response = await agent.chat("현재 디렉토리에 어떤 파일이 있어?")
        print(await response.text())

if __name__ == "__main__":
    asyncio.run(main())
```

```bash
python test_agent.py
```

- 현재 폴더의 파일 목록을 설명하는 답변이 출력되면 정상입니다.

---

# 3. Claude Code CLI 설치 (선택)

**Claude Code CLI**는 터미널에서 동작하는 Anthropic의 AI 코딩 에이전트입니다.<br/>
IDE 없이 터미널만으로 코드를 읽고 수정할 수 있어요!

> Antigravity만으로도 충분해요!
> 클로드 코드는 필수 설치가 아닙니다!

## 가. 시스템 요구 사항

| 구분 | 요구 사항 | 비고 |
| :---: | :---: | :---: |
| Windows | Windows 10 (1809) 이상 | Git for Windows 설치 권장 |
| macOS | macOS 13 이상 | - |
| Linux | Ubuntu 20.04 이상,<br/>Debian 10 이상 | WSL에서도 동작 |
| 하드웨어 | RAM 4GB 이상 | x64 또는 ARM64 |
| 셸 | Bash, Zsh, PowerShell, CMD | - |

## 나. 설치 절차

운영체제에 맞는 명령어를 **하나만** 실행하시면 됩니다.<br/>
공식 설치 스크립트 방식을 권장합니다. 자동 업데이트를 지원하기 때문입니다.

### 1) Windows (PowerShell)

```powershell
irm https://claude.ai/install.ps1 | iex
```

- PowerShell을 관리자 권한으로 실행하지 않으셔도 됩니다.
- `irm이(가) 인식되지 않습니다` 오류가 나오면 CMD 창입니다. PowerShell을 여신 뒤 다시 실행해 주세요.

### 2) macOS · Linux · WSL

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

### 3) 패키지 관리자 이용 (선택)

```bash
# macOS (Homebrew)
brew install --cask claude-code

# Windows (WinGet)
winget install Anthropic.ClaudeCode

# npm (Node.js 22 이상 필요)
npm install -g @anthropic-ai/claude-code
```

- 패키지 관리자 설치 방식은 자동 업데이트를 지원하지 않습니다.
- `sudo npm install -g` 명령은 권한 문제를 일으키므로 사용하지 않습니다.

## 다. 로그인

1. 작업할 프로젝트 폴더에서 터미널을 엽니다.
2. `claude` 명령을 입력하여 실행합니다.
3. 브라우저가 열리면 Anthropic 계정으로 로그인합니다.
4. 인증이 끝나면 터미널로 자동 복귀합니다.

```bash
claude
```

## 라. 설치 확인

```bash
claude --version
claude doctor
```

- `claude --version`은 `2.x.x (Claude Code)` 형태의 버전을 출력합니다.
- `claude doctor`는 설치 상태와 설정 오류를 함께 점검합니다.

---

# 4. Codex CLI 설치 (선택)

**Codex CLI**는 OpenAI가 제공하는 터미널 기반 코딩 에이전트입니다.<br/>
Claude Code와 사용 방식이 비슷하므로 비교 실습에 활용합니다.

> Antigravity만으로도 충분해요!
> 코덱스는 필수 설치가 아닙니다!

## 가. 시스템 요구 사항

| 구분 | 요구 사항 | 비고 |
| :---: | :---: | :---: |
| 운영체제 | Windows, macOS, Linux | Windows는 PowerShell 사용 |
| Node.js | 22 이상 권장 | npm 설치 방식에만 해당 |
| 계정 | ChatGPT Plus 이상 | API Key 방식도 가능 |

## 나. 설치 절차

### 1) npm 이용 (공통)

```bash
npm install -g @openai/codex
```

- 패키지명은 반드시 `@openai/codex`로 입력합니다.
- 이름이 비슷한 `codex` 패키지는 전혀 다른 프로젝트입니다.

### 2) Windows (PowerShell)

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"
```

### 3) macOS · Linux

```bash
# 설치 스크립트
curl -fsSL https://chatgpt.com/codex/install.sh | sh

# Homebrew (macOS)
brew install --cask codex
```

## 다. 로그인

1. 작업할 프로젝트 폴더에서 터미널을 엽니다.
2. `codex` 명령을 입력하여 실행합니다.
3. `Sign in with ChatGPT`를 선택합니다.
4. 브라우저에서 ChatGPT 계정으로 로그인합니다.

```bash
codex
```

- 인증 정보는 시스템 키체인에 안전하게 저장합니다.
- API Key를 쓰실 경우 별도 환경 변수 설정이 필요합니다.

## 라. 설치 확인 및 초기 설정

```bash
codex --version
```

- 실행 후 `/init` 명령으로 프로젝트용 `AGENTS.md` 파일을 만들 수 있습니다.
- `/model` 명령으로 모델과 추론 강도를 선택할 수 있습니다.
- `/permissions` 명령으로 에이전트의 실행 권한을 조정할 수 있습니다.

---

# 5. 설치 완료 체크리스트

1차시 수업 전에 아래 항목을 모두 확인해 주세요!

| 구분 | 확인 항목 | 확인 명령 또는 방법 | 필수 여부 | 완료 여부 |
| :---: | :---: | :---: | :---: | :---: |
| 기본 도구 | Git 설치 | `git --version` | 필수 | ☐ |
| 기본 도구 | Node.js 설치 | `node --version` | 필수 | ☐ |
| Antigravity 2.0 | 설치 및 Google 로그인 | 채팅 창에서 응답 확인 | 필수 | ☐ |
| Antigravity IDE | 설치 및 프로젝트 열기 | 검은색 아이콘 앱 실행 | 필수 | ☐ |
| Antigravity IDE | 기존 VS Code 환경 이전 | 확장·테마 적용 확인 | 권장 | ☐ |
| Antigravity CLI | 설치 및 로그인 | `agy` 실행 | 선택 | ☐ |
| Antigravity SDK | 설치 및 API Key 설정 | `test_agent.py` 실행 | 선택 | ☐ |
| Claude Code | 설치 및 로그인 | `claude doctor` | 선택 | ☐ |
| Codex | 설치 및 로그인 | `codex --version` | 선택 | ☐ |

---

# 6. 자주 발생하는 문제와 해결 방법

## 가. `command not found` 오류가 발생하는 경우

설치는 끝났지만 PATH 환경 변수가 반영되지 않은 상태입니다.<br/>
터미널이 실행 파일의 위치를 아직 모르기 때문이에요!

- 열려 있는 터미널을 모두 닫고 새 터미널을 엽니다.
- 그래도 해결되지 않으면 컴퓨터를 재부팅합니다.

## 나. Windows에서 명령어가 인식되지 않는 경우

PowerShell 명령을 CMD 창에서 실행하면 오류가 발생합니다.<br/>
두 셸의 문법이 서로 다르기 때문입니다.

- 프롬프트가 `PS C:\`로 시작하면 **PowerShell**입니다.
- 프롬프트가 `C:\`로 시작하면 **CMD**입니다.
- `Windows 키 + S`를 눌러 `PowerShell`을 검색한 뒤 실행합니다.

## 다. 어떤 Antigravity 앱을 실행했는지 헷갈리는 경우

두 앱은 이름이 비슷하지만 완전히 다른 프로그램입니다.<br/>
아이콘 색으로 구분하시면 가장 빠릅니다.

- **흰색 배경 로고**는 Antigravity 2.0입니다. 에이전트 대화 화면이 먼저 나옵니다.
- **검은색 격자 로고**는 Antigravity IDE입니다. 코드 편집기가 먼저 나옵니다.
- 코드를 직접 보고 싶은데 채팅 화면만 나온다면 IDE를 실행해 주세요.

## 라. Antigravity에서 VS Code 확장이 검색되지 않는 경우

Antigravity IDE는 OpenVSX 레지스트리를 사용합니다.<br/>
VS Code 마켓플레이스와 등록된 확장 목록이 다르기 때문입니다.

- 확장 배포 페이지에서 `.vsix` 파일을 직접 내려받습니다.
- 확장 패널의 `Install from VSIX...`로 설치합니다.

## 마. `agy` 명령을 찾을 수 없는 경우

Antigravity CLI의 실행 파일 이름은 `antigravity`가 아닙니다.<br/>
설치 시 `agy`라는 이름으로 등록하기 때문입니다.

- 명령어를 `agy`로 정확히 입력했는지 확인합니다.
- 설치 직후라면 터미널을 새로 열어 PATH를 반영합니다.

## 바. Claude Code 로그인이 되지 않는 경우

무료 요금제 계정으로는 로그인할 수 없습니다.<br/>
Claude Code는 Pro 이상 구독에서만 동작하기 때문입니다.

- 계정의 구독 상태를 먼저 확인합니다.
- 구독 없이 참여하실 경우 Antigravity 위주로 실습합니다.

## 사. macOS에서 Antigravity가 실행되지 않는 경우

macOS 버전이 낮으면 앱이 실행되지 않습니다.<br/>
Antigravity가 macOS 12(Monterey) 이상을 요구하기 때문입니다.

- macOS 버전이 12 이상인지 확인합니다.
- Apple Silicon과 Intel Mac은 설치 파일이 다르므로 구분하여 내려받습니다.

---

# 7. 참고 자료

- [Antigravity 공식 다운로드](https://antigravity.google/download)
- [Antigravity 2.0 소개 (공식 블로그)](https://antigravity.google/blog/introducing-google-antigravity-2)
- [네 가지 도구 선택 가이드 (Google Cloud 블로그)](https://cloud.google.com/blog/topics/developers-practitioners/choosing-your-surface-antigravity-20-antigravity-cli-antigravity-ide-or-antigravity-sdk)
- [Antigravity IDE 시작 가이드](https://antigravity.google/docs/ide/getting-started)
- [Antigravity CLI 설치 및 인증](https://antigravity.google/docs/cli/install)
- [Antigravity SDK 개요](https://antigravity.google/docs/sdk/overview)
- [Antigravity SDK GitHub 저장소](https://github.com/google-antigravity/antigravity-sdk-python)
- [Antigravity 시작하기 Codelab](https://codelabs.developers.google.com/getting-started-google-antigravity)
- [Claude Code 설치 가이드](https://code.claude.com/docs/en/setup)
- [Claude Code 설치 문제 해결](https://code.claude.com/docs/en/troubleshoot-install)
- [Codex CLI 공식 문서](https://learn.chatgpt.com/docs/codex/cli)
- [Codex CLI GitHub 저장소](https://github.com/openai/codex)
- [Git for Windows 다운로드](https://git-scm.com/downloads/win)
- [Node.js 다운로드](https://nodejs.org/en/download)

---

> 🔗 8차시 상세 커리큘럼은 아래의 링크를 참고해주세요!<br>
> [👉 상세 커리큘럼 확인하러 가기!](./Curriculum.md)
