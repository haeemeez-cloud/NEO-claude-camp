# AI Native Camp - MD 에디션

> 5일 후, 당신의 업무 방식은 영구적으로 바뀐다.

패션 플랫폼 MD를 위한 Claude Code 5일 집중 캠프.
코딩 경험 없이도, CSV 데이터 전처리부터 AI 에이전트 활용까지.

## Step 0: Claude Code 설치

스킬을 사용하려면 먼저 Claude Code가 설치되어 있어야 합니다.

### 사전 확인

| 항목 | 조건 |
|------|------|
| **OS** | Windows 10+ (PowerShell 또는 CMD), macOS 10.15+, Ubuntu 20.04+ |
| **RAM** | 4GB 이상 |
| **네트워크** | 인터넷 연결 필수 (오프라인 사용 불가) |
| **계정** | Claude Pro, Max, Teams, Enterprise 중 하나 |

> **Day 1에서 Git, Python, Node.js, Claude Code를 모두 설치합니다.** 미리 설치할 필요 없습니다.

### 설치 방법

[https://claude.ai](https://claude.ai) 에 접속해서 대화창에 이렇게 입력하세요:

```
Claude Code 설치하는 방법 알려줘
```

Claude가 여러분의 환경에 맞는 설치 방법을 단계별로 안내해줍니다. 그대로 따라하세요.

<details>
<summary>설치 명령어 직접 보기 (참고용)</summary>

**Windows (PowerShell):**

```powershell
irm https://claude.ai/install.ps1 | iex
```

**Windows (CMD):**

```cmd
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

**macOS / Linux / WSL:**

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

</details>

### 설치 확인

터미널을 열고 아래 명령어를 입력합니다:

```
claude
```

Claude가 인사하면 성공입니다. 계정 인증(로그인) 안내가 나오면 그대로 진행하세요.

## Step 1: 스킬 설치

```bash
npx skills add ai-native-camp/camp-2 --agent claude-code --yes
```

이 한 줄이면 모든 커리큘럼 스킬이 Claude Code에 설치됩니다.

> 설치 후 Claude Code에서 `/day1-setup-and-data` 로 시작하세요.

## Skills as Curriculum

이 캠프의 커리큘럼은 **Claude Code Skills 그 자체**다.

슬라이드를 넘기며 듣는 강의가 아니다. `/day1-setup-and-data`를 실행하면 Claude가 직접 가르치고, 질문하고, 실습을 안내한다. 매일 새로운 Skill이 열리고, 어제 배운 것 위에 오늘을 쌓는다.

Skill을 만드는 법을 Skill로 배운다. 이것이 이 캠프의 방식이다.

## 커리큘럼

| Day | Skill | 주제 |
|-----|-------|------|
| 1 | `day1-setup-and-data` | 환경 설치(Git/Python/Node.js/CC) + 기본 개념(CLAUDE.md/Memory/Skill) + CSV 전처리 실습 + 스킬 만들기 |
| 2 | `day2-review-and-features` | Day 1 퀴즈 복습 + 새 데이터로 실습 복습 + MCP, Hook, Plugin |
| 3 | `day3-mcp-deep-dive` | MCP 딥다이브 + Context Sync 스킬 구축 |
| 4 | `day4-clarify-and-github` | Clarify 플러그인 활용 + 나만의 스킬 만들기 + PRD & GitHub |
| 5 | `day5-agent-and-orchestration` | Subagent + Agent Teams + 멀티에이전트 패턴 + 세션 분석 + 콘텐츠 소화 |

## 샘플 데이터

Day 1 실습에 사용하는 패션 플랫폼 샘플 데이터:

| 파일 | 내용 |
|------|------|
| `data/products.csv` | 상품 마스터 (SKU, 브랜드, 카테고리, 가격, 재고, 시즌) |
| `data/sales.csv` | 일별 매출 (주문일, 수량, 매출, 반품, 채널) |
| `data/brands.csv` | 입점 브랜드 관리 (수수료율, 계약기간, 담당자) |

> 의도적으로 데이터 품질 이슈(날짜 형식 불일치, 카테고리명 불통일, 중복 등)가 포함되어 있습니다. 전처리 실습용입니다.

## 캠프가 끝나면

수료가 아니라 시작이다. Claude Code라는 불을 다루는 신인류 커뮤니티의 일원이 된다.
