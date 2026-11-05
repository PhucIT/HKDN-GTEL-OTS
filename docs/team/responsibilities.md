# Phân công hiện tại
Vai trò là phân công hiện tại; phạm vi kỹ thuật chi tiết là đề xuất cần cả nhóm thống nhất.

| Thành viên | Vai trò | Phạm vi |
| --- | --- | --- |
| Khả Như | Leader / BA | Làm rõ yêu cầu, nghiệp vụ, tiêu chí nghiệm thu, backlog, tiến độ, báo cáo và trao đổi với mentor. |
| Nhật Thúy | QA / Tester | Test plan, test case, kiểm thử API và giao diện, quản lý lỗi và minh chứng kiểm thử. |
| Hoàng Đấu | Integration / Analytics | Tích hợp frontend–backend, gateway, Docker Compose, phối hợp kiểm thử tích hợp và thống kê theo yêu cầu. Không tự thêm AI. |
| Nguyễn Tân | Frontend | Giao diện, bảng dữ liệu, tìm kiếm, bản đồ, gọi API và trạng thái loading, empty, error, forbidden. |
| Ngọc Phúc | Backend / Database | Chủ trì core-service, ERD và dữ liệu nghiệp vụ. Ràng buộc dữ liệu, migration, dữ liệu giả, API nghiệp vụ, tìm kiếm, lọc, phân trang và liên kết. Phối hợp Thành về kiểm tra quyền và Nhật Thúy về kiểm thử API. |
| Tiến Thành | Backend / Security | Chủ trì identity-service, tài khoản, xác thực, vai trò và quy tắc phân quyền. Phối hợp Phúc về quyền truy cập dữ liệu và nhật ký thao tác. |

Người phụ trách không phải người duy nhất được sửa thư mục.
Thay đổi ảnh hưởng API hoặc database cần trao đổi và review.
Không tách service theo sáu thành viên. Chi tiết nhật ký và thống kê cần làm rõ trước triển khai.
