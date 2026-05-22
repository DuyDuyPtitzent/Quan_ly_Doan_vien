# Kế Hoạch Chi Tiết Các Trang Theo Vai Trò Trong Dự Án Đoàn Số

## 1. Mục tiêu

Tài liệu này mô tả các trang/chức năng chính theo từng vai trò người dùng trong hệ thống Đoàn số. Mục tiêu là giúp khi triển khai frontend và backend không bị loạn quyền, không nhầm chức năng giữa sinh viên, cán bộ Chi đoàn, cán bộ Liên chi, cán bộ Đoàn trường và Admin.

Nguyên tắc chung:

- Sinh viên chủ yếu thao tác với dữ liệu của chính mình.
- Cán bộ Chi đoàn thao tác trong phạm vi Chi đoàn được gán.
- Cán bộ Liên chi thao tác trong phạm vi Liên chi được gán.
- Cán bộ Đoàn trường thao tác trong phạm vi toàn trường.
- Admin quản trị cấu hình hệ thống, tài khoản và phân quyền.

## 2. Trang dành cho Sinh viên

### 2.1. Dashboard sinh viên

Mục đích: hiển thị tổng quan tình trạng hồ sơ và hoạt động của sinh viên.

Thông tin chính:

- Họ tên.
- Mã sinh viên.
- Lớp.
- Chi đoàn.
- Khoa/Liên chi.
- Trạng thái đoàn viên.
- Tổng số hoạt động đã tham gia.
- Tổng số minh chứng đã nộp.
- Số minh chứng chờ duyệt.
- Số minh chứng đã duyệt.
- Tiêu chí Sinh viên 5 tốt đã đạt/chưa đạt.
- Thông báo mới nhất.

### 2.2. Hồ sơ sinh viên

Mục đích: sinh viên xem và cập nhật thông tin cá nhân được phép sửa.

Trường thông tin chính:

- Ảnh đại diện.
- Họ và tên.
- Mã sinh viên.
- Email trường.
- Số điện thoại.
- Ngày sinh.
- Giới tính.
- Địa chỉ.
- Lớp.
- Chi đoàn.
- Khoa/Liên chi.
- Niên khóa.
- Trạng thái đoàn viên.
- Ngày vào Đoàn nếu có.
- Chức vụ trong Chi đoàn nếu có.
- Ghi chú cá nhân nếu cần.

Quyền thao tác:

- Sinh viên được xem hồ sơ của mình.
- Sinh viên chỉ được sửa các trường được cho phép như số điện thoại, địa chỉ, ảnh đại diện.
- Các trường như mã sinh viên, lớp, chi đoàn, khoa nên do cán bộ hoặc admin quản lý.

### 2.3. Hoạt động/Sự kiện

Mục đích: sinh viên xem và đăng ký các hoạt động trong hệ thống.

Trường thông tin chính:

- Tên hoạt động.
- Mã hoạt động nếu có.
- Đơn vị tổ chức.
- Thời gian bắt đầu.
- Thời gian kết thúc.
- Địa điểm.
- Hình thức tổ chức: trực tiếp/online/kết hợp.
- Số lượng tối đa.
- Số lượng đã đăng ký.
- Hạn đăng ký.
- Nhóm kỹ năng liên quan.
- Tiêu chí Sinh viên 5 tốt liên quan.
- Trạng thái đăng ký: chưa đăng ký, đã đăng ký, đã tham gia, vắng mặt.

Quyền thao tác:

- Xem danh sách hoạt động.
- Đăng ký hoạt động còn mở.
- Hủy đăng ký nếu còn trong thời gian cho phép.
- Xem lịch sử tham gia.

### 2.4. Minh chứng tự khai báo

Mục đích: sinh viên nộp minh chứng ngoài hệ thống để cán bộ duyệt.

Trường thông tin chính:

- Tên hoạt động/chứng chỉ/thành tích.
- Đơn vị tổ chức.
- Thời gian bắt đầu.
- Thời gian kết thúc.
- Địa điểm/hình thức.
- Loại minh chứng:
  - Chứng chỉ.
  - Giấy chứng nhận.
  - Giải thưởng.
  - Hoạt động tình nguyện.
  - Nghiên cứu khoa học.
  - Hội thảo/tập huấn.
  - Khác.
- Nhóm kỹ năng đề xuất.
- Tiêu chí Sinh viên 5 tốt đề xuất.
- Vai trò/mức độ tham gia.
- File minh chứng.
- Link xác minh nếu có.
- Ghi chú.
- Trạng thái: nháp, chờ duyệt, đã duyệt, từ chối, yêu cầu bổ sung.
- Lý do từ chối hoặc nội dung yêu cầu bổ sung nếu có.
- Kết quả duyệt nếu có.

Quyền thao tác:

- Tạo minh chứng.
- Lưu nháp.
- Nộp minh chứng.
- Sửa minh chứng khi ở trạng thái nháp hoặc yêu cầu bổ sung.
- Xem kết quả duyệt.
- Không được sửa minh chứng đã duyệt hoặc đã từ chối, trừ khi hệ thống cho phép nộp lại bản mới.

### 2.5. Hồ sơ năng lực / lịch sử hoạt động

Mục đích: tổng hợp toàn bộ hoạt động và minh chứng đã được ghi nhận.

Thông tin chính:

- Danh sách hoạt động đã tham gia.
- Danh sách minh chứng đã duyệt.
- Nguồn ghi nhận: hoạt động hệ thống hoặc minh chứng tự khai báo.
- Nhóm kỹ năng đạt được.
- Tiêu chí Sinh viên 5 tốt liên quan.
- Năm học/học kỳ.
- Ngày được ghi nhận.

### 2.6. Kết quả xét tiêu chí / Sinh viên 5 tốt

Mục đích: sinh viên theo dõi trạng thái đạt/chưa đạt các tiêu chí.

Thông tin chính:

- Đợt xét.
- Năm học.
- Tiêu chí.
- Minh chứng/hoạt động liên quan.
- Trạng thái: đạt, chưa đạt, chờ duyệt.
- Ghi chú của cán bộ nếu có.

### 2.7. Hồ sơ chính thức

Mục đích: sinh viên tự tạo yêu cầu xuất hồ sơ chính thức cho các loại hồ sơ được phép tự khởi tạo.

Thông tin chính:

- Loại hồ sơ yêu cầu.
- Hồ sơ học bổng Nhà nước.
- Hồ sơ chương trình lãnh đạo trẻ.
- Hồ sơ Đại hội Đoàn/Hội các cấp.
- Hồ sơ chương trình/diễn đàn thanh niên.
- Hồ sơ khác/tùy chỉnh.
- Dữ liệu được chọn đưa vào hồ sơ.
- Trạng thái yêu cầu xác thực.
- File PDF chính thức nếu đã xác thực.
- Link tra cứu.
- Mã QR xác minh.
- Lịch sử hồ sơ đã xuất.

Quyền thao tác:

- Sinh viên tự tạo yêu cầu với các loại hồ sơ được phép.
- Sinh viên không tự tạo hồ sơ giới thiệu Đoàn viên ưu tú vào Đảng nếu quy trình yêu cầu cán bộ Chi đoàn đề xuất.
- Hồ sơ chỉ có giá trị chính thức sau khi Ban Đoàn trường/Đoàn Học viện xác thực.

### 2.8. Thông báo

Thông tin chính:

- Tiêu đề thông báo.
- Nội dung ngắn.
- Loại thông báo.
- Thời gian gửi.
- Trạng thái đã đọc/chưa đọc.
- Link đến dữ liệu liên quan.

## 3. Trang dành cho Cán bộ Chi đoàn

### 3.1. Dashboard Chi đoàn

Mục đích: cán bộ Chi đoàn xem tổng quan dữ liệu trong Chi đoàn mình phụ trách.

Thông tin chính:

- Tên Chi đoàn.
- Lớp/khoa trực thuộc.
- Số lượng sinh viên.
- Số sinh viên đã tham gia hoạt động.
- Số minh chứng chờ duyệt cấp Chi đoàn.
- Số minh chứng đã duyệt/từ chối.
- Số sinh viên đạt/chưa đạt tiêu chí.
- Hoạt động sắp diễn ra.
- Thông báo cần xử lý.

### 3.2. Quản lý sinh viên trong Chi đoàn

Thông tin chính:

- Họ tên.
- Mã sinh viên.
- Email.
- Số điện thoại.
- Lớp.
- Chi đoàn.
- Trạng thái đoàn viên.
- Chức vụ nếu có.
- Tổng hoạt động đã tham gia.
- Tổng minh chứng đã nộp.
- Trạng thái xét tiêu chí.

Quyền thao tác:

- Xem danh sách sinh viên thuộc Chi đoàn mình.
- Xem hồ sơ chi tiết từng sinh viên.
- Cập nhật một số thông tin hành chính nếu được phân quyền.
- Không xem/sửa sinh viên ngoài Chi đoàn mình.

### 3.3. Duyệt minh chứng cấp Chi đoàn

Thông tin chính:

- Sinh viên nộp.
- Mã sinh viên.
- Tên minh chứng.
- Loại minh chứng.
- Thời gian diễn ra.
- File minh chứng.
- Link xác minh.
- Nhóm kỹ năng đề xuất.
- Tiêu chí đề xuất.
- Trạng thái duyệt.
- Ghi chú sinh viên.
- Ghi chú cán bộ.

Quyền thao tác:

- Duyệt minh chứng thuộc sinh viên trong Chi đoàn mình.
- Từ chối minh chứng.
- Yêu cầu bổ sung.
- Chuyển lên cấp Liên chi nếu cần.
- Xác nhận nhóm kỹ năng và tiêu chí nếu được phân quyền.

### 3.4. Xác nhận tham gia hoạt động

Thông tin chính:

- Tên hoạt động.
- Thời gian.
- Danh sách sinh viên đăng ký.
- Trạng thái tham gia: đã tham gia, vắng mặt, chưa xác nhận.
- Ghi chú điểm danh nếu có.

Quyền thao tác:

- Xác nhận tham gia cho sinh viên thuộc Chi đoàn mình.
- Không xác nhận sinh viên ngoài phạm vi Chi đoàn.

### 3.5. Theo dõi tiêu chí Chi đoàn

Thông tin chính:

- Sinh viên.
- Tiêu chí đã đạt.
- Tiêu chí chưa đạt.
- Minh chứng/hoạt động dùng để xét.
- Trạng thái xác nhận.

Quyền thao tác:

- Xem tổng hợp trong Chi đoàn.
- Đề xuất/xác nhận cấp Chi đoàn nếu quy trình yêu cầu.

### 3.6. Tạo yêu cầu đề xuất đoàn viên

Thông tin chính:

- Loại hồ sơ đề xuất.
- Đoàn viên được đề xuất.
- Hồ sơ cá nhân.
- Tổng quan hồ sơ năng lực.
- Minh chứng liên quan.
- Danh hiệu đã đạt.
- Nhận xét của Chi đoàn.
- Cấp xử lý tiếp theo.
- Trạng thái yêu cầu.

Quyền thao tác:

- Cán bộ Chi đoàn tạo yêu cầu đề xuất cho đoàn viên thuộc Chi đoàn mình.
- Áp dụng cho giới thiệu Đoàn viên ưu tú vào Đảng, đề xuất đoàn viên tiêu biểu, nhân sự/đại biểu/gương mặt tiêu biểu cần bình xét nội bộ.
- Sau khi tạo, yêu cầu được chuyển lên Liên chi/Đoàn khoa/Đoàn Học viện theo quy trình.

### 3.7. Báo cáo Chi đoàn

Thông tin chính:

- Số lượng sinh viên theo trạng thái.
- Số hoạt động đã tham gia.
- Số minh chứng theo trạng thái.
- Danh sách sinh viên đạt/chưa đạt tiêu chí.
- Export Excel nếu cần.

## 4. Trang dành cho Cán bộ Liên chi

### 4.1. Dashboard Liên chi

Thông tin chính:

- Tên Liên chi/Khoa.
- Tổng số Chi đoàn trực thuộc.
- Tổng số sinh viên.
- Số minh chứng chờ duyệt cấp Liên chi.
- Số hoạt động cấp Liên chi.
- Tỷ lệ sinh viên tham gia hoạt động.
- Tỷ lệ đạt tiêu chí.
- Báo cáo nhanh theo Chi đoàn.

### 4.2. Quản lý Chi đoàn trực thuộc

Thông tin chính:

- Tên Chi đoàn.
- Lớp.
- Số lượng sinh viên.
- Cán bộ Chi đoàn phụ trách.
- Số minh chứng chờ duyệt.
- Số sinh viên đạt/chưa đạt tiêu chí.

Quyền thao tác:

- Xem danh sách Chi đoàn thuộc Liên chi mình.
- Xem dữ liệu tổng hợp từng Chi đoàn.
- Không xem dữ liệu ngoài Liên chi mình.

### 4.3. Quản lý sinh viên trong Liên chi

Thông tin chính:

- Họ tên.
- Mã sinh viên.
- Lớp.
- Chi đoàn.
- Trạng thái đoàn viên.
- Trạng thái tiêu chí.
- Số minh chứng đã nộp.

Quyền thao tác:

- Xem sinh viên thuộc các Chi đoàn trong Liên chi mình.
- Lọc theo Chi đoàn, lớp, trạng thái, tiêu chí.

### 4.4. Duyệt minh chứng cấp Liên chi

Thông tin chính:

- Sinh viên.
- Chi đoàn.
- Tên minh chứng.
- Loại minh chứng.
- File minh chứng.
- Link xác minh.
- Ý kiến cán bộ Chi đoàn nếu có.
- Nhóm kỹ năng đề xuất/chính thức.
- Tiêu chí đề xuất/chính thức.
- Lịch sử duyệt.

Quyền thao tác:

- Duyệt minh chứng trong phạm vi Liên chi.
- Từ chối.
- Yêu cầu bổ sung.
- Chuyển cấp Đoàn trường nếu cần.
- Xác nhận nhóm kỹ năng và tiêu chí nếu quy trình giao cho cấp Liên chi.

### 4.5. Quản lý hoạt động cấp Liên chi

Thông tin chính:

- Tên hoạt động.
- Đơn vị tổ chức.
- Chi đoàn/lớp được tham gia.
- Thời gian.
- Địa điểm.
- Số lượng đăng ký.
- Số lượng tham gia thực tế.
- Nhóm kỹ năng.
- Tiêu chí liên quan.
- Trạng thái hoạt động.

Quyền thao tác:

- Tạo hoạt động cấp Liên chi nếu được phân quyền.
- Quản lý danh sách đăng ký.
- Theo dõi xác nhận tham gia.

### 4.6. Phân công cán bộ Chi đoàn

Thông tin chính:

- Người được phân công.
- Mã sinh viên/email.
- Chi đoàn được gán.
- Vai trò: cán bộ Chi đoàn.
- Thời gian bắt đầu.
- Thời gian kết thúc nếu có.
- Người phân công.
- Trạng thái hiệu lực.

Quyền thao tác:

- Cán bộ Liên chi chỉ được gán cán bộ Chi đoàn cho các Chi đoàn thuộc Liên chi mình.
- Không được gán cán bộ Liên chi hoặc cán bộ Đoàn trường nếu không có quyền.

### 4.7. Xử lý yêu cầu đề xuất đoàn viên

Thông tin chính:

- Yêu cầu từ Chi đoàn.
- Đoàn viên được đề xuất.
- Loại hồ sơ đề xuất.
- Hồ sơ năng lực.
- Minh chứng liên quan.
- Nhận xét của Chi đoàn.
- Nhận xét của Liên chi/Đoàn khoa.
- Kết quả xử lý.
- Cấp chuyển tiếp.
- Trạng thái yêu cầu.

Quyền thao tác:

- Cán bộ Liên chi/Đoàn khoa kiểm tra, nhận xét và phê duyệt yêu cầu trong phạm vi quản lý.
- Có thể yêu cầu bổ sung, từ chối hoặc chuyển tiếp lên Đoàn trường/Đoàn Học viện.

### 4.8. Báo cáo Liên chi

Thông tin chính:

- Báo cáo theo Chi đoàn.
- Báo cáo theo lớp.
- Số lượng hoạt động.
- Số lượt tham gia.
- Minh chứng theo trạng thái.
- Tỷ lệ đạt/chưa đạt tiêu chí.
- Danh sách sinh viên đạt/chưa đạt tiêu chí.
- Export Excel/PDF nếu cần.

## 5. Trang dành cho Cán bộ Đoàn trường

### 5.1. Dashboard Đoàn trường

Thông tin chính:

- Tổng số Liên chi.
- Tổng số Chi đoàn.
- Tổng số sinh viên.
- Tổng số hoạt động.
- Tổng số minh chứng chờ duyệt.
- Số minh chứng đã duyệt/từ chối.
- Tỷ lệ sinh viên tham gia hoạt động.
- Tỷ lệ đạt tiêu chí Sinh viên 5 tốt.
- Báo cáo nhanh theo Khoa/Liên chi.

### 5.2. Quản lý toàn bộ tổ chức Đoàn

Thông tin chính:

- Khoa/Liên chi.
- Chi đoàn.
- Lớp.
- Cán bộ phụ trách.
- Số lượng sinh viên.
- Trạng thái hoạt động của đơn vị.

Quyền thao tác:

- Xem toàn bộ Liên chi, Chi đoàn, lớp.
- Cập nhật cơ cấu tổ chức nếu được phân quyền.
- Gán cán bộ phụ trách cấp Liên chi hoặc Chi đoàn.

### 5.3. Quản lý sinh viên toàn trường

Thông tin chính:

- Họ tên.
- Mã sinh viên.
- Email.
- Lớp.
- Chi đoàn.
- Liên chi/Khoa.
- Trạng thái đoàn viên.
- Trạng thái tiêu chí.

Quyền thao tác:

- Xem sinh viên toàn trường.
- Lọc theo khoa, liên chi, chi đoàn, lớp, năm học, trạng thái.

### 5.4. Quản lý hoạt động cấp trường

Thông tin chính:

- Tên hoạt động.
- Mã hoạt động.
- Đơn vị tổ chức.
- Phạm vi tham gia: toàn trường, theo khoa, theo chi đoàn.
- Thời gian.
- Địa điểm.
- Số lượng tối đa.
- Số lượng đăng ký.
- Số lượng tham gia thực tế.
- Nhóm kỹ năng.
- Tiêu chí Sinh viên 5 tốt.
- Trạng thái hoạt động.

Quyền thao tác:

- Tạo hoạt động cấp trường.
- Cập nhật hoạt động.
- Đóng/mở đăng ký.
- Theo dõi danh sách đăng ký.
- Xem kết quả điểm danh.

### 5.5. Duyệt minh chứng cấp Đoàn trường

Thông tin chính:

- Sinh viên.
- Mã sinh viên.
- Chi đoàn.
- Liên chi.
- Tên minh chứng.
- Loại minh chứng.
- File minh chứng.
- Link xác minh.
- Lịch sử duyệt cấp dưới.
- Nhóm kỹ năng chính thức.
- Tiêu chí chính thức.
- Ghi chú duyệt.

Quyền thao tác:

- Duyệt minh chứng toàn trường.
- Từ chối.
- Yêu cầu bổ sung.
- Xác nhận nhóm kỹ năng và tiêu chí cuối.
- Xem lịch sử duyệt.

### 5.6. Xác thực hồ sơ chính thức

Thông tin chính:

- Người gửi yêu cầu.
- Loại hồ sơ.
- Hồ sơ cá nhân.
- Tổng quan hồ sơ năng lực.
- 6 nhóm kỹ năng.
- 5 tiêu chí Sinh viên 5 tốt.
- Danh hiệu đã đạt.
- Hoạt động nổi bật.
- Minh chứng đã phê duyệt.
- Ý kiến nhận xét các cấp nếu có.
- File PDF chính thức.
- Chữ ký số/dấu xác thực.
- Mã QR tra cứu.
- Link hồ sơ gốc.
- Trạng thái xác thực.

Quyền thao tác:

- Ban Đoàn trường/Đoàn Học viện kiểm tra cuối và xác thực hồ sơ.
- Có thể phê duyệt, yêu cầu bổ sung hoặc từ chối.
- Sau khi xác thực, hệ thống tạo PDF chính thức, QR và link tra cứu.

### 5.7. Tạo chương trình / sự kiện cấp Học viện

Thông tin chính:

- Tên chương trình/sự kiện.
- Loại chương trình.
- Phạm vi tham gia.
- Form đăng ký.
- Thời gian đăng ký.
- Danh sách đăng ký.
- Chi đoàn của sinh viên đăng ký.
- Cán bộ Chi đoàn phụ trách.
- Trạng thái phân công xử lý.
- Kết quả xác thực cuối.

Quyền thao tác:

- Đoàn trường/Đoàn Học viện tạo chương trình cấp Học viện, cấp Nhà nước hoặc Trung ương Đoàn.
- Hệ thống tự phân dữ liệu đăng ký về đúng Cán bộ Chi đoàn theo Chi đoàn của sinh viên.
- Cán bộ Chi đoàn tiếp tục xác nhận, đề xuất hoặc xử lý hồ sơ theo quy trình.

### 5.8. Xử lý hồ sơ Đảng - Đoàn - Nhà nước

Thông tin chính:

- Hồ sơ sinh viên tự tạo.
- Hồ sơ cán bộ Chi đoàn đề xuất.
- Hồ sơ từ chương trình cấp Học viện.
- Cấp xử lý hiện tại.
- Lịch sử phê duyệt.
- Quyết định/biên bản điện tử nếu có.
- Phụ lục minh chứng nếu có.
- Trạng thái hồ sơ.

Quyền thao tác:

- Theo dõi và xử lý các hồ sơ chính thức phục vụ chương trình Đảng, Đoàn, Nhà nước.
- Hỗ trợ tạo quyết định giới thiệu, biên bản điện tử hoặc phụ lục minh chứng nếu quy trình yêu cầu.

### 5.9. Phân quyền cán bộ Liên chi và Chi đoàn

Thông tin chính:

- Người được gán quyền.
- Mã sinh viên/mã cán bộ/email.
- Vai trò được gán:
  - Cán bộ Liên chi.
  - Cán bộ Chi đoàn.
- Phạm vi:
  - Liên chi cụ thể.
  - Chi đoàn cụ thể.
- Ngày bắt đầu hiệu lực.
- Ngày hết hiệu lực nếu có.
- Người gán.
- Trạng thái hiệu lực.

Quyền thao tác:

- Gán cán bộ Liên chi cho các Liên chi.
- Gán cán bộ Chi đoàn cho các Chi đoàn.
- Thu hồi quyền.
- Xem lịch sử phân quyền.

### 5.10. Quản lý đợt xét và tiêu chí

Thông tin chính:

- Năm học.
- Học kỳ.
- Đợt xét.
- Thời gian mở nộp minh chứng.
- Thời gian đóng nộp minh chứng.
- Thời gian duyệt.
- Bộ tiêu chí áp dụng.
- Trạng thái đợt xét.

Quyền thao tác:

- Tạo đợt xét.
- Cập nhật thời gian.
- Mở/đóng đợt xét.
- Gắn bộ tiêu chí.

### 5.11. Báo cáo toàn trường

Thông tin chính:

- Báo cáo theo Liên chi/Khoa.
- Báo cáo theo Chi đoàn.
- Số hoạt động đã tổ chức.
- Số lượt tham gia.
- Số minh chứng theo trạng thái.
- Tổng hợp tiêu chí.
- Danh sách sinh viên đạt/chưa đạt tiêu chí.
- Export Excel/PDF.

## 6. Trang dành cho Admin hệ thống

### 6.1. Dashboard Admin

Thông tin chính:

- Tổng số tài khoản.
- Tổng số vai trò đang được gán.
- Số tài khoản bị khóa.
- Số cấu hình đang hoạt động.
- Log thao tác gần đây.
- Cảnh báo hệ thống nếu có.

### 6.2. Quản lý tài khoản

Thông tin chính:

- Họ tên.
- Email.
- Mã sinh viên/mã cán bộ.
- Số điện thoại.
- Vai trò hiện tại.
- Trạng thái tài khoản.
- Ngày tạo.
- Lần đăng nhập gần nhất.

Quyền thao tác:

- Tạo tài khoản.
- Cập nhật tài khoản.
- Khóa/mở khóa tài khoản.
- Reset mật khẩu.
- Import danh sách tài khoản nếu cần.

### 6.3. Quản lý vai trò và phân quyền

Thông tin chính:

- Vai trò.
- Danh sách permission của vai trò.
- Người đang giữ vai trò.
- Phạm vi được gán.
- Người gán.
- Ngày gán.
- Trạng thái hiệu lực.

Quyền thao tác:

- Tạo/sửa vai trò nếu hệ thống cho phép.
- Gán quyền cho vai trò.
- Gán vai trò cho người dùng.
- Thu hồi vai trò.
- Xem lịch sử phân quyền.

### 6.4. Quản lý danh mục hệ thống

Thông tin chính:

- Danh mục nhóm kỹ năng.
- Danh mục tiêu chí Sinh viên 5 tốt.
- Danh mục loại minh chứng.
- Danh mục trạng thái.
- Danh mục năm học/học kỳ.

Quyền thao tác:

- Tạo danh mục.
- Cập nhật danh mục.
- Bật/tắt danh mục.
- Không nên xóa cứng danh mục đã có dữ liệu phát sinh.

### 6.5. Quản lý cấu hình hệ thống

Thông tin chính:

- Cấu hình upload file.
- Dung lượng file tối đa.
- Định dạng file được phép.
- Cấu hình email/thông báo nếu có.
- Cấu hình thời gian phiên đăng nhập.

### 6.6. Log và audit

Thông tin chính:

- Người thao tác.
- Hành động.
- Đối tượng bị tác động.
- Dữ liệu trước/sau nếu cần.
- Thời gian thao tác.
- IP hoặc thiết bị nếu có.

Mục đích:

- Truy vết phân quyền.
- Truy vết duyệt minh chứng.
- Truy vết thay đổi tiêu chí và kết quả duyệt.
- Truy vết thay đổi cấu hình quan trọng.

## 7. Ma trận quyền tổng quát

| Chức năng | Sinh viên | Cán bộ Chi đoàn | Cán bộ Liên chi | Cán bộ Đoàn trường | Admin |
| --- | --- | --- | --- | --- | --- |
| Xem hồ sơ cá nhân | Có | Có | Có | Có | Có |
| Sửa hồ sơ cá nhân | Một phần | Một phần | Một phần | Một phần | Có |
| Xem sinh viên | Chỉ bản thân | Trong Chi đoàn | Trong Liên chi | Toàn trường | Toàn hệ thống |
| Tạo hoạt động | Không | Nếu được cấp quyền | Cấp Liên chi | Cấp trường | Có |
| Đăng ký hoạt động | Có | Có nếu cũng là sinh viên | Có nếu cũng là sinh viên | Có nếu cũng là sinh viên | Không bắt buộc |
| Xác nhận tham gia | Không | Trong Chi đoàn | Trong Liên chi | Toàn trường | Có |
| Nộp minh chứng | Có | Có nếu cũng là sinh viên | Có nếu cũng là sinh viên | Có nếu cũng là sinh viên | Không bắt buộc |
| Duyệt minh chứng | Không | Trong Chi đoàn | Trong Liên chi | Toàn trường | Có |
| Gán cán bộ Chi đoàn | Không | Không | Trong Liên chi | Toàn trường | Có |
| Gán cán bộ Liên chi | Không | Không | Không | Toàn trường | Có |
| Xem báo cáo | Cá nhân | Chi đoàn | Liên chi | Toàn trường | Toàn hệ thống |
| Quản lý cấu hình | Không | Không | Không | Một phần | Có |

## 8. Gợi ý thứ tự triển khai giao diện

1. Layout chung, đăng nhập, menu theo vai trò.
2. Trang hồ sơ cá nhân.
3. Trang quản lý tổ chức Đoàn và sinh viên.
4. Trang hoạt động/sự kiện.
5. Trang đăng ký và xác nhận tham gia.
6. Trang minh chứng tự khai báo.
7. Trang duyệt minh chứng theo từng cấp.
8. Trang hồ sơ năng lực và xét tiêu chí.
9. Trang xét tiêu chí/Sinh viên 5 tốt.
10. Trang thông báo.
11. Trang báo cáo.
12. Trang quản trị hệ thống.

## 9. Lưu ý khi code phân quyền cho các trang

- Không chỉ ẩn menu ở frontend; backend vẫn phải kiểm tra quyền ở từng API.
- Mỗi API quan trọng cần kiểm tra cả permission và scope.
- Role quyết định người dùng được làm hành động gì.
- Scope quyết định người dùng được làm trên dữ liệu nào.
- Với dữ liệu sinh viên, scope nên căn theo Chi đoàn, Liên chi hoặc toàn trường.
- Với dữ liệu minh chứng, scope nên căn theo sinh viên nộp minh chứng thuộc đơn vị nào.
- Với dữ liệu hoạt động, scope nên căn theo đơn vị tổ chức và phạm vi hoạt động.
