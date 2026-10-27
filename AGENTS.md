# Codex Repository Instructions — NSB Page Manager

- Ngôn ngữ làm việc và tài liệu: tiếng Việt. Tên hàm/biến, commit và mã nguồn: tiếng Anh.
- Source of truth: các tài liệu từ `01_REQUIREMENTS.md` đến `08_OPERATIONS.md`.
- Code chạy trên Windows 10/11 x64, triển khai ưu tiên local single-user, không bắt buộc Docker, server thuê hay API AI trả phí.
- Trước mỗi phase: đọc tài liệu liên quan, lập plan ngắn, lập tests; hoàn tất phase phải chạy test + báo số test thành công/thất bại, ghi changelog và các hạn chế còn lại.
- Không tự ý loại bỏ/chỉnh sửa feature đã nghiệm thu. Không bịa ra khả năng/permission/metrics chưa xác nhận của Meta. Luôn tham khảo docs hiện hành khi có thể.
- Đặt `META_GRAPH_VERSION` trong cấu hình (mặc định v26.0 lúc khởi tạo dự án; kiểm tra lại khi implement).
- Tất cả ghi dữ liệu Meta phải đi qua API service, không thông qua trình duyệt auto click. Chỉ kết nối page được cấp quyền, token mã hóa DPAPI, không lưu password Facebook, không log bí mật.
- Browser launcher chỉ để mở session thủ công; proxy do người dùng chủ động cấu hình khi có nhu cầu hợp lệ, không có anti-detect/fingerprint spoof/captcha bypass hoặc stealth.
- Không tự động buff like/view/follow, không comment spam/không seeding chéo nhiều Page; ưu tiên trả lời bình luận thật trên Page mình quản lý, có phê duyệt và giới hạn tốc độ.
- Bộ nền phải chạy được ở chế độ MOCK mà không cần Meta token, để UI/test ngay.
- Lập migration, data integrity check, backup/restore test, app event logs, cập nhật README sau phase.
- Đường dẫn tương đối; hạn chế dependency phức tạp. Tests bằng pytest; lint bằng ruff; typecheck nếu hợp lý.
- Sau mỗi phase ghi `PROGRESS.md`: hoàn thành gì, lệnh test, phát hiện, bước kế tiếp, commit SHA (nếu git khả dụng). Mỗi phase tạo git commit khi repo cho phép.

## Các yêu cầu mới chốt (ưu tiên cao nhất)
- Thương hiệu chính thức: **NSB Page Manager**, đơn vị **NSB Group**. Dùng nhất quán ở title, sidebar, executable, installer, logs và tài liệu.
- **Project Manager**: một dự án chứa nhiều Page theo chủ đề; ví dụ 10 Page Ẩm thực, 10 Page Câu cá. Mỗi Page chỉ thuộc một dự án mặc định; có thể chuyển nhóm có xác nhận.
- **One video -> many Pages**: chọn một video, một dự án, mặc định tick toàn bộ Page dự án, có thể bỏ chọn; mỗi Page sinh một job riêng cùng một batch_id, có caption chung hoặc override riêng.
- **Tắt PC vẫn đăng được**: không bao giờ hứa local scheduler hoạt động khi PC tắt. Chỉ đánh dấu OFFLINE_READY khi Meta đã xác nhận native schedule hoặc cloud đã xác nhận media lưu bền + job lưu bền + quyền và thời gian hợp lệ. Cloud VPS worker chạy độc lập với PC.
- UI tiếng Việt 100%, ưu tiên thao tác ít click, dashboard project-centric; duyệt trước phát hành, theo dõi từng Page; không báo thành công giả.
- Nghiêm cấm in token/password trong console, prompt hoặc commit. Tuân thủ rate limit, chính sách Meta, duyệt trước thao tác xuất bản.
