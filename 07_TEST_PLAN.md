# Kịch bản nghiệm thu

1. Mock-mode khởi tạo 500 Pages trong vòng một thao tác và mở bảng có sort/search/pagination.
2. Nhập 2.000 scheduled jobs/ngày, restart PC/agent giữa chừng, không mất/copy job.
3. Network timeout ở thời điểm API đã xử lý publish nhưng trước khi client nhận response -> remote reconcile hoặc `needs_review`, không blind retry.
4. Rate-limit code/headers -> ngưng request liên quan và chạy lại khi cho phép.
5. Token hết hạn/thiếu quyền -> Page `attention_required`, không tự chuyển sang browser click.
6. Reel upload ngắt ở các pha START/UPLOAD/PROCESSING/FINISH -> lưu remote video id & tiếp tục hoặc chuyển manual review.
7. So sánh các metric legacy bị deprecated -> không crash; UI thể hiện unavailable, không biến thành zero.
8. Comment Hub không gửi reply chưa duyệt, không reply trùng, có nút stop.
9. Kiểm tra CSV export: không lộ access tokens/proxy passwords.
10. Quản lý browser profiles: mỗi profile dùng thư mục riêng, login thủ công, không bao giờ lưu mật khẩu vào DB tool.
11. Backup và restore từ bản test: Pages/assets/job states hoàn chỉnh; test DB corruption.
12. Stress 500 Pages, 10.000 posts trong analytics (mock), màn dashboard không đứng hình.
13. Security: chỉ bind 127.0.0.1, log redaction, encryption DPAPI, protect backup.
14. Test UI ở Windows 10/11 1080p, high DPI, path có tiếng Việt.
15. Live test ban đầu với 1–3 Pages thuộc quyền thật và nội dung thử, sau đó 10 -> 50 -> 200 -> 500 nếu quyền và giới hạn cho phép.

Mỗi case cần có ID, kết quả PASSED/FAILED/NOT_TESTED, log bằng chứng, ngày chạy.


> **Phần cập nhật bắt buộc:** đọc thêm `09_PROJECT_MANAGER.md`, `10_BULK_PUBLISHER_UI.md`, `11_OFFLINE_CLOUD_SCHEDULING.md`, `12_UI_UX_SPEC.md`, `13_API_CONTRACTS.md`, `14_SECURITY_POLICY.md` và `15_ACCEPTANCE_CHECKLIST.md`. Nếu có khác biệt, các tài liệu 09–15 và AGENTS.md được ưu tiên.
