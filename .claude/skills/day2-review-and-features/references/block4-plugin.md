# Block 4: Plugin

> **Phase A 시작 시 반드시 아래 형태로 출력한다:**
> ```
> 공식 문서: https://docs.anthropic.com/en/docs/claude-code/plugins
> ```

## EXPLAIN

### Plugin이란?

Plugin = **Skill + MCP + Hook + Agent**를 묶은 설치 패키지.

### 비유: 앱스토어 앱

| 앱스토어 | Claude Code Plugin |
|---------|-------------------|
| 앱 하나 설치 | Plugin 하나 설치 |
| 카메라 + 필터 + 공유 기능이 한번에 | Skill + MCP + Hook + Agent가 한번에 |
| 설치 버튼 한 번 | `/plugin install` 한 번 |
| 앱 삭제 → 깔끔하게 제거 | `/plugin remove` → 깔끔하게 제거 |

### 개별 설치 vs Plugin

```
개별 설치 (Plugin 없이)           Plugin (한 번에)
┌─────────────┐                 ┌──────────────────┐
│ Skill 복사    │ ← 수동          │ clarify 플러그인   │
│ MCP 설정     │ ← 수동    vs    │ ┌─ Skill (질문)   │
│ Hook 설정    │ ← 수동          │ ├─ MCP (없음)     │
│ Agent 설정   │ ← 수동          │ └─ Hook (없음)    │
└─────────────┘                 └────────┬─────────┘
  팀원 각자 반복                          │
                                /plugin install
                                  한 줄이면 끝
```

### Skill과 Plugin의 차이

| | Skill | Plugin |
|--|-------|--------|
| 정의 | 단일 작업 지시서 (SKILL.md) | 여러 기능의 묶음 패키지 |
| 포함 가능 | 자기 자신만 | Skill + MCP + Hook + Agent |
| 설치 방식 | 파일 복사 | `/plugin install` |
| 용도 | 하나의 반복 작업 자동화 | 완전한 워크플로우 배포 |

## EXECUTE

참가자에게 아래 3단계를 순서대로 실행하라고 안내한다.

### 1단계: 현재 플러그인 확인

Claude Code에서 아래 명령어를 입력한다:

```
/plugin
```

> 현재 설치된 플러그인 목록이 표시된다.
> Day 1에서 설치한 플러그인이 있을 수도 있다.

### 2단계: clarify 플러그인 설치

Claude Code에서 아래와 같이 입력한다:

```
clarify 플러그인을 설치해줘
```

또는 직접 명령어를 입력한다:

```
/plugin install clarify
```

> clarify는 모호한 요청을 받으면 Claude가 질문으로 명확하게 만들어주는 플러그인이다.
> Day 3에서 깊이 다룰 예정이다.

### 3단계: 설치 결과 확인

설치가 끝나면 어떤 구성 요소가 추가되었는지 확인한다:

```
방금 설치한 clarify 플러그인에 어떤 Skill, MCP, Hook이 포함되어 있는지 알려줘
```

> Plugin 하나를 설치했을 뿐인데, 필요한 Skill/MCP/Hook이 한번에 추가된 것을 확인할 수 있다.
> 이것이 Plugin의 핵심 가치: 복잡한 설정을 한 줄로 끝내는 것.

## QUIZ

```json
AskUserQuestion({
  "questions": [{
    "question": "Plugin은 무엇들을 묶은 패키지인가요?",
    "header": "Plugin 퀴즈 1/2",
    "options": [
      {"label": "Skill + MCP + Hook + Agent", "description": "여러 기능을 하나의 설치 단위로"},
      {"label": "Skill만", "description": "Skill 외에도 MCP, Hook, Agent 포함"},
      {"label": "MCP + Hook만", "description": "Skill과 Agent도 포함"}
    ],
    "multiSelect": false
  }]
})
```

정답: Skill + MCP + Hook + Agent
피드백 (정답): "맞습니다! Plugin은 Skill, MCP, Hook, Agent를 하나의 패키지로 묶어서 한 줄로 설치할 수 있게 해줍니다."
피드백 (오답): "Skill + MCP + Hook + Agent가 정답입니다. Plugin의 핵심은 여러 기능을 하나의 패키지로 묶어 팀 전체가 동일한 환경을 갖출 수 있게 하는 것입니다."

```json
AskUserQuestion({
  "questions": [{
    "question": "Plugin과 Skill의 차이는?",
    "header": "Plugin 퀴즈 2/2",
    "options": [
      {"label": "Plugin은 여러 기능의 묶음, Skill은 단일 작업 지시서", "description": "Plugin이 Skill을 포함할 수 있음"},
      {"label": "같은 것의 다른 이름", "description": "완전히 다른 개념"},
      {"label": "Plugin이 더 작은 단위", "description": "Plugin이 Skill보다 큰 단위"}
    ],
    "multiSelect": false
  }]
})
```

정답: Plugin은 여러 기능의 묶음, Skill은 단일 작업 지시서
피드백 (정답): "정확합니다! Skill은 SKILL.md 하나로 된 단일 작업 레시피이고, Plugin은 Skill + MCP + Hook + Agent를 묶은 종합 패키지입니다. 앱스토어의 앱처럼 설치 한 번이면 모든 기능이 추가돼요."
피드백 (오답): "'Plugin은 여러 기능의 묶음, Skill은 단일 작업 지시서'가 정답입니다. Skill이 하나의 레시피라면, Plugin은 레시피 + 재료 + 도구를 한 상자에 넣은 밀키트라고 생각하세요."
