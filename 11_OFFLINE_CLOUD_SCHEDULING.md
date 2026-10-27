# Luồng đăng lịch khi PC đã tắt — kiến trúc bắt buộc

**Không thể thực hiện offline schedule thật chỉ với SQLite + Windows Task Scheduler khi máy tắt.** Hai tuyến cho phép:

1. `META_NATIVE`: chỉ nếu endpoint/content type hiện hành hỗ trợ schedule native; upload/submit và nhận xác nhận schedule id/status từ Meta. Khi Meta nhận việc, có thể tắt PC. Phải kiểm tra riêng Video/Reels, không giả định có chức năng đặt lịch native.
2. `CLOUD_WORKER`: PC gửi media đến durable object storage (S3-compatible/private object store), gửi job payload có chữ ký/nonce và thời gian UTC lên VPS API; VPS lưu transaction trong PostgreSQL, worker độc lập chờ giờ, lấy media rồi gọi Graph API. Secret cloud giữ bảo mật, TLS, token encryption; không cần PC bật.

`LOCAL_ONLY` -> `PREPARING` -> `UPLOADING` -> `CLOUD_SYNCING` -> `CLOUD_READY` -> `SCHEDULED` -> `PUBLISHING` -> `PUBLISHED` / `FAILED`. Meta route dùng `META_SCHEDULED` thay `CLOUD_READY`. `UNKNOWN` khi timeout không chắc thành công, đối soát trước retry.

**Offline-ready invariant:** đã có durable media URI, remote job durable ack, hash match, quyền/credential phù hợp, scheduled_time đã được server xác nhận; không chỉ nhận HTTP 202 mà chưa lưu, không đánh dấu ready khi chưa upload xong. Kiểm tra remote health trước xác nhận.

Cloud API đề xuất: POST /v1/media/prepare; PUT presigned storage URL (nếu triển khai); POST /v1/batches; GET /v1/batches/{id}/jobs; POST /v1/jobs/{id}/cancel (policy), GET /health. Signature/auth/token; correlation_id; idempotency per batch+page+media+schedule version.

VPS outage: retry exponential backoff có jitter, dead-letter queue, monitoring, alert; yêu cầu cân bằng giờ đăng và queue, không hứa giờ tuyệt đối nếu Meta/network down.

Nguồn chân lý trạng thái là cloud DB/Meta confirmation, local cache đồng bộ hai chiều. Khi tắt PC, server vẫn chạy. Cloud chi phí lưu media, lưu lượng và worker cần dự toán theo số file được upload.

Mock testing: giả lập PC offline, vẫn kích hoạt worker mô phỏng remote; xác minh `LOCAL_ONLY` không được gọi `OFFLINE_READY`.
