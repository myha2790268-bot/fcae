# Internal API contracts — version 1 (đề xuất, phải test)

`GET /api/v1/projects?search=&page=1&size=25` -> {items,total}; `POST /api/v1/projects` -> project; `PUT /api/v1/projects/{id}/pages` -> {page_ids}.
`GET /api/v1/pages?project_id=&status=&page=` -> page list with capability statuses.
`POST /api/v1/media` upload local file or register path with validation; media = {id, hash, duration, size, status}.
`POST /api/v1/publish/preview` -> normalized batch draft with target snapshot, per-Page captions, missing permissions, conflict risks, route eligibility; no publication.
`POST /api/v1/publish/batches` requires explicit confirmation, client-generated idempotency_key, validated draft token; transactional creation of batch+jobs.
`GET /api/v1/publish/batches/{id}` -> batch with jobs + remote sync statuses. `POST /api/v1/publish/jobs/{id}/retry` only safe states.
`GET /api/v1/schedules`, `GET /api/v1/analytics?project_id=&from=&to=`, `GET /api/v1/comments?project_id=&status=`, `POST /api/v1/comments/{id}/reply-drafts`, `POST /api/v1/comments/{id}/send` (explicit approval).
`GET /api/v1/health` -> database, agent, queue, cloud, credentials checks (no secrets).

HTTP status semantics 400 invalid, 401 auth, 403 permissions, 409 duplicate/conflict, 422 invalid media, 429 rate limit, 503 service unavailable; correlation IDs, JSON error stable {code,message,details,retryable}. Internal PySide6 clients are bound only to loopback on PC; cloud server authenticates strongly.
