# MibaBlog 프로젝트 구성

## 목적

게임별 자료조사와 네이버 블로그 원고 작성을 분리하고, 세션이 바뀌거나 다른 기기에서 접속해도 GitHub 문서를 기준으로 작업을 이어간다.

## 저장소 구조

```text
MibaBlog/
├── AGENTS.md
├── MIBA_BLOG_CURRENT_STYLE_GUIDE.md
├── 00_Project_Control/
│   ├── PROJECT_SETUP.md
│   ├── SESSION_MAP.md
│   ├── OPERATING_AGENDA.md
│   ├── DECISION_LOG.md
│   └── TASK_BOARD.md
├── 01_Sessions/
├── 02_Session_Messages/
├── 03_Research/
│   ├── 도깨비의세계/
│   └── 디아블로4/
├── 04_Handoffs/
├── 05_Posts/
│   ├── 도깨비의세계/
│   └── 디아블로4/
└── assets/
```

## 운영 기준

GitHub가 공용 작업 기억이다. 대화 기억보다 저장소의 최신 MD를 우선한다.

각 세션은 첫 메시지에서 자신의 역할 문서와 필수 파일을 읽도록 지시받는다. 작업이 끝나면 결과와 다음 세션이 알아야 할 내용을 MD와 Git 커밋으로 남긴다.

## 세션 실행 방식

이 저장소는 세션 간 공용 기억이며 세션 실행기가 아니다. `TASK_BOARD.md`를 수정하거나 `02_Session_Messages/`에 지시 파일을 추가해도 이미 열려 있는 다른 채팅 세션에 메시지가 자동 전송되거나 작업이 자동 시작되지 않는다.

대상 세션을 실제로 시작하려면 다음 중 하나가 필요하다.

1. 대상 세션에서 최신 `main`을 읽고 해당 작업 지시 파일을 실행하도록 직접 메시지를 보낸다.
2. 세션을 호출할 수 있는 별도 자동화 도구나 오케스트레이터가 명시적으로 작업을 전달한다.

작업 배정만 완료된 상태는 `TODO`로 유지한다. 대상 세션의 착수 응답, 실제 출처 접근 기록, 작업 파일 생성 중 하나 이상을 확인한 뒤에만 `IN_PROGRESS`로 변경한다.

## 상태 표기

- `TODO`: 아직 시작하지 않았거나 배정만 완료됨
- `IN_PROGRESS`: 작업 중
- `BLOCKED`: 자료 또는 권한 부족
- `REVIEW`: 검토 필요
- `DONE`: 산출물과 근거 확인 완료

