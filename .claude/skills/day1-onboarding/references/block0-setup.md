# Block 0: Setup

> Claude Code 설치는 이미 README의 Step 0에서 완료한 상태다.
> 이 블록에서는 첫 실행 설정과 에디터를 안내한다.

## EXPLAIN

> **Phase A 시작 시 반드시 아래 형태로 출력한다:**
> ```
> 📖 공식 문서: https://code.claude.com/docs/ko/setup
> 📖 빠른 시작: https://code.claude.com/docs/ko/quickstart
> ```

### Windows 터미널 환경 확인

이 캠프에서는 **Git Bash**를 기본 터미널로 사용한다. 아래 표로 각 터미널이 뭔지 간단히 짚고 넘어간다:

| 터미널 | 뭔가요? | 어디에 쓰나요? | 이 캠프에서는? |
|--------|---------|---------------|---------------|
| **Git Bash** | Git 설치 시 함께 오는 Linux 스타일 터미널 | `ls`, `cd`, `cat` 등 Linux 명령어를 Windows에서 사용 | **기본 터미널로 사용** |
| **PowerShell** | Windows에 기본 내장된 터미널 | Windows 시스템 관리, 스크립트 실행 | Claude Code 설치 시에만 사용 |
| **CMD** | Windows 초기부터 있던 명령 프롬프트 | 간단한 명령 실행 | 거의 안 씀 |
| **WSL** | Windows 안에 Linux를 통째로 설치 | 개발자가 Linux 환경이 필요할 때 | 이 캠프에서는 불필요 |
| **VS Code 터미널** | VS Code 하단의 내장 터미널 | 코드 편집 + 터미널을 한 화면에서 | Git Bash로 설정하면 편리 |

> **"Git Bash를 열고 `claude`를 입력하세요."** 이게 이 캠프에서 가장 많이 하는 동작이다.
> VS Code 터미널을 Git Bash로 설정해서 쓰는 것도 좋은 방법이다.

### 사전 설치 확인

캠프를 시작하기 전에 아래 도구들이 모두 설치되어 있는지 확인한다. Git Bash에서 하나씩 입력해본다:

```bash
git --version       # Git 설치 확인
node --version      # Node.js 설치 확인
npm --version       # npm 설치 확인
python --version    # Python 설치 확인
pip --version       # pip 설치 확인
claude              # Claude Code 설치 확인
```

> 하나라도 "command not found"가 나오면 README의 Step 0을 다시 확인한다.

### 에디터 (선택사항)

Claude Code는 터미널에서 `claude`만 치면 된다. 하지만 파일을 눈으로 보면서 작업하고 싶다면 에디터를 설치할 수 있다:

| 에디터 | 특징 | 추천 대상 | 공식 사이트 |
|--------|------|-----------|-------------|
| [VS Code](https://code.visualstudio.com/) | 범용적, 확장 풍부, 회사에서 이미 사용 중일 가능성 높음 | **대부분의 참가자** | code.visualstudio.com |
| [Cursor](https://www.cursor.com/) | AI 내장, Claude Code와 시너지 | AI 도구를 적극 활용할 분 | cursor.com |
| [Antigravity](https://antigravity.google/) | 무료, AI 내장, 가장 간단 | 가볍게 시작할 분 | antigravity.google |

> "이 캠프에서는 에디터 없이 터미널에서 `claude`만 쳐도 충분합니다. 에디터는 나중에 필요할 때 설치해도 됩니다."

### Windows 꿀팁: 숨겨진 폴더 보기

Windows에서는 `.`으로 시작하는 폴더(`.claude`, `.git` 등)가 기본적으로 안 보인다. 파일 탐색기에서 보이게 설정하자:

**방법 1 — 파일 탐색기에서 직접 설정:**
- 파일 탐색기 상단 → **보기** 탭 → **숨겨진 항목** 체크

**방법 2 — Claude에게 시키기:**
```
파일 탐색기에서 .claude, .git 같은 숨겨진 폴더도 볼 수 있게 설정해줘
```

설정이 끝나면 파일 탐색기로 직접 확인해보자:

```bash
start .
```

> `.claude/skills/` 폴더 안에 지금 배우고 있는 교안이 들어있다! 파일 탐색기에서 직접 눈으로 확인해보자.

### 첫 실행

Git Bash(또는 VS Code 터미널)에 `claude` 한 글자를 입력하라고 안내한다. Anthropic 계정 로그인 + Claude 구독(Pro, Max, Teams, Enterprise) 연결을 확인시킨다.

### Output Style 설정

로그인이 끝나면 아래 순서로 Output Style을 설정하라고 안내한다:

1. Claude Code 대화창에 `/output-style` 입력
2. 선택지에서 **Explanatory** 선택

```
/output-style
→ Explanatory 선택
```

> Explanatory 모드로 설정하면 Claude가 코드를 작성할 때 왜 그렇게 하는지 설명을 함께 해준다. 배우는 단계에서 가장 적합한 모드다.

## EXECUTE

참가자에게 순서대로 실행하라고 안내한다:

1. **사전 확인**: Git Bash에서 `git --version`, `node --version`, `python --version`, `claude` 입력하여 모두 설치 확인
2. **숨겨진 폴더**: 파일 탐색기에서 숨겨진 항목 보이기 설정 → `start .`로 확인
3. **첫 실행**: Git Bash에서 `claude` 입력
4. **첫 대화**: "안녕, 나는 [이름]이고 경영지원본부 [팀명]팀에서 일하고 있어. 나한테 인사해줘"
5. **Output Style**: `/output-style` → Explanatory 선택
6. **자유 대화**: 5분간 자유롭게 대화 (예: "우리 팀 업무 중에 AI로 자동화할 수 있는 게 뭐가 있을까?")

## QUIZ

```json
AskUserQuestion({
  "questions": [{
    "question": "설치와 첫 대화까지 완료했나요?",
    "header": "Setup 확인",
    "options": [
      {"label": "아직 진행 중", "description": "더 시간이 필요함"},
      {"label": "모두 완료!", "description": "Block 1로 이동"},
      {"label": "트러블슈팅 필요", "description": "설치나 실행에 문제 발생"}
    ],
    "multiSelect": false
  }]
})
```

> Block 0은 퀴즈 대신 완료 확인만 한다.
