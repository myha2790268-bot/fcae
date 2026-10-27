# Dự toán chi phí (VND, lập ngân sách, KHÔNG phải báo giá)

## Giả định
- Một người dùng, Windows PC sẵn có, 200–500+ Page được phép, Graph API chính thống.
- `Graph API` thông thường không có giá tính theo lượt gọi cho các tác vụ Pages; chịu permissions, App Review và rate limits.
- Không dùng AI trả phí ở cấu hình cơ bản, template caption offline.

## Đầu tư một lần
| Khoản | Khoảng ước tính |
|---|---:|
| Python/FastAPI/PySide6/SQLite/FFmpeg (giấy phép phần mềm) | 0đ (kiểm tra điều khoản từng gói khi phân phối) |
| Meta developer app đăng ký | 0đ phí đăng ký thông thường; xét duyệt là điều kiện, không phải mua quyền |
| SSD backup/media 1–2 TB (nếu thiếu) | khoảng 1,5–4 triệu |
| Nâng RAM 16–32 GB (nếu thiếu) | phụ thuộc máy/loại RAM, chỉ cần khi benchmark yêu cầu |
| Thuê lập trình viên xây tool đầy đủ | phụ thuộc scope; tham khảo 200–380 giờ phát triển+test, tự viết Codex vẫn phải review |

## Hàng tháng tăng thêm
| Khoản | Khoảng ước tính |
|---|---:|
| API Facebook Pages theo lượt gọi | thông thường 0đ (không bao gồm sản phẩm Meta tính phí khác) |
| Chạy PC/điện tăng thêm | ~50–300k (phụ thuộc thời gian và tải) |
| Internet nếu đã có đường truyền | 0đ tăng thêm; nếu mua riêng báo theo ISP |
| Backup ngoài máy/cloud | 0–300k tùy dung lượng/lưu lượng |
| AI caption (templates offline) | 0đ API |
| VPS/webhook callback public HTTPS tùy chọn | ~100–300k; có thể không cần giai đoạn đầu |
| Proxy | 0đ nếu không sử dụng; nếu dùng, giá = số proxy cần x giá nhà cung cấp, không phải 1 proxy/Page |

Nếu giả định mỗi IP proxy 80–350k/tháng (không phải báo giá), 5 profile tốn 400k–1,75 triệu/tháng; 500 IP riêng = 40–175 triệu/tháng, không khuyến khích và không cần cho quản lý 500 Page qua API.

## Năng lực truyền dữ liệu
- 500 Page × 1 Reel/ngày × 100 MB/Reel = **50 GB upload/ngày**, **1.500 GB/tháng**. Đường truyền thực tế upload ổn định 20 Mbps: ít nhất ~5 giờ 33 phút cho 50 GB chưa tính overhead/retry, và chỉ khi file khác nhau thực sự cần upload; chính sách bản quyền/chất lượng phải tuân thủ.
- Để không giữ quá nhiều dữ liệu: archive hoặc xóa media cũ sau 7–14 ngày theo retention policy, hoặc bổ sung NAS/ổ lưu trữ.
- 500 Page × 1 post + 1 Reel/ngày = 1.000 lịch đăng/ngày, không có nghĩa Meta sẽ cho xuất bản đồng thời; hệ thống queue phải tuân giới hạn thực.

## Phần cứng
- i3-10105F + GTX 1650 4GB có thể điều phối API và UI nếu tránh mở nhiều browser/FFmpeg cùng lúc; RAM nên >=16GB, SSD ưu tiên; nếu 500 Page có media cao, 32GB + SSD lớn đáng cân nhắc.
- Đừng chạy hàng trăm profile trình duyệt song song; dùng Meta API cho đăng tải.
