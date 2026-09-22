# Assignment2
### WebCraft 실시간 게임 서버 구현

여러 플레이어가 같은 월드에 접속해 이동하고 채팅할 수 있는 Spring Boot 기반 실시간 게임 서버입니다.

### API 명세

| Method | URL | 기능 |
|---|---|---|
| POST | `/players` | 플레이어 등록 |
| POST | `/worlds` | 새 월드 생성 |
| GET | `/worlds` | 월드 목록 조회 |
| GET | `/worlds/{worldId}/chats` | 최근 채팅 조회 |
| WebSocket | `/ws/worlds/{worldId}?nickname={nickname}` | 월드 실시간 연결 |

### ERD

worlds  1  ──────  N  chat_messages

- `worlds.id` (PK) ↔ `chat_messages.world_id` (FK)
- 하나의 월드는 여러 개의 채팅 메시지를 가질 수 있습니다.
- 플레이어 정보는 `players` 테이블에서 관리합니다.

### players

| Column | 설명 |
|---|---|
| id | 플레이어 ID (PK) |
| nickname | 플레이어 닉네임 |

### worlds

| Column | 설명 |
|---|---|
| id | 월드 ID (PK) |
| seed | 월드 생성 Seed |
| difficulty | 월드 난이도 |

### chat_messages

| Column | 설명 |
|---|---|
| id | 채팅 ID (PK) |
| world_id | 월드 ID (FK) |
| sender_nickname | 채팅을 보낸 플레이어 |
| content | 채팅 내용 |
| created_at | 채팅 생성 시간 |