# Vận hành local và cứu hộ phiên Codex

## Chạy hằng ngày
- Backend agent chạy lúc người dùng log on trên Windows (Task Scheduler), có watchdog/recovery.
- Màn Health: service up, DB writable, free disk, token health, pending jobs, upload throughput, rate usage.
- Chạy lịch theo UTC; UI GMT+7. Windows sleep và mất Internet -> các job quá hạn chuyển `delayed`, cần chính sách có đăng bù hay skip (người dùng cấu hình), không spam khi khởi động lại.
- Local mode không thể đăng khi máy tắt hoặc mất mạng. Nếu muốn 24/7 khi máy tắt, phải thuê worker server/PC luôn bật.

## Sao lưu
- `backups/` tách khỏi media working path; SQLite backup API/checkpoint, không chỉ copy file WAL lúc đang ghi.
- Hằng ngày 1 bản DB, giữ 7 bản gần nhất và 4 bản tuần; backup sang ổ khác nếu có.
- Token/secret có DPAPI người dùng Windows; chuyển sang máy khác có thể cần reconnect Meta thay vì giải mã xuyên Windows.
- Xuất metadata/CSV không bao gồm bí mật. Có nút Restore test và cảnh báo mất dữ liệu.

## Để không mất dự án khi Codex chat biến mất
- Source code nằm trong thư mục trên máy, KHÔNG lệ thuộc lịch sử chat Codex.
- Bắt Codex luôn cập nhật `PROGRESS.md`, `CHANGELOG.md`, git commits sau mỗi phase.
- Định kỳ ZIP cả source (`.git` tùy cách backup) nhưng KHÔNG đính kèm `.env`, token, DB có dữ liệu nhạy cảm hoặc browser user data vào ZIP đưa người khác.
- Khi đổi tài khoản Codex: mở đúng thư mục và yêu cầu “Đọc AGENTS.md, PROGRESS.md, toàn bộ repo, tiếp tục phase chưa hoàn thành, đừng viết lại”.


> **Phần cập nhật bắt buộc:** đọc thêm `09_PROJECT_MANAGER.md`, `10_BULK_PUBLISHER_UI.md`, `11_OFFLINE_CLOUD_SCHEDULING.md`, `12_UI_UX_SPEC.md`, `13_API_CONTRACTS.md`, `14_SECURITY_POLICY.md` và `15_ACCEPTANCE_CHECKLIST.md`. Nếu có khác biệt, các tài liệu 09–15 và AGENTS.md được ưu tiên.
