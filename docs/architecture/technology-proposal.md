# Công nghệ đề xuất — chưa phê duyệt
| Phần | Công nghệ dự kiến | Cần chốt |
| --- | --- | --- |
| Backend | Python, FastAPI | Phiên bản, tổ chức API và vận hành |
| Dữ liệu | SQLAlchemy, Alembic | Phiên bản, transaction và migration |
| Database | PostgreSQL | Phiên bản, bố trí dữ liệu và sao lưu |
| Không gian | Cân nhắc PostGIS | Chỉ chọn khi nhu cầu truy vấn không gian được xác nhận |
| Frontend | React, TypeScript | Phiên bản, công cụ build và thư viện bản đồ |
| Gateway | Nginx | Định tuyến và chính sách truy cập |
| Phát triển | Docker Compose | Image, cổng, mạng, volume và biến môi trường |

Không cài dependency, chọn phiên bản, chạy Docker hoặc kết nối database trong lần dựng khung.
Không thêm Redis, RabbitMQ, Elasticsearch, AI hoặc monitoring stack khi chưa có yêu cầu.
Chỉ ghi dependency sau khi thống nhất và review; không tạo lockfile giả.
