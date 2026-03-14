# Block 1: 기본 개념 — CLAUDE.md, Memory, Skill

> Claude Code의 3가지 핵심 개념을 배운다.

> **Phase A 시작 시 반드시 아래 형태로 출력한다:**
> ```
> 📖 공식 문서 (CLAUDE.md): https://docs.anthropic.com/en/docs/claude-code/memory#claudemd
> 📖 공식 문서 (Memory): https://docs.anthropic.com/en/docs/claude-code/memory
> 📖 공식 문서 (Skill): https://docs.anthropic.com/en/docs/claude-code/skills
> ```

## EXPLAIN

### 1. CLAUDE.md — 프로젝트의 설명서

CLAUDE.md는 프로젝트 폴더에 넣어두는 파일이다. Claude Code를 실행하면 이 파일을 자동으로 읽는다.

| 항목 | 내용 |
|------|------|
| 역할 | 프로젝트의 배경, 규칙, 스타일을 Claude에게 알려준다 |
| 비유 | 신입사원에게 주는 업무 매뉴얼. "우리 팀은 이렇게 일해" |
| 위치 | 프로젝트 폴더 최상위에 `CLAUDE.md` 파일로 저장 |
| 특징 | Claude Code를 실행할 때마다 **항상 자동으로** 읽힌다 |

예시: 패션 플랫폼 MD라면 이런 내용을 넣을 수 있다.

```markdown
# CLAUDE.md

## 프로젝트 소개
패션 플랫폼 상품 관리 프로젝트

## 규칙
- 브랜드명은 한글로 표기
- 가격은 원 단위, 천 단위 쉼표 표기
- 시즌 표기: 25SS, 24FW 형식
```

### 2. Memory — 대화 사이의 기억

Memory는 Claude가 세션이 바뀌어도 기억하는 메모장이다.

| 항목 | 내용 |
|------|------|
| 역할 | 사용자의 선호, 환경, 습관 등을 세션 간에 기억 |
| 비유 | 포스트잇 메모. "이 사람은 Windows 사용자" |
| 관리 | `/memory` 명령어로 확인 및 수정 |
| 특징 | CLAUDE.md와 달리 프로젝트가 아닌 **사용자 단위** |

CLAUDE.md vs Memory 차이:

```
CLAUDE.md ─── 프로젝트에 대한 정보 ─── 파일로 저장 ─── 팀원과 공유 가능
Memory    ─── 사용자에 대한 정보 ─── Claude가 관리 ─── 개인적
```

### 3. Skill — 작업 레시피

Skill은 Claude에게 특정 작업 방법을 가르치는 문서다.

| 항목 | 내용 |
|------|------|
| 역할 | 반복 작업을 한 번 정의하면 다음부터 한 줄로 실행 |
| 비유 | 요리 레시피. "이 순서대로 이렇게 해줘" |
| 실행 | 슬래시 명령어 (예: `/data-cleanup`) 또는 자동 매칭 |
| 위치 | `.claude/skills/스킬이름/SKILL.md` |

> 지금 이 수업 자체도 Skill이다! `.claude/skills/day1-setup-and-data/SKILL.md`에 저장되어 있다.

### 3가지의 관계

```
┌─ CLAUDE.md ──────────────────────────────────┐
│ 항상 읽힘. 프로젝트 전체의 규칙/배경          │
└──────────────────────────────────────────────┘
         ▲ 프로젝트 단위

┌─ Memory ─────────────────────────────────────┐
│ 항상 읽힘. 사용자 개인의 선호/환경            │
└──────────────────────────────────────────────┘
         ▲ 사용자 단위

┌─ Skill A ──┐  ┌─ Skill B ──┐  ┌─ Skill C ──┐
│ 필요할 때만  │  │ 필요할 때만  │  │ 필요할 때만  │
│ 로딩        │  │ 로딩        │  │ 로딩        │
└────────────┘  └────────────┘  └────────────┘
         ▲ 작업 단위
```

## EXECUTE

아래 3가지를 순서대로 실행해보세요:

### 1. CLAUDE.md 만들기

Claude Code 대화창에 아래를 입력한다:

```
이 프로젝트의 CLAUDE.md를 만들어줘.
나는 패션 플랫폼 MD이고, 상품 데이터와 매출 데이터를 다뤄.
Windows를 사용해.
```

> Claude가 CLAUDE.md 파일을 자동으로 만들어준다. 내용을 읽어보고 마음에 안 드는 부분이 있으면 수정을 요청하자.

### 2. Memory 체험

Claude Code 대화창에 아래를 입력한다:

```
내가 Windows를 사용한다는 걸 기억해줘
```

그 다음 `/memory` 명령어를 입력해서 저장된 내용을 확인한다.

### 3. Skill 체험

Claude Code 대화창에 아래를 입력한다:

```
/day1-test-skill
```

> 테스트 스킬이 실행되면서 축하 메시지가 나온다. Skill이 어떻게 동작하는지 직접 느껴보자.

## QUIZ

```json
AskUserQuestion({
  "questions": [{
    "question": "CLAUDE.md의 역할은 무엇인가요?",
    "header": "Quiz 1-1: CLAUDE.md",
    "options": [
      {"label": "프로젝트 설명서/매뉴얼", "description": "프로젝트의 배경, 규칙, 스타일을 Claude에게 알려주는 파일"},
      {"label": "Claude의 설치 파일", "description": "Claude Code를 설치할 때 필요한 설정 파일"},
      {"label": "대화 기록 저장소", "description": "이전 대화 내용을 저장하는 파일"}
    ],
    "multiSelect": false
  }]
})
```

정답: 1번. CLAUDE.md는 프로젝트의 설명서/매뉴얼이다. 신입사원에게 주는 업무 매뉴얼처럼, Claude에게 "이 프로젝트는 이렇게 해"를 알려준다.

```json
AskUserQuestion({
  "questions": [{
    "question": "Memory와 CLAUDE.md의 차이는 무엇인가요?",
    "header": "Quiz 1-2: Memory vs CLAUDE.md",
    "options": [
      {"label": "Memory는 사용자 기억, CLAUDE.md는 프로젝트 설명", "description": "Memory는 대화 간 개인 기억, CLAUDE.md는 프로젝트 고정 정보"},
      {"label": "둘 다 같은 역할이다", "description": "저장 방식만 다르고 기능은 같다"},
      {"label": "Memory가 CLAUDE.md보다 우선순위가 높다", "description": "충돌 시 Memory가 이긴다"}
    ],
    "multiSelect": false
  }]
})
```

정답: 1번. Memory는 사용자 개인의 선호/환경을 세션 간에 기억하는 것이고, CLAUDE.md는 프로젝트의 고정 정보(규칙, 배경)를 담는 파일이다.

```json
AskUserQuestion({
  "questions": [{
    "question": "Skill은 어떻게 실행하나요?",
    "header": "Quiz 1-3: Skill 실행",
    "options": [
      {"label": "슬래시 명령어로 실행", "description": "/스킬이름 형태로 입력"},
      {"label": "CLAUDE.md에 적어두면 자동 실행", "description": "CLAUDE.md에 스킬 이름을 적는다"},
      {"label": "별도 프로그램을 설치해야 한다", "description": "npm으로 스킬을 설치한다"}
    ],
    "multiSelect": false
  }]
})
```

정답: 1번. Skill은 `/스킬이름` 형태의 슬래시 명령어로 실행한다. 또는 대화 내용에 따라 자동으로 매칭되기도 한다.
