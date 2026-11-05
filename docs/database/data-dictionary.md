# Bản nháp từ điển dữ liệu nghiệp vụ

## Trạng thái và căn cứ
**Dữ kiện đã có từ yêu cầu nhóm:** phạm vi dự kiến gồm cá nhân, phương tiện, địa điểm,
sự kiện và liên kết; core-service sở hữu dữ liệu nghiệp vụ, identity-service sở hữu tài khoản,
thông tin xác thực và vai trò. Phạm vi tổng thể vẫn chờ mentor xác nhận.
`persons` chỉ là tên kỹ thuật tạm cho đối tượng là cá nhân.

**Giả định đề xuất:** toàn bộ tên trường, kiểu, tính bắt buộc, khóa và ràng buộc dưới đây
là phương án để thảo luận, chưa được mentor phê duyệt. Không có schema, bảng, ORM model,
migration hoặc API được tạo từ bản nháp này. Module không đồng nghĩa với bảng.
Chỉ dùng dữ liệu giả; chưa đề xuất thu thập số giấy tờ, sinh trắc học hoặc dữ liệu cá nhân nhạy cảm.

## Quy ước đọc bản nháp
- B = đề xuất bắt buộc; T = đề xuất tùy chọn. Cả hai đều chờ xác nhận.
- Kiểu là kiểu logic dự kiến cho PostgreSQL, chưa chốt độ dài, độ chính xác hoặc phiên bản.
- UUID là ứng viên cho định danh nội bộ, không phải giấy tờ hoặc định danh nghiệp vụ.
- Tùy chọn để trống nghĩa là chưa biết/chưa ghi nhận; không tự suy ra giá trị phủ định.
- Ngày sinh, năm sản xuất và thời gian thiếu độ chính xác không được điền giá trị giả để đủ trường.

## Trường chung đề xuất
Áp dụng cho năm nhóm bản ghi bên dưới, tất cả thuộc core-service.

| Trường dự kiến | Kiểu dự kiến | B/T | Ý nghĩa và ràng buộc đề xuất |
| --- | --- | --- | --- |
| id | UUID | B | Khóa chính nội bộ, duy nhất và ổn định trong loại thực thể |
| created_at | timestamp có múi giờ | B | Thời điểm tạo bản ghi, không phải thời điểm sự kiện/quan sát |
| updated_at | timestamp có múi giờ | B | Thời điểm cập nhật bản ghi, không sớm hơn created_at |
| source_note | text | T | Nguồn ghi nhận được phép lưu, không chứa bí mật; riêng quan hệ đề xuất B |

Chưa chốt soft delete, trạng thái duyệt, mã nghiệp vụ hoặc trường nhật ký người thao tác.
Nếu cần tham chiếu người thao tác, phải theo hợp đồng danh tính, không dùng FK sang bảng
identity-service và không chia sẻ ORM model. Quyền đọc/sửa dữ liệu được kiểm tra tại core-service.

## Cá nhân — persons (tạm thời)
**Mục đích đề xuất:** quản lý hồ sơ cá nhân trong phạm vi được phép, làm đầu mối liên kết
với phương tiện, địa điểm và sự kiện. Hồ sơ cá nhân không mặc nhiên là tài khoản đăng nhập.

Ngoài các trường chung:

| Trường dự kiến | Kiểu dự kiến | B/T | Ý nghĩa và ràng buộc đề xuất |
| --- | --- | --- | --- |
| display_name | text | B | Tên hiển thị/nhãn hồ sơ, không rỗng; không mặc định là họ tên pháp lý hoặc duy nhất |
| birth_date | date | T | Chỉ lưu khi cần và được phép; không ở tương lai; cách xử lý ngày sinh không đầy đủ chờ xác nhận |
| description | text | T | Mô tả trung tính trong phạm vi yêu cầu, không gán kết luận vi phạm |

**Khóa và quan hệ đề xuất:** dùng id; không đặt UNIQUE lên tên hoặc tên + ngày sinh.
Có thể liên kết nhiều phương tiện, địa điểm, sự kiện qua bản ghi quan hệ có loại/vai trò/thời gian.
Không thêm trường vị trí hiện tại suy từ lần xuất hiện.

**Cần mentor xác nhận:** đối tượng có bao gồm tổ chức không; tên/nhãn nào đủ để tạo hồ sơ;
có cần ngày sinh không; quy tắc chống trùng, gộp hồ sơ và quyền xem từng trường? Xem M01–M03.

## Phương tiện — vehicles
**Mục đích đề xuất:** quản lý hồ sơ phương tiện và các liên kết được ghi nhận,
độc lập với danh tính chủ sở hữu hoặc người điều khiển tại một thời điểm.

Ngoài các trường chung:

| Trường dự kiến | Kiểu dự kiến | B/T | Ý nghĩa và ràng buộc đề xuất |
| --- | --- | --- | --- |
| display_label | text | B | Nhãn mô tả hồ sơ, không rỗng; cho phép ghi nhận khi chưa biết biển số |
| vehicle_type | text hoặc mã danh mục | T | Loại phương tiện; danh mục chưa chốt |
| registration_number | text | T | Biển/số đăng ký nếu được phép; quy tắc chuẩn hóa, phạm vi và thời gian duy nhất chưa chốt |
| brand | text | T | Nhãn hiệu nếu được ghi nhận |
| color | text hoặc mã danh mục | T | Màu được ghi nhận, chưa chốt danh mục |
| description | text | T | Mô tả trung tính, không thay thế nguồn xác nhận |

**Khóa và quan hệ đề xuất:** id là khóa; chưa đặt UNIQUE toàn cục lên biển số vì cần làm rõ
phạm vi đăng ký và thay đổi theo thời gian. Liên kết cá nhân sở hữu và cá nhân điều khiển
là các vai trò riêng, có thời gian và nguồn. Không mặc định chủ sở hữu là người điều khiển;
không bắt buộc mỗi phương tiện có đúng một cá nhân liên quan.

**Cần mentor xác nhận:** loại phương tiện, có cho hồ sơ chưa biết biển số không;
biển số thay đổi/tái cấp xử lý thế nào; cần lịch sử sở hữu và ghi nhận người điều khiển ra sao? Xem M04, M07.

## Địa điểm — locations
**Mục đích đề xuất:** mô tả địa điểm được tham chiếu bởi sự kiện hoặc quan hệ;
không mặc nhiên là nơi cư trú hay vị trí hiện tại của cá nhân/phương tiện.

Ngoài các trường chung:

| Trường dự kiến | Kiểu dự kiến | B/T | Ý nghĩa và ràng buộc đề xuất |
| --- | --- | --- | --- |
| name | text | B | Tên/nhãn địa điểm, không rỗng; không mặc định duy nhất |
| address_text | text | T | Địa chỉ mô tả nếu có, chưa ép cấu trúc hành chính |
| latitude | numeric | T | Vĩ độ đề xuất theo WGS84, trong [-90, 90] |
| longitude | numeric | T | Kinh độ đề xuất theo WGS84, trong [-180, 180] |
| description | text | T | Ghi chú phạm vi/ý nghĩa địa điểm |

**Khóa và ràng buộc đề xuất:** id là khóa; cặp tọa độ cùng có hoặc cùng trống.
Không dùng (0, 0) để thay cho tọa độ chưa biết. Không đặt UNIQUE theo tên/địa chỉ/tọa độ.
Độ chính xác và hệ tọa độ cần mentor xác nhận; chưa chọn kiểu PostGIS.
Đề xuất điểm là phương án ban đầu; vùng/đường chỉ cân nhắc nếu có nhu cầu được duyệt.

**Quan hệ đề xuất:** một địa điểm có thể được nhiều sự kiện/quan hệ tham chiếu;
quan hệ xuất hiện phải có thời gian ghi nhận, không tạo thuộc tính vị trí hiện tại.

**Cần mentor xác nhận:** định nghĩa địa điểm, có chấp nhận thiếu tọa độ không,
độ chính xác, hệ tọa độ, điểm/vùng/đường và quyền xem thông tin bản đồ? Xem M05, M10.

## Sự kiện — events
**Mục đích đề xuất:** ghi nhận một sự việc trong phạm vi nghiệp vụ được xác nhận,
có thể liên kết cá nhân, phương tiện và địa điểm. Sự kiện không đồng nghĩa với vi phạm.

Ngoài các trường chung:

| Trường dự kiến | Kiểu dự kiến | B/T | Ý nghĩa và ràng buộc đề xuất |
| --- | --- | --- | --- |
| title | text | B | Tiêu đề mô tả trung tính, không rỗng |
| event_type | text hoặc mã danh mục | T | Phân loại nghiệp vụ chờ duyệt; không tự đặt loại vi phạm |
| occurred_from | timestamp có múi giờ | T | Thời điểm bắt đầu/xảy ra theo nguồn, không thay bằng created_at |
| occurred_to | timestamp có múi giờ | T | Thời điểm kết thúc; chỉ có khi có occurred_from và không sớm hơn nó |
| description | text | T | Nội dung sự việc theo thông tin được phép ghi nhận |

**Khóa và quan hệ đề xuất:** id là khóa; không suy ra trùng sự kiện chỉ từ tiêu đề/thời gian.
Cho phép chưa biết thời điểm trong phương án nháp; nếu nguồn chỉ có ngày/khoảng thời gian
thì cần chốt cách biểu diễn độ chính xác trước khi thiết kế schema, không tự gán giờ.
Vai trò cá nhân/phương tiện và địa điểm được biểu diễn qua liên kết; chưa mặc định sự kiện
có đúng một địa điểm hoặc bắt buộc có người liên quan.

**Cần mentor xác nhận:** thế nào là sự kiện hợp lệ, trường tối thiểu, loại/trạng thái,
thời gian không đầy đủ, một hay nhiều địa điểm và quy tắc tham gia? Xem M06–M08.

## Quan hệ liên quan — relationships
**Mục đích đề xuất:** biểu diễn một mối liên hệ được ghi nhận giữa hai thực thể nghiệp vụ,
kèm ý nghĩa, vai trò, thời gian và nguồn; không diễn giải liên quan thành hành vi vi phạm.
Đây là cấu trúc logic để thảo luận, chưa chọn bảng đa hình hay bảng liên kết riêng theo loại.

Ngoài các trường chung (source_note đề xuất bắt buộc riêng cho quan hệ):

| Trường dự kiến | Kiểu dự kiến | B/T | Ý nghĩa và ràng buộc đề xuất |
| --- | --- | --- | --- |
| source_kind | text hoặc mã danh mục | B | Loại thực thể đầu nguồn đã duyệt: person, vehicle, location hoặc event |
| source_id | UUID, tham chiếu logic | B | Bản ghi đầu nguồn phải tồn tại và đúng source_kind |
| target_kind | text hoặc mã danh mục | B | Loại thực thể đầu đích đã duyệt |
| target_id | UUID, tham chiếu logic | B | Bản ghi đầu đích phải tồn tại và đúng target_kind |
| relationship_type | text hoặc mã danh mục | B | Loại quan hệ theo cặp thực thể và hướng được duyệt |
| role | text hoặc mã danh mục | T | Vai trò chi tiết; bắt buộc theo loại nếu được duyệt; không thay thế relationship_type |
| valid_from | timestamp có múi giờ | T | Đầu khoảng hiệu lực của quan hệ, không phải thời điểm nhập liệu |
| valid_to | timestamp có múi giờ | T | Cuối khoảng hiệu lực; có valid_from và không sớm hơn nó |
| observed_at | timestamp có múi giờ | T | Bắt buộc có điều kiện với loại ghi nhận xuất hiện/điều khiển tại thời điểm, nếu loại đó được duyệt |
| description | text | T | Diễn giải trung tính và giới hạn của ghi nhận |

**Khóa, ràng buộc và quan hệ đề xuất:** id là khóa; source/target chỉ trỏ tới thực thể
trong core-service, không trỏ tới bảng tài khoản. source_note ghi nguồn được phép lưu,
không yêu cầu đính kèm tài liệu nội bộ. Không cho quan hệ trỏ tới chính bản ghi quan hệ.
Chưa mặc định cho phép tự liên kết cùng một thực thể. Chỉ cho cặp loại/hướng/vai trò đã duyệt;
quy tắc trùng, đối xứng, giao khoảng và xóa xem [bản nháp quan hệ](relationships.md).
Các tham chiếu logic này không phải khai báo FK có thể chạy được.

**Cần mentor xác nhận:** danh mục loại quan hệ/vai trò, cặp hợp lệ, bội số, đối xứng,
nguồn tối thiểu, độ chính xác thời gian, quyền duyệt/sửa và lịch sử? Xem M07–M09.

## Nội dung cần chốt trước thiết kế schema
Chốt các câu hỏi tại [mentor-questions.md](../requirements/mentor-questions.md), rồi cập nhật
bảng trường, ERD, quyền dữ liệu, migration và hợp đồng API qua review.
Ngọc Phúc chủ trì dữ liệu nghiệp vụ, phối hợp Tiến Thành về quyền và Nhật Thúy về kiểm thử.
Không lấy bản nháp này làm bằng chứng đã triển khai hoặc đã phê duyệt thu thập dữ liệu.
