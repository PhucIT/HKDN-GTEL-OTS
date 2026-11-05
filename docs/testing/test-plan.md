# Kế hoạch kiểm thử đề xuất
Chưa có chức năng, test tự động hoặc kết quả kiểm thử hệ thống.
Nhật Thúy chủ trì, phối hợp người phụ trách từng thành phần.

| Cấp | Phạm vi dự kiến | Vị trí |
| --- | --- | --- |
| Unit | Nghiệp vụ, validation và quyền sau khi duyệt | `backend/*-service/tests/unit/` |
| Integration | API, transaction, xác minh danh tính và ranh giới service | `backend/*-service/tests/integration/` |
| Frontend | Nhập liệu, API và loading/empty/error/forbidden | `frontend/tests/` |
| E2E | Luồng qua frontend, gateway và backend | `tests/e2e/` |

Kiểm tra hợp lệ, không hợp lệ, không xác thực và thiếu quyền, bao gồm gọi API trực tiếp
để xác nhận core-service thực thi quyền. Chốt môi trường cô lập, dữ liệu giả, công cụ,
điều kiện đầu vào/đầu ra và tiêu chí đạt với mentor.
Không dùng dữ liệu thật hoặc kết nối database thật để kiểm tra bộ khung.
Hiện chỉ kiểm tra cấu trúc, cú pháp và nội dung tĩnh; không viết test chỉ kiểm tra thư mục
và không coi kiểm tra tĩnh là kiểm thử chức năng.
