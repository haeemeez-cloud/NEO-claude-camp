# Block 0: 환경 설치

> 이 블록은 Windows 환경 기준으로 작성되었다.
> Git, Python, Node.js, Claude Code를 설치한다.

> **Phase A 시작 시 반드시 아래 형태로 출력한다:**
> ```
> 📖 공식 문서: https://docs.anthropic.com/en/docs/claude-code/overview
> 📖 설치 가이드: https://docs.anthropic.com/en/docs/claude-code/getting-started
> ```

## EXPLAIN

### 터미널이 뭔가요?

터미널은 컴퓨터에게 글자로 명령을 내리는 창이다.

- **마우스로 하는 것**: 폴더 클릭 → 파일 더블클릭 → 프로그램 실행
- **터미널로 하는 것**: 명령어 입력 → Enter → 끝

Windows에서는 **PowerShell**이 기본 터미널이다. 시작 메뉴에서 "PowerShell"을 검색하면 나온다.

> 비유: 터미널 = 카카오톡 채팅창. 상대방(컴퓨터)에게 메시지(명령어)를 보내면 답장(결과)이 온다.

### PATH가 뭔가요?

PATH는 **프로그램의 주소록**이다.

터미널에서 `python`이라고 치면, 컴퓨터가 PATH 목록을 뒤져서 Python이 어디 설치되어 있는지 찾는다. PATH에 등록되지 않으면 "찾을 수 없습니다" 에러가 난다.

> 비유: 핸드폰 연락처에 번호를 저장해야 이름으로 전화할 수 있는 것과 같다. PATH에 등록 = 연락처에 저장.

### 왜 이것들을 설치하나요?

| 도구 | 왜 필요한가 |
|------|------------|
| **Git** | 파일 변경 이력 관리. Claude Code가 코드를 수정할 때 "되돌리기"가 가능해진다 |
| **Python** | Claude Code가 데이터 분석, 차트 생성 등을 할 때 내부적으로 사용 |
| **Node.js** | Claude Code 자체가 Node.js로 만들어져서, 설치하려면 필요 |
| **Claude Code** | AI와 터미널에서 대화하면서 작업하는 도구. 오늘의 주인공 |

## EXECUTE

### 1단계: Git 설치

1. 브라우저에서 **https://git-scm.com** 접속
2. "Download for Windows" 클릭
3. 다운로드된 파일 실행 → 기본 설정 그대로 "Next" 연타 → "Install"
4. 설치 완료 후 PowerShell을 열고 확인:

```powershell
git --version
```

> `git version 2.xx.x` 같은 숫자가 나오면 성공이다.

### 2단계: Python 설치

1. 브라우저에서 **https://www.python.org** 접속
2. "Downloads" → "Download Python 3.xx.x" 클릭
3. 다운로드된 파일 실행
4. **⚠️ 중요: 맨 아래 "Add Python to PATH" 체크박스를 반드시 체크한다**
5. "Install Now" 클릭
6. 설치 완료 후 PowerShell을 **새로** 열고 확인:

```powershell
python --version
```

> `Python 3.xx.x` 같은 숫자가 나오면 성공이다.
> 만약 "인식할 수 없습니다" 에러가 나면, PATH 체크를 안 한 것이다. 다시 설치하면서 체크하자.

### 3단계: Node.js 설치

1. 브라우저에서 **https://nodejs.org** 접속
2. **LTS** 버전 (왼쪽, "Recommended For Most Users") 클릭
3. 다운로드된 파일 실행 → 기본 설정 그대로 "Next" 연타 → "Install"
4. 설치 완료 후 PowerShell을 **새로** 열고 확인:

```powershell
node --version
```

> `v20.xx.x` 또는 `v22.xx.x` 같은 숫자가 나오면 성공이다.

### 4단계: Claude Code 설치

PowerShell에서 아래 명령어를 입력한다:

```powershell
npm install -g @anthropic-ai/claude-code
```

설치가 끝나면 실행:

```powershell
claude
```

> 처음 실행하면 Anthropic 계정 로그인 화면이 나온다. Claude Pro, Max, Teams, Enterprise 중 하나의 구독이 필요하다.

## QUIZ

> Block 0은 퀴즈 없음. 설치 확인만 진행한다.

```json
AskUserQuestion({
  "questions": [{
    "question": "4가지 도구 설치가 모두 완료되었나요?\n\n확인 방법: PowerShell에서 아래 명령어가 모두 동작하면 완료입니다.\n- git --version\n- python --version\n- node --version\n- claude",
    "header": "설치 확인",
    "options": [
      {"label": "모두 완료!", "description": "4가지 모두 정상 동작 → Block 1로 이동"},
      {"label": "아직 진행 중", "description": "좀 더 시간이 필요함"},
      {"label": "트러블슈팅 필요", "description": "설치 중 에러 발생"}
    ],
    "multiSelect": false
  }]
})
```

> "트러블슈팅 필요" 선택 시: 에러 메시지를 물어보고, 일반적인 해결법을 안내한다.
> - PATH 문제: PowerShell을 닫았다가 새로 열어보기
> - npm 권한 문제: PowerShell을 "관리자 권한으로 실행"
> - Python PATH 누락: Python 재설치 시 "Add to PATH" 체크
