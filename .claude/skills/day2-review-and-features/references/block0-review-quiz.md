# Block 0: Day 1 퀴즈 복습

> Block 0 특수 규칙: Phase A에서 AskUserQuestion으로 퀴즈 5문항을 출제한다 (AskUserQuestion 예외).
> Phase B 없음. 틀린 문제는 피드백 후 다음 문제로 넘어간다.

## EXPLAIN

"어제 배운 내용을 빠르게 복습합시다!"

Day 1에서 다룬 것:
- 터미널에서 `claude` 실행
- Git 기초 (commit = 게임 세이브)
- Python/Node.js 설치
- CLAUDE.md (항상 로딩되는 프로젝트 설명서)
- Memory (`/memory` 명령어)
- Skill (슬래시 명령어로 실행하는 업무 레시피)
- CSV 데이터 전처리 실습

## EXECUTE

아래 5문항을 AskUserQuestion으로 **한 문항씩 순서대로** 출제한다.
각 문항의 정답/오답 피드백을 즉시 제공한 뒤 다음 문항으로 넘어간다.

### 문항 1

```json
AskUserQuestion({
  "questions": [{
    "question": "CLAUDE.md는 어디에 저장되나요?",
    "header": "복습 퀴즈 1/5",
    "options": [
      {"label": "프로젝트 루트 폴더", "description": "프로젝트 최상위에 위치"},
      {"label": ".claude/skills/ 폴더 안", "description": "스킬 저장 위치와 혼동"},
      {"label": "홈 디렉토리", "description": "전역 설정 위치"},
      {"label": "아무 데나 상관없음", "description": "위치가 중요하지 않다고 생각"}
    ],
    "multiSelect": false
  }]
})
```

정답: 프로젝트 루트 폴더
피드백 (정답): "맞습니다! CLAUDE.md는 프로젝트 루트에 있어야 Claude Code가 자동으로 읽습니다."
피드백 (오답): "CLAUDE.md는 프로젝트 루트(최상위 폴더)에 저장해야 합니다. Claude Code가 시작할 때 자동으로 읽는 프로젝트 설명서예요."

### 문항 2

```json
AskUserQuestion({
  "questions": [{
    "question": "Memory를 확인하는 명령어는?",
    "header": "복습 퀴즈 2/5",
    "options": [
      {"label": "/memory", "description": "메모리 확인 명령어"},
      {"label": "/skill", "description": "스킬 관련 명령어"},
      {"label": "/status", "description": "상태 확인 명령어"},
      {"label": "/history", "description": "히스토리 명령어"}
    ],
    "multiSelect": false
  }]
})
```

정답: /memory
피드백 (정답): "정확합니다! /memory로 Claude가 기억하고 있는 내용을 확인할 수 있습니다."
피드백 (오답): "/memory가 정답입니다. Claude Code에서 `/memory`를 입력하면 저장된 기억을 확인하고 편집할 수 있어요."

### 문항 3

```json
AskUserQuestion({
  "questions": [{
    "question": "Skill을 실행하는 방법은?",
    "header": "복습 퀴즈 3/5",
    "options": [
      {"label": "슬래시 명령어 (예: /skill-name)", "description": "/ + 스킬 이름"},
      {"label": "터미널에서 python 실행", "description": "Python 스크립트 실행"},
      {"label": "CLAUDE.md에 적어두기", "description": "설명서와 혼동"},
      {"label": "Claude에게 '스킬 실행해줘'라고 말하기", "description": "자연어 요청"}
    ],
    "multiSelect": false
  }]
})
```

정답: 슬래시 명령어 (예: /skill-name)
피드백 (정답): "맞습니다! `/스킬이름`을 입력하면 해당 스킬이 실행됩니다. 어제 `/day1-test-skill`을 직접 해봤죠!"
피드백 (오답): "슬래시 명령어가 정답입니다. `/day1-test-skill`처럼 `/` + 스킬 이름을 입력하면 Claude가 해당 SKILL.md를 읽고 실행해요."

### 문항 4

```json
AskUserQuestion({
  "questions": [{
    "question": "CSV 전처리에서 가장 먼저 할 일은?",
    "header": "복습 퀴즈 4/5",
    "options": [
      {"label": "데이터 구조 파악", "description": "컬럼, 행 수, 데이터 타입 확인"},
      {"label": "바로 정리 시작", "description": "구조 파악 없이 작업"},
      {"label": "새 파일로 복사", "description": "백업부터"},
      {"label": "Claude에게 '알아서 해줘'라고 하기", "description": "자동 처리 요청"}
    ],
    "multiSelect": false
  }]
})
```

정답: 데이터 구조 파악
피드백 (정답): "정확합니다! 어떤 데이터든 먼저 구조를 파악해야 합니다. 컬럼이 뭐가 있는지, 몇 행인지, 데이터 타입은 뭔지 확인하는 게 첫 단계예요."
피드백 (오답): "데이터 구조 파악이 정답입니다. '알아서 해줘'보다 '먼저 이 CSV의 구조를 보여줘'라고 하면 훨씬 정확한 결과를 얻을 수 있어요."

### 문항 5

```json
AskUserQuestion({
  "questions": [{
    "question": "스킬을 만드는 이유는?",
    "header": "복습 퀴즈 5/5",
    "options": [
      {"label": "반복 작업 자동화", "description": "같은 작업을 매번 설명하지 않아도 됨"},
      {"label": "Claude가 더 빨라짐", "description": "속도와는 무관"},
      {"label": "필수 요구사항", "description": "없어도 Claude 사용 가능"},
      {"label": "코딩 연습", "description": "코딩이 목적은 아님"}
    ],
    "multiSelect": false
  }]
})
```

정답: 반복 작업 자동화
피드백 (정답): "맞습니다! 스킬은 반복되는 업무를 한 번 만들어두면 `/스킬이름` 한 마디로 실행할 수 있게 해줍니다."
피드백 (오답): "반복 작업 자동화가 정답입니다. 매번 같은 지시를 반복하는 대신, 스킬로 만들어두면 슬래시 명령어 한 번이면 끝이에요."

5문항 완료 후: "복습 완료! 다음 블록으로 넘어갈까요?"라고 안내하고 다음 블록으로 진행한다.

## QUIZ

> Block 0은 블록 자체가 퀴즈이므로 별도 QUIZ 섹션 없음.
