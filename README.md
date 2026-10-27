# NSB Page Manager — NSB Group

**BỘ DỰ ÁN ĐỂ GỬI CODEX, CHƯA PHẢI ỨNG DỤNG ĐÃ LẬP TRÌNH XONG.** Mục tiêu: quản lý 200–500+ Facebook Page đã được cấp quyền trên Windows; 1 video đăng lên nhiều Page trong một dự án; lịch Cloud tiếp tục khi PC tắt.

## Cách dùng ngay
1. Giải nén ZIP vào `D:\NSB_Page_Manager` (hoặc thư mục riêng).
2. Mở **chính thư mục chứa AGENTS.md** bằng Codex. Đọc `START_HERE.txt`, rồi dán nguyên nội dung `00_CODEX_MASTER_PROMPT.md`.
3. Codex lập trình M0/M1 ở thư mục này và tạo `PROGRESS.md`. Các giai đoạn sau dùng `16_CODEX_PHASE_PROMPTS.md`.
4. Để xem mock UI: mở `ui_preview/index.html` trong Chrome/Edge. Không có chức năng đăng thật.

## Tài liệu
`AGENTS.md` quy tắc; `00` master prompt; `01–08` yêu cầu/kiến trúc/roadmap/database/permissions/chi phí/test/vận hành; `09` dự án; `10` giao diện bulk video; `11` cloud offline; `12` UI/UX; `13` API contracts; `14` security; `15` acceptance; `16` phase prompts. `mock_data/` là dữ liệu kiểm thử.

## Thiết kế mấu chốt
- PROJECT: 10 Page Ẩm thực -> chỉ cần chọn dự án Ẩm thực.
- VIDEO: 1 file -> 10 publishing jobs độc lập, caption chung hoặc riêng.
- CLOUD: tắt PC chỉ tiếp tục đăng khi cloud đã nhận đủ media+schedule hoặc Meta đã xác nhận native schedule; nếu không, hiển thị cảnh báo.
- ACCOUNT/PROXY: quản trị có quyền; không anti-detect hoặc né hạn chế.

## Phạm vi
Tài liệu/Mock UI chỉ để lập kế hoạch và bắt đầu phát triển. Đăng thật cần Meta App và quyền tương ứng; Cloud worker thật cần VPS/storage/bảo mật.
