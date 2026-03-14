# Block 3-Break: 쉬어가기 — 터미널 & Status Line

> 이 블록은 퀴즈 없이 가볍게 진행한다. Phase A만 있고 Phase B는 없다.
> 사용자가 "완료" 또는 "다음"이라고 하면 Block 3-5로 넘어간다.

## EXPLAIN

여기까지 Claude Code의 핵심 기능 4개(Memory, Skill, MCP, Subagent)를 배웠다. 잠깐 숨 고르기.

Claude Code는 **터미널**에서 돌아간다. 어떤 터미널을 쓰느냐에 따라 경험이 달라진다.

### 터미널 추천 (Windows)

| 터미널 | 특징 | 설치 |
|--------|------|------|
| **Windows Terminal** | Windows 공식 터미널. 탭, 분할 화면, Git Bash 통합 가능 | Microsoft Store에서 설치 |
| **Git Bash** | 이 캠프의 기본 터미널. 이미 설치되어 있음 | Git과 함께 설치됨 |
| **VS Code 터미널** | 코드 편집 + 터미널 한 화면에서. Git Bash로 설정 가능 | VS Code 내장 |
| **WezTerm** | 크로스플랫폼. 커스터마이즈 자유도 높음 | [wezfurlong.org/wezterm](https://wezfurlong.org/wezterm) |

> 이미 Git Bash를 쓰고 있다면 그대로 충분하다. Windows Terminal에서 Git Bash를 프로필로 추가하면 탭 관리가 편해진다.

### Windows Terminal에 Git Bash 추가하기 (선택)

Windows Terminal 설정(`Ctrl + ,`) → 새 프로필 추가:
- 이름: Git Bash
- 명령줄: `C:\Program Files\Git\bin\bash.exe`
- 아이콘: `C:\Program Files\Git\mingw64\share\git\git-for-windows.ico`

### Claude Code Status Line

Claude Code 화면 맨 아래에 **상태 표시줄**을 커스터마이즈할 수 있다.
지금 쓰는 모델, 컨텍스트 사용량, Git 브랜치 등을 실시간으로 보여준다.

**설정하는 가장 쉬운 방법:**

Claude Code에 이렇게 말하면 된다:

```
/statusline 모델 이름과 컨텍스트 사용률을 보여줘
```

이 한 줄이면 Claude가 알아서 스크립트를 만들고 설정까지 해준다.

**직접 만들고 싶다면:**

`%USERPROFILE%\.claude\settings.json` (Git Bash에서는 `~/.claude/settings.json`)에 추가:

```json
{
  "statusLine": {
    "type": "command",
    "command": "~/.claude/statusline.sh"
  }
}
```

그리고 `~/.claude/statusline.sh`를 만든다 (Git Bash에서 동작):

```bash
#!/bin/bash
input=$(cat)
MODEL=$(echo "$input" | python -c "import sys,json; print(json.load(sys.stdin).get('model',{}).get('display_name','?'))")
PCT=$(echo "$input" | python -c "import sys,json; print(int(json.load(sys.stdin).get('context_window',{}).get('used_percentage',0)))")

# 프로그레스 바
BAR_WIDTH=10
FILLED=$((PCT * BAR_WIDTH / 100))
EMPTY=$((BAR_WIDTH - FILLED))
BAR=$(printf "%${FILLED}s" | tr ' ' '#')$(printf "%${EMPTY}s" | tr ' ' '-')

echo "[$MODEL] [$BAR] $PCT%"
```

결과: `[Opus] [##--------] 25%`

> `jq` 대신 Python을 사용했다. Python은 이미 설치되어 있으므로 별도 설치가 필요 없다.

## EXECUTE

두 가지를 해보라고 안내한다:

1. **Status Line 설정**: Claude Code에 `/statusline 모델 이름과 컨텍스트 사용률을 프로그레스 바로 보여줘`라고 입력
2. **터미널 구경**: Windows Terminal이 없다면 Microsoft Store에서 설치해보기 (선택)
