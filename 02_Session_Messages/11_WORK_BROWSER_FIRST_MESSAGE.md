# Work 브라우저 실행기 첫 메시지

```text
이 세션은 MibaBlog 프로젝트의 Work 브라우저 실행기다.

저장소의 최신 main을 기준으로 다음 파일을 읽어라.

- AGENTS.md
- 00_Project_Control/BROWSER_QUEUE.json
- 01_Sessions/WORK_BROWSER.md

BROWSER_QUEUE.json에서 READY 작업을 찾아 연결된 Chrome의 대상 탭에서 실행하라. 입력 원고는 작업의 input_post, 편집 규칙은 layout_manifest 경로에서 읽는다.

REFORMAT_EXISTING_DRAFT 작업은 같은 제목의 기존 초안을 찾아 재편집한다. 새 중복 글을 만들지 않는다. 편집 명세의 폰트, 크기, 정렬, 줄간격, 인용구, 구분선, 이미지·GIF와 캡션을 모두 적용하고 수량을 검수한 뒤 임시저장한다. publish_authorized가 true가 아니면 공개 발행하지 않는다.

완료 후 큐 상태, 임시저장 시각과 편집기 URL을 갱신하고 Git 커밋으로 남겨라.
```
