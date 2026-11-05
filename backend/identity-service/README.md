# identity-service
Sở hữu tài khoản, thông tin xác thực và vai trò; giao tiếp xác minh danh tính qua API theo hợp đồng được duyệt.

Bộ khung chưa chạy được; Python/FastAPI/SQLAlchemy/Alembic và PostgreSQL là đề xuất chưa chốt phiên bản.
`app/main.py` chưa khởi tạo ứng dụng; chưa có endpoint, model, bảng, nghiệp vụ hoặc database thật.
`app/api/`, `app/core/`, `app/db/`, `app/modules/` giữ chỗ theo trách nhiệm.
`migrations/versions/` và `tests/` chưa có migration hoặc test thực thi.
Dockerfile, requirements.txt, alembic.ini chỉ có TODO, chưa thể build/chạy.
Không dùng chung ORM model hoặc truy cập trực tiếp bảng service khác.
Xem [ranh giới](../../docs/architecture/service-boundaries.md) và
[hợp đồng tích hợp](../../docs/api/integration-contract.md).

Module auth chưa có nhu cầu lưu trữ riêng: không tạo model hoặc repository riêng; chỉ giữ chỗ schema, service và router.
