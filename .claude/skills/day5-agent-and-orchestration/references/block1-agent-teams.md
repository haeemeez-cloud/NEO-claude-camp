# Block 1: Agent Teams

> 공식 문서: https://docs.anthropic.com/en/docs/claude-code/agent-teams

## EXPLAIN

### 1. Agent Teams란?

**비유: "프로젝트 TF팀"**

Block 0에서 배운 Subagent는 **1:1 관계**였습니다. 팀장이 팀원 한 명에게 "이거 해와"라고 시키는 것이죠.

**Agent Teams**는 여러 에이전트를 **팀으로 묶어서 협력**하게 하는 것입니다. 프로젝트 TF(Task Force)팀을 만드는 것과 같습니다.

```
Subagent (Block 0):
  Claude(팀장) → Claude(팀원 A): "이거 해와"
  Claude(팀장) → Claude(팀원 B): "저거 해와"
  (각자 독립적으로 일함)

Agent Teams (Block 1):
  Claude(PM) → TF팀 구성
    ├─ Claude(기획자): 방향 설정
    ├─ Claude(분석가): 데이터 분석
    ├─ Claude(실행자): 구현
    └─ Claude(검증자): 품질 확인
  (역할이 정해지고, 결과를 공유하며 협력)
```

---

### 2. Subagent vs Agent Teams

| 비교 | Subagent | Agent Teams |
|------|----------|-------------|
| **관계** | 1:1 (팀장 ↔ 팀원) | 1:N (PM ↔ TF팀) |
| **역할** | 단순 위임 | 전문 역할 부여 |
| **협력** | 독립적 실행 | 결과 공유 + 순서 조율 |
| **적합한 상황** | 단순한 병렬 작업 | 복잡한 프로젝트 |
| **비유** | "팀원에게 심부름" | "프로젝트 TF팀 구성" |

**언제 Subagent, 언제 Agent Teams?**

- "파일 3개 동시에 분석해줘" → Subagent (단순 병렬)
- "이 데이터를 분석해서 보고서 쓰고 검증까지 해줘" → Agent Teams (역할 분리 + 순서)

---

### 3. Agent Teams의 구조

Agent Teams는 4단계로 동작합니다:

```
1. TeamCreate: 팀을 만든다 ("프로젝트팀 만들어")
      ↓
2. TaskCreate: 각 팀원에게 할 일을 배정한다 ("너는 분석, 너는 실행")
      ↓
3. Task 실행: 각 팀원이 일을 한다 (병렬 또는 순차)
      ↓
4. 결과 종합: PM이 결과를 모아서 보고한다
```

회사에서 프로젝트를 시작할 때와 동일합니다:
1. TF팀을 구성하고
2. 각자 역할을 정하고
3. 일을 진행하고
4. 결과를 모아서 보고

---

### 4. team-assemble 스킬

이 프로젝트에는 **team-assemble**이라는 스킬이 이미 설치되어 있습니다. 이 스킬은 위 4단계를 자동으로 처리해줍니다:

- 작업을 분석해서 필요한 역할을 자동으로 설계
- 팀을 구성하고 각 역할에 최적의 모델을 배정
- 병렬로 실행하고 결과를 종합

team-assemble은 Agent Teams의 "자동화된 버전"입니다. 직접 팀을 구성하지 않아도, 작업을 주면 알아서 팀을 만들어줍니다.

---

## EXECUTE

아래 순서대로 따라해보세요.

### Step 1. team-assemble 스킬 구조 확인

Claude에게 아래와 같이 입력하세요:

```
team-assemble 스킬의 구조를 보여줘. SKILL.md 내용을 읽고 핵심 구조를 표로 정리해줘.
```

> **관찰 포인트**: Phase 1(분석) → Phase 2(팀 생성) → Phase 3(실행) → Phase 4(정리) 4단계 구조를 확인하세요.

### Step 2. Agent Teams로 분석 프로젝트 실행

Claude에게 아래와 같이 입력하세요 (data/ 폴더에 CSV가 있는 경우):

```
에이전트 팀을 구성해서 다음 작업을 해줘:
1) 분석팀원: data/ 폴더의 CSV 파일을 분석해서 핵심 인사이트 추출
2) 보고서팀원: 분석 결과를 보고서 형태로 정리
3) 검증팀원: 보고서의 정확성을 검증

브랜드별 1월 매출 분석 보고서를 만들어줘.
```

CSV 파일이 없다면 아래를 입력하세요:

```
에이전트 팀을 구성해서 다음 작업을 해줘:
1) 조사팀원: .claude/skills/ 폴더의 모든 스킬을 분석
2) 정리팀원: 각 스킬의 목적과 사용법을 표로 정리
3) 검증팀원: 정리된 내용이 정확한지 확인

이 프로젝트의 스킬 가이드를 만들어줘.
```

> **관찰 포인트**:
> - 팀 구성 제안이 나오면 내용을 읽고 "좋아요, 실행해주세요"를 선택하세요
> - 여러 팀원이 동시에 일하는 것을 관찰하세요
> - 최종 결과에서 각 팀원의 기여가 어떻게 합쳐지는지 확인하세요

### Step 3. Subagent와 비교

Claude에게 아래와 같이 물어보세요:

```
방금 Agent Teams로 한 것과, Block 0에서 Subagent로 한 것의 차이가 뭐였어?
```

---

## QUIZ

```json
AskUserQuestion({
  "questions": [
    {
      "question": "Subagent와 Agent Teams의 가장 큰 차이는?",
      "header": "Quiz 1-1",
      "options": [
        {"label": "Subagent는 무료, Agent Teams는 유료", "description": "비용 차이"},
        {"label": "Subagent는 1:1 위임, Agent Teams는 여러 명이 역할을 나눠 협력", "description": "관계와 협력 구조의 차이"},
        {"label": "Subagent는 느리고, Agent Teams는 빠르다", "description": "속도 차이"}
      ],
      "multiSelect": false
    },
    {
      "question": "Agent Teams에서 각 팀원의 역할을 정하는 이유는?",
      "header": "Quiz 1-2",
      "options": [
        {"label": "Claude가 역할이 없으면 동작하지 않아서", "description": "기술적 제약 때문"},
        {"label": "전문성을 분리하면 각 역할의 품질이 올라가서", "description": "분석가는 분석에, 검증자는 검증에 집중"},
        {"label": "비용을 절약하기 위해 작은 모델을 쓰려고", "description": "경제적 이유"}
      ],
      "multiSelect": false
    }
  ]
})
```

**정답 1-1: 2번.** Subagent는 1:1로 단순히 일을 위임하는 것이고, Agent Teams는 여러 에이전트가 각자 전문 역할을 맡아서 협력하는 것이다. TF팀처럼 기획자, 분석가, 검증자가 함께 일한다.

**정답 1-2: 2번.** 역할을 명확히 분리하면 각 팀원이 자기 전문 분야에 집중할 수 있다. "분석도 하고 보고서도 쓰고 검증도 해"보다 "너는 분석만, 너는 보고서만, 너는 검증만"이 품질이 더 높다.
