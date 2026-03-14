# Block 4: 콘텐츠 소화 + 캠프 마무리

> 공식 문서: https://code.claude.com/docs/ko/skills

## EXPLAIN

### 1. 스킬 체이닝 (Skill Chaining)

**비유: "공장 생산라인"**

지금까지 스킬을 하나씩 따로 사용했습니다. 하지만 실전에서는 **한 스킬의 결과를 다른 스킬의 입력으로 연결**하는 경우가 많습니다.

```
[URL 입력] → [fetch-tweet: 원문 추출 + 번역] → [content-digest: 퀴즈로 학습]
```

이것을 **스킬 체이닝**이라고 합니다. 공장에서 원자재가 생산라인을 타고 완제품이 되는 것처럼, 콘텐츠가 스킬을 거치면서 "나의 지식"이 됩니다.

---

### 2. fetch-tweet: 트윗 가져오기

X/Twitter URL을 받으면:
1. **원문 추출**: FxEmbed API로 트윗 텍스트, 작성자, 반응 수치를 가져옴
2. **번역 파이프라인**: 요약(3-5문장) → 인사이트(3개) → 전체 번역

```
원래 URL: https://x.com/user/status/123456
변환 URL: https://api.fxtwitter.com/user/status/123456
```

왜 요약부터? **전체 번역을 먼저 보면 핵심을 놓치기 쉽습니다.** 요약으로 핵심을 잡고, 인사이트로 의미를 파악한 뒤, 전체를 읽으면 이해도가 훨씬 높아집니다.

---

### 3. content-digest: Quiz-First 학습법

가져온 콘텐츠를 "소화"하는 스킬입니다.

**핵심 원칙: "요약을 먼저 보여주지 않는다"**

보통은 요약을 읽고 → 퀴즈를 풀지만, 연구에 따르면 **반대로 하는 것이 9-12% 더 효과적**입니다.

```
일반적 순서: 요약 읽기 → 퀴즈
Quiz-First:  퀴즈 먼저 → 틀린 부분 확인 → 선택적으로 읽기
```

- **Pretesting Effect**: 학습 전 테스트가 기억력을 9-12% 향상 (Richland et al.)
- **Information Gap Theory**: 틀린 문제가 "궁금함"을 만들고, 궁금함이 도파민 → 기억 강화

**간단히 말해: 틀려야 배운다.**

---

### 4. compound: 인사이트 축적

작업 중 발견한 인사이트를 구조화된 문서로 기록하는 스킬입니다.

**비유: "복리 통장"**

매일 100원씩 넣으면 처음에는 별것 아니지만, 1년이 지나면 큰 금액이 됩니다. compound도 마찬가지입니다. 작은 인사이트를 매일 기록하면, 나만의 지식 베이스가 복리로 성장합니다.

```
/compound → 도메인 선택 (work/learning/project/tool/personal) → 인사이트 기록 → knowledge/ 폴더에 저장
```

---

### 5. team-assemble: 전문가 팀 구성

Block 1에서 체험한 team-assemble을 다시 한번 살펴봅니다.

복잡한 작업을 주면:
1. 필요한 전문가 역할을 자동으로 설계
2. 각 역할에 최적의 모델을 배정 (복잡한 판단 = opus, 실행 = sonnet)
3. 병렬로 실행하고 결과를 종합

이것이 Block 0(Subagent) → Block 1(Agent Teams) → Block 2(Multi-agent) 의 최종 형태입니다.

---

### 6. 5일 캠프 전체 흐름

| Day | 배운 것 | 만든 것 |
|-----|---------|---------|
| Day 1 | Claude Code 핵심 기능, CLAUDE.md, Memory, Skill | 첫 Memory, 첫 스킬, Plugin 설치 |
| Day 2 | MCP, Hook, Plugin, Context Sync | MCP 연결, Context Sync 스킬 |
| Day 3 | Clarify, Plugin 심화, GitHub | 나만의 Clarify 스킬, PRD 제출 |
| Day 4 | session-wrap, 세션 분석, 콘텐츠 소화 | session-wrap 스킬, content-digest 체험 |
| Day 5 | Subagent, Agent Teams, Multi-agent, Orchestration | my-session-wrap, 에이전트 팀 실행, 세션 분석 |

**성장 궤적:**

```
Day 1: "Claude에게 질문하기"
Day 2: "외부 도구 연결하기"
Day 3: "나만의 스킬 만들기"
Day 4: "Multi-agent 스킬 만들기"
Day 5: "에이전트 팀을 오케스트레이션하기"
```

도구 사용자 → 스킬 제작자 → 오케스트레이터로 성장했습니다.

---

## EXECUTE

### 선택 실습

아래 3가지 중 하나를 선택해서 체험합니다. (AskUserQuestion으로 선택)

**A) content-digest 체험: Quiz-First로 학습하기**

관심있는 URL을 하나 찾아서 Claude에게 이렇게 입력하세요:

```
/content-digest [URL을 여기에 붙여넣기]
```

> URL 예시:
> - 좋아하는 영어 트윗 URL
> - 관심있는 기술 블로그 글 URL
> - YouTube 영상 URL

Quiz-First 방식으로 퀴즈가 먼저 출제됩니다. 틀려도 괜찮습니다. 틀려야 배웁니다!

**B) compound 체험: 인사이트 기록하기**

오늘 배운 인사이트를 compound로 기록합니다:

```
/compound
```

예시 인사이트:
- "Subagent는 1:1 위임, Agent Teams는 N명 협력이라는 구조적 차이가 있다"
- "2-Phase Pipeline에서 Phase 2(검증)가 필수인 이유는 병렬 작업의 중복 제거 때문이다"
- "스킬 체이닝은 공장 생산라인처럼 결과를 연결하는 것이다"

**C) team-assemble 체험: 에이전트 팀으로 프로젝트 실행**

```
/team-assemble 이 프로젝트의 스킬 목록을 분석하고, 각 스킬의 활용 가이드를 만들고, 품질을 검증해줘
```

### 5일 캠프 전체 회고

선택 실습이 끝나면, Claude에게 이렇게 요청하세요:

```
이 5일간 내가 배운 것들을 정리해줘. Day 1부터 Day 5까지 어떤 성장을 했는지, 앞으로 어떻게 활용할 수 있는지 포함해서.
```

---

## QUIZ

```json
AskUserQuestion({
  "questions": [
    {
      "question": "5일간 배운 핵심 기능을 3가지 이상 나열한다면?",
      "header": "종합 Quiz 1 (자유 응답)",
      "options": [
        {"label": "CLAUDE.md, Memory, Skill, MCP, Hook, Plugin", "description": "Day 1~2에서 배운 기초 기능들"},
        {"label": "Clarify, GitHub, Subagent, Agent Teams", "description": "Day 3~5에서 배운 심화 기능들"},
        {"label": "위 두 가지 모두", "description": "기초부터 심화까지 전체"}
      ],
      "multiSelect": false
    },
    {
      "question": "AI 네이티브 워크플로우란?",
      "header": "종합 Quiz 2",
      "options": [
        {"label": "AI가 사람의 일을 대신하는 완전 자동화", "description": "사람은 관여하지 않는다"},
        {"label": "AI를 도구가 아닌 업무 파트너로 활용하는 방식", "description": "사람과 AI가 협력하여 더 나은 결과를 만든다"},
        {"label": "AI를 사용하는 모든 업무 방식", "description": "AI를 쓰기만 하면 된다"}
      ],
      "multiSelect": false
    },
    {
      "question": "앞으로 Claude Code를 어떻게 활용할 계획인가요?",
      "header": "종합 Quiz 3 (자유 응답)",
      "options": [
        {"label": "업무 자동화 스킬을 만들어서 반복 작업 줄이기", "description": "효율성 향상"},
        {"label": "팀 워크플로우를 AI 네이티브로 재설계하기", "description": "조직 차원의 변화"},
        {"label": "아직 구체적인 계획은 없지만 천천히 적용해보기", "description": "점진적 도입"}
      ],
      "multiSelect": true
    }
  ]
})
```

**정답 종합 Quiz 1: 3번.** 5일간 CLAUDE.md, Memory, Skill, MCP, Hook, Plugin, Clarify, GitHub, Subagent, Agent Teams, Multi-agent, session-wrap, content-digest 등 다양한 기능을 배웠다. 기초(Day 1~2)와 심화(Day 3~5) 모두 중요하다.

**정답 종합 Quiz 2: 2번.** AI 네이티브 워크플로우는 AI가 사람을 대체하는 것이 아니라, AI를 업무 파트너로 활용하는 방식이다. 사람이 방향을 정하고, AI가 실행을 돕고, 함께 더 나은 결과를 만든다.

**정답 종합 Quiz 3: 모두 정답.** 어떤 계획이든 좋다. 중요한 것은 실제로 사용하면서 배우는 것이다.

### 5일 캠프 마무리

축하합니다! 5일 캠프를 모두 마쳤습니다.

5일 전에는 Claude Code가 뭔지도 몰랐을 수 있습니다. 지금은:

- **CLAUDE.md**로 AI에게 맥락을 줄 수 있고
- **Skill**을 직접 만들 수 있고
- **MCP**로 외부 도구를 연결할 수 있고
- **Clarify**로 모호한 요구사항을 명확하게 만들 수 있고
- **Subagent**와 **Agent Teams**로 여러 AI를 오케스트레이션할 수 있습니다

이제 Claude Code라는 도구를 자유롭게 활용할 수 있는 **AI 네이티브**가 되었습니다.

> **수료가 아니라 시작입니다.** 만든 스킬을 매일 사용하면서 개선해보세요. 실제 사용이 최고의 학습입니다.
