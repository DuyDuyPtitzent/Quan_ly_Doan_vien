# Kế Hoạch Triển Khai Dự Án Đoàn Số Theo Module

## 1. Mục tiêu

Tài liệu này mô tả thứ tự triển khai các module của dự án Đoàn số sao cho dễ kiểm soát, đúng phụ thuộc nghiệp vụ và tránh làm rối luồng. Nguyên tắc chính là xây nền tảng hệ thống trước, sau đó đến dữ liệu gốc, nghiệp vụ chính, luồng duyệt, xét tiêu chí, báo cáo và quản trị.

## 2. Nguyên tắc triển khai

- Làm backend data model và API trước, sau đó mới làm giao diện.
- Module nào là dữ liệu nền thì làm trước module nghiệp vụ.
- Module nào cần phân quyền thì chỉ làm sau khi module tài khoản và tổ chức Đoàn đã ổn định.
- Không xử lý điểm rèn luyện trong hệ thống Đoàn số vì phần này thuộc phòng CT&CTSV quản lý.
- Minh chứng tự khai báo phải đi qua duyệt trước khi được ghi nhận vào hồ sơ năng lực.
- Mỗi module có trạng thái rõ ràng để dễ kiểm soát: nháp, chờ duyệt, đã duyệt, từ chối, yêu cầu bổ sung.
- Mỗi module nên hoàn thành theo thứ tự: database, service nghiệp vụ, API, giao diện, test.

## 3. Thứ tự module cần triển khai

### 3.1. Module nền tảng hệ thống

Mục tiêu: tạo khung chạy ổn định cho toàn bộ dự án.

Cần làm:

- Khởi tạo cấu trúc backend, frontend và database.
- Cấu hình môi trường dev, staging, production.
- Cấu hình kết nối database.
- Cấu hình upload file dùng chung.
- Cấu hình logging và error handling.
- Tạo chuẩn response API.
- Tạo cơ chế validate dữ liệu.
- Tạo phân trang, filter, sort dùng chung.

Lý do làm đầu tiên:

- Tất cả module sau đều dùng chung chuẩn API, validate, database và upload file.

### 3.2. Module tài khoản và phân quyền

Mục tiêu: xác định ai đang sử dụng hệ thống và được làm gì.

Cần làm:

- Đăng nhập.
- Đăng xuất.
- Đổi mật khẩu.
- Quên mật khẩu nếu cần.
- Quản lý vai trò:
  - Sinh viên.
  - Cán bộ Chi đoàn.
  - Cán bộ Liên chi.
  - Cán bộ Đoàn trường.
  - Admin hệ thống.
- Thiết kế rule phân quyền theo cấp quản lý.
- Middleware/guard kiểm tra quyền cho API.

Lý do làm sớm:

- Các module như duyệt minh chứng, quản lý sinh viên, tạo sự kiện và báo cáo đều phụ thuộc vào quyền người dùng.

### 3.3. Module hồ sơ sinh viên / đoàn viên

Mục tiêu: quản lý thông tin gốc của sinh viên và đoàn viên.

Cần làm:

- Quản lý thông tin cá nhân.
- Quản lý mã sinh viên.
- Quản lý lớp, khoa, chi đoàn, niên khóa.
- Quản lý trạng thái đoàn viên.
- Sinh viên xem hồ sơ cá nhân.
- Cán bộ xem danh sách sinh viên trong phạm vi quản lý.

Phụ thuộc:

- Module tài khoản và phân quyền.

### 3.4. Module tổ chức Đoàn

Mục tiêu: mô tả cơ cấu quản lý của Đoàn trong hệ thống.

Cần làm:

- Quản lý khoa.
- Quản lý liên chi.
- Quản lý chi đoàn.
- Quản lý lớp.
- Gán cán bộ phụ trách từng đơn vị.
- Thiết lập quan hệ cấp trên - cấp dưới.

Lý do làm trước các module duyệt:

- Quyền duyệt và phạm vi xem dữ liệu phụ thuộc vào cơ cấu tổ chức Đoàn.

### 3.5. Module năm học / học kỳ / đợt xét

Mục tiêu: tạo mốc thời gian dùng chung cho hoạt động, minh chứng và xét danh hiệu.

Cần làm:

- Tạo năm học.
- Tạo học kỳ.
- Tạo đợt xét danh hiệu hoặc đợt tổng hợp minh chứng.
- Cấu hình thời gian mở/đóng đăng ký.
- Cấu hình thời gian nộp minh chứng.
- Cấu hình thời gian cán bộ duyệt.

Phụ thuộc:

- Module nền tảng hệ thống.

### 3.6. Module danh mục tiêu chí và nhóm kỹ năng

Mục tiêu: tạo bộ danh mục để gắn cho hoạt động, minh chứng và tiêu chí xét.

Cần làm:

- Tạo danh mục nhóm kỹ năng.
- Tạo tiêu chí Sinh viên 5 tốt.
- Tạo bộ tiêu chí và điều kiện xét.
- Cấu hình tiêu chí nào được tính cho năm học/đợt xét nào.

Lý do làm trước module sự kiện và minh chứng:

- Sự kiện và minh chứng cần gắn vào nhóm kỹ năng và tiêu chí.

### 3.7. Module sự kiện / hoạt động trong hệ thống

Mục tiêu: quản lý các hoạt động do nhà trường/Đoàn tạo sẵn.

Cần làm:

- Cán bộ tạo hoạt động, chương trình, sự kiện.
- Cấu hình thời gian đăng ký.
- Cấu hình số lượng tham gia.
- Cấu hình địa điểm.
- Cấu hình đơn vị tổ chức.
- Gắn hoạt động với nhóm kỹ năng.
- Gắn hoạt động với tiêu chí Sinh viên 5 tốt.
- Sinh viên đăng ký tham gia.
- Cán bộ xem danh sách đăng ký.

Phụ thuộc:

- Tài khoản và phân quyền.
- Tổ chức Đoàn.
- Năm học / học kỳ / đợt xét.
- Danh mục tiêu chí và nhóm kỹ năng.

### 3.8. Module điểm danh / xác nhận tham gia

Mục tiêu: xác nhận sinh viên có tham gia hoạt động thực tế hay không.

Cần làm giai đoạn 1:

- Cán bộ tick danh sách sinh viên tham gia.
- Lưu trạng thái tham gia.
- Ghi nhận hoạt động vào hồ sơ sinh viên khi đã được xác nhận.

Có thể mở rộng sau:

- QR check-in.
- Import Excel.
- Điểm danh nhiều buổi.

Phụ thuộc:

- Module sự kiện / hoạt động trong hệ thống.
- Module hồ sơ sinh viên.

### 3.9. Module minh chứng tự khai báo

Mục tiêu: cho phép sinh viên nộp minh chứng ngoài hệ thống.

Cần làm:

- Tạo form sinh viên nộp minh chứng.
- Các trường cần có:
  - Tên hoạt động/chứng chỉ/thành tích.
  - Đơn vị tổ chức.
  - Thời gian.
  - Địa điểm/hình thức.
  - Loại minh chứng.
  - Nhóm kỹ năng đề xuất.
  - Tiêu chí Sinh viên 5 tốt đề xuất.
  - File minh chứng.
  - Link xác minh nếu có.
  - Ghi chú.
- Kiểm tra sơ bộ:
  - File hợp lệ.
  - Có bị trùng minh chứng cũ không.
  - Thời gian có thuộc năm học không.
  - Link xác minh có đúng định dạng không.
- Trạng thái sau khi nộp: chờ duyệt.

Nguyên tắc:

- Không ghi nhận minh chứng vào hồ sơ khi sinh viên vừa nộp.
- Hệ thống chỉ gợi ý nhóm kỹ năng và tiêu chí phù hợp.

Phụ thuộc:

- Hồ sơ sinh viên.
- Năm học / học kỳ / đợt xét.
- Danh mục tiêu chí và nhóm kỹ năng.
- Upload file dùng chung.

### 3.10. Module duyệt minh chứng

Mục tiêu: cán bộ xem, kiểm tra và quyết định minh chứng có được ghi nhận hay không.

Cần làm:

- Danh sách minh chứng chờ duyệt.
- Chi tiết minh chứng.
- Xem file đính kèm.
- Xem link xác minh.
- Xem thông tin sinh viên.
- Các hành động duyệt:
  - Duyệt.
  - Từ chối.
  - Yêu cầu bổ sung.
  - Chuyển cấp cao hơn.
- Khi duyệt, cán bộ xác nhận:
  - Minh chứng hợp lệ hay không.
  - Nhóm kỹ năng chính thức.
  - Tiêu chí Sinh viên 5 tốt chính thức.
- Lưu lịch sử duyệt.

Nguyên tắc:

- Chỉ khi đã duyệt thì minh chứng mới được ghi vào hồ sơ năng lực.
- Nếu từ chối thì minh chứng không được ghi nhận.
- Nếu yêu cầu bổ sung thì sinh viên được cập nhật và nộp lại.

Phụ thuộc:

- Minh chứng tự khai báo.
- Tài khoản và phân quyền.
- Tổ chức Đoàn.

### 3.11. Module hồ sơ năng lực / lịch sử hoạt động

Mục tiêu: tổng hợp những gì sinh viên đã tham gia và đã được công nhận.

Nguồn dữ liệu:

- Hoạt động trong hệ thống đã được xác nhận tham gia.
- Minh chứng tự khai báo đã được duyệt.

Cần làm:

- Sinh viên xem lịch sử hoạt động.
- Sinh viên xem minh chứng đã được duyệt.
- Sinh viên xem nhóm kỹ năng đạt được.
- Sinh viên xem tiêu chí liên quan.
- Cán bộ xem hồ sơ năng lực của sinh viên trong phạm vi quản lý.

Phụ thuộc:

- Điểm danh / xác nhận tham gia.
- Duyệt minh chứng.

### 3.12. Module xét tiêu chí

Mục tiêu: tổng hợp trạng thái tiêu chí theo năm học hoặc học kỳ, không xử lý điểm rèn luyện.

Cần làm:

- Tính trạng thái tiêu chí đạt/chưa đạt.
- Tổng hợp hoạt động và minh chứng liên quan đến từng tiêu chí.
- Phân biệt nguồn ghi nhận:
  - Hoạt động trong hệ thống.
  - Minh chứng tự khai báo đã duyệt.
- Cho cán bộ kiểm tra và xác nhận kết quả cuối.

Nguyên tắc:

- Không sử dụng minh chứng chưa duyệt để xét tiêu chí.
- Điểm rèn luyện không nằm trong phạm vi module này.

Phụ thuộc:

- Hồ sơ năng lực / lịch sử hoạt động.
- Danh mục tiêu chí và nhóm kỹ năng.

### 3.13. Module xét duyệt Sinh viên 5 tốt / đánh giá đoàn viên

Mục tiêu: hỗ trợ xét danh hiệu và đánh giá dựa trên dữ liệu đã tổng hợp.

Cần làm:

- Sinh viên xem tiêu chí đã đạt/chưa đạt.
- Hệ thống gợi ý trạng thái đạt tiêu chí.
- Cán bộ duyệt kết quả cuối.
- Lưu lịch sử xét duyệt theo từng đợt.
- Cho phép xem lại kết quả các đợt trước.

Phụ thuộc:

- Xét tiêu chí.
- Năm học / học kỳ / đợt xét.

### 3.14. Module hồ sơ chính thức / chương trình Đảng - Đoàn - Nhà nước

Mục tiêu: hỗ trợ tạo, xử lý và xác thực hồ sơ chính thức phục vụ học bổng, chương trình Đảng - Đoàn - Nhà nước, Đoàn viên ưu tú và các chương trình cần bình xét nội bộ.

Cần làm:

- Sinh viên tự tạo yêu cầu xuất hồ sơ chính thức cho học bổng Nhà nước, chương trình lãnh đạo trẻ, Đại hội Đoàn/Hội, chương trình/diễn đàn thanh niên hoặc hồ sơ tùy chỉnh.
- Cán bộ Chi đoàn tạo yêu cầu đề xuất đoàn viên cho hồ sơ giới thiệu Đoàn viên ưu tú vào Đảng, đoàn viên tiêu biểu, nhân sự/đại biểu/gương mặt tiêu biểu.
- Liên chi/Đoàn khoa kiểm tra, nhận xét, phê duyệt hoặc chuyển tiếp yêu cầu đề xuất.
- Đoàn trường/Đoàn Học viện tạo chương trình/sự kiện cấp Học viện, công bố form đăng ký và phân dữ liệu về đúng Cán bộ Chi đoàn.
- Ban Đoàn trường/Đoàn Học viện xác thực hồ sơ cuối cùng.
- Sau xác thực, hệ thống tạo PDF chính thức, chữ ký số/dấu xác thực, mã QR, link hồ sơ gốc và lưu lịch sử phê duyệt.

Phụ thuộc:

- Hồ sơ sinh viên / đoàn viên.
- Hồ sơ năng lực / lịch sử hoạt động.
- Minh chứng đã duyệt.
- Xét tiêu chí và danh hiệu.
- Tổ chức Đoàn và phân quyền theo cấp.

### 3.15. Module thông báo

Mục tiêu: báo cho đúng người đúng lúc khi có thay đổi quan trọng.

Cần làm giai đoạn 1:

- Thông báo trong hệ thống.
- Gửi thông báo khi:
  - Sinh viên nộp minh chứng.
  - Minh chứng được duyệt.
  - Minh chứng bị từ chối.
  - Cán bộ yêu cầu bổ sung.
  - Có hoạt động mới.
  - Sắp hết hạn nộp hồ sơ.
  - Có yêu cầu hồ sơ chính thức cần xử lý.
  - Hồ sơ chính thức được xác thực hoặc bị yêu cầu bổ sung.

Có thể mở rộng sau:

- Email.
- Push notification.

Phụ thuộc:

- Tài khoản người dùng.
- Minh chứng.
- Sự kiện.
- Đợt xét.
- Hồ sơ chính thức.

### 3.16. Module báo cáo và thống kê

Mục tiêu: cung cấp số liệu cho cán bộ theo dõi và tổng hợp.

Cần làm:

- Báo cáo số lượng sinh viên tham gia hoạt động.
- Báo cáo minh chứng theo trạng thái.
- Báo cáo tiêu chí theo lớp/khoa/chi đoàn.
- Báo cáo danh sách sinh viên đạt/chưa đạt tiêu chí.
- Báo cáo hồ sơ chính thức theo trạng thái.
- Filter theo năm học, học kỳ, đơn vị, trạng thái.
- Export Excel/PDF nếu cần.

Phụ thuộc:

- Hoạt động.
- Minh chứng.
- Xét tiêu chí.
- Hồ sơ chính thức.
- Tổ chức Đoàn.

### 3.17. Module quản trị hệ thống

Mục tiêu: cho admin cấu hình và kiểm soát toàn bộ hệ thống.

Cần làm:

- Quản lý tài khoản.
- Quản lý vai trò và quyền.
- Quản lý danh mục.
- Quản lý cấu hình tiêu chí.
- Quản lý năm học, học kỳ, đợt xét.
- Quản lý mẫu hồ sơ chính thức, mẫu giấy giới thiệu, mẫu biên bản và mẫu quyết định.
- Xem log thao tác quan trọng.

Phụ thuộc:

- Các module nền tảng và danh mục đã có sẵn.

## 4. Thứ tự code trong mỗi module

Mỗi module nên được triển khai theo thứ tự sau:

1. Phân tích nghiệp vụ chi tiết của module.
2. Thiết kế database/model.
3. Viết migration.
4. Viết enum/constant nếu có.
5. Viết validation/schema.
6. Viết service xử lý nghiệp vụ.
7. Viết API/controller.
8. Viết phân quyền cho API.
9. Viết giao diện danh sách.
10. Viết giao diện tạo/sửa/chi tiết.
11. Viết test backend.
12. Viết test UI hoặc test luồng chính.
13. Kiểm tra lại với dữ liệu mẫu.

## 5. Mốc kiểm soát theo giai đoạn

### Giai đoạn 1: Nền tảng và dữ liệu gốc

Hoàn thành:

- Nền tảng hệ thống.
- Tài khoản và phân quyền.
- Hồ sơ sinh viên / đoàn viên.
- Tổ chức Đoàn.
- Năm học / học kỳ / đợt xét.
- Danh mục tiêu chí và nhóm kỹ năng.

Kết quả cần đạt:

- Đăng nhập được.
- Phân quyền theo vai trò hoạt động.
- Có dữ liệu sinh viên, đơn vị Đoàn, năm học và tiêu chí.

### Giai đoạn 2: Hoạt động trong hệ thống

Hoàn thành:

- Sự kiện / hoạt động.
- Đăng ký tham gia.
- Điểm danh / xác nhận tham gia.
- Ghi nhận vào hồ sơ năng lực.

Kết quả cần đạt:

- Cán bộ tạo được hoạt động.
- Sinh viên đăng ký được.
- Cán bộ xác nhận tham gia được.
- Hoạt động đã xác nhận hiện trong hồ sơ sinh viên.

### Giai đoạn 3: Minh chứng và duyệt

Hoàn thành:

- Minh chứng tự khai báo.
- Duyệt minh chứng.
- Lịch sử duyệt.
- Cập nhật hồ sơ sau khi duyệt.

Kết quả cần đạt:

- Sinh viên nộp minh chứng được.
- Cán bộ duyệt/từ chối/yêu cầu bổ sung được.
- Minh chứng đã duyệt mới được tính vào hồ sơ.

### Giai đoạn 4: Xét tiêu chí và danh hiệu

Hoàn thành:

- Xét tiêu chí.
- Xét duyệt Sinh viên 5 tốt / đánh giá đoàn viên.

Kết quả cần đạt:

- Hệ thống tổng hợp trạng thái tiêu chí đúng theo năm học/học kỳ.
- Hệ thống gợi ý đạt/chưa đạt tiêu chí.
- Cán bộ xác nhận kết quả cuối.

### Giai đoạn 5: Hồ sơ chính thức, thông báo, báo cáo và quản trị

Hoàn thành:

- Hồ sơ chính thức / chương trình Đảng - Đoàn - Nhà nước.
- Thông báo.
- Báo cáo và thống kê.
- Quản trị hệ thống.

Kết quả cần đạt:

- Sinh viên tạo được yêu cầu hồ sơ chính thức thuộc nhóm được phép tự tạo.
- Cán bộ Chi đoàn tạo được yêu cầu đề xuất đoàn viên.
- Đoàn trường/Đoàn Học viện xác thực được hồ sơ chính thức và xuất PDF/QR/link tra cứu.
- Người dùng nhận thông báo đúng luồng.
- Cán bộ xem được báo cáo.
- Admin cấu hình và kiểm soát được hệ thống.

## 6. Test plan tổng quát

- Test đăng nhập và phân quyền theo từng vai trò.
- Test sinh viên chỉ xem/sửa được dữ liệu của mình.
- Test cán bộ chỉ xem/duyệt dữ liệu trong phạm vi quản lý.
- Test tạo hoạt động, đăng ký hoạt động và xác nhận tham gia.
- Test nộp minh chứng tự khai báo hợp lệ.
- Test minh chứng thiếu file hoặc sai định dạng bị chặn.
- Test minh chứng trùng dữ liệu được cảnh báo hoặc bị chặn theo rule.
- Test cán bộ duyệt minh chứng thì hồ sơ được cập nhật.
- Test từ chối minh chứng thì không ghi nhận vào hồ sơ năng lực.
- Test yêu cầu bổ sung thì sinh viên được sửa và nộp lại.
- Test tổng hợp trạng thái tiêu chí theo năm học/học kỳ.
- Test xét tiêu chí đạt/chưa đạt.
- Test sinh viên tạo yêu cầu hồ sơ chính thức và nhận kết quả xác thực.
- Test cán bộ Chi đoàn tạo yêu cầu đề xuất Đoàn viên ưu tú và chuyển đúng cấp xử lý.
- Test Đoàn trường/Đoàn Học viện xác thực hồ sơ chính thức, tạo PDF, QR và link tra cứu.
- Test báo cáo đúng theo dữ liệu đã duyệt.

## 7. Giả định mặc định

- Dự án Đoàn số có các nghiệp vụ chính: quản lý sinh viên, hoạt động Đoàn, minh chứng, xét duyệt, tiêu chí, hồ sơ chính thức và báo cáo.
- Phân quyền theo mô hình nhiều cấp: Chi đoàn, Liên chi, Đoàn trường, Admin.
- File minh chứng dùng chung một cơ chế upload file cho toàn hệ thống.
- Điểm rèn luyện do phòng CT&CTSV quản lý, hệ thống Đoàn số chỉ phục vụ hồ sơ năng lực, minh chứng, tiêu chí và báo cáo liên quan.
- Thông báo trong hệ thống làm trước, email/push notification có thể làm sau.
