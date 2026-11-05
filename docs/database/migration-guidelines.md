# Hướng dẫn migration dự kiến
Chưa có schema, cấu hình Alembic hoặc migration chạy được.

Sau khi ERD, công nghệ và phiên bản được duyệt:
1. Người sở hữu dữ liệu chuẩn bị thay đổi và trao đổi ảnh hưởng API/database.
2. Tạo migration riêng trong service sở hữu; review ràng buộc và nguy cơ mất dữ liệu.
3. Thống nhất thứ tự triển khai, dữ liệu cũ, sao lưu và phương án khôi phục phù hợp.
4. Kiểm tra trong môi trường cô lập với dữ liệu giả, ghi minh chứng rồi mở PR.

Không sửa bảng service khác, chia sẻ ORM model hoặc tự chạy migration lên database thật.
`alembic.ini` và `migrations/versions/` chỉ giữ chỗ, chưa có lệnh Alembic được cấu hình.
