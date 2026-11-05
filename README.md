# HKDN-GTEL-OTS
Nhóm Khả Như – sinh viên UTH phối hợp Gtel OTS.

## Đề tài G1.4
**Xây dựng hệ thống quản lý đối tượng, phương tiện và địa điểm cần giám sát.**
Phạm vi và kiến trúc là đề xuất, đang chờ mentor xác nhận.

Phạm vi dự kiến: quản lý đối tượng, phương tiện, địa điểm, sự kiện và liên kết;
tìm kiếm, lọc, phân trang; hiển thị thông tin có tọa độ trên bản đồ;
tài khoản và kiểm soát quyền truy cập. `persons` là tên kỹ thuật tạm cho cá nhân.
Không bổ sung nhận diện khuôn mặt, tracking video, xử lý vi phạm giao thông hoặc AI.
Chỉ dùng dữ liệu giả trong ví dụ và kiểm thử.

## Tình trạng
Đã tạo cấu trúc monorepo, tài liệu đề xuất và các file giữ chỗ có chú thích.
Chưa triển khai CRUD, endpoint, đăng nhập, ORM model, database thật hoặc giao diện hoàn chỉnh.
Chưa cài dependency, chọn phiên bản công nghệ hoặc cấu hình triển khai.
**Đây là bộ khung chưa thể khởi chạy hệ thống.** Các cấu hình còn TODO;
`compose.yaml` chỉ có `services: {}`. Kiểm tra tĩnh không chứng minh chức năng đã chạy.

## Cấu trúc
- `docs/`: yêu cầu, kiến trúc, dữ liệu, API, phân công và kiểm thử.
- `backend/core-service/`: dữ liệu nghiệp vụ, liên kết và kiểm tra quyền dữ liệu.
- `backend/identity-service/`: tài khoản, thông tin xác thực và vai trò.
- `frontend/`: một ứng dụng giao diện gọi API qua gateway.
- `gateway/`: điểm vào API dự kiến bằng Nginx.
- `infra/`: hạ tầng và database.
- `scripts/`: nơi bổ sung công cụ phát triển sau khi thống nhất.
- `tests/e2e/`: nơi bổ sung kiểm thử xuyên hệ thống.

Các thành phần có định hướng triển khai độc lập về sau. Các thực thể nghiệp vụ cùng nằm
trong core-service để xử lý quan hệ và giao dịch thuận tiện. Không chia service theo thực thể
hoặc theo số thành viên.

## Công nghệ đề xuất
Python, FastAPI, SQLAlchemy, Alembic; PostgreSQL; React và TypeScript; Nginx; Docker Compose.
Chỉ cân nhắc PostGIS khi nhu cầu truy vấn không gian được xác nhận. Chưa chốt phiên bản.
Không thêm Redis, RabbitMQ, Elasticsearch, AI hoặc monitoring stack khi chưa có yêu cầu.

## Bước tiếp theo
1. Cùng mentor xác nhận phạm vi, người dùng, quyền, dữ liệu và tiêu chí nghiệm thu.
2. Thống nhất từ điển dữ liệu, ERD, hợp đồng API và cơ chế xác minh danh tính.
3. Chốt công nghệ, phiên bản, dependency và chính sách bảo mật qua review.
4. Cấu hình môi trường, migration, gateway và Docker; triển khai từng lát chức năng.
5. Tạo dữ liệu giả, kiểm thử và ghi minh chứng trước khi báo cáo hệ thống chạy được.

Xem [mục lục tài liệu](docs/README.md), [phân công](docs/team/responsibilities.md)
và [hướng dẫn đóng góp](CONTRIBUTING.md).
