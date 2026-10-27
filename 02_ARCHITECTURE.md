# Kiến trúc kỹ thuật

```text
PySide6 Desktop UI (Windows)
   | http://127.0.0.1:PORT / IPC
   v
Local FastAPI Service
   |---- Auth + Secrets (Windows DPAPI / Credential Manager)
   |---- Page Manager / Content Library / Approval Engine
   |---- Scheduler + Persistent Queue + Retry + Reconcile
   |---- Meta Graph API Adapter (v26.0 configurable)
   |---- Insights collector + comments moderator
   |---- Media validator/FFmpeg
   |---- Browser Profile Launcher (manual use only)
   v
SQLite WAL + local media directory + backups
   |
   +--> Meta API over HTTPS (authorized Pages only)
```

## Thành phần
- UI không gọi Meta trực tiếp; sử dụng local API; progress streaming/polling.
- Backend là một tiến trình độc lập với UI; Windows startup Task Scheduler chạy backend khi đăng nhập; UI tắt mà queue không dừng.
- SQLite WAL, single writer coordination, unique constraints, transactions. Database migrations bằng Alembic. Nếu multi-machine, sau này có adapter PostgreSQL.
- Job scheduler poll DB, đặt due jobs vào hàng đợi bền vững và worker xử lý; tránh race bằng lease và expires_at.
- HTTPX async hỗ trợ adaptive concurrency; mặc định `API_WORKERS=4`, `UPLOAD_WORKERS=1`, `TRANSCODE_WORKERS=1`; mọi ngưỡng có thể chỉnh sau đo hiệu năng.
- `RateLimiter` theo Page, endpoint và app; tiêu thụ rate usage headers, phản ứng với 429 hoặc lỗi rate-limit Meta, có exponential backoff + jitter và circuit breaker. Không cố thử liên tục khi bị limit.
- Idempotency: UUID job local; unique(page_id, content_version_id, slot_id), lưu remote_object_id; sau network timeout ở bước publish, query lại nếu có thể, nếu không chuyển `needs_review` thay vì blind retry.
- Worker lưu states: `draft -> approved -> scheduled -> queued -> uploading -> processing -> publishing -> published`, các ngã rẽ `retry_wait/failed/needs_review/cancelled`.
- Page Insights: metric registry (name, semantics, active versions, replacement, granularity), không hardcode metric đã bị khai tử; null nếu unavailable.
- Asset fingerprint (SHA-256, perceptual video/image fingerprint) dùng cảnh báo sao chép, không biến đổi media để tránh detection.

## Chế độ local
- `MOCK_MODE=true`: 500 Pages giả, không gửi HTTP lên Meta, mô phỏng giới hạn, timeout và upload processing.
- `LIVE_MODE=true`: chỉ bật sau kiểm tra token/permissions; có confirm xuất bản, có log event rõ ràng.

## Bảo mật
- OAuth redirect phải tuân yêu cầu hiện hành của Meta (nếu local callback không được chấp nhận, dùng HTTPS callback do người dùng kiểm soát); không dùng cách dán mật khẩu.
- Secrets mã hóa bằng Windows DPAPI, lock dưới tài khoản Windows người dùng; không bao giờ in bearer token vào log.
- Bind API local vào `127.0.0.1`; CSRF/auth nội bộ nếu frontend hoặc browser có thể gọi; không lộ API trên LAN.
- Cloud endpoint nếu bật webhooks: xác thực chữ ký, HTTPS, và không gửi token/PII vào log.
- Trình duyệt được mở để admin thao tác thủ công; không có robotic DOM clicks để publish/comment/scrape.

## Giao diện
- Sidebar: Dashboard, Accounts, Pages, Content, Bulk Publisher, Reels, Calendar, Comment Hub, Analytics, Browsers, Logs, Settings.
- Bảng 500 Page có virtual scrolling/pagination, tìm kiếm nhanh, bulk selection, status icon, last sync.
- Dashboard totals (Page online, scheduled, failed, posts today), 7/30d charts, top videos, alert panel.


> **Phần cập nhật bắt buộc:** đọc thêm `09_PROJECT_MANAGER.md`, `10_BULK_PUBLISHER_UI.md`, `11_OFFLINE_CLOUD_SCHEDULING.md`, `12_UI_UX_SPEC.md`, `13_API_CONTRACTS.md`, `14_SECURITY_POLICY.md` và `15_ACCEPTANCE_CHECKLIST.md`. Nếu có khác biệt, các tài liệu 09–15 và AGENTS.md được ưu tiên.
