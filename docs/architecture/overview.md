# Tổng quan kiến trúc đề xuất
Một frontend → gateway → identity-service hoặc core-service.
Đây là luồng logic, chưa chốt đường dẫn, cổng, mạng hoặc cơ chế bảo mật.

Frontend hiển thị và gọi API. Gateway là điểm vào API dự kiến bằng Nginx.
identity-service quản lý tài khoản, xác thực và vai trò.
core-service quản lý persons, vehicles, locations, events và relationships.
Giữ nghiệp vụ trong cùng core-service để xử lý quan hệ và giao dịch thuận tiện.
Không chia service theo thực thể hoặc số thành viên; định hướng triển khai độc lập về sau.

core-service phải kiểm tra quyền dữ liệu phía server, không chỉ ẩn nút frontend.
Giao tiếp qua API, cơ chế xác minh danh tính chờ thống nhất.
Không chia sẻ ORM model, đọc trực tiếp bảng service khác hoặc tạo shared chứa model database.
Xem [ranh giới](service-boundaries.md) và [hợp đồng tích hợp](../api/integration-contract.md).
