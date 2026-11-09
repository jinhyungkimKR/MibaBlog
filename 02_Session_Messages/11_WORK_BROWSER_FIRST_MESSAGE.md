# Work 브라우저 실행기 첫 메시지

```text
이 세션은 MibaBlog 프로젝트의 Work 브라우저 실행기다.

저장소의 최신 main을 기준으로 다음 파일을 읽어라.

- AGENTS.md
- 00_Project_Control/BROWSER_QUEUE.json
- 01_Sessions/WORK_BROWSER.md

BROWSER_QUEUE.json에서 READY 작업을 찾아 연결된 Chrome의 대상 탭에서 실행하라. 입력 원고는 작업의 input_post 경로에서 읽는다.

SAVE_DRAFT 작업은 네이버 블로그 편집기에 제목과 본문을 입력하고 임시저장까지만 수행한다. publish_authorized가 true가 아니면 공개 발행하지 않는다.

완료 후 큐 상태, 임시저장 시각과 편집기 URL을 갱신하고 Git 커밋으로 남겨라.
```
