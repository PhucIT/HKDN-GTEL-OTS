# Ranh giới service đề xuất
| Thành phần | Trách nhiệm | Dữ liệu sở hữu |
| --- | --- | --- |
| core-service | Nghiệp vụ, liên kết, tìm kiếm/lọc/phân trang và kiểm tra quyền dữ liệu | Cá nhân tạm gọi persons, phương tiện, địa điểm, sự kiện, quan hệ |
| identity-service | Tài khoản, xác thực và vai trò/quy tắc quyền đã thống nhất | Tài khoản, thông tin xác thực, vai trò |
| frontend | Hiển thị, nhập liệu và gọi API qua gateway | Không là nguồn dữ liệu nghiệp vụ chính thức |
| gateway | Điểm vào API và định tuyến sau khi duyệt hợp đồng | Không sở hữu dữ liệu nghiệp vụ/tài khoản |

Không dùng chung ORM model hoặc đọc trực tiếp bảng service khác.
Không tạo shared chứa model database. Bố trí database/schema vật lý còn chờ chốt;
ranh giới sở hữu và truy cập dữ liệu vẫn phải được giữ.

core-service xác minh danh tính theo hợp đồng API với identity-service, rồi quyết định
quyền truy cập dữ liệu mình sở hữu. Chi tiết xác minh, thời hạn, lỗi và cập nhật vai trò chưa chốt.
Frontend hỗ trợ trải nghiệm; gateway không thay thế kiểm tra quyền nghiệp vụ.
Thay đổi xuyên service phải trao đổi và review hợp đồng trước triển khai.
