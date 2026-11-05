# Hạ tầng database dự kiến
PostgreSQL là đề xuất chưa chốt phiên bản, chưa tạo database thật.
Chỉ cân nhắc PostGIS khi nhu cầu truy vấn không gian được xác nhận.
Cần thống nhất database/schema vật lý, tài khoản riêng, volume, sao lưu và khôi phục.
core-service sở hữu nghiệp vụ; identity-service sở hữu tài khoản/xác thực/vai trò.
Không đọc trực tiếp bảng service khác hoặc dùng chung ORM model.
Schema, ERD và migration chờ duyệt tại `docs/database/`; chỉ dùng dữ liệu giả khi phát triển/kiểm thử.
Không đặt thông tin kết nối thật hoặc bản sao lưu trong repository.
