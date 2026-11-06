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

## 상태 표기

- `TODO`: 아직 시작하지 않음
- `IN_PROGRESS`: 작업 중
- `BLOCKED`: 자료 또는 권한 부족
- `REVIEW`: 검토 필요
- `DONE`: 산출물과 근거 확인 완료

