# Frontend
Một ứng dụng React và TypeScript dự kiến; chưa chọn phiên bản hoặc công cụ build.
Chỉ có cấu trúc giữ chỗ, chưa có giao diện, package.json, lockfile hoặc dependency; chưa thể cài/chạy.

`src/app/` tổ chức ứng dụng; `components/`, `layouts/`, `pages/` tổ chức giao diện;
`features/` chia theo nghiệp vụ, bản đồ và xác thực; `services/` dành cho API qua gateway;
`hooks/`, `types/`, `utils/`, `assets/` cho phần hỗ trợ tương ứng.
`public/` giữ tài nguyên công khai; `tests/` dành cho kiểm thử sau này.
Cần có loading, empty, error, forbidden theo hợp đồng được duyệt.
core-service phải kiểm tra quyền dữ liệu; ẩn nút frontend không thay thế kiểm tra phía server.
Không đưa bí mật vào biến môi trường hoặc mã frontend.
