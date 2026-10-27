# Yêu cầu chức năng

## Quy mô
- MỘT người dùng trên Windows 10/11 x64; tối đa 500+ Page có quyền quản trị thật, nhiều Page có thể dùng chung một tài khoản quản trị được phép.
- Một máy hoạt động tốt nhất như worker API/điều phối; không mở hàng trăm trình duyệt đồng thời.
- Các Page thuộc nhiều nhóm content: có các cột page_id, page_name, group, category, timezone, connection_health, last_post_at, total_followers (nếu hỗ trợ), last_sync_at.

## Module chi tiết
| ID | Module | Yêu cầu |
|---|---|---|
| A | Accounts/Auth | OAuth, danh sách admin accounts được ủy quyền, Page token, trạng thái permissions, re-auth, hủy kết nối |
| B | Pages | Sync, tag/group, bulk select, search, filter, sort, import Page metadata nếu có API |
| C | Browsers | Mở profile riêng của từng người quản lý, login thủ công, proxy optional, trạng thái riêng |
| D | Media Library | Thư viện file, hash, bản quyền nguồn, phân loại, preview, FFprobe, hợp lệ định dạng |
| E | Composer | Text/photo/album/link/video/Reels, caption tùy Page, preview, approval, duplicate checks |
| F | Schedule | Calendar, timezones, bulk scheduling, repeating templates có giới hạn/kiểm duyệt |
| G | Publisher | API adapters, logs, remote IDs, idempotency, retry, compensation, per-Page limits |
| H | Reels | Session upload, chunk/upload theo API, status processing, finish publish, verify link |
| I | Comment Hub | Đọc bình luận thật, reply/moderate các post mình sở hữu, templates/gợi ý, hàng chờ duyệt |
| J | Insights | Metric registry, snapshots, follower trend, views/reactions/comments/shares, per-Page/post/reel |
| K | AI Assist | Template-based captions, nội dung gốc và tùy chỉnh theo Page; provider AI optional OFF |
| L | Notifications | Token expiry, permission issue, rate-limit, failed publish, backup warnings |
| M | Security/Backup | DPAPI, redaction, backup/restore, access logs, health checks |
| N | Settings/Reports | Export, storage retention, network testing, mock/live badge, giới hạn tải |

## Khác
- Bất kỳ hành động nhiều Page đều có xác nhận rõ lựa chọn Page và preview số job phát sinh.
- Người vận hành xác nhận lịch/nội dung; AI không đăng nội dung mới do AI sinh một cách vô hạn/không xét duyệt.
- Hiển thị 'không có dữ liệu' khác '0'; số liệu phải kèm last_updated_at và định nghĩa.
- Không có chức năng buff view, follow, like hay spam bình luận; chỉ quản lý và phục vụ người thật.


> **Phần cập nhật bắt buộc:** đọc thêm `09_PROJECT_MANAGER.md`, `10_BULK_PUBLISHER_UI.md`, `11_OFFLINE_CLOUD_SCHEDULING.md`, `12_UI_UX_SPEC.md`, `13_API_CONTRACTS.md`, `14_SECURITY_POLICY.md` và `15_ACCEPTANCE_CHECKLIST.md`. Nếu có khác biệt, các tài liệu 09–15 và AGENTS.md được ưu tiên.
