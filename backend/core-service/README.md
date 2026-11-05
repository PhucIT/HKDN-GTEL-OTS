# core-service
Sở hữu dữ liệu nghiệp vụ, liên kết và kiểm tra quyền dữ liệu phía server.

Bộ khung chưa chạy được; Python/FastAPI/SQLAlchemy/Alembic và PostgreSQL là đề xuất chưa chốt phiên bản.
`app/main.py` chưa khởi tạo ứng dụng; chưa có endpoint, model, bảng, nghiệp vụ hoặc database thật.
`app/api/`, `app/core/`, `app/db/`, `app/modules/` giữ chỗ theo trách nhiệm.
`migrations/versions/` và `tests/` chưa có migration hoặc test thực thi.
Dockerfile, requirements.txt, alembic.ini chỉ có TODO, chưa thể build/chạy.
Không dùng chung ORM model hoặc truy cập trực tiếp bảng service khác.
Xem [ranh giới](../../docs/architecture/service-boundaries.md) và
[hợp đồng tích hợp](../../docs/api/integration-contract.md).
