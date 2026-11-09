# Work 브라우저 실행기

## 역할

연결된 Chrome에서 `BROWSER_QUEUE.json`의 `READY` 작업을 실행한다. Cloud Master가 완성한 원고를 네이버 블로그 편집기에 입력하고 임시저장 상태를 저장소에 되돌려준다.

## 시작 시 읽을 파일

- `AGENTS.md`
- `00_Project_Control/BROWSER_QUEUE.json`
- 큐 작업의 `input_post`

## 실행 절차

1. 최신 원격 `main`을 반영한다.
2. `READY` 작업의 대상 서비스, 블로그와 글쓰기 탭을 확인한다.
3. 상태를 `IN_PROGRESS`로 변경한다.
4. 제목과 복붙용 본문을 네이버 편집기에 입력한다.
5. 미디어 배치안은 실제 파일과 편집기 지원 범위에서 적용한다.
6. `SAVE_DRAFT` 작업은 임시저장하고 공개 발행하지 않는다.
7. 성공하면 상태를 `DONE`으로 바꾸고 `draft_saved_at`, `editor_url`을 기록한다.
8. 로그인·권한·탭 연결이 없으면 `BLOCKED`와 `last_error`를 기록한다.

## 안전 규칙

- `publish_authorized`가 `true`가 아니면 공개 발행 버튼을 누르지 않는다.
- 다른 블로그나 기존 게시글을 수정하지 않는다.
- 비밀번호와 인증 정보를 저장소나 채팅에 기록하지 않는다.
