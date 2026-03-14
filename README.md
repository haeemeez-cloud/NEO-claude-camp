# AI Native Camp - 경영지원본부

> 7일 후, 당신의 업무 방식은 영구적으로 바뀐다.

경영지원본부(재무, 회계, 인사기획, 인사운영, 총무) 대상 Claude Code 집중 캠프.

## Step 0: 사전 준비 (Windows)

스킬을 사용하려면 아래 도구들이 설치되어 있어야 합니다.

### 0-1. 사전 확인

| 항목 | 조건 |
|------|------|
| **OS** | Windows 10 이상 |
| **RAM** | 4GB 이상 |
| **네트워크** | 인터넷 연결 필수 (오프라인 사용 불가) |
| **계정** | Claude Pro, Max, Teams, Enterprise 중 하나 |

---

### 0-2. 터미널 환경 이해하기

Windows에는 여러 종류의 터미널(명령 입력 창)이 있습니다. 각각이 뭔지, 이 캠프에서 왜 필요한지 정리합니다.

| 터미널 | 한 줄 설명 | 이 캠프에서의 역할 |
|--------|-----------|-------------------|
| **Git Bash** | Git 설치 시 함께 오는 Linux 스타일 터미널 | **이 캠프의 기본 터미널.** `ls`, `cd`, `cat` 등 Linux 명령어를 Windows에서 쓸 수 있다 |
| **PowerShell** | Windows 기본 내장 터미널 | Claude Code 설치 시 사용. 일부 Windows 전용 작업에 필요 |
| **CMD (명령 프롬프트)** | Windows 구형 터미널 | 거의 안 씀. 혹시 PowerShell이 안 되면 대안으로 사용 |
| **WSL** | Windows 안에 Linux를 설치해서 쓰는 것 | 이 캠프에서는 불필요. 개발자가 아니면 설치할 이유 없음 |

> **결론: Git Bash를 기본으로 씁니다.** 회사에서 이미 쓰고 있고, Claude Code와 호환이 좋습니다.
> VS Code 터미널에서 Git Bash를 쓰는 것도 좋은 방법입니다.

---

### 0-3. Git 설치 (Git Bash 포함)

> 이미 Git이 설치되어 있다면 건너뛰세요. Git Bash를 열 수 있으면 설치된 겁니다.

1. https://git-scm.com/download/win 에서 다운로드
2. 설치 중 기본 옵션 그대로 진행 (Next만 누르면 됨)
3. 설치 완료 후 바탕화면이나 시작 메뉴에서 **Git Bash** 실행
4. 아래 명령어로 확인:

```bash
git --version
```

버전이 출력되면 성공입니다.

---

### 0-4. Node.js 설치

Node.js는 JavaScript 실행 환경입니다. Claude Code 스킬 설치(`npx`)에 필요합니다.

1. https://nodejs.org 에서 **LTS 버전** 다운로드 (왼쪽 초록 버튼)
2. 설치 중 기본 옵션 그대로 진행
3. **Git Bash를 닫았다가 다시 열고** 아래 명령어로 확인:

```bash
node --version
npm --version
```

두 개 모두 버전이 출력되면 성공입니다.

> **왜 필요한가요?** 스킬 설치 명령어 `npx skills add ...`가 Node.js 위에서 동작합니다. Claude Code 자체는 Node.js 없이 설치 가능하지만, 스킬 관리에 필요합니다.

---

### 0-5. Python 설치

Python은 데이터 처리, 자동화 스크립트에 사용되는 프로그래밍 언어입니다. Day 2에서 MCP 서버 검색 스크립트 등에 필요합니다.

1. https://www.python.org/downloads/ 에서 최신 버전 다운로드
2. **설치 첫 화면에서 "Add Python to PATH" 체크박스를 반드시 체크!** (가장 중요)
3. "Install Now" 클릭
4. **Git Bash를 닫았다가 다시 열고** 아래 명령어로 확인:

```bash
python --version
pip --version
```

두 개 모두 버전이 출력되면 성공입니다.

> **왜 필요한가요?** Day 2에서 MCP 서버를 검색하는 Python 스크립트를 실행하고, 이후 자동화 워크플로우를 만들 때 활용합니다. 경영지원 업무 자동화(엑셀 처리, 데이터 수집 등)에도 Python이 많이 쓰입니다.

---

### 0-6. Claude Code 설치

**PowerShell에서 설치** (관리자 권한 불필요):

```powershell
irm https://claude.ai/install.ps1 | iex
```

또는 **CMD에서 설치**:

```cmd
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

> 설치는 PowerShell 또는 CMD에서 하지만, 이후 캠프 진행은 **Git Bash**에서 합니다.

### 설치 확인

Git Bash를 열고 아래 명령어를 입력합니다:

```bash
claude
```

Claude가 인사하면 성공입니다. 계정 인증(로그인) 안내가 나오면 그대로 진행하세요.

---

### 0-7. VS Code + Claude Code 연결 (선택)

Git Bash 단독으로도 캠프 진행이 가능하지만, VS Code를 함께 쓰면 파일을 눈으로 보면서 작업할 수 있습니다.

1. VS Code가 없다면: https://code.visualstudio.com/ 에서 설치
2. VS Code 터미널을 Git Bash로 변경:
   - `Ctrl + Shift + P` → "Terminal: Select Default Profile" 검색 → **Git Bash** 선택
3. VS Code 터미널(`Ctrl + ~`)에서 `claude` 입력하면 바로 사용 가능

---

### 전체 설치 체크리스트

| # | 항목 | 확인 명령어 (Git Bash) | 통과 기준 |
|---|------|----------------------|----------|
| 1 | Git (+ Git Bash) | `git --version` | 버전 출력 |
| 2 | Node.js | `node --version` | 버전 출력 |
| 3 | npm | `npm --version` | 버전 출력 |
| 4 | Python | `python --version` | 버전 출력 |
| 5 | pip | `pip --version` | 버전 출력 |
| 6 | Claude Code | `claude` | Claude 인사 또는 로그인 안내 |

> 6개 모두 통과하면 준비 완료입니다!

---

## Step 1: 스킬 설치

Git Bash에서 캠프 커리큘럼 폴더로 이동한 뒤:

```bash
npx skills add ai-native-camp/camp-2 --agent claude-code --yes
```

이 한 줄이면 모든 커리큘럼 스킬이 Claude Code에 설치됩니다.

> 설치 후 Claude Code에서 `/day1-onboarding` 으로 시작하세요.

## Skills as Curriculum

이 캠프의 커리큘럼은 **Claude Code Skills 그 자체**다.

슬라이드를 넘기며 듣는 강의가 아니다. `/day1-onboarding`을 실행하면 Claude가 직접 가르치고, 질문하고, 실습을 안내한다. 매일 새로운 Skill이 열리고, 어제 배운 것 위에 오늘을 쌓는다.

Skill을 만드는 법을 Skill로 배운다. 이것이 이 캠프의 방식이다.

## 커리큘럼

| Day | Skill | 주제 |
|-----|-------|------|
| 1 | `day1-onboarding` | 7개 핵심 기능 (Memory, Skill, MCP, Subagent, Agent Teams, Hook, Plugin) |
| 2 | `day2-mcp-and-context-sync` | MCP 딥다이브 + Context Sync 스킬 구축 |
| 3 | `day3-clarify` | Clarify 플러그인 활용 + 나만의 스킬 만들기 + Plugin 심화 + PRD & GitHub |
| 4 | `day4-wrap-and-analyze` | Wrap & Analyze: 세션 분석 스킬 구축 + 콘텐츠 소화 체험 |

## 대상

경영지원본부 전 팀원:

| 팀 | 업무 예시 (캠프에서 다루는 시나리오) |
|----|-------------------------------------|
| 재무 | 월간 재무 보고서 자동 수집, 예산 집행 현황 추적 |
| 회계 | 전표 처리 현황 모니터링, 결산 일정 관리 |
| 인사기획 | 인력 계획 대시보드, 조직 개편 의사결정 추적 |
| 인사운영 | 급여/복리후생 문의 자동 정리, 입퇴사 프로세스 관리 |
| 총무 | 자산 관리 현황, 사무실 운영 이슈 트래킹 |

## 캠프가 끝나면

수료가 아니라 시작이다. Claude Code라는 불을 다루는 신인류 커뮤니티의 일원이 된다.
