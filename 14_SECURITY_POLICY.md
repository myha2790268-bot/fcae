# An toàn, vận hành và trách nhiệm

- Chính sách: chỉ Facebook Pages do người vận hành có quyền hợp lệ; không tự tạo view, like, follow, spam comments, thao túng tương tác hay dùng mạng tài khoản để né hạn chế.
- Credentials: local DPAPI/Windows Credential Manager; không lưu mật khẩu Facebook, không tự điền 2FA/CAPTCHA. Trên cloud cần KMS/secret encryption và phân quyền; HTTPS, không in secrets vào logs.
- Graph API app review: hiện trạng quyền và endpoint phải xác minh từ Meta docs khi implement. Danh sách quyền tham khảo từ `05_META_PERMISSIONS.md`; quyền khác nhau theo hành động, app type và cấp truy cập.
- Browser profiles: hỗ trợ launch bằng Chrome/Edge theo sự đồng ý; proxy chỉ là tính năng kết nối mạng hợp pháp, không anti-detect, fingerprint spoof, captcha bypass, IP rotation evade.
- Không hứa số view/reach/follower có thể lấy đủ: các Insights metric có thể đổi; lưu `null` + reason `UNSUPPORTED`/`MISSING_PERMISSION`/`NOT_AVAILABLE`.
- Nội dung: quyền sử dụng media, chống đăng nhầm dự án, cảnh báo video trùng lặp; không hứa đăng lặp video lên nhiều Page sẽ được phân phối tối ưu.
- Idempotency: không blind retry publish sau timeout. Quá trình kiểm tra status remote trước khi retry tránh double post.
- Backup: encrypt secrets separately, test restore, scrub logs before sharing.
