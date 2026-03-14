# Block 2: MCP

> **Phase A 시작 시 반드시 아래 형태로 출력한다:**
> ```
> 공식 문서: https://docs.anthropic.com/en/docs/claude-code/mcp
> ```

## EXPLAIN

### MCP란?

MCP = **M**odel **C**ontext **P**rotocol. AI와 외부 도구를 연결하는 오픈 표준 프로토콜이다.

### 비유: USB-C

USB-C를 생각해보자:
- 충전기, 모니터, 외장하드 — 기기가 달라도 USB-C 하나면 연결된다
- MCP도 마찬가지: Slack, Notion, 파일시스템 — 도구가 달라도 MCP 하나면 Claude에 연결된다

| USB-C | MCP |
|-------|-----|
| 노트북 | Claude Code (Host) |
| USB-C 포트 | MCP Client (연결 관리자) |
| 외장하드, 모니터 | MCP Server (외부 도구) |
| USB-C 케이블 | Transport (통신 방식) |

### 구조

```
Claude Code (Host)
  │
  ├─ MCP Client ──── stdio ──── 파일시스템 Server (로컬)
  │
  ├─ MCP Client ──── HTTP ───── Slack Server (클라우드)
  │
  └─ MCP Client ──── HTTP ───── Notion Server (클라우드)
```

- **Host**: Claude Code. MCP의 진입점
- **Client**: Host 안에서 각 Server와의 연결을 관리하는 중간 관리자
- **Server**: 실제 도구를 제공하는 프로그램
- **Transport**: 통신 방식. stdio(로컬 프로그램)와 HTTP(클라우드 서비스) 두 가지

### 왜 MCP가 필요한가?

MCP 없이: Claude는 텍스트만 생성 → "Slack 메시지 보내줘" → 불가능
MCP 있으면: Claude가 Slack Server에 도구 호출(Tool Calling) → 실제로 메시지 전송

## EXECUTE

참가자에게 아래 3단계를 순서대로 실행하라고 안내한다.

### 1단계: 현재 MCP 서버 확인

Claude Code에서 아래 명령어를 입력한다:

```
/mcp
```

> 현재 연결된 MCP 서버 목록이 표시된다. 처음이라면 비어있을 수 있다.

### 2단계: MCP 서버 추가 명령어 소개

Claude Code 밖의 터미널에서 `claude mcp add` 명령어로 서버를 추가할 수 있다.

형식:
```
claude mcp add <서버이름> -- <실행명령어>
```

### 3단계: 파일시스템 MCP 서버 추가

Claude Code를 `/exit`으로 나온 뒤, 터미널에서 아래 명령어를 입력한다:

```
claude mcp add filesystem -- npx -y @anthropic-ai/mcp-filesystem
```

> 이 서버를 추가하면 Claude가 파일시스템을 MCP 표준으로 접근할 수 있다.
> 추가 후 다시 `claude`로 들어가서 `/mcp`로 확인해본다.

## QUIZ

```json
AskUserQuestion({
  "questions": [{
    "question": "MCP는 무엇의 약자인가요?",
    "header": "MCP 퀴즈 1/2",
    "options": [
      {"label": "Model Context Protocol", "description": "AI와 외부 도구를 연결하는 표준"},
      {"label": "Multi Connection Platform", "description": "연결 플랫폼이 아닌 프로토콜"},
      {"label": "Machine Code Processor", "description": "코드 처리와 무관"}
    ],
    "multiSelect": false
  }]
})
```

정답: Model Context Protocol
피드백 (정답): "맞습니다! Model Context Protocol — AI 모델이 외부 맥락(Context)에 접근하기 위한 프로토콜(규약)입니다."
피드백 (오답): "Model Context Protocol이 정답입니다. Model(AI) + Context(외부 맥락) + Protocol(표준 규약)으로 기억하세요."

```json
AskUserQuestion({
  "questions": [{
    "question": "MCP의 역할을 USB-C에 비유하면?",
    "header": "MCP 퀴즈 2/2",
    "options": [
      {"label": "다양한 도구를 하나의 표준으로 연결", "description": "USB-C처럼 하나의 규격으로 여러 기기 연결"},
      {"label": "데이터를 빠르게 전송", "description": "속도가 핵심이 아님"},
      {"label": "보안을 강화", "description": "보안 도구가 아님"}
    ],
    "multiSelect": false
  }]
})
```

정답: 다양한 도구를 하나의 표준으로 연결
피드백 (정답): "정확합니다! USB-C 하나로 충전기, 모니터, 외장하드를 연결하듯, MCP 하나로 Slack, Notion, 파일시스템 등을 Claude에 연결합니다."
피드백 (오답): "'다양한 도구를 하나의 표준으로 연결'이 정답입니다. MCP의 핵심 가치는 도구마다 다른 연결 방식이 아니라, 하나의 표준 프로토콜로 통일한다는 것입니다."
