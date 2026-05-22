# Tree Trang Và Trường Thông Tin Chính Theo Vai Trò

Ghi chú:

- Nhánh `Chung cho mọi tài khoản` là dữ liệu của chính người đang đăng nhập.
- Nhánh `Sinh viên`, `Cán bộ Chi đoàn`, `Cán bộ Liên chi`, `Cán bộ Đoàn trường`, `Admin hệ thống` là chức năng theo vai trò.
- Cán bộ vẫn xem được hồ sơ cá nhân của chính mình ở nhánh chung.
- Cán bộ chỉ xem được hồ sơ người khác thông qua các trang quản lý và bị giới hạn theo phạm vi được phân quyền.

## Tree rút gọn các trang chính

```text
Đoàn Số
├── Chung cho mọi tài khoản
│   ├── Hồ sơ cá nhân
│   ├── Hoạt động của tôi
│   ├── Minh chứng của tôi
│   ├── Hồ sơ năng lực của tôi
│   ├── Kết quả xét tiêu chí của tôi
│   ├── Hồ sơ chính thức của tôi
│   └── Thông báo của tôi
│
├── Sinh viên
│   ├── Dashboard
│   ├── Hồ sơ sinh viên
│   ├── Hồ sơ năng lực trung tâm
│   ├── Bảng theo dõi tiến độ
│   ├── AI tư vấn lộ trình
│   ├── Hoạt động / Sự kiện
│   ├── Nạp & xác nhận hoạt động
│   ├── Minh chứng tự khai báo
│   ├── Hồ sơ năng lực / Lịch sử hoạt động
│   ├── Kết quả xét tiêu chí
│   ├── Hồ sơ chính thức
│   └── Thông báo
│
├── Cán bộ Chi đoàn
│   ├── Dashboard Chi đoàn
│   ├── Quản lý sinh viên Chi đoàn
│   ├── Quản lý sự kiện & hoạt động Chi đoàn
│   ├── Duyệt minh chứng cấp Chi đoàn
│   ├── Xác nhận tham gia hoạt động
│   ├── Theo dõi tiêu chí
│   ├── Bàn giao cán bộ Chi đoàn
│   └── Báo cáo Chi đoàn
│
├── Cán bộ Liên chi
│   ├── Dashboard Liên chi
│   ├── Quản lý Chi đoàn trực thuộc
│   ├── Quản lý sinh viên trong Liên chi
│   ├── Duyệt minh chứng cấp Liên chi
│   ├── Quản lý hoạt động cấp Liên chi
│   ├── Quản lý Sinh viên 5 tốt cấp Liên chi
│   ├── Phân công cán bộ Chi đoàn
│   ├── Bàn giao cán bộ Liên chi / Chi đoàn
│   └── Báo cáo Liên chi
│
├── Cán bộ Đoàn trường
│   ├── Dashboard Đoàn trường
│   ├── Quản lý tổ chức Đoàn
│   ├── Quản lý sinh viên toàn trường
│   ├── Quản lý hoạt động cấp trường
│   ├── Duyệt minh chứng cấp Đoàn trường
│   ├── Phân quyền cán bộ
│   ├── Bàn giao cán bộ Đoàn trường / Liên chi / Chi đoàn
│   ├── Quản lý đợt xét và tiêu chí
│   ├── Quản lý khung tiêu chí
│   ├── Quản lý quy trình phê duyệt
│   ├── Tích hợp hệ thống
│   ├── Phân tích dữ liệu toàn trường
│   └── Báo cáo toàn trường
│
└── Admin hệ thống
    ├── Dashboard Admin
    ├── Quản lý tài khoản
    ├── Quản lý vai trò và phân quyền
    ├── Quản lý bàn giao quyền
    ├── Quản lý danh mục hệ thống
    ├── Quản lý cấu hình hệ thống
    ├── Cấu hình đơn vị triển khai / Trường
    ├── Cấu hình cơ cấu tổ chức
    ├── Cấu hình tiêu chí
    ├── Cấu hình quy trình phê duyệt
    ├── Cấu hình mẫu biểu
    ├── Cấu hình tích hợp
    └── Log và audit
```
---------------------------------------------------------------------------------------------------------

## Tree sidebar thực tế khi người dùng sử dụng

### Sidebar mặc định cho mọi tài khoản

```text
Sidebar
├── Trang chủ
├── Hồ sơ của tôi
├── Hoạt động của tôi
├── Minh chứng của tôi
├── Hồ sơ năng lực của tôi
├── Tiêu chí của tôi
├── Hồ sơ chính thức của tôi
└── Thông báo
```

### Sidebar khi tài khoản là Sinh viên

```text
Sidebar Sinh viên
├── Trang chủ
├── Hồ sơ của tôi
├── Hoạt động
│   ├── Danh sách hoạt động
│   ├── Hoạt động đã đăng ký
│   └── Lịch sử tham gia
├── Minh chứng
│   ├── Nộp minh chứng tự khai báo
│   ├── Minh chứng nháp
│   ├── Minh chứng chờ duyệt
│   └── Minh chứng đã xử lý
├── Hồ sơ năng lực
├── Tiêu chí / Danh hiệu
├── AI tư vấn lộ trình
├── Hồ sơ chính thức
│   ├── Yêu cầu xuất hồ sơ chính thức
│   ├── Hồ sơ học bổng Nhà nước
│   ├── Hồ sơ chương trình lãnh đạo trẻ
│   ├── Hồ sơ Đại hội Đoàn / Hội các cấp
│   ├── Hồ sơ chương trình / diễn đàn thanh niên
│   ├── Hồ sơ khác / tùy chỉnh
│   └── Lịch sử hồ sơ đã xuất
└── Thông báo
```

### Sidebar khi tài khoản là Cán bộ Chi đoàn

```text
Sidebar Cán bộ Chi đoàn
├── Trang chủ
├── Hồ sơ của tôi
├── Công việc Chi đoàn
│   ├── Dashboard Chi đoàn
│   ├── Sinh viên trong Chi đoàn
│   ├── Hoạt động Chi đoàn
│   ├── Xác nhận tham gia
│   ├── Duyệt minh chứng
│   ├── Theo dõi tiêu chí
│   ├── Tạo yêu cầu đề xuất đoàn viên
│   ├── Bàn giao cán bộ
│   └── Báo cáo Chi đoàn
├── Hoạt động của tôi
├── Minh chứng của tôi
├── Hồ sơ năng lực của tôi
├── Tiêu chí của tôi
└── Thông báo
```

### Sidebar khi tài khoản là Cán bộ Liên chi / Đoàn khoa

```text
Sidebar Cán bộ Liên chi
├── Trang chủ
├── Hồ sơ của tôi
├── Công việc Liên chi
│   ├── Dashboard Liên chi
│   ├── Chi đoàn trực thuộc
│   ├── Sinh viên trong Liên chi
│   ├── Hoạt động cấp Liên chi
│   ├── Duyệt minh chứng
│   ├── Xét tiêu chí / Sinh viên 5 tốt
│   ├── Xử lý yêu cầu đề xuất đoàn viên
│   ├── Phân công cán bộ Chi đoàn
│   ├── Bàn giao cán bộ
│   └── Báo cáo Liên chi
├── Hoạt động của tôi
├── Minh chứng của tôi
├── Hồ sơ năng lực của tôi
├── Tiêu chí của tôi
└── Thông báo
```

### Sidebar khi tài khoản là Cán bộ Đoàn trường

```text
Sidebar Cán bộ Đoàn trường
├── Trang chủ
├── Hồ sơ của tôi
├── Công việc Đoàn trường
│   ├── Dashboard Đoàn trường
│   ├── Tổ chức Đoàn
│   ├── Sinh viên toàn trường
│   ├── Hoạt động cấp trường
│   ├── Duyệt minh chứng
│   ├── Xét tiêu chí / Sinh viên 5 tốt
│   ├── Xác thực hồ sơ chính thức
│   ├── Tạo chương trình / sự kiện cấp Học viện
│   ├── Xử lý hồ sơ Đảng - Đoàn - Nhà nước
│   ├── Phân quyền cán bộ
│   ├── Bàn giao cán bộ
│   ├── Đợt xét và tiêu chí
│   ├── Quy trình phê duyệt
│   ├── Tích hợp hệ thống
│   ├── Phân tích dữ liệu
│   └── Báo cáo toàn trường
├── Hoạt động của tôi
├── Minh chứng của tôi
├── Hồ sơ năng lực của tôi
├── Tiêu chí của tôi
└── Thông báo
```

### Sidebar khi tài khoản là Admin hệ thống

```text
Sidebar Admin
├── Trang chủ
├── Hồ sơ của tôi
├── Quản trị hệ thống
│   ├── Dashboard Admin
│   ├── Tài khoản
│   ├── Vai trò và phân quyền
│   ├── Bàn giao quyền
│   ├── Danh mục hệ thống
│   ├── Cấu hình hệ thống
│   ├── Cấu hình trường / đơn vị triển khai
│   ├── Cơ cấu tổ chức
│   ├── Tiêu chí
│   ├── Quy trình phê duyệt
│   ├── Mẫu biểu
│   │   ├── Mẫu hồ sơ chính thức
│   │   ├── Mẫu hồ sơ Đảng - Đoàn - Nhà nước
│   │   ├── Mẫu giấy giới thiệu Đoàn viên ưu tú
│   │   ├── Mẫu hồ sơ học bổng
│   │   └── Mẫu quyết định công nhận
│   ├── Tích hợp
│   └── Log / Audit
└── Thông báo
```

### Sidebar khi một người có nhiều vai trò

Ví dụ một sinh viên đồng thời là cán bộ Chi đoàn thì sidebar thực tế nên gộp như sau:

```text
Sidebar Sinh viên kiêm Cán bộ Chi đoàn
├── Trang chủ
├── Hồ sơ của tôi
├── Hoạt động của tôi
├── Minh chứng của tôi
├── Hồ sơ năng lực của tôi
├── Tiêu chí của tôi
├── Hồ sơ chính thức của tôi
├── Công việc Chi đoàn
│   ├── Dashboard Chi đoàn
│   ├── Sinh viên trong Chi đoàn
│   ├── Hoạt động Chi đoàn
│   ├── Xác nhận tham gia
│   ├── Duyệt minh chứng
│   ├── Theo dõi tiêu chí
│   ├── Bàn giao cán bộ
│   └── Báo cáo Chi đoàn
└── Thông báo
```
----------------------------------------------------------------------------------------------------------------

Nguyên tắc hiển thị sidebar thực tế:

- Nhóm `... của tôi` luôn là dữ liệu cá nhân của người đăng nhập.
- Nhóm `Công việc ...` là phần quản lý theo vai trò và phạm vi được gán.
- Nếu một người có nhiều vai trò, sidebar gộp các nhóm công việc tương ứng.
- Không hiển thị menu mà người dùng không có permission.
- Backend vẫn phải kiểm tra quyền ở API, không chỉ ẩn menu ở frontend.

## Tree chi tiết các trang và trường thông tin

```text
Đoàn Số
├── Chung cho mọi tài khoản
│   ├── Hồ sơ cá nhân
│   │   ├── Ảnh đại diện
│   │   ├── Họ và tên
│   │   ├── Mã sinh viên / mã cán bộ
│   │   ├── Email trường
│   │   ├── Số điện thoại
│   │   ├── Ngày sinh
│   │   ├── Giới tính
│   │   ├── Địa chỉ
│   │   ├── Đơn vị trực thuộc
│   │   ├── Vai trò hiện tại
│   │   └── Trạng thái tài khoản
│   ├── Hoạt động của tôi
│   │   ├── Hoạt động đã đăng ký
│   │   ├── Hoạt động đã tham gia
│   │   ├── Hoạt động chờ xác nhận
│   │   ├── Vai trò tham gia
│   │   └── Trạng thái tham gia
│   ├── Minh chứng của tôi
│   │   ├── Minh chứng đã nộp
│   │   ├── Minh chứng nháp
│   │   ├── Minh chứng chờ duyệt
│   │   ├── Minh chứng đã duyệt
│   │   ├── Minh chứng bị từ chối
│   │   └── Minh chứng cần bổ sung
│   ├── Hồ sơ năng lực của tôi
│   │   ├── Nhóm kỹ năng đã ghi nhận
│   │   ├── Hoạt động đã xác thực
│   │   ├── Minh chứng đã xác thực
│   │   ├── Năm học / học kỳ
│   │   └── Lịch sử ghi nhận
│   ├── Kết quả xét tiêu chí của tôi
│   │   ├── Đợt xét
│   │   ├── Tiêu chí đã đạt
│   │   ├── Tiêu chí chưa đạt
│   │   ├── Tiêu chí chờ duyệt
│   │   ├── Minh chứng liên quan
│   │   └── Ghi chú cán bộ
│   ├── Hồ sơ chính thức của tôi
│   │   ├── CV năng lực PDF
│   │   ├── Hồ sơ Sinh viên 5 tốt PDF
│   │   ├── Hộ chiếu năng lực số
│   │   ├── Link profile công khai
│   │   ├── Trạng thái bật/tắt công khai
│   │   └── Mã QR cá nhân
│   └── Thông báo của tôi
│       ├── Tiêu đề
│       ├── Nội dung
│       ├── Loại thông báo
│       ├── Thời gian gửi
│       ├── Trạng thái đọc
│       └── Link liên quan
│
├── Sinh viên
│   ├── Dashboard
│   │   ├── Họ tên
│   │   ├── Mã sinh viên
│   │   ├── Lớp
│   │   ├── Chi đoàn
│   │   ├── Khoa / Liên chi
│   │   ├── Trạng thái đoàn viên
│   │   ├── Tổng hoạt động đã tham gia
│   │   ├── Tổng minh chứng đã nộp
│   │   ├── Minh chứng chờ duyệt
│   │   ├── Minh chứng đã duyệt
│   │   └── Thông báo mới
│   ├── Hồ sơ sinh viên
│   │   ├── Ảnh đại diện
│   │   ├── Họ và tên
│   │   ├── Mã sinh viên
│   │   ├── Email trường
│   │   ├── Số điện thoại
│   │   ├── Ngày sinh
│   │   ├── Giới tính
│   │   ├── Địa chỉ
│   │   ├── Lớp
│   │   ├── Chi đoàn
│   │   ├── Khoa / Liên chi
│   │   ├── Niên khóa
│   │   ├── Trạng thái đoàn viên
│   │   ├── Ngày vào Đoàn
│   │   └── Chức vụ trong Chi đoàn
│   ├── Hồ sơ năng lực trung tâm
│   │   ├── 6 nhóm kỹ năng
│   │   ├── Mức độ từng nhóm
│   │   ├── Tiến độ phần trăm
│   │   ├── Danh sách hoạt động theo nhóm
│   │   ├── 5 tiêu chí Sinh viên 5 tốt
│   │   ├── Mức độ đạt từng tiêu chí
│   │   ├── Biểu đồ Radar 6 nhóm kỹ năng
│   │   └── Biểu đồ tiến độ Sinh viên 5 tốt
│   ├── Bảng theo dõi tiến độ
│   │   ├── Biểu đồ Radar
│   │   ├── Biểu đồ cột theo kỳ học
│   │   ├── Minh chứng theo học kỳ
│   │   ├── Minh chứng theo năm học
│   │   ├── Dự báo khả năng đạt Sinh viên 5 tốt
│   │   ├── Lịch sử hoạt động
│   │   ├── Bộ lọc nhóm kỹ năng
│   │   └── Bộ lọc tiêu chí Sinh viên 5 tốt
│   ├── AI tư vấn lộ trình
│   │   ├── Câu hỏi của sinh viên
│   │   ├── Mục tiêu cá nhân
│   │   ├── Mục tiêu nghề nghiệp
│   │   ├── Mục tiêu Sinh viên 5 tốt
│   │   ├── Nhóm kỹ năng còn thiếu
│   │   ├── Tiêu chí còn thiếu
│   │   ├── Hoạt động được gợi ý
│   │   └── Lộ trình đề xuất
│   ├── Hoạt động / Sự kiện
│   │   ├── Tên hoạt động
│   │   ├── Mã hoạt động
│   │   ├── Đơn vị tổ chức
│   │   ├── Thời gian bắt đầu
│   │   ├── Thời gian kết thúc
│   │   ├── Địa điểm
│   │   ├── Hình thức tổ chức
│   │   ├── Số lượng tối đa
│   │   ├── Số lượng đã đăng ký
│   │   ├── Hạn đăng ký
│   │   ├── Nhóm kỹ năng
│   │   ├── Tiêu chí Sinh viên 5 tốt
│   │   └── Trạng thái đăng ký
│   ├── Nạp & xác nhận hoạt động
│   │   ├── Mã QR check-in
│   │   ├── Hoạt động check-in
│   │   ├── Thời gian check-in
│   │   ├── File minh chứng
│   │   ├── Tên hoạt động
│   │   ├── Thời gian hoạt động
│   │   ├── Địa điểm
│   │   ├── Nhóm kỹ năng
│   │   ├── Tiêu chí Sinh viên 5 tốt
│   │   ├── Vai trò tham gia
│   │   ├── Đánh giá chéo từ bạn bè
│   │   └── Trạng thái xác nhận
│   ├── Minh chứng tự khai báo
│   │   ├── Tên hoạt động / chứng chỉ / thành tích
│   │   ├── Đơn vị tổ chức
│   │   ├── Thời gian bắt đầu
│   │   ├── Thời gian kết thúc
│   │   ├── Địa điểm / hình thức
│   │   ├── Loại minh chứng
│   │   ├── Nhóm kỹ năng đề xuất
│   │   ├── Tiêu chí Sinh viên 5 tốt đề xuất
│   │   ├── Vai trò / mức độ tham gia
│   │   ├── File minh chứng
│   │   ├── Link xác minh
│   │   ├── Ghi chú
│   │   ├── Trạng thái duyệt
│   │   ├── Lý do từ chối / yêu cầu bổ sung
│   │   └── Kết quả duyệt
│   ├── Hồ sơ năng lực / Lịch sử hoạt động
│   │   ├── Hoạt động đã tham gia
│   │   ├── Minh chứng đã duyệt
│   │   ├── Nguồn ghi nhận
│   │   ├── Nhóm kỹ năng đạt được
│   │   ├── Tiêu chí liên quan
│   │   ├── Năm học / học kỳ
│   │   └── Ngày ghi nhận
│   ├── Kết quả xét tiêu chí
│   │   ├── Đợt xét
│   │   ├── Năm học
│   │   ├── Tiêu chí
│   │   ├── Minh chứng / hoạt động liên quan
│   │   ├── Trạng thái
│   │   └── Ghi chú cán bộ
│   ├── Hồ sơ chính thức
│   │   ├── Loại hồ sơ yêu cầu
│   │   ├── Hồ sơ học bổng Nhà nước
│   │   ├── Hồ sơ chương trình lãnh đạo trẻ
│   │   ├── Hồ sơ Đại hội Đoàn / Hội các cấp
│   │   ├── Hồ sơ chương trình / diễn đàn thanh niên
│   │   ├── Dữ liệu được chọn đưa vào hồ sơ
│   │   ├── Trạng thái yêu cầu xác thực
│   │   ├── File PDF chính thức
│   │   ├── Link tra cứu
│   │   ├── Mã QR xác minh
│   │   └── Lịch sử hồ sơ đã xuất
│   └── Thông báo
│       ├── Tiêu đề
│       ├── Nội dung
│       ├── Loại thông báo
│       ├── Thời gian gửi
│       ├── Trạng thái đọc
│       └── Link liên quan
│
├── Cán bộ Chi đoàn
│   ├── Dashboard Chi đoàn
│   │   ├── Tên Chi đoàn
│   │   ├── Lớp / khoa trực thuộc
│   │   ├── Số lượng sinh viên
│   │   ├── Số sinh viên đã tham gia hoạt động
│   │   ├── Minh chứng chờ duyệt
│   │   ├── Minh chứng đã duyệt / từ chối
│   │   ├── Sinh viên đạt / chưa đạt tiêu chí
│   │   ├── Tỷ lệ đạt Sinh viên 5 tốt
│   │   ├── Tiến độ theo 6 nhóm kỹ năng
│   │   ├── Top 10 đoàn viên xuất sắc
│   │   ├── Cảnh báo nguy cơ không đủ điều kiện
│   │   ├── Hoạt động sắp diễn ra
│   │   └── Thông báo cần xử lý
│   ├── Quản lý sinh viên Chi đoàn
│   │   ├── Họ tên
│   │   ├── Mã sinh viên
│   │   ├── Email
│   │   ├── Số điện thoại
│   │   ├── Lớp
│   │   ├── Chi đoàn
│   │   ├── Trạng thái đoàn viên
│   │   ├── Chức vụ
│   │   ├── Tổng hoạt động đã tham gia
│   │   ├── Tổng minh chứng đã nộp
│   │   ├── Trạng thái xét tiêu chí
│   │   └── Bộ lọc điều kiện / nhóm mạnh / nhóm yếu
│   ├── Quản lý sự kiện & hoạt động Chi đoàn
│   │   ├── Tên sự kiện
│   │   ├── Nhóm kỹ năng được gán
│   │   ├── Tiêu chí Sinh viên 5 tốt được gán
│   │   ├── Thời gian
│   │   ├── Địa điểm
│   │   ├── Danh sách đăng ký
│   │   ├── QR code check-in
│   │   ├── Trạng thái sự kiện
│   │   └── Kết quả xác nhận tham gia
│   ├── Duyệt minh chứng cấp Chi đoàn
│   │   ├── Sinh viên nộp
│   │   ├── Mã sinh viên
│   │   ├── Tên minh chứng
│   │   ├── Loại minh chứng
│   │   ├── Thời gian diễn ra
│   │   ├── File minh chứng
│   │   ├── Link xác minh
│   │   ├── Nhóm kỹ năng đề xuất
│   │   ├── Tiêu chí đề xuất
│   │   ├── Trạng thái duyệt
│   │   ├── Ghi chú sinh viên
│   │   └── Ghi chú cán bộ
│   ├── Xác nhận tham gia hoạt động
│   │   ├── Tên hoạt động
│   │   ├── Thời gian
│   │   ├── Danh sách sinh viên đăng ký
│   │   ├── Trạng thái tham gia
│   │   └── Ghi chú điểm danh
│   ├── Theo dõi tiêu chí
│   │   ├── Sinh viên
│   │   ├── Tiêu chí đã đạt
│   │   ├── Tiêu chí chưa đạt
│   │   ├── Minh chứng / hoạt động dùng để xét
│   │   └── Trạng thái xác nhận
│   ├── Tạo yêu cầu đề xuất đoàn viên
│   │   ├── Loại hồ sơ đề xuất
│   │   ├── Đoàn viên được đề xuất
│   │   ├── Hồ sơ cá nhân
│   │   ├── Tổng quan hồ sơ năng lực
│   │   ├── Minh chứng liên quan
│   │   ├── Danh hiệu đã đạt
│   │   ├── Nhận xét của Chi đoàn
│   │   ├── Cấp xử lý tiếp theo
│   │   └── Trạng thái yêu cầu
│   ├── Bàn giao cán bộ Chi đoàn
│   │   ├── Cán bộ hiện tại
│   │   ├── Mã sinh viên / email cán bộ hiện tại
│   │   ├── Cán bộ nhận bàn giao
│   │   ├── Mã sinh viên / email cán bộ nhận bàn giao
│   │   ├── Chi đoàn bàn giao
│   │   ├── Vai trò bàn giao
│   │   ├── Ngày bắt đầu hiệu lực
│   │   ├── Ngày kết thúc quyền cũ
│   │   ├── Người xác nhận bàn giao
│   │   ├── Lý do bàn giao
│   │   └── Trạng thái bàn giao
│   └── Báo cáo Chi đoàn
│       ├── Số lượng sinh viên theo trạng thái
│       ├── Số hoạt động đã tham gia
│       ├── Minh chứng theo trạng thái
│       ├── Sinh viên đạt / chưa đạt tiêu chí
│       └── Export Excel
│
├── Cán bộ Liên chi
│   ├── Dashboard Liên chi
│   │   ├── Tên Liên chi / Đoàn khoa
│   │   ├── Tổng số Chi đoàn
│   │   ├── Tổng số sinh viên
│   │   ├── Minh chứng chờ duyệt cấp Liên chi
│   │   ├── Hoạt động cấp Liên chi
│   │   ├── Tỷ lệ tham gia hoạt động
│   │   ├── Tỷ lệ đạt tiêu chí
│   │   └── Báo cáo nhanh theo Chi đoàn
│   ├── Quản lý Chi đoàn trực thuộc
│   │   ├── Tên Chi đoàn
│   │   ├── Lớp
│   │   ├── Số lượng sinh viên
│   │   ├── Cán bộ Chi đoàn phụ trách
│   │   ├── Minh chứng chờ duyệt
│   │   └── Sinh viên đạt / chưa đạt tiêu chí
│   ├── Quản lý sinh viên trong Liên chi
│   │   ├── Họ tên
│   │   ├── Mã sinh viên
│   │   ├── Lớp
│   │   ├── Chi đoàn
│   │   ├── Trạng thái đoàn viên
│   │   ├── Trạng thái tiêu chí
│   │   └── Số minh chứng đã nộp
│   ├── Duyệt minh chứng cấp Liên chi
│   │   ├── Sinh viên
│   │   ├── Chi đoàn
│   │   ├── Tên minh chứng
│   │   ├── Loại minh chứng
│   │   ├── File minh chứng
│   │   ├── Link xác minh
│   │   ├── Ý kiến cán bộ Chi đoàn
│   │   ├── Nhóm kỹ năng đề xuất / chính thức
│   │   ├── Tiêu chí đề xuất / chính thức
│   │   └── Lịch sử duyệt
│   ├── Quản lý hoạt động cấp Liên chi
│   │   ├── Tên hoạt động
│   │   ├── Đơn vị tổ chức
│   │   ├── Chi đoàn / lớp được tham gia
│   │   ├── Thời gian
│   │   ├── Địa điểm
│   │   ├── Số lượng đăng ký
│   │   ├── Số lượng tham gia thực tế
│   │   ├── Nhóm kỹ năng
│   │   ├── Tiêu chí liên quan
│   │   └── Trạng thái hoạt động
│   ├── Quản lý Sinh viên 5 tốt cấp Liên chi
│   │   ├── Đợt xét
│   │   ├── Sinh viên
│   │   ├── Chi đoàn
│   │   ├── Tiêu chí đạt / chưa đạt
│   │   ├── Minh chứng liên quan
│   │   ├── Ý kiến Chi đoàn
│   │   ├── Kết quả xét cấp Liên chi
│   │   └── Ghi chú xét duyệt
│   ├── Xử lý yêu cầu đề xuất đoàn viên
│   │   ├── Yêu cầu từ Chi đoàn
│   │   ├── Đoàn viên được đề xuất
│   │   ├── Loại hồ sơ đề xuất
│   │   ├── Hồ sơ năng lực
│   │   ├── Minh chứng liên quan
│   │   ├── Nhận xét của Chi đoàn
│   │   ├── Nhận xét của Liên chi / Đoàn khoa
│   │   ├── Kết quả xử lý
│   │   ├── Cấp chuyển tiếp
│   │   └── Trạng thái yêu cầu
│   ├── Phân công cán bộ Chi đoàn
│   │   ├── Người được phân công
│   │   ├── Mã sinh viên / email
│   │   ├── Chi đoàn được gán
│   │   ├── Vai trò
│   │   ├── Thời gian bắt đầu
│   │   ├── Thời gian kết thúc
│   │   ├── Người phân công
│   │   └── Trạng thái hiệu lực
│   ├── Bàn giao cán bộ Liên chi / Chi đoàn
│   │   ├── Cán bộ bàn giao
│   │   ├── Cán bộ nhận bàn giao
│   │   ├── Vai trò bàn giao
│   │   ├── Phạm vi bàn giao
│   │   ├── Liên chi / Chi đoàn liên quan
│   │   ├── Ngày bắt đầu hiệu lực
│   │   ├── Ngày thu hồi quyền cũ
│   │   ├── Người tạo yêu cầu
│   │   ├── Người duyệt yêu cầu
│   │   ├── Lý do bàn giao
│   │   └── Trạng thái bàn giao
│   └── Báo cáo Liên chi
│       ├── Báo cáo theo Chi đoàn
│       ├── Báo cáo theo lớp
│       ├── Số lượng hoạt động
│       ├── Số lượt tham gia
│       ├── Minh chứng theo trạng thái
│       ├── Sinh viên đạt / chưa đạt tiêu chí
│       └── Export Excel / PDF
│
├── Cán bộ Đoàn trường
│   ├── Dashboard Đoàn trường
│   │   ├── Tổng số Liên chi
│   │   ├── Tổng số Chi đoàn
│   │   ├── Tổng số sinh viên
│   │   ├── Tổng số hoạt động
│   │   ├── Minh chứng chờ duyệt
│   │   ├── Minh chứng đã duyệt / từ chối
│   │   ├── Tỷ lệ tham gia hoạt động
│   │   ├── Tỷ lệ đạt Sinh viên 5 tốt
│   │   └── Báo cáo nhanh theo Liên chi
│   ├── Quản lý tổ chức Đoàn
│   │   ├── Khoa / Liên chi
│   │   ├── Chi đoàn
│   │   ├── Lớp
│   │   ├── Cán bộ phụ trách
│   │   ├── Số lượng sinh viên
│   │   └── Trạng thái đơn vị
│   ├── Quản lý sinh viên toàn trường
│   │   ├── Họ tên
│   │   ├── Mã sinh viên
│   │   ├── Email
│   │   ├── Lớp
│   │   ├── Chi đoàn
│   │   ├── Liên chi / khoa
│   │   ├── Trạng thái đoàn viên
│   │   └── Trạng thái tiêu chí
│   ├── Quản lý hoạt động cấp trường
│   │   ├── Tên hoạt động
│   │   ├── Mã hoạt động
│   │   ├── Đơn vị tổ chức
│   │   ├── Phạm vi tham gia
│   │   ├── Thời gian
│   │   ├── Địa điểm
│   │   ├── Số lượng tối đa
│   │   ├── Số lượng đăng ký
│   │   ├── Số lượng tham gia thực tế
│   │   ├── Nhóm kỹ năng
│   │   ├── Tiêu chí Sinh viên 5 tốt
│   │   └── Trạng thái hoạt động
│   ├── Duyệt minh chứng cấp Đoàn trường
│   │   ├── Sinh viên
│   │   ├── Mã sinh viên
│   │   ├── Chi đoàn
│   │   ├── Liên chi
│   │   ├── Tên minh chứng
│   │   ├── Loại minh chứng
│   │   ├── File minh chứng
│   │   ├── Link xác minh
│   │   ├── Lịch sử duyệt cấp dưới
│   │   ├── Nhóm kỹ năng chính thức
│   │   ├── Tiêu chí chính thức
│   │   └── Ghi chú duyệt
│   ├── Xác thực hồ sơ chính thức
│   │   ├── Người gửi yêu cầu
│   │   ├── Loại hồ sơ
│   │   ├── Hồ sơ cá nhân
│   │   ├── Tổng quan hồ sơ năng lực
│   │   ├── 6 nhóm kỹ năng
│   │   ├── 5 tiêu chí Sinh viên 5 tốt
│   │   ├── Danh hiệu đã đạt
│   │   ├── Hoạt động nổi bật
│   │   ├── Minh chứng đã phê duyệt
│   │   ├── Ý kiến nhận xét các cấp
│   │   ├── File PDF chính thức
│   │   ├── Chữ ký số / dấu xác thực
│   │   ├── Mã QR tra cứu
│   │   ├── Link hồ sơ gốc
│   │   └── Trạng thái xác thực
│   ├── Tạo chương trình / sự kiện cấp Học viện
│   │   ├── Tên chương trình / sự kiện
│   │   ├── Loại chương trình
│   │   ├── Phạm vi tham gia
│   │   ├── Form đăng ký
│   │   ├── Thời gian đăng ký
│   │   ├── Danh sách đăng ký
│   │   ├── Chi đoàn của sinh viên đăng ký
│   │   ├── Cán bộ Chi đoàn phụ trách
│   │   ├── Trạng thái phân công xử lý
│   │   └── Kết quả xác thực cuối
│   ├── Xử lý hồ sơ Đảng - Đoàn - Nhà nước
│   │   ├── Hồ sơ sinh viên tự tạo
│   │   ├── Hồ sơ cán bộ Chi đoàn đề xuất
│   │   ├── Hồ sơ từ chương trình cấp Học viện
│   │   ├── Cấp xử lý hiện tại
│   │   ├── Lịch sử phê duyệt
│   │   ├── Quyết định / biên bản điện tử
│   │   ├── Phụ lục minh chứng
│   │   └── Trạng thái hồ sơ
│   ├── Phân quyền cán bộ
│   │   ├── Người được gán quyền
│   │   ├── Mã sinh viên / mã cán bộ / email
│   │   ├── Vai trò được gán
│   │   ├── Phạm vi
│   │   ├── Ngày bắt đầu hiệu lực
│   │   ├── Ngày hết hiệu lực
│   │   ├── Người gán
│   │   └── Trạng thái hiệu lực
│   ├── Bàn giao cán bộ Đoàn trường / Liên chi / Chi đoàn
│   │   ├── Cán bộ bàn giao
│   │   ├── Mã sinh viên / mã cán bộ / email người bàn giao
│   │   ├── Cán bộ nhận bàn giao
│   │   ├── Mã sinh viên / mã cán bộ / email người nhận
│   │   ├── Vai trò bàn giao
│   │   ├── Phạm vi bàn giao
│   │   ├── Đơn vị liên quan
│   │   ├── Quyền cần chuyển
│   │   ├── Ngày bắt đầu hiệu lực
│   │   ├── Ngày thu hồi quyền cũ
│   │   ├── Người tạo yêu cầu
│   │   ├── Người phê duyệt
│   │   ├── Lý do bàn giao
│   │   ├── Ghi chú
│   │   └── Trạng thái bàn giao
│   ├── Quản lý đợt xét và tiêu chí
│   │   ├── Năm học
│   │   ├── Học kỳ
│   │   ├── Đợt xét
│   │   ├── Thời gian mở nộp minh chứng
│   │   ├── Thời gian đóng nộp minh chứng
│   │   ├── Thời gian duyệt
│   │   ├── Bộ tiêu chí áp dụng
│   │   └── Trạng thái đợt xét
│   ├── Quản lý khung tiêu chí
│   │   ├── 6 nhóm kỹ năng
│   │   ├── Tiêu chí con từng nhóm
│   │   ├── 5 tiêu chí Sinh viên 5 tốt
│   │   ├── Điều kiện đạt từng tiêu chí
│   │   ├── Hệ số vai trò tham gia
│   │   └── Điều kiện xét danh hiệu
│   ├── Quản lý quy trình phê duyệt
│   │   ├── Loại quy trình
│   │   ├── Cấp duyệt thứ nhất
│   │   ├── Cấp duyệt thứ hai
│   │   ├── Cấp xác nhận cuối
│   │   ├── Điều kiện chuyển cấp
│   │   ├── Loại minh chứng áp dụng
│   │   └── Trạng thái quy trình
│   ├── Tích hợp hệ thống
│   │   ├── Đồng bộ danh sách sinh viên
│   │   ├── Đồng bộ GPA
│   │   ├── Xuất dữ liệu sang CT&CTSV
│   │   ├── Đăng nhập SSO
│   │   ├── Zalo OA
│   │   ├── Email trường
│   │   ├── Cổng dịch vụ sinh viên
│   │   └── Trạng thái tích hợp
│   ├── Phân tích dữ liệu toàn trường
│   │   ├── Xu hướng kỹ năng toàn trường
│   │   ├── Tỷ lệ Sinh viên 5 tốt theo khoa
│   │   ├── Tỷ lệ Sinh viên 5 tốt theo năm
│   │   ├── Tỷ lệ tham gia hoạt động
│   │   ├── Nhóm kỹ năng mạnh / yếu
│   │   ├── Dự báo nhu cầu đào tạo kỹ năng
│   │   └── Dự báo hoạt động Đoàn năm sau
│   └── Báo cáo toàn trường
│       ├── Báo cáo theo Liên chi / khoa
│       ├── Báo cáo theo Chi đoàn
│       ├── Số hoạt động đã tổ chức
│       ├── Số lượt tham gia
│       ├── Minh chứng theo trạng thái
│       ├── Sinh viên đạt / chưa đạt tiêu chí
│       └── Export Excel / PDF
│
└── Admin hệ thống
    ├── Dashboard Admin
    │   ├── Tổng số tài khoản
    │   ├── Tổng số vai trò đang được gán
    │   ├── Số tài khoản bị khóa
    │   ├── Số cấu hình đang hoạt động
    │   ├── Log thao tác gần đây
    │   └── Cảnh báo hệ thống
    ├── Quản lý tài khoản
    │   ├── Họ tên
    │   ├── Email
    │   ├── Mã sinh viên / mã cán bộ
    │   ├── Số điện thoại
    │   ├── Vai trò hiện tại
    │   ├── Trạng thái tài khoản
    │   ├── Ngày tạo
    │   └── Lần đăng nhập gần nhất
    ├── Quản lý vai trò và phân quyền
    │   ├── Vai trò
    │   ├── Danh sách permission
    │   ├── Người đang giữ vai trò
    │   ├── Phạm vi được gán
    │   ├── Người gán
    │   ├── Ngày gán
    │   └── Trạng thái hiệu lực
    ├── Quản lý bàn giao quyền
    │   ├── Người bàn giao
    │   ├── Người nhận bàn giao
    │   ├── Vai trò bàn giao
    │   ├── Phạm vi bàn giao
    │   ├── Đơn vị liên quan
    │   ├── Quyền cũ được thu hồi
    │   ├── Quyền mới được gán
    │   ├── Người tạo yêu cầu
    │   ├── Người phê duyệt
    │   ├── Thời gian hiệu lực
    │   ├── Lý do bàn giao
    │   └── Trạng thái bàn giao
    ├── Quản lý danh mục hệ thống
    │   ├── Nhóm kỹ năng
    │   ├── Tiêu chí Sinh viên 5 tốt
    │   ├── Loại minh chứng
    │   ├── Trạng thái
    │   ├── Năm học
    │   └── Học kỳ
    ├── Quản lý cấu hình hệ thống
    │   ├── Cấu hình upload file
    │   ├── Dung lượng file tối đa
    │   ├── Định dạng file được phép
    │   ├── Cấu hình email / thông báo
    │   └── Cấu hình phiên đăng nhập
    ├── Cấu hình đơn vị triển khai / Trường
    │   ├── Tên trường
    │   ├── Logo
    │   ├── Tên viết tắt
    │   ├── Địa chỉ
    │   ├── Email liên hệ
    │   ├── Website
    │   ├── Màu nhận diện
    │   ├── Tên miền
    │   ├── Tài khoản quản trị ban đầu
    │   └── Tên đơn vị quản lý
    ├── Cấu hình cơ cấu tổ chức
    │   ├── Khoa
    │   ├── Viện
    │   ├── Bộ môn
    │   ├── Lớp
    │   ├── Chi đoàn
    │   ├── Liên chi đoàn
    │   ├── Đoàn khoa
    │   ├── Cơ sở đào tạo
    │   └── Khóa học
    ├── Cấu hình tiêu chí
    │   ├── Bộ tiêu chí mặc định
    │   ├── Bộ tiêu chí tùy chỉnh
    │   ├── 6 nhóm kỹ năng
    │   ├── 5 tiêu chí Sinh viên 5 tốt
    │   ├── Hệ số vai trò
    │   ├── Điều kiện xét danh hiệu
    │   └── Loại minh chứng được chấp nhận
    ├── Cấu hình quy trình phê duyệt
    │   ├── Quy trình minh chứng thường
    │   ├── Quy trình minh chứng quan trọng
    │   ├── Quy trình hồ sơ chính thức
    │   ├── Cấp duyệt Chi đoàn
    │   ├── Cấp duyệt Liên chi / Đoàn khoa
    │   ├── Cấp xác nhận Đoàn trường
    │   └── Điều kiện chuyển cấp
    ├── Cấu hình mẫu biểu
    │   ├── Mẫu hồ sơ PDF
    │   ├── Mẫu danh sách Excel
    │   ├── Mẫu biên bản xét
    │   ├── Mẫu giấy xác nhận hoạt động
    │   ├── Mẫu quyết định công nhận
    │   └── Mẫu báo cáo tổng kết
    ├── Cấu hình tích hợp
    │   ├── Đồng bộ danh sách sinh viên
    │   ├── Đồng bộ GPA
    │   ├── Xuất dữ liệu sang CT&CTSV
    │   ├── Đăng nhập SSO
    │   ├── Zalo OA
    │   ├── Email trường
    │   └── Cổng dịch vụ sinh viên
    └── Log và audit
        ├── Người thao tác
        ├── Hành động
        ├── Đối tượng bị tác động
        ├── Dữ liệu trước / sau
        ├── Thời gian thao tác
        └── IP / thiết bị
```
