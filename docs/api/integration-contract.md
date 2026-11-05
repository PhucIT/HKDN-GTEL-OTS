# Khung hợp đồng tích hợp
Chưa chốt endpoint hoặc payload, chưa có API chạy được.

| Bên trao đổi | Nội dung cần thống nhất |
| --- | --- |
| Frontend ↔ gateway | Đường dẫn công khai, cấu hình môi trường, lỗi và timeout |
| Gateway ↔ service | Định tuyến, header chuyển tiếp và ranh giới tin cậy |
| Frontend ↔ identity-service qua gateway | Luồng tài khoản/xác thực, dữ liệu và lỗi |
| Frontend ↔ core-service qua gateway | Thực thể/liên kết, tìm kiếm, lọc, phân trang và quyền |
| core-service ↔ identity-service qua API | Xác minh danh tính/vai trò, tính hợp lệ, lỗi và hành vi khi không xác minh được |

Mỗi hợp đồng cần chủ sở hữu, bên tiêu thụ, endpoint/phương thức, request/response,
validation, xác thực, quyền, định dạng lỗi, timeout, phiên bản và kiểm thử bằng dữ liệu giả.
Cơ chế xác minh danh tính và thuật toán bảo mật chưa được chọn.
Không mặc nhiên tin danh tính từ client. core-service phải xác minh danh tính và kiểm tra
quyền dữ liệu phía server theo cơ chế được duyệt; không chỉ dựa vào frontend hoặc gateway.
Không đọc trực tiếp bảng service khác hoặc dùng chung ORM model.
Thay đổi hợp đồng phải trao đổi giữa Phúc, Thành, Tân, Đấu và QA khi liên quan.
