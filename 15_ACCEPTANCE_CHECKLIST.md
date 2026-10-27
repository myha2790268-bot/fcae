# Tiêu chí nghiệm thu theo giai đoạn

- [ ] App title `NSB Page Manager` / `NSB Group`, .exe named correctly.
- [ ] Mock desktop mở mà không cần Meta token, tạo 50 projects và 500 Page trong vài giây; UI không treo, có search/pagination.
- [ ] Tạo Ẩm thực 10 Page, Câu cá 10 Page; project selector Ẩm thực auto chọn đúng 10, không lẫn Câu cá.
- [ ] Chọn 1 video -> đúng 10 jobs trong 1 batch; caption chung + overrides; review snapshot chính xác.
- [ ] Khi chuyển Page sang dự án khác, batch cũ vẫn giữ Page snapshot; batch mới theo danh sách mới.
- [ ] Cloud offline status dựa vào remote ack + durable media, LOCAL_ONLY không bao giờ hiển thị Cloud Ready.
- [ ] Test scheduler remote chạy mô phỏng khi PC client tắt; cloud server có restart recovery.
- [ ] Retry an toàn không tạo duplicate bài đăng khi HTTP timeout / ambiguous response.
- [ ] Thử nghiệm Meta trên test Page có quyền hợp lệ; lưu Post ID/Reel ID + URL; không dùng automation browser để đăng.
- [ ] Dashboard dự án / Page có missing-data states, không bịa Insights.
- [ ] Bình luận cần duyệt thật, không spam chéo; token/credential mã hóa và không có trong logs.
- [ ] Backup restore + installer build + hướng dẫn triển khai VPS thực tế.
