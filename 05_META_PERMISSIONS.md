# Tích hợp Meta — kiểm chứng lại theo tài liệu hiện hành khi Codex code

Current reference date: 26/10/2026. Graph API latest v26.0 (released 29/07/2026); không hardcode suốt đời. Dùng `META_GRAPH_VERSION`.

## Dự kiến permissions
- `pages_show_list`: lấy Page người dùng có quyền truy cập.
- `pages_read_engagement`: đọc nội dung/engagement các Page được quyền.
- `pages_manage_posts`: đăng, quản lý bài text/ảnh/video/Reels trên Page.
- `pages_read_user_content`: đọc nội dung/bình luận do người dùng khác đăng vào Page, nếu endpoint yêu cầu.
- `pages_manage_engagement`: phản hồi/kiểm duyệt comment và hành động tương tác chính đáng dưới danh nghĩa Page.
- `pages_manage_metadata`: quản lý subscription và Page webhooks, nếu bật.
- `read_insights`: quyền thống kê khi endpoint yêu cầu; xác minh chi tiết cho từng metric/endpoint.
- `business_management`: CHỈ xin nếu luồng quản lý Business assets/system user thực sự cần, không xin mặc định.
- `pages_messaging`: KHÔNG yêu cầu trừ khi sau này thêm module Messenger riêng.

**Phân quyền:** Standard Access dành cho app users có role trên app; khi yêu cầu user không có role trên app / Pages của doanh nghiệp ngoài, thường cần Advanced Access + App Review, Business Verification theo yêu cầu Meta. Số 500 Page không có nghĩa app tự động được quyền với cả 500.

## Endpoint dự kiến
- `GET /me/accounts` để lấy danh sách Pages và Page tokens (qua OAuth hợp lệ).
- `POST /{page-id}/feed`, `/photos`, `/videos` khi đúng loại bài và quyền.
- Reels theo Meta official Postman: `POST /me/video_reels?upload_phase=start` -> upload tới URL trả về -> kiểm tra status -> `POST /me/video_reels?upload_phase=finish` với params phiên bản hiện hành.
- `GET /{page-id}/insights` hoặc post/video insights với tập metric tương thích; không request hàng loạt metric cũ.
- `GET/POST /{object-id}/comments` nếu endpoint, scopes và loại post cho phép.
- Webhooks (nếu cấu hình HTTPS endpoint, signature validation, pages_manage_metadata khi cần).

## Rate limits
- Rate limit thay đổi theo token, app, Page, use case. Luôn dùng feedback headers và error responses (ví dụ 80001 Page rate limit), không dựa vào hằng số requests/hour tự tưởng tượng.
- Dừng hẳn theo retry-after/cooldown và thông báo người dùng; không xoay account/proxy để vượt hạn mức.

## Insights 2026
- Ngày 15/06/2026 nhiều chỉ số Reach/Impressions/3-second views cũ ngừng hỗ trợ. Lập registry + replacement; xem thông báo version/current. Dùng Page follows, media views (như page_media_view) nơi API xác nhận.

## Nguồn gốc
- Official Meta Postman Collection: https://www.postman.com/meta/facebook/documentation/r56bjfd/facebook-api
- Meta Permissions: https://developers.facebook.com/docs/permissions/reference
- Meta Access Levels: https://developers.facebook.com/docs/graph-api/overview/access-levels
- Meta rate-limiting: https://developers.facebook.com/docs/graph-api/overview/rate-limiting
- Graph API changelog: https://developers.facebook.com/docs/graph-api/changelog
- Meta anti-spam: https://about.fb.com/news/2025/04/cracking-down-spammy-content-facebook/
- Meta original content: https://about.fb.com/news/2026/03/rewarding-original-creators-on-facebook/
