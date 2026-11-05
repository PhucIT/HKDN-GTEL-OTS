# Câu hỏi cần mentor xác nhận

## Trạng thái
**Dữ kiện đã có:** nhóm đang dựng bộ khung G1.4; phân công hiện tại tại
[responsibilities.md](../team/responsibilities.md). Phạm vi và kiến trúc vẫn là đề xuất.

**Chưa xác nhận:** các trường, kiểu, B/T, khóa, bội số, vai trò và quy tắc trong
[từ điển dữ liệu](../database/data-dictionary.md) và [quan hệ](../database/relationships.md).
Bản nháp không phải schema được duyệt. Tất cả câu hỏi bên dưới đang mở.
Chỉ dùng dữ liệu giả; chưa tạo ORM, migration, API hoặc chức năng mới.

## M01 — Phạm vi và người dùng
- “Đối tượng” có bao gồm tổ chức hoặc loại thực thể khác không? Có chấp nhận tên kỹ thuật
  tạm `persons` chỉ cho cá nhân không?
- Người dùng, đơn vị sử dụng, mục đích nghiệp vụ và phạm vi dữ liệu được phép quản lý là gì?
- Các thực thể cá nhân, phương tiện, địa điểm, sự kiện và quan hệ có đủ cho giai đoạn đầu không?

## M02 — Định danh và quy ước dữ liệu chung
- UUID nội bộ có phù hợp không? Có cần mã nghiệp vụ riêng; phạm vi duy nhất và cách cấp mã là gì?
- Trường tối thiểu để tạo bản ghi là gì? Đề xuất tên/nhãn bắt buộc, các trường mô tả tùy chọn có phù hợp không?
- Quy tắc chuẩn hóa, giới hạn độ dài, tìm trùng/gộp hồ sơ và xử lý thông tin chưa biết là gì?
- Có cần created_at/updated_at và nguồn ghi nhận cho mỗi thực thể không? Ai được sửa nguồn?

## M03 — Cá nhân
- Cần tên hiển thị hay họ tên pháp lý? Hồ sơ chưa rõ danh tính được tạo như thế nào?
- Ngày sinh có thật sự cần và được phép lưu không? Nếu chỉ biết năm/tháng thì biểu diễn thế nào?
- Trường cá nhân nào bị hạn chế quyền xem/sửa? Không bổ sung số giấy tờ hoặc dữ liệu nhạy cảm
  khi chưa có yêu cầu và quyền sử dụng được xác nhận.
- Quy tắc phân biệt người trùng tên và gộp hồ sơ sai là gì? Hồ sơ cá nhân có cần liên kết tài khoản không?

## M04 — Phương tiện
- Quản lý loại phương tiện nào, danh mục loại/nhãn hiệu/màu ra sao?
- Có cho tạo hồ sơ chưa biết biển số bằng nhãn mô tả không?
- Biển/số đăng ký duy nhất trong phạm vi nào, có thay đổi hoặc tái cấp theo thời gian không?
- Có đồng sở hữu, lịch sử chuyển quyền, hoặc chủ sở hữu là tổ chức không?
- Ghi nhận người điều khiển dựa nguồn nào và tại thời điểm nào? Xác nhận không suy từ chủ sở hữu.

## M05 — Địa điểm và ghi nhận xuất hiện
- Địa điểm là địa chỉ, điểm, vùng hay đường? Có chấp nhận địa điểm chưa biết tọa độ không?
- Tên/địa chỉ và cặp vĩ độ–kinh độ đề xuất đã đủ chưa? Hệ WGS84, độ chính xác và chuẩn hóa có phù hợp không?
- Có cần ghi nhận cá nhân/phương tiện xuất hiện tại địa điểm không; mục đích và nguồn nào được phép?
- Xác nhận một lần xuất hiện không phải vị trí hiện tại, nơi cư trú hoặc thông tin thời gian thực.
  Nếu có nhu cầu riêng về vị trí hiện tại, cần đặc tả và nguồn xác nhận nào?

## M06 — Sự kiện
- Thế nào là một sự kiện trong phạm vi đề tài? Các loại, trạng thái và vòng đời được phép là gì?
- Tiêu đề có đủ làm trường bắt buộc ban đầu không, hay phải có thời gian/địa điểm/nguồn?
- Một sự kiện có bao nhiêu địa điểm, cá nhân hoặc phương tiện; có cho chưa biết các liên kết không?
- Có cần khoảng thời gian, sự kiện chỉ biết ngày hoặc chưa rõ thời điểm không?
- Những vai trò liên quan nào được phép? Xác nhận sự kiện hoặc sự liên quan không tự hàm ý vi phạm.

## M07 — Loại quan hệ, vai trò và bội số
- Những cặp thực thể và loại quan hệ nào trong bản nháp được duyệt, loại nào phải bỏ?
- Sở hữu và điều khiển có được ghi thành hai loại riêng với nguồn và thời gian độc lập không?
- Bội số đề xuất 0..N mỗi phía phù hợp ở đâu; có quy tắc bắt buộc hoặc duy nhất theo thời gian không?
- Vai trò nào bắt buộc theo từng loại? Quan hệ nào có hướng, đối xứng hoặc cho tự liên kết?
- Nguồn ghi nhận tối thiểu là gì, có cần bước xác nhận/duyệt và xử lý nguồn mâu thuẫn không?
- Khóa chống trùng, nhiều lần xuất hiện và nhiều nguồn cho cùng quan hệ được xử lý thế nào?
- Chọn bảng liên kết riêng hay cấu trúc chung; cách bảo đảm toàn vẹn hai đầu và giao dịch là gì?

## M08 — Thời gian và ý nghĩa ghi nhận
- Múi giờ lưu/hiển thị và độ chính xác theo từng loại là gì? timestamp có múi giờ có phù hợp không?
- Phân biệt thời điểm nhập, xảy ra, quan sát và khoảng hiệu lực như thế nào?
- observed_at bắt buộc cho ghi nhận xuất hiện/điều khiển có phù hợp không?
- Khi chỉ biết ngày/năm/khoảng thời gian hoặc thiếu đầu/cuối thì lưu và tìm kiếm ra sao,
  để không gán giờ giả hoặc coi thiếu mốc là đang còn hiệu lực?
- Có cho nhiều nguồn ghi nhận chồng thời gian không? Ai được sửa và có cần giữ lịch sử không?

## M09 — Sửa, xóa, lưu giữ và lịch sử
- Xóa thực thể có liên kết: chặn xóa, lưu trữ, soft delete hay xử lý khác?
- Thời hạn lưu giữ/xóa, nguồn bị rút lại, quan hệ sai và gộp hồ sơ được xử lý thế nào?
- Có cần duyệt thay đổi, lịch sử hoặc nhật ký thao tác; được ghi những nội dung gì, ai được xem?
- Quy tắc sao lưu/khôi phục và tránh mất liên kết khi sửa/xóa là gì?

## M10 — Bản đồ, tìm kiếm và quy mô
- Bản đồ hiển thị thực thể/lớp dữ liệu nào theo quyền; nguồn, giấy phép và cách dùng bản đồ?
- Chỉ cần hiển thị điểm hay có truy vấn khoảng cách/vùng? Có thực sự cần PostGIS không?
- Trường tìm kiếm, xử lý dấu tiếng Việt, bộ lọc, sắp xếp và phân trang mong muốn là gì?
- Quy mô dữ liệu, số người dùng và ngưỡng thời gian phản hồi dùng để nghiệm thu là gì?

## M11 — Quyền, xác thực và nguồn dữ liệu
- Những vai trò nào được xem/thêm/sửa/xóa theo thực thể, bản ghi, trường hoặc đơn vị?
- Quyền đối với quan hệ và hai đầu được kiểm tra ra sao để không lộ bản ghi bị hạn chế?
- Luồng tài khoản, cơ chế xác thực/xác minh danh tính giữa service, vòng đời phiên/token,
  cập nhật/thu hồi vai trò và hành vi khi không xác minh được cần gì?
- Nguồn dữ liệu, quyền sử dụng, cách nhập/cập nhật và mức độ kiểm chứng được yêu cầu là gì?
- Xác nhận dùng dữ liệu giả cho phát triển/kiểm thử; dữ liệu cá nhân, bí mật và tài liệu nội bộ
  được bảo vệ/giới hạn chia sẻ thế nào? Chưa chốt thuật toán bảo mật.

## M12 — Công nghệ và hợp đồng tích hợp
- Python/FastAPI/SQLAlchemy/Alembic, PostgreSQL, React/TypeScript, Nginx và Docker Compose có phù hợp không?
  Phiên bản nào được duyệt? Bố trí database/schema và quyền truy cập riêng cho service thế nào?
- Endpoint, payload, validation, định dạng lỗi và quy tắc tương thích API cần thống nhất ra sao?
- Cách tham chiếu danh tính qua API được duyệt là gì, bảo đảm không dùng chung ORM hoặc đọc bảng service khác?

## M13 — Nghiệm thu và ưu tiên triển khai
- Use case ưu tiên, tiêu chí đạt cụ thể, dữ liệu giả, môi trường, thời hạn và minh chứng cần gì?
- Ai xác nhận yêu cầu, thiết kế dữ liệu, hợp đồng API và kết quả nghiệm thu?
- Những câu hỏi nào phải chốt trước khi thiết kế ERD, viết ORM, migration và API?

## Ghi nhận quyết định
Chưa có quyết định được mentor xác nhận trong tài liệu này. Khả Như tổng hợp trao đổi;
Ngọc Phúc chuẩn bị phương án dữ liệu, Tiến Thành phối hợp quyền/bảo mật, Nhật Thúy chuẩn bị
các tình huống nghiệm thu. Người phụ trách không độc quyền sửa tài liệu.

| Mã câu hỏi | Quyết định / phạm vi được duyệt | Người xác nhận | Ngày | Tài liệu được cập nhật |
| --- | --- | --- | --- | --- |

Sau khi có câu trả lời, cập nhật đồng bộ từ điển dữ liệu, quan hệ, ERD và hợp đồng API qua review.
Không coi phương án nháp hoặc câu trả lời chưa xác nhận là yêu cầu chính thức.
