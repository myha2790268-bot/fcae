# Màn hình Đăng 1 video -> nhiều Page (Project Bulk Video Publisher)

Luồng chính có 3 bước rõ ràng: **CHUẨN BỊ -> DUYỆT -> TRẠNG THÁI**. Design system: sidebar navy #14243B, blue #2563EB, nền #F4F6FA, light content, typography Segoe UI, component >44px touch target khi phù hợp, tiếng Việt, responsive ở 1280x720.

### Chuẩn bị
- Project selector mặc định dự án gần nhất; tên chủ đề và số Page; chọn `Ẩm thực` -> 10 Page sẵn; count selected/total.
- Drag & drop một video; chọn `Chọn video`; xem preview frame, path, duration, size, encoding, ratio và validation tình trạng theo endpoint.
- Caption chung và template vars được cho phép; toggle `Caption riêng` mở bảng text overrides theo Page. Không AI-spin rập khuôn để tránh phát tán spam.
- Check list searchable multi-select: chọn tất cả/bỏ chọn; trạng thái quyền từng Page; disable nếu không đủ quyền.
- Mode `Đăng ngay` hoặc `Lên lịch Cloud` với timezone Asia/Ho_Chi_Minh; có giờ riêng từng Page trong optional table.
- Estimated transfer/upload size, publisher route `META_NATIVE`, `CLOUD_WORKER` hoặc `LOCAL_NOW`, chỉ route được phép.
### Duyệt
- Snapshot project_id, page_ids, media_hash/version, caption per Page, thời gian UTC và giờ GMT+7.
- Liệt kê validation: Page role/token, video constraints, lịch tương lai, storage ready, duplicate detection, user approval.
- Button `Xác nhận` cần xác thực lại số page, tránh click nhầm.
### Trạng thái
- One batch, N jobs; table columns Page, thời gian, route, state, % upload, post/reel ID, URL, last error, retry/inspect (chỉ khi an toàn).
- States chi tiết trong `11_OFFLINE_CLOUD_SCHEDULING.md`.
- Counts queued/syncing/offline-ready/published/failed; realtime polling có giới hạn, app close không ảnh hưởng cloud worker.
- Preview phải khác trạng thái thực tế, không hiển thị Cloud Ready/Published nếu chưa có acknowledgement từ hệ thống.
