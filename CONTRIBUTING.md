# Hướng dẫn đóng góp
Làm trên nhánh cá nhân, commit thay đổi của mình, mở PR vào `main`, review rồi merge.
Dùng đúng chữ hoa/thường của nhánh hiện có: `Nhu`, `Thuy`, `Dau`, `Tan`, `Phuc`, `Thanh`.
Không tự tạo hoặc đổi tên nhánh thành viên khác. Khi dựng khung từ `main`, dùng
`chore/project-scaffold`; nếu đã ở nhánh cá nhân thì giữ nguyên.

Trước khi sửa, đọc hướng dẫn và file liên quan, kiểm tra trạng thái Git.
Không ghi đè công việc hiện có. Nếu chuyển nhánh bị chặn bởi công việc chưa lưu,
dừng thao tác Git và giải thích; không reset, clean hoặc tự stash.
Chỉ đưa thay đổi thuộc phạm vi của mình vào commit.

Thay đổi ảnh hưởng API hoặc database phải trao đổi và review hợp đồng/migration.
Người phụ trách không phải người duy nhất được sửa thư mục.
PR mô tả mục đích, thay đổi, cách kiểm tra và giới hạn còn lại.
Chỉ dùng dữ liệu giả; không đưa `.env`, mật khẩu, token, dữ liệu cá nhân thật hoặc tài liệu
nội bộ chưa được phép lên GitHub.

Hiện chưa có lệnh chạy hệ thống hoặc bộ kiểm thử chức năng.
Kiểm tra cú pháp Python bằng `ast.parse` không cần cài dependency hoặc tạo cache.
Không chạy Docker hoặc kết nối database trong lần dựng khung này; không commit, push hoặc merge.
Xem [quy trình nhóm](docs/team/workflow.md).
