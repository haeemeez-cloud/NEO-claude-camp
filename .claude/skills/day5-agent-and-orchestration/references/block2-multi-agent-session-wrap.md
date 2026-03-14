# Block 2: Multi-agent 패턴 + session-wrap 만들기

> 공식 문서: https://docs.anthropic.com/en/docs/claude-code/sub-agents
> 공식 문서: https://code.claude.com/docs/ko/skills

## EXPLAIN

### 1. Multi-agent 패턴 복습

Block 0에서 Subagent(1:1 위임), Block 1에서 Agent Teams(N명 협력)를 배웠습니다. 이제 실전에서 가장 많이 쓰이는 **Multi-agent 패턴**을 정리합니다.

**핵심 패턴: 2-Phase Pipeline**

```
Phase 1: 여러 전문가가 동시에 분석 (병렬)
  ┌────────────────┬────────────────┐
  │  전문가 A       │  전문가 B       │
  ├────────────────┼────────────────┤
  │  전문가 C       │  전문가 D       │
  └────────────────┴────────────────┘
         │                │
         ▼                ▼
Phase 2: 검증자가 결과를 정리 (순차)
  ┌────────────────────────────────┐
  │         검증자                  │
  │  (중복 제거, 품질 확인)          │
  └────────────────────────────────┘
```

**비유: 경영 회의**

- Phase 1: 각 팀장이 동시에 보고서를 작성한다 (마케팅팀, 개발팀, 디자인팀, 운영팀)
- Phase 2: 총괄이 4개 보고서를 모아서 중복을 정리하고 최종 보고서를 만든다

Phase 1은 **병렬**(동시에), Phase 2는 **순차**(Phase 1이 끝난 뒤)입니다.

---

### 2. session-wrap이 2-Phase Pipeline을 쓰는 이유

Day 4에서 배운 session-wrap을 기억하시나요? session-wrap은 바로 이 2-Phase Pipeline을 사용합니다:

| Phase | 에이전트 | 하는 일 |
|-------|----------|---------|
| Phase 1 (병렬) | doc-updater | 문서 중 업데이트가 필요한 곳을 찾아냄 |
| Phase 1 (병렬) | automation-scout | 반복되는 패턴을 발견하고 자동화를 제안 |
| Phase 1 (병렬) | learning-extractor | 오늘 배운 것을 정리 |
| Phase 1 (병렬) | followup-suggester | 다음에 할 일을 제안 |
| Phase 2 (순차) | duplicate-checker | Phase 1 결과에서 겹치는 내용을 걸러냄 |

4명이 독립적으로 일하면 비슷한 제안이 나올 수 있습니다. 예를 들어 doc-updater가 "README 업데이트 필요"라고 하고, followup-suggester도 "다음에 README 수정하세요"라고 할 수 있죠. duplicate-checker가 이런 중복을 정리합니다.

---

### 3. 오늘 할 것: session-wrap 스킬 직접 만들기

원본 session-wrap 스킬은 플러그인으로 이미 설치되어 있습니다. 오늘은 이것을 참고해서 **나만의 session-wrap 스킬**을 직접 만들어봅니다.

만들 파일: `.claude/skills/my-session-wrap/SKILL.md`

**왜 직접 만드나요?**
- 원본을 읽기만 하면 "아 그렇구나"에서 끝남
- 직접 만들면 "왜 이렇게 구성했는지"를 이해하게 됨
- 나중에 자기 업무에 맞는 multi-agent 스킬을 만들 수 있게 됨

---

## EXECUTE

아래 순서대로 따라해보세요. Claude가 안내하는 대로 Step-by-Step으로 진행합니다.

### Step 1. 원본 구조 파악

먼저 원본 session-wrap 스킬을 읽어봅니다:

```
설치된 session-wrap 스킬의 SKILL.md 내용을 보여줘. 핵심 구조를 표로 정리해줘.
```

> 원본의 구조를 파악한 뒤, 이것을 참고해서 나만의 버전을 만듭니다.

### Step 2. my-session-wrap 스킬 만들기

Claude에게 아래와 같이 입력하세요:

```
나만의 session-wrap 스킬을 만들어줘. 아래 조건으로:

1. 경로: .claude/skills/my-session-wrap/SKILL.md
2. frontmatter에 name과 description 포함
3. 2-Phase Pipeline 구조:
   - Phase 1 (병렬): 에이전트 3~4개 (역할은 원본 참고하되, 내가 이해한 대로)
   - Phase 2 (순차): 검증 에이전트 1개
4. 각 에이전트의 역할과 출력 형식을 명시
5. 전체 실행 흐름을 다이어그램으로 표현

원본 session-wrap을 참고하되, 복붙이 아니라 내가 이해한 구조로 다시 작성해줘.
```

> **핵심**: "복붙이 아니라 내가 이해한 구조로"가 중요합니다. 원본을 그대로 복사하면 학습 효과가 없습니다.

### Step 3. 만든 스킬 확인

스킬이 만들어졌으면 아래와 같이 확인하세요:

```
내가 만든 my-session-wrap 스킬을 읽고, 원본과 비교해서 차이점을 알려줘.
```

### Step 4. 만든 스킬 실행

직접 만든 스킬을 실행해봅니다:

```
/my-session-wrap
```

> **관찰 포인트**:
> - Phase 1 에이전트들이 병렬로 실행되는지
> - Phase 2 검증 에이전트가 중복을 잡아내는지
> - 최종 결과가 깔끔하게 정리되는지

---

## QUIZ

```json
AskUserQuestion({
  "questions": [
    {
      "question": "2-Phase Pipeline에서 Phase 1과 Phase 2의 차이는?",
      "header": "Quiz 2-1",
      "options": [
        {"label": "Phase 1은 쉬운 작업, Phase 2는 어려운 작업", "description": "난이도에 따른 구분"},
        {"label": "Phase 1은 병렬 분석, Phase 2는 순차 검증", "description": "여러 전문가가 동시에 분석한 뒤, 검증자가 결과를 정리"},
        {"label": "Phase 1은 사용자가, Phase 2는 Claude가 하는 것", "description": "실행 주체에 따른 구분"}
      ],
      "multiSelect": false
    },
    {
      "question": "session-wrap은 언제 사용하나요?",
      "header": "Quiz 2-2",
      "options": [
        {"label": "프로젝트를 처음 시작할 때", "description": "초기 설정을 위해"},
        {"label": "세션이나 작업이 끝날 때 정리용으로", "description": "퇴근 전 책상 정리 루틴처럼"},
        {"label": "에러가 발생했을 때 디버깅용으로", "description": "문제 해결을 위해"}
      ],
      "multiSelect": false
    }
  ]
})
```

**정답 2-1: 2번.** Phase 1은 여러 전문가 에이전트가 동시에(병렬) 각자 분석하는 단계이고, Phase 2는 검증 에이전트가 Phase 1의 결과를 모아서 중복을 제거하고 정리하는 순차 단계이다.

**정답 2-2: 2번.** session-wrap은 코딩 세션이나 작업이 끝날 때 사용하는 정리 스킬이다. 오늘 한 일, 배운 것, 다음 할 일을 자동으로 정리해준다. 퇴근 전 책상 정리 루틴과 같다.
