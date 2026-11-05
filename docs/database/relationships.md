# Bản nháp quan hệ nghiệp vụ

## Dữ kiện và giả định
**Dữ kiện từ yêu cầu nhóm:** core-service quản lý thực thể và liên kết; identity-service
sở hữu danh tính/tài khoản. Không chia sẻ ORM model hoặc đọc trực tiếp bảng service khác.
Phạm vi hệ thống vẫn là đề xuất chờ mentor xác nhận.

**Giả định đề xuất:** mọi loại, hướng, bội số, vai trò và ràng buộc bên dưới chỉ để thảo luận.
Không có quan hệ nghiệp vụ cụ thể nào được xem là đã xác nhận. Không tạo bảng, ORM, migration hoặc API.
Trường dự kiến và B/T xem [từ điển dữ liệu](data-dictionary.md).

## Các quan hệ ban đầu để thảo luận
N:N có nghĩa là phương án cho phép nhiều bản ghi ở cả hai phía, không khẳng định mỗi
bản ghi phải có liên kết. Bội số cuối cùng và trường hợp bắt buộc chờ mentor xác nhận.
Tên loại trong bảng là mô tả nghiệp vụ, chưa phải enum hoặc tên endpoint.

| Nguồn → đích đề xuất | Mục đích / loại quan hệ ứng viên | Bội số đề xuất | Vai trò và thời gian | Câu hỏi mentor |
| --- | --- | --- | --- | --- |
| Cá nhân → phương tiện | Ghi nhận sở hữu | 0..N ↔ 0..N qua quan hệ | Vai trò chủ sở hữu; khoảng hiệu lực nếu biết; có nguồn | Có đồng sở hữu, chuyển nhượng và lịch sử không? M04, M07 |
| Cá nhân → phương tiện | Ghi nhận điều khiển tại thời điểm | 0..N ↔ 0..N qua quan hệ | Vai trò người điều khiển; observed_at đề xuất bắt buộc, không suy từ sở hữu | Dựa nguồn nào và cần độ chính xác thời gian ra sao? M04, M07 |
| Cá nhân → sự kiện | Ghi nhận cá nhân liên quan | 0..N ↔ 0..N qua quan hệ | Vai trò chưa chốt; không gán mặc định người vi phạm | Có những vai trò nào, bắt buộc/được phép ghi gì? M06–M07 |
| Phương tiện → sự kiện | Ghi nhận phương tiện liên quan | 0..N ↔ 0..N qua quan hệ | Vai trò theo sự kiện, không suy ra người sở hữu/điều khiển | Khi nào phương tiện được liên kết và dựa nguồn nào? M06–M07 |
| Sự kiện → địa điểm | Gắn địa điểm được ghi nhận cho sự kiện | 0..N ↔ 0..N qua quan hệ | Vai trò địa điểm chưa chốt; thời gian sự kiện không tự điền cho liên kết khác | Mỗi sự kiện một hay nhiều địa điểm, có cho chưa biết không? M05–M06 |
| Cá nhân → địa điểm | Ghi nhận xuất hiện tại một thời điểm | 0..N ↔ 0..N qua quan hệ | observed_at đề xuất bắt buộc, có nguồn; không là vị trí hiện tại/nơi cư trú | Có thuộc phạm vi không, và biểu diễn thời gian chưa rõ thế nào? M05, M07–M08 |
| Phương tiện → địa điểm | Ghi nhận xuất hiện tại một thời điểm | 0..N ↔ 0..N qua quan hệ | observed_at đề xuất bắt buộc, có nguồn; không suy ra vị trí hiện tại | Có thuộc phạm vi không, và nguồn nào đủ để ghi nhận? M05, M07–M08 |

Không mặc định cho phép mọi cặp thực thể. Quan hệ cá nhân–cá nhân, phương tiện–phương tiện,
địa điểm–địa điểm hoặc sự kiện–sự kiện chỉ bổ sung nếu mentor xác nhận nhu cầu và ý nghĩa.
Bảng không đề xuất thêm service; các quan hệ đều ở core-service.

## Ràng buộc logic đề xuất
- Mỗi quan hệ có khóa id nội bộ; hai đầu tồn tại và đúng loại. Không cho bản ghi mồ côi.
- Danh mục loại quan hệ xác định cặp loại nguồn/đích, hướng và vai trò được phép.
  Sở hữu và điều khiển là hai loại riêng; không tự sinh quan hệ này từ quan hệ kia.
- Quan hệ có hướng chỉ lưu theo hướng quy ước; cách truy vấn ngược phải giữ nguyên ý nghĩa.
  Chưa có quan hệ đối xứng được duyệt; không tự tạo bản ghi đảo chiều.
- Chưa cho phép tự liên kết một bản ghi với chính nó khi chưa có use case được duyệt.
- Không đặt UNIQUE chỉ trên cặp nguồn–đích: cùng cặp có thể có loại khác hoặc nhiều lần ghi nhận.
  Cần chốt khóa chống trùng theo loại, vai trò, thời gian và nguồn; không tự gộp các nguồn khác nhau.
- valid_to chỉ có khi có valid_from và không sớm hơn valid_from. Bỏ trống mốc thời gian
  nghĩa là chưa biết, không tự coi là còn hiệu lực hoặc hiệu lực vô hạn.
- observed_at là thời điểm ghi nhận theo nguồn; created_at là thời điểm nhập hệ thống.
  Không thay thế lẫn nhau hoặc giả định tất cả liên kết cùng thời điểm với sự kiện.
- Với ghi nhận xuất hiện/điều khiển, đề xuất yêu cầu observed_at. Nếu nguồn chỉ có ngày hoặc
  khoảng thời gian, cần điều chỉnh thiết kế sau xác nhận, không tự đặt giờ giả.
- Không suy diễn bắc cầu: cá nhân liên quan phương tiện và phương tiện liên quan sự kiện
  không tự chứng minh cá nhân có mặt tại sự kiện.
- Không suy ra vị trí hiện tại từ bản ghi xuất hiện mới nhất; không suy ra vi phạm từ sự kiện,
  quan hệ hoặc vai trò. Nội dung mô tả cần trung tính và có nguồn.

## Toàn vẹn dữ liệu và cách lưu còn mở
source_kind/source_id và target_kind/target_id trong bản nháp là tham chiếu logic.
Một FK thông thường không thể tự trỏ tới nhiều bảng theo trường loại; chưa chọn cách lưu.
Nhóm cần so sánh bảng liên kết riêng theo cặp với cách biểu diễn chung, rồi quyết định cách
bảo đảm tồn tại, kiểm tra loại, chống trùng và giao dịch trước khi viết ORM/migration.
Không để tham chiếu đa hình làm mất ràng buộc dữ liệu.

Đề xuất tạm thời không xóa dây chuyền quan hệ khi xóa thực thể. Quy tắc chặn xóa,
lưu lịch sử, lưu trữ hoặc xóa theo chính sách phải được mentor xác nhận trước khi thiết kế.
Không mặc định soft delete. Sửa quan hệ sai, nguồn bị rút lại và gộp hồ sơ cần có quy trình được duyệt.

## Quyền và nguồn xác nhận
core-service kiểm tra quyền đọc/thêm/sửa/xóa liên kết và dữ liệu hai đầu theo chính sách được duyệt,
kể cả khi gọi API trực tiếp; tránh lộ thông tin qua liên kết tới bản ghi không được phép xem.
identity-service cung cấp thông tin danh tính qua hợp đồng API; không dùng FK sang bảng tài khoản.
Chưa chốt chính sách duyệt, nhật ký thao tác hoặc thuật toán bảo mật.

Nguồn ghi nhận đề xuất bắt buộc cho quan hệ, chỉ mô tả/tham chiếu nội dung được phép sử dụng.
Không đưa tài liệu nội bộ, token hoặc dữ liệu cá nhân thật vào ví dụ/Git.

Các quyết định còn mở: M04–M09 và M11 tại [câu hỏi mentor](../requirements/mentor-questions.md).
Ngọc Phúc chủ trì rà soát dữ liệu; phối hợp Thành về quyền, Thúy về tình huống kiểm thử.
