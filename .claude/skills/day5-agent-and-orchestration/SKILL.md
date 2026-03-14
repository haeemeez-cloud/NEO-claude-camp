---
name: day5-agent-and-orchestration
description: AI Native Camp Day 5 Agent & Orchestration. Subagent, Agent Teams, 멀티에이전트 패턴을 배우고, 세션 분석과 콘텐츠 소화를 체험한다. "5일차", "Day 5", "agent", "에이전트", "subagent", "orchestration" 요청에 사용.
---

# Day 5: Agent & Orchestration

이 스킬이 호출되면 아래 **STOP PROTOCOL**을 반드시 따른다.

---

## 용어 정리

이 스킬에서 사용하는 핵심 용어:

| 용어 | 설명 |
|------|------|
| **Subagent** | Claude가 다른 Claude를 불러서 일을 시키는 것. "팀장이 팀원에게 조사 지시" |
| **Agent Teams** | 여러 에이전트를 팀으로 묶어서 협력하게 하는 구조. "프로젝트 TF팀" |
| **Orchestration** | 여러 에이전트의 실행 순서와 역할을 조율하는 것. "지휘자가 오케스트라를 이끄는 것" |
| **병렬(Parallel)** | 여러 작업을 동시에 처리하는 것. "4명에게 한꺼번에 보고 받기" |
| **순차(Sequential)** | 작업을 차례대로 하나씩 처리하는 것. "한 명씩 순서대로 보고 받기" |
| **Pipeline** | 앞 단계의 결과를 다음 단계의 입력으로 연결하는 구조. "공장 생산라인" |
| **2-Phase Pipeline** | Phase 1(분석, 병렬) → Phase 2(검증, 순차). "전문가 의견 수집 후 팀장이 중복 체크" |
| **Multi-agent** | 여러 에이전트가 단계별로 일하는 구조 |
| **session-wrap** | 코딩 세션이 끝날 때 작업을 정리하는 multi-agent 스킬. "퇴근 전 책상 정리" |
| **history-insight** | 과거 세션 기록에서 인사이트를 추출하는 스킬 |
| **session-analyzer** | 스킬이 의도대로 실행됐는지 검증하는 분석 도구 |
| **content-digest** | 콘텐츠를 Quiz-First 방식으로 소화하는 스킬 |
| **fetch-tweet** | X/Twitter 트윗을 가져와서 번역/요약하는 스킬 |
| **compound** | 인사이트를 구조화된 문서로 축적하는 스킬. "배운 것을 노트에 정리" |
| **team-assemble** | 복잡한 작업을 전문가 팀으로 분해하여 병렬 실행하는 스킬 |
| **스킬 체이닝** | 한 스킬의 결과를 다른 스킬의 입력으로 연결하는 것. "fetch → digest 파이프라인" |
| **Quiz-First** | 요약 먼저 보지 않고 퀴즈부터 푸는 학습법. 9-12% 기억력 향상 효과 |

---

## STOP PROTOCOL — 절대 위반 금지

> 이 프로토콜은 이 스킬의 최우선 규칙이다.
> 아래 규칙을 위반하면 수업이 망가진다.

### 각 블록은 반드시 2턴에 걸쳐 진행한다

```
┌─ Phase A (첫 번째 턴) ──────────────────────────────┐
│ 1. references/에서 해당 블록 파일의 EXPLAIN 섹션을 읽는다    │
│ 2. 기능을 설명한다                                        │
│ 3. references/에서 해당 블록 파일의 EXECUTE 섹션을 읽는다    │
│ 4. "지금 직접 실행해보세요"라고 안내한다                     │
│ 5. ⛔ 여기서 반드시 STOP. 턴을 종료한다.                    │
│                                                          │
│ ❌ 절대 하지 않는 것: 퀴즈 출제, QUIZ 섹션 읽기             │
│ ❌ 절대 하지 않는 것: AskUserQuestion 호출                  │
│ ❌ 절대 하지 않는 것: "실행해봤나요?" 질문                   │
└──────────────────────────────────────────────────────────┘

  ⬇️ 사용자가 돌아와서 "했어", "완료", "다음" 등을 입력한다

┌─ Phase B (두 번째 턴) ──────────────────────────────┐
│ 1. references/에서 해당 블록 파일의 QUIZ 섹션을 읽는다       │
│ 2. AskUserQuestion으로 퀴즈를 출제한다                     │
│ 3. 정답/오답 피드백을 준다                                 │
│ 4. 다음 블록으로 이동할지 AskUserQuestion으로 묻는다         │
│ 5. ⛔ 다음 블록을 시작하면 다시 Phase A부터.                │
└──────────────────────────────────────────────────────────┘
```

### 핵심 금지 사항 (절대 위반 금지)

1. **Phase A에서 AskUserQuestion을 호출하지 않는다** — 설명 + 실행 안내 후 바로 Stop
2. **Phase A에서 퀴즈를 내지 않는다** — QUIZ 섹션은 Phase B에서만 읽는다
3. **Phase A에서 "실행해봤나요?"를 묻지 않는다** — 사용자가 먼저 말할 때까지 기다린다
4. **한 턴에 EXPLAIN + QUIZ를 동시에 하지 않는다** — 반드시 2턴으로 나눈다

### 공식 문서 URL 출력 (절대 누락 금지)

모든 블록의 Phase A 시작 시, 해당 reference 파일 상단의 `> 공식 문서:` URL을 **반드시 그대로 출력**한다.

```
📖 공식 문서: [URL]
```

- reference 파일에 URL이 여러 개 있으면 전부 출력한다
- URL을 요약하거나 생략하지 않는다

### Phase A 종료 시 필수 문구

Phase A의 마지막에는 반드시 아래 형태의 문구를 출력하고 Stop한다:

```
---
👆 위 내용을 직접 실행해보세요.
실행이 끝나면 "완료" 또는 "다음"이라고 입력해주세요.
```

이 문구 이후에 어떤 도구 호출(AskUserQuestion 포함)이나 추가 텍스트도 출력하지 않는다.

---

## 소요 시간 가이드

| Block | 주제 | 예상 시간 |
|-------|------|-----------|
| 0 | Subagent 개념 | ~15분 |
| 1 | Agent Teams | ~20분 |
| 2 | Multi-agent 패턴 + session-wrap 만들기 | ~35분 |
| 3 | 세션 분석 도구 | ~20분 |
| 4 | 콘텐츠 소화 + 캠프 마무리 | ~25분 |
| **합계** | | **~115분** |

> 참가자 속도에 따라 100~130분 소요될 수 있습니다. Block 2가 가장 시간이 오래 걸리는 핵심 블록입니다. Block 4(콘텐츠 소화 + 마무리)는 체험 중심이라 빠르게 진행됩니다.

---

## 핵심 전략: Subagent에서 Orchestration까지

아래 방식으로 진행한다:

1. Block 0에서 Subagent 개념을 이해하고 직접 사용해본다
2. Block 1에서 Agent Teams 개념을 이해하고 팀 구조를 체험한다
3. Block 2에서 Multi-agent 패턴을 배우고 session-wrap 스킬을 직접 만든다
4. Block 3에서 history-insight와 session-analyzer로 세션을 분석한다
5. Block 4에서 콘텐츠 소화 파이프라인을 체험하고 5일 캠프를 마무리한다

```
Day 5 학습 흐름

Block 0          Block 1          Block 2
┌──────────┐    ┌──────────┐    ┌──────────────────┐
│ Subagent │ ─▶ │  Agent   │ ─▶ │ Multi-agent +    │
│ 1:1 위임 │    │  Teams   │    │ session-wrap     │
│          │    │ N명 협력  │    │ 직접 만들기       │
└──────────┘    └──────────┘    └──────────────────┘
                                        │
              ┌─────────────────────────┘
              ▼
Block 3                    Block 4
┌──────────────────┐      ┌──────────────────┐
│ 세션 분석         │ ──▶  │ 콘텐츠 소화 +    │
│ history-insight  │      │ 5일 캠프 마무리   │
│ session-analyzer │      │                  │
└──────────────────┘      └──────────────────┘
```

---

## 블록 특수 규칙

- **Block 0 (Subagent)**: 표준 Phase A/B. Subagent 개념 설명 + Explore 에이전트와 병렬 분석 실습.
- **Block 1 (Agent Teams)**: 표준 Phase A/B. 여러 에이전트가 협력하는 팀 구조 + team-assemble 스킬 체험.
- **Block 2 (Multi-agent + session-wrap)**: Phase A에서 multi-agent 패턴 설명 + session-wrap 스킬 직접 만들기 안내 → Stop. Phase B에서 퀴즈 + 만든 스킬 실행.
  - 참가자가 `.claude/skills/my-session-wrap/SKILL.md`를 직접 작성 (단계별 안내)
  - session-wrap 원본은 플러그인에 설치되어 있으므로 참고 가능
- **Block 3 (세션 분석)**: Phase A에서 history-insight + session-analyzer 소개 및 실습 안내 → Stop. Phase B에서 퀴즈.
- **Block 4 (콘텐츠 소화 + 마무리)**: Phase A에서 fetch-tweet + content-digest + compound + team-assemble 체험 안내 → Stop. Phase B에서 종합 퀴즈 + 5일 캠프 전체 마무리.

---

## References 파일 맵

| 블록 | 파일 | 주제 |
|------|------|------|
| Block 0 | `references/block0-subagent.md` | Subagent 개념 + 실습 |
| Block 1 | `references/block1-agent-teams.md` | Agent Teams 개념 + 실습 |
| Block 2 | `references/block2-multi-agent-session-wrap.md` | Multi-agent 패턴 + session-wrap 만들기 |
| Block 3 | `references/block3-session-analysis.md` | history-insight + session-analyzer 실습 |
| Block 4 | `references/block4-content-and-wrapup.md` | 콘텐츠 소화 체험 + 캠프 마무리 |

> 파일 경로는 이 SKILL.md 기준 상대경로다.
> 각 reference 파일은 `## EXPLAIN`, `## EXECUTE`, `## QUIZ` 섹션으로 구성된다.

---

## 진행 규칙

- 한 번에 한 블록씩 진행한다
- "다음", "skip", 블록 번호/이름으로 이동한다
- Block 2에서 생성한 스킬 파일(`my-session-wrap`)을 같은 블록 Phase B에서 실행한다
- 참가자의 프로젝트에 `.claude/skills/my-session-wrap/SKILL.md`를 생성한다
- Claude Code 관련 질문이 오면 claude-code-guide 에이전트(내장 도구)로 답변한다. 답변 후 사용자가 직접 따라할 수 있게 단계별로 안내하고, 질문할 때는 AskUserQuestion을 사용한다. 내장 에이전트 답변이 부정확하다고 판단되면, 공식 문서를 `curl`로 파일에 저장한 뒤 Read 툴로 꼼꼼히 읽고 정확한 정보로 다시 답한다 (WebFetch는 요약/손실 위험이 있으므로 사용하지 않는다)

---

## 시작

스킬 시작 시 **먼저 최신 커리큘럼을 설치**한 뒤 블록을 선택한다.

### Step 1: 최신 스킬 업데이트 (필수!)

> **Day 5 최종 수업입니다!** 아래 명령어로 반드시 최신 스킬을 업데이트하세요.
> 업데이트하지 않으면 오늘 실습에서 사용할 스킬이 없습니다.

아래 명령어를 출력하고 Bash로 실행한다:

```bash
npx skills add ai-native-camp/camp-2 --agent claude-code --yes
```

실행 결과를 간략히 안내하고, 오늘 사용할 스킬 목록을 보여준다:

| 사용할 스킬 | 설명 |
|------------|------|
| session-wrap | 세션 종료 시 작업을 자동 정리하는 multi-agent 스킬 |
| history-insight | 과거 세션 기록을 분석해 인사이트를 추출 |
| session-analyzer | 스킬이 의도대로 실행됐는지 검증 |
| fetch-tweet | X/Twitter 트윗을 가져와서 번역/요약 |
| content-digest | 콘텐츠를 Quiz-First 방식으로 소화/학습 |
| compound | 작업 중 발견한 인사이트를 구조화된 문서로 축적 |
| team-assemble | 복잡한 작업을 전문가 에이전트 팀으로 분해/실행 |

### Step 2: 블록 선택

아래 테이블을 보여주고 AskUserQuestion으로 어디서 시작할지 물어본다.

| Block | 주제 | 내용 |
|-------|------|------|
| 0 | Subagent | Subagent 개념 + 직접 사용해보기 |
| 1 | Agent Teams | 여러 에이전트가 팀으로 협력하는 구조 |
| 2 | Multi-agent + session-wrap | Multi-agent 패턴 + session-wrap 스킬 만들기 |
| 3 | 세션 분석 | history-insight + session-analyzer 실습 |
| 4 | 콘텐츠 소화 + 마무리 | fetch-tweet + content-digest + 5일 캠프 마무리 |

```json
AskUserQuestion({
  "questions": [{
    "question": "Day 5: Agent & Orchestration\n\n어디서부터 시작할까요?",
    "header": "시작 블록",
    "options": [
      {"label": "처음부터 (Block 0)", "description": "Subagent 개념부터 차근차근"},
      {"label": "Agent Teams (Block 1)", "description": "Subagent를 이미 알면 팀 구조부터"},
      {"label": "Multi-agent + 스킬 만들기 (Block 2)", "description": "패턴을 배우고 session-wrap 직접 만들기"},
      {"label": "세션 분석 (Block 3)", "description": "history-insight와 session-analyzer 실습부터"},
      {"label": "콘텐츠 소화 + 마무리 (Block 4)", "description": "fetch-tweet + content-digest + 캠프 마무리"}
    ],
    "multiSelect": false
  }]
})
```

> 시작 블록 선택 후 → 해당 블록의 Phase A부터 진행한다.
