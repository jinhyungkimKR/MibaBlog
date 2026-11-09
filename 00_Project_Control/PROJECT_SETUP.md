# MibaBlog 프로젝트 구성

## 목적

게임별 자료조사와 네이버 블로그 원고 작성을 분리하고, 세션이 바뀌거나 다른 기기에서 접속해도 GitHub 문서를 기준으로 작업을 이어간다.

## 저장소 구조

```text
MibaBlog/
├── .github/workflows/task-dispatch.yml
├── AGENTS.md
├── MIBA_BLOG_CURRENT_STYLE_GUIDE.md
├── 00_Project_Control/
│   ├── PROJECT_SETUP.md
│   ├── SESSION_MAP.md
│   ├── OPERATING_AGENDA.md
│   ├── DECISION_LOG.md
│   ├── TASK_BOARD.md
│   ├── AUTO_QUEUE.json
│   ├── BROWSER_QUEUE.json
│   └── AUTOMATION.md
├── 01_Sessions/
├── 02_Session_Messages/
├── 03_Research/
│   ├── 도깨비의세계/
│   └── 디아블로4/
├── 04_Handoffs/
├── 05_Posts/
│   ├── 도깨비의세계/
│   └── 디아블로4/
├── scripts/task_dispatch.py
└── assets/
```

## 운영 기준

GitHub가 공용 작업 기억이다. 대화 기억보다 저장소의 최신 MD를 우선한다.

각 세션은 첫 메시지에서 자신의 역할 문서와 필수 파일을 읽도록 지시받는다. 작업이 끝나면 결과와 다음 세션이 알아야 할 내용을 MD와 Git 커밋으로 남긴다.

## 세션 실행 방식

이 저장소는 세션 간 공용 기억이다. Master 자체가 상위 오케스트레이터 에이전트이며, `AUTO_QUEUE.json`에서 실행 가능한 작업을 발견하면 별도 착수 요청을 기다리지 않고 아구몬·파피몬·차원의문 역할 에이전트를 직접 생성하거나 재개한다.

Master가 닫힌 뒤의 상시 실행은 `.github/workflows/task-dispatch.yml`과 `scripts/task_dispatch.py`가 담당한다. GitHub Actions에 `OPENAI_API_KEY`가 설정돼 있으면 대기 작업을 Codex 실행기로 전달하고 결과를 `main`에 커밋한다. 키가 없으면 안전하게 큐 검사만 수행하며 AI 작업은 시작하지 않는다.

이 장치는 사용자가 열어 둔 별도 채팅 탭을 원격 조작하지 않는다. Master 에이전트의 하위 역할 에이전트 또는 GitHub Actions의 독립 Codex 실행기가 산출물을 저장소에 작성하는 방식이다.

브라우저 작업은 Work 브라우저 실행기가 `BROWSER_QUEUE.json`을 읽어 수행한다. Cloud Master와 Work는 같은 브라우저 세션이나 대화 기억을 공유하지 않지만, GitHub `main`의 큐·원고·상태를 통해 한 작업 흐름으로 공존한다.

작업 배정만 완료된 상태는 `TODO`로 유지한다. 대상 세션의 착수 응답, 실제 출처 접근 기록, 작업 파일 생성 중 하나 이상을 확인한 뒤에만 `IN_PROGRESS`로 변경한다.

## 상태 표기

- `TODO`: 아직 시작하지 않았거나 배정만 완료됨
- `IN_PROGRESS`: 작업 중
- `BLOCKED`: 자료 또는 권한 부족
- `REVIEW`: 검토 필요
- `DONE`: 산출물과 근거 확인 완료

