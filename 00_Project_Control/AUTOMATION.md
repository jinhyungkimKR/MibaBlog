# 작업 자동 실행

## 동작 범위

- Master는 상위 오케스트레이터 에이전트다. 새 작업과 의존성이 해제된 후속 작업을 즉시 하위 역할 에이전트에 배정하고, 완료 보고를 받으면 검수·병합·후속 실행까지 반복한다.
- 비활성 Master: GitHub Actions가 10분마다 자동 큐를 검사하고, 실행 자격증명이 있으면 Codex 실행기로 전달한다.
- 별도 채팅 탭: 저장소에서 직접 원격 조작하지 않는다. 결과는 Git 커밋으로 공유한다.

## Master 에이전트 실행 루프

1. 사용자 요청 또는 하위 에이전트 완료 이벤트를 받는다.
2. `AUTO_QUEUE.json`과 실제 산출물 경로를 검사한다.
3. 실행 가능한 작업마다 독립 작업공간을 만들고 해당 역할 에이전트를 생성하거나 재개한다.
4. 하위 에이전트가 조사·전달·원고 산출물을 커밋한다.
5. Master가 파일과 Git 기록을 검수해 `main`에 병합한다.
6. 완료 또는 차단 상태를 기록하고 큐를 다시 검사한다.
7. 실행 가능한 작업이 남아 있으면 3단계부터 반복한다.

이 루프가 자동 착수의 주 실행 장치다. GitHub Actions는 Master 에이전트가 활성화되지 않은 시간의 보조 실행기다.

## 구성 파일

- 큐: `00_Project_Control/AUTO_QUEUE.json`
- 브라우저 큐: `00_Project_Control/BROWSER_QUEUE.json`
- 검사·실행기: `scripts/task_dispatch.py`
- 정기 실행: `.github/workflows/task-dispatch.yml`
- 작업 지시: `02_Session_Messages/*.md`

## 큐 상태

- `TODO`: 입력 또는 의존성 검사 대상
- `IN_PROGRESS`: 실행기가 작업 중
- `BLOCKED`: 자료·접근 권한·자격증명 부족
- `DONE`: 산출물 생성과 자동 검증 완료

`TODO` 작업은 모든 `depends_on`이 `DONE`이고 `required_paths`가 존재하면 실행 가능하다. 실행 후 산출물에 `BLOCKED`가 기록되면 후속 작업을 열지 않는다.

## GitHub Actions 자격증명

저장소 Actions secret에 `OPENAI_API_KEY`가 있어야 AI 실행이 활성화된다. 키가 없으면 워크플로는 큐와 경로만 검사하고 실행 대기 사유를 Job Summary에 남긴다.

자격증명 값은 문서, 로그, 커밋에 기록하지 않는다.

## 새 작업 등록

1. `TASK_BOARD.md`에 `TODO` 행을 추가한다.
2. `02_Session_Messages/`에 역할별 작업 지시를 작성한다.
3. `AUTO_QUEUE.json`에 고유 ID, 역할, 지시 파일, 의존성, 필수 입력, 예상 산출물을 추가한다.
4. 활성 Master는 즉시 큐를 검사한다. 비활성 상태에서는 GitHub Actions가 다음 주기에 검사한다.

## Cloud와 Work 연결

Cloud Master는 원고 완성 후 네이버 작업을 `BROWSER_QUEUE.json`에 `READY`로 등록한다. 연결된 Chrome이 있는 Work 대화는 최신 `main`을 읽고 `READY` 작업을 실행한다.

Work는 글쓰기 탭과 대상 블로그를 확인한 뒤 제목·본문을 입력하고 임시저장한다. 완료 후 큐 상태를 `DONE`으로 바꾸고 임시저장 시각과 확인 가능한 편집기 URL을 기록한다. 공개 발행은 큐의 `publish_authorized`가 `true`일 때만 수행한다.

## 로컬 검사

```bash
python3 scripts/task_dispatch.py
```

실행 가능한 작업, 차단 사유와 누락 경로를 JSON으로 출력한다.
