# Block 3: 세션 분석 도구

> 공식 문서: https://code.claude.com/docs/ko/skills

## EXPLAIN

### 1. 왜 세션 분석이 필요한가?

지금까지 Claude Code로 많은 작업을 했습니다. 하지만 "내가 어떤 패턴으로 일하는지", "스킬이 제대로 실행됐는지"를 돌아본 적은 없을 겁니다.

**비유: 업무 일지 + 품질 감사**

- **history-insight** = 업무 일지를 돌아보며 패턴 발견하기
- **session-analyzer** = 체크리스트로 "이거 제대로 했나?" 확인하기

둘 다 "과거를 돌아보는 도구"이지만, 목적이 다릅니다.

---

### 2. history-insight: 인사이트 추출

**비유: "한 달 치 업무 일지를 읽고, 숨겨진 패턴을 찾는 것"**

history-insight는 과거 세션 기록에서 인사이트를 추출합니다:

| 분석 항목 | 예시 |
|-----------|------|
| **자주 하는 작업** | "CSV 분석을 가장 많이 했네요" |
| **반복 패턴** | "매번 같은 전처리를 하고 있어요" |
| **성장 포인트** | "Day 1에는 단순 질문, Day 5에는 multi-agent를 씁니다" |
| **개선 기회** | "이 작업은 스킬로 만들면 자동화할 수 있어요" |

**언제 쓰나요?**
- 일주일에 한 번 "이번 주 내가 뭘 했지?" 돌아볼 때
- 자주 반복하는 작업을 발견해서 자동화하고 싶을 때
- 학습 성장 궤적을 확인하고 싶을 때

---

### 3. session-analyzer: 실행 검증

**비유: "체크리스트로 품질 감사하는 것"**

session-analyzer는 스킬이 의도대로 실행됐는지 검증합니다:

```
스킬 설계: "Phase 1에서 4개 에이전트 병렬 실행"
실제 실행: "3개만 실행됨"
검증 결과: "⚠️ 1개 에이전트 누락"
```

| 검증 항목 | 확인 내용 |
|-----------|-----------|
| **실행 완료** | 모든 단계가 실행됐는지 |
| **순서 준수** | Phase 1 → Phase 2 순서가 맞는지 |
| **결과 품질** | 각 에이전트의 출력이 의도한 형식인지 |
| **에러 발견** | 실행 중 오류가 있었는지 |

**언제 쓰나요?**
- 만든 스킬이 제대로 동작하는지 확인할 때
- "왜 결과가 이상하지?" 싶을 때
- 스킬을 개선하기 위해 어디가 문제인지 찾을 때

---

### 4. 두 도구의 관계

```
history-insight (넓게 보기)     session-analyzer (좁게 보기)
┌─────────────────────┐       ┌─────────────────────┐
│ "이번 주 전체 패턴"    │       │ "이 스킬 실행 결과"    │
│  어떤 작업을 했나      │       │  제대로 동작했나       │
│  반복 패턴은 뭔가      │       │  어디가 문제인가       │
│  성장했나             │       │  어떻게 개선하나       │
└─────────────────────┘       └─────────────────────┘
```

- history-insight: **숲 보기** (전체 패턴)
- session-analyzer: **나무 보기** (개별 실행 검증)

---

## EXECUTE

아래 순서대로 따라해보세요.

### Step 1. history-insight 실행

Claude에게 아래와 같이 입력하세요:

```
/history-insight
```

> history-insight가 지금까지의 세션 기록을 분석합니다.
>
> **관찰 포인트**:
> - 자주 사용한 기능이 뭔지
> - 반복되는 패턴이 있는지
> - 성장 궤적이 보이는지

### Step 2. session-analyzer 실행

Block 2에서 만든 my-session-wrap 스킬의 실행 결과를 검증합니다:

```
/session-analyzer
```

> session-analyzer가 직전 세션에서 스킬이 어떻게 실행됐는지 분석합니다.
>
> **관찰 포인트**:
> - 모든 Phase가 실행됐는지
> - 에이전트 실행 순서가 맞는지
> - 개선할 점이 있는지

### Step 3. 두 도구의 차이 느끼기

Claude에게 아래와 같이 물어보세요:

```
history-insight와 session-analyzer의 결과를 비교해줘.
하나는 전체 패턴을 보는 것이고, 다른 하나는 개별 실행을 검증하는 건데, 실제로 어떤 차이가 있었어?
```

---

## QUIZ

```json
AskUserQuestion({
  "questions": [
    {
      "question": "history-insight와 session-analyzer의 차이는?",
      "header": "Quiz 3-1",
      "options": [
        {"label": "history-insight는 과거 기록, session-analyzer는 미래 예측", "description": "시간 관점의 차이"},
        {"label": "history-insight는 전체 패턴에서 인사이트 추출, session-analyzer는 개별 스킬 실행 검증", "description": "숲 보기 vs 나무 보기"},
        {"label": "history-insight는 자동 실행, session-analyzer는 수동 실행", "description": "실행 방식의 차이"}
      ],
      "multiSelect": false
    },
    {
      "question": "세션 분석이 유용한 이유는?",
      "header": "Quiz 3-2",
      "options": [
        {"label": "Claude Code의 버그를 찾기 위해", "description": "소프트웨어 디버깅 목적"},
        {"label": "작업 패턴을 파악하고 개선점을 찾기 위해", "description": "반복 작업 자동화, 스킬 개선, 성장 추적"},
        {"label": "세션 비용을 계산하기 위해", "description": "비용 관리 목적"}
      ],
      "multiSelect": false
    }
  ]
})
```

**정답 3-1: 2번.** history-insight는 전체 세션 기록에서 패턴과 인사이트를 추출하는 "숲 보기" 도구이고, session-analyzer는 특정 스킬이 의도대로 실행됐는지 검증하는 "나무 보기" 도구이다.

**정답 3-2: 2번.** 세션 분석의 핵심 가치는 자기 작업 패턴을 객관적으로 파악하는 것이다. 반복 작업을 발견하면 자동화하고, 스킬 실행에 문제가 있으면 개선하고, 시간에 따른 성장을 추적할 수 있다.
