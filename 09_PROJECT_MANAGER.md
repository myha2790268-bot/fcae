# Module Project Manager — yêu cầu khóa

**Ví dụ:** project `Ẩm thực` có 10 Page; project `Câu cá` có 10 Page. Khi đăng món ăn chỉ chọn project `Ẩm thực` là cả 10 Page được mặc định chọn.

## Giao diện
Danh sách dự án có card/tile và bảng; tạo/sửa/lưu trữ dự án, icon, màu, slug, topic, mô tả, template hashtag/caption, múi giờ; sắp xếp, tìm kiếm, hiển thị tổng Page/bài đang chờ/views/follower khả dụng. Trang chi tiết dự án gồm tabs: **Page**, **Kho nội dung**, **Lịch**, **Thống kê**, **Cài đặt**.

## Logic
- Gán Page bằng multi-select, hỗ trợ nhập CSV hợp lệ, tìm kiếm/ phân trang; đề xuất mặc định `page.project_id` là duy nhất để tránh đăng chéo nhầm dự án.
- Khi chuyển Page sang project khác phải có modal xác nhận và audit log. Page đổi dự án **không tự sửa batch đã lên lịch** vì snapshot đích khi confirm.
- Không tự tạo/truy cập Page mà người dùng chưa cấp quyền. Page bị thu hồi quyền: đánh dấu access lost và chặn jobs mới.
- Default settings dự án: caption template, hashtag, preferred content type, default schedule timezone, posting restrictions và content ownership checklist.
- API: GET/POST/PATCH /projects, GET/PUT /projects/{id}/pages; POST /projects/{id}/validate; GET /projects/{id}/analytics.
- Bắt buộc test: 50 projects x 10 pages, không đổ dữ liệu sang project khác, project rỗng, chuyển Page khi jobs tồn tại, rollback transaction.
