# NSB Page Manager — MASTER INSTRUCTION FOR CODEX

BẠN PHẢI ĐỌC `AGENTS.md`, `README.md` VÀ TOÀN BỘ 01–16 trước khi bắt tay lập trình. Đây là repo **NSB Page Manager** thuộc **NSB Group**; không đổi tên, không tạo repo mới khác.

Vai trò: senior Python/PySide6 Windows engineer, API architect, database/queue engineer, security engineer, designer, QA. Ngôn ngữ giao diện và tài liệu: tiếng Việt. Code identifiers: English.

## Thành phẩm cuối
Ứng dụng desktop Windows 10/11 x64 với PySide6, nền FastAPI hoặc dịch vụ Python độc lập phù hợp, SQLite + migration, backend worker durable, FFmpeg/ffprobe, Meta adapter cấu hình phiên bản và quyền, dự án + Page + thư viện nội dung + publisher theo batch + bình luận thật + Analytics + browser profile thủ công + proxy cấu hình hợp lệ + logs + backup/restore + cloud schedule. Có mock mode chạy không cần khóa API. Installer `NSB_Page_Manager_Setup.exe`.

## Luồng ưu tiên số 1
1. Chọn Dự án Ẩm thực (đã gán 10 Page).
2. Chọn một file video; hệ thống hiển thị thumbnail, độ dài, định dạng, cảnh báo chưa hợp lệ.
3. Mặc định tích toàn bộ 10 Page nhưng có thể bỏ chọn; không chọn lại qua các đợt.
4. Caption chung, override theo Page, chọn đăng ngay hoặc đặt lịch GMT+7.
5. Màn REVIEW hiển thị video, dự án, danh sách Page snapshot, caption, thời gian, quyền, cảnh báo nội dung lặp, chi phí dữ liệu.
6. Sau xác nhận, tạo batch và 10 publishing_jobs bền vững, idempotency; theo dõi từng Page riêng biệt.
7. Nếu muốn tắt máy, bắt buộc route qua Meta native scheduling đã xác thực hoặc VPS (media + schedule lưu trước). Cảnh báo nếu LOCAL_ONLY/UPLOAD_PENDING, không gắn CLOUD_READY giả.
8. Màn kết quả: statuses + post_id/reel_id + url + lỗi + retry an toàn; không retry mù nếu trạng thái đăng chưa xác định.

## Luồng ưu tiên số 2
Tạo/sửa dự án, gán/rút/chuyển Page, quản lý nhiều dự án; xem Dashboard, Analytics theo dự án/đơn Page; quản lý 200–500+ Pages bằng pagination và filter, không mở hàng trăm browser đồng thời.

## Quy tắc code
- Chỉ tự động hóa Page được cấp quyền hợp pháp bằng Graph API; permission/capability detection từ tài liệu hiện hành.
- Không chế tạo tương tác giả, view/like/follow seeding, spam comment, CAPTCHA bypass, anti-detect, proxy rotation để né rate limit.
- `META_GRAPH_VERSION` là config. Kết nối external phải đi qua adapter với mock tests.
- Secrets -> Windows DPAPI/Credential Manager, cloud -> secrets manager; TLS, tránh plaintext token.
- Không triển khai nhiều chức năng bằng mock giả rồi tuyên bố là production.
- Viết test cho tính đúng của dự án, snapshot Page, batching, idempotency, offline readiness, restart/recovery, quyền truy cập, upload failure.

## Trình tự bắt buộc
1. Khảo sát file, viết `IMPLEMENTATION_PLAN.md`, `PROGRESS.md`, lập ưu tiên thực tế.
2. Hoàn thành M0: chạy UI PySide6, mock 500 Pages/50 projects, DB + migrations, smoke tests.
3. Hoàn thành M1: Project Manager + Bulk Publisher + Preview + Batch status trên mock mode.
4. M2: scheduler/jobs persistent, kiểm soát duplicate, upload adapter, retry.
5. M3: Meta OAuth/API + review quyền, thật trên test Page theo quyền được cấp.
6. M4: Cloud scheduling với triển khai thật VPS + signed contract; tạo `/cloud` như service deploy độc lập, native scheduling nếu endpoint hỗ trợ.
7. M5: Comments, Analytics, Browser/Proxy, AI optional, Backups, installer, load test.
8. Sau mỗi milestone: chạy tests, ghi kết quả và hạn chế vào PROGRESS.md, cập nhật tài liệu, git commit.

**BẮT ĐẦU NGAY** bằng M0 + M1; không chỉ tóm tắt yêu cầu. Nếu thiếu thông tin xác thực Meta, tiếp tục đầy đủ Mock Mode, không hỏi lại những điều đã chốt.
