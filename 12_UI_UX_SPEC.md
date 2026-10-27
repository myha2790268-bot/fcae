# Toàn bộ giao diện NSB Page Manager

Tên window/logo/title: **NSB Page Manager**; subtitle `by NSB Group`; tên thương hiệu nhất quán mọi vị trí. Sidebar navy `#14243B`; blue primary `#2563EB`; background `#F4F6FA`; green success, amber warning, red failure. Font Segoe UI; hỗ trợ DPI, bàn phím, thanh tìm kiếm, phân trang, thông báo lỗi chi tiết.

## Sidebar (theo thứ tự)
1. Tổng quan — stats total pages/projects, connection health, queue, cloud-ready, last-7-day insights (chỉ metrics được API hỗ trợ).
2. Dự án — grid/list, tạo dự án, quản lý Page trong dự án, dự án riêng Ẩm thực/Câu cá.
3. Fanpage — Page list + trạng thái token/permission, filters, pagination, chuyển dự án.
4. Đăng Reels/Video — **ưu tiên cao nhất**: 1 video, 1 project, nhiều pages, review, status.
5. Đăng bài — text, link, ảnh/album, cùng workflow theo project.
6. Lịch đăng Cloud — calendar + queue, mỗi job có nguồn Meta/Cloud/local, offline readiness rõ.
7. Kho nội dung — folders theo project, caption, video metadata, content hash, thumbnails.
8. Bình luận — inbox bình luận thật, trạng thái đã duyệt/nháp/gửi, chỉ Page được ủy quyền.
9. Thống kê — date filter, so sánh Page/project, follower, view, engagement, missing-data reason.
10. Tài khoản & Proxy — OAuth state, token health, browser launcher manual, proxy setting/test theo hồ sơ hợp lệ.
11. Cài đặt — language, timezone, Meta app, cloud endpoint, backups, logs, AI optional, theme.

## Mỗi màn có
Loading state, empty state, permission error, offline state, confirmed success, error retry where safe. Không hiển thị 500 Page cùng lúc mà virtualization/pagination. Tooltips cho status. Mỗi button thực hiện hành động thật trong backend hoặc bị disabled và ghi `chưa kết nối` trong mock mode.

## Preview HTML
Mở `ui_preview/index.html` bằng Chrome/Edge để xem bố cục demo; đây là mô hình giao diện, không phải phần mềm quản lý Facebook thật. UI Windows phải giữ luồng và visual tokens này.
