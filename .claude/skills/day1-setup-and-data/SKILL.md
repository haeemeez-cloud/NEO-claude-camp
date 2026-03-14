---
name: day1-setup-and-data
description: AI Native Camp Day 1 환경 설치 + 데이터 실습. Git/Python/Node.js/Claude Code를 설치하고, CSV 데이터 전처리를 실습하고, 나만의 전처리 스킬을 만든다. "1일차", "Day 1", "설치", "설정", "CSV" 요청에 사용.
---

# Day 1: 설치 + 데이터 실습

이 스킬이 호출되면 아래 **STOP PROTOCOL**을 반드시 따른다.

---

## 용어 정리

이 스킬에서 사용하는 핵심 용어:

| 용어 | 설명 |
|------|------|
| **CLI** | Command Line Interface. 마우스 대신 글자를 입력해서 컴퓨터를 조작하는 방식 |
| **터미널** | CLI를 사용하는 프로그램. Windows에서는 PowerShell이 기본 터미널 |
| **Git** | 파일의 변경 이력을 관리하는 도구. "되돌리기"를 무한히 할 수 있는 타임머신 |
| **Python** | 프로그래밍 언어. Claude Code가 데이터 분석할 때 내부적으로 사용 |
| **Node.js** | JavaScript 실행 환경. Claude Code를 설치하려면 필요 |
| **pip** | Python 패키지(추가 기능) 설치 도구 |
| **npm** | Node.js 패키지 설치 도구. Claude Code도 npm으로 설치 |
| **PATH** | 프로그램의 주소록. 터미널에서 프로그램 이름만 치면 찾을 수 있게 등록하는 것 |
| **CLAUDE.md** | 프로젝트의 설명서. Claude에게 "이 프로젝트는 이런 거야"를 알려주는 파일 |
| **Memory** | Claude가 대화 사이에 기억하는 것. /memory로 관리 |
| **Skill** | Claude에게 특정 작업 방법을 가르치는 문서. 슬래시 명령어로 실행 |
| **CSV** | Comma-Separated Values. 쉼표로 구분된 데이터 파일. 엑셀의 텍스트 버전 |
| **전처리** | 데이터를 분석하기 전에 깨끗하게 정리하는 작업. 오타 수정, 형식 통일 등 |
| **데이터 정제** | 전처리와 같은 뜻. 데이터의 오류를 찾아서 고치는 것 |

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
- 참가자가 직접 클릭해서 공식 문서를 볼 수 있어야 한다

### Phase A 종료 시 필수 문구

Phase A의 마지막에는 반드시 아래 형태의 문구를 출력하고 Stop한다:

```
---
👆 위 내용을 직접 실행해보세요.
실행이 끝나면 "완료" 또는 "다음"이라고 입력해주세요.
```

이 문구 이후에 어떤 도구 호출(AskUserQuestion 포함)이나 추가 텍스트도 출력하지 않는다.

---

## 소요 시간

| Block | 주제 | 예상 시간 |
|-------|------|-----------|
| 0 | 환경 설치 | ~40분 |
| 1 | 기본 개념 | ~25분 |
| 2 | CSV 전처리 실습 | ~35분 |
| 3 | 스킬 만들기 + 내 데이터 | ~30분 |
| **합계** | | **~130분** |

---

## 블록 특수 규칙

- **Block 0 (환경 설치)**: 퀴즈 없음. Phase A에서 설치 안내 → Stop. Phase B에서 설치 확인만.
- **Block 1 (기본 개념)**: 표준 Phase A/B. CLAUDE.md, Memory, Skill 3가지를 설명하고 실습.
- **Block 2 (CSV 전처리)**: Phase A에서 샘플 CSV 3종 소개 + Claude에게 전처리 시키는 법 안내 → Stop. Phase B에서 퀴즈.
- **Block 3 (스킬 + 내 데이터)**: Phase A에서 전처리 작업을 Skill로 만드는 안내 → Stop. Phase B에서 퀴즈 + AskUserQuestion으로 본인 데이터 도전 여부 확인. "예"면 본인 데이터로 추가 실습 진행.

---

## References 파일 맵

| 블록 | 파일 | 주제 |
|------|------|------|
| Block 0 | `references/block0-install.md` | Git, Python, Node.js, Claude Code 설치 |
| Block 1 | `references/block1-basics.md` | CLAUDE.md, Memory, Skill 기본 개념 |
| Block 2 | `references/block2-csv-practice.md` | 샘플 CSV 전처리 실습 |
| Block 3 | `references/block3-skill-and-mydata.md` | 전처리 스킬 만들기 + 내 데이터 도전 |

> 파일 경로는 이 SKILL.md 기준 상대경로다.
> 각 reference 파일은 `## EXPLAIN`, `## EXECUTE`, `## QUIZ` 섹션으로 구성된다.

---

## Data 파일 맵

| 파일 | 설명 |
|------|------|
| `data/products.csv` | 상품 마스터 데이터 (SKU, 브랜드, 카테고리, 가격, 재고, 시즌) |
| `data/sales.csv` | 일별 매출 데이터 (주문일, SKU, 수량, 매출, 반품) |
| `data/brands.csv` | 입점 브랜드 관리 데이터 (수수료율, 계약기간, 담당자) |

---

## 진행 규칙

- 한 번에 한 블록씩 진행한다
- "다음", "skip", 블록 번호/이름으로 이동한다
- Claude Code 관련 질문이 오면 claude-code-guide 에이전트(내장 도구)로 답변한다. 답변 후 사용자가 직접 따라할 수 있게 단계별로 안내하고, 질문할 때는 AskUserQuestion을 사용한다. 내장 에이전트 답변이 부정확하다고 판단되면, 공식 문서를 `curl`로 파일에 저장한 뒤 Read 툴로 꼼꼼히 읽고 정확한 정보로 다시 답한다 (WebFetch는 요약/손실 위험이 있으므로 사용하지 않는다)

---

## 시작

스킬 시작 시 아래 테이블을 보여주고 AskUserQuestion으로 어디서 시작할지 물어본다.

| Block | 주제 | 내용 |
|-------|------|------|
| 0 | 환경 설치 | Git, Python, Node.js, Claude Code 설치 |
| 1 | 기본 개념 | CLAUDE.md, Memory, Skill |
| 2 | CSV 전처리 실습 | 샘플 데이터 분석 + 정제 + 통합 |
| 3 | 스킬 만들기 + 내 데이터 | 전처리 스킬 만들기 + 본인 데이터 도전 |

```json
AskUserQuestion({
  "questions": [{
    "question": "Day 1: 설치 + 데이터 실습\n\n어디서부터 시작할까요?",
    "header": "시작 블록",
    "options": [
      {"label": "Block 0: 환경 설치", "description": "Git, Python, Node.js, Claude Code 설치부터"},
      {"label": "Block 1: 기본 개념", "description": "설치는 끝났고, CLAUDE.md/Memory/Skill 개념부터"},
      {"label": "Block 2: CSV 전처리 실습", "description": "개념은 알고, 데이터 실습부터"},
      {"label": "Block 3: 스킬 만들기", "description": "전처리까지 했고, 스킬 만들기부터"}
    ],
    "multiSelect": false
  }]
})
```

> 시작 블록 선택 후 → 해당 블록의 Phase A부터 진행한다.
