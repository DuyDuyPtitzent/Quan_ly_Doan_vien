# Cây Frontend Và Giải Thích Theo Tầng

## 1. Mục Đích

Tài liệu này mô tả cấu trúc frontend cho hệ thống Đoàn số. Mục tiêu là để:

- Dễ đọc cấu trúc dự án.
- Dễ sửa từng phần mà không làm vỡ toàn bộ giao diện.
- Dễ thêm trang, thêm vai trò, thêm module nghiệp vụ.
- Dễ thay backend, API, cách xác thực hoặc thư viện UI mà không phải đập dự án xây lại.
- Không để màn hình giao diện phụ thuộc trực tiếp vào database hay cấu trúc bảng.

Nguyên tắc quan trọng:

- Frontend không gọi database trực tiếp.
- Frontend chỉ làm việc qua API client, DTO, type và adapter.
- Trang chỉ điều phối giao diện, không nhét toàn bộ logic nghiệp vụ vào component.
- Quyền hiển thị menu, nút bấm, trang và thao tác phải đi qua module phân quyền.
- Mỗi module nghiệp vụ tách riêng để sửa `sinh-vien` không ảnh hưởng `su-kien`, sửa `minh-chung` không ảnh hưởng `phan-quyen`.

## 2. Ý Nghĩa Từng Tầng

### `app`

Tầng khởi động ứng dụng frontend.

Tầng này phụ trách:

- khai báo router
- khai báo layout tổng
- gắn provider toàn cục
- xử lý bảo vệ route
- cấu hình lỗi chung
- cấu hình theme chung

Không nên viết logic nghiệp vụ chi tiết ở tầng này.

### `shared`

Tầng dùng chung cho toàn frontend.

Tầng này chứa:

- component dùng lại nhiều nơi
- hook dùng chung
- helper xử lý ngày, tiền, file, phân trang
- kiểu dữ liệu chung
- hằng số chung
- rule kiểm tra quyền ở phía giao diện

Không đặt logic riêng của một module nghiệp vụ vào `shared`.

### `features`

Tầng chứa các module nghiệp vụ theo chức năng.

Ví dụ:

- `xac-thuc`
- `sinh-vien`
- `su-kien`
- `minh-chung`
- `phan-quyen`
- `bao-cao`

Mỗi feature tự quản lý:

- trang con
- component riêng
- API riêng
- hook riêng
- type riêng
- form riêng
- mapper riêng nếu dữ liệu API cần chuyển đổi trước khi hiển thị

### `entities`

Tầng chứa mô hình dữ liệu phía frontend.

Tầng này không phải database model. Đây là kiểu dữ liệu dùng cho giao diện, ví dụ:

- `NguoiDung`
- `SinhVien`
- `SuKien`
- `MinhChung`
- `VaiTro`
- `Quyen`
- `PhamVi`

Nếu backend đổi tên trường hoặc đổi database, frontend chỉ cần sửa adapter/API mapper, không sửa lan sang toàn bộ component.

### `services`

Tầng gọi API và tích hợp kỹ thuật.

Tầng này phụ trách:

- cấu hình HTTP client
- gắn token
- refresh token
- xử lý lỗi API
- upload file
- tải file
- websocket nếu có

Không gọi API trực tiếp trong component. Component phải gọi qua hook hoặc service của feature.

### `routes`

Tầng khai báo đường dẫn trang.

Tầng này phụ trách:

- route công khai
- route cần đăng nhập
- route theo vai trò
- route theo quyền
- route fallback lỗi 404/403/500

Khi thêm trang mới, phải đăng ký ở đây hoặc trong route config của feature.

### `layouts`

Tầng bố cục màn hình.

Tầng này phụ trách:

- layout đăng nhập
- layout đoàn viên
- layout cán bộ
- layout quản trị
- sidebar
- header
- breadcrumb

Không viết logic nghiệp vụ nặng trong layout. Layout chỉ hiển thị khung và điều hướng.

### `pages`

Tầng ghép màn hình hoàn chỉnh.

Tầng này phụ trách:

- lấy dữ liệu từ hook
- gọi component của feature
- xử lý trạng thái loading/error/empty
- điều hướng người dùng

Không nên viết API call trực tiếp trong page.

## 3. Cây Frontend

```text
frontend/                                             # Toàn bộ frontend của hệ thống
├── public/                                           # Tài nguyên tĩnh không cần build
│   ├── favicon.ico                                   # Icon trình duyệt
│   ├── logo-ptit.png                                 # Logo Học viện
│   ├── logo-doan.png                                 # Logo Đoàn Thanh niên
│   └── images/                                       # Ảnh tĩnh dùng chung
│       ├── empty-state.png                           # Ảnh trạng thái không có dữ liệu
│       └── default-avatar.png                        # Ảnh đại diện mặc định
│
├── src/                                              # Mã nguồn frontend chính
│   ├── main.tsx                                      # Điểm khởi động React
│   ├── App.tsx                                       # Component gốc của ứng dụng
│   ├── vite-env.d.ts                                 # Kiểu môi trường của Vite
│   │
│   ├── app/                                          # Tầng khởi tạo ứng dụng
│   │   ├── providers/                                # Provider toàn cục
│   │   │   ├── app-provider.tsx                      # Gom toàn bộ provider chính
│   │   │   ├── query-provider.tsx                    # Cấu hình React Query hoặc thư viện gọi dữ liệu
│   │   │   ├── auth-provider.tsx                     # Lưu trạng thái đăng nhập toàn cục
│   │   │   ├── theme-provider.tsx                    # Cấu hình giao diện sáng/tối, màu hệ thống
│   │   │   └── permission-provider.tsx               # Cung cấp quyền hiện tại cho toàn ứng dụng
│   │   ├── router/                                   # Khai báo router tổng
│   │   │   ├── app-router.tsx                        # Router chính của hệ thống
│   │   │   ├── protected-route.tsx                   # Chặn route nếu chưa đăng nhập
│   │   │   ├── permission-route.tsx                  # Chặn route nếu thiếu quyền
│   │   │   └── route-path.ts                         # Hằng số đường dẫn dùng chung
│   │   ├── config/                                   # Cấu hình frontend theo môi trường
│   │   │   ├── app.config.ts                         # Tên app, phiên bản, thông tin hiển thị
│   │   │   ├── api.config.ts                         # Base URL API, timeout
│   │   │   ├── auth.config.ts                        # Cấu hình token, storage key
│   │   │   └── feature-flag.config.ts                # Bật/tắt tính năng theo môi trường
│   │   └── error-boundary/                           # Bắt lỗi giao diện
│   │       ├── app-error-boundary.tsx                # Bắt lỗi React toàn cục
│   │       └── error-page.tsx                        # Trang lỗi chung
│   │
│   ├── services/                                     # Tầng kỹ thuật gọi API và tích hợp
│   │   ├── http/                                     # HTTP client
│   │   │   ├── http-client.ts                        # Tạo instance gọi API
│   │   │   ├── http-error.ts                         # Chuẩn hóa lỗi API
│   │   │   ├── request-interceptor.ts                # Gắn token, request id
│   │   │   ├── response-interceptor.ts               # Xử lý refresh token, lỗi chung
│   │   │   └── api-response.type.ts                  # Kiểu response chuẩn từ backend
│   │   ├── storage/                                  # Lưu dữ liệu phía trình duyệt
│   │   │   ├── token-storage.ts                      # Lưu, lấy, xóa access token và refresh token
│   │   │   ├── local-storage.service.ts              # Đọc ghi localStorage có kiểm soát
│   │   │   └── session-storage.service.ts            # Đọc ghi sessionStorage có kiểm soát
│   │   ├── file/                                     # Upload, tải file
│   │   │   ├── upload-file.service.ts                # Upload minh chứng/avatar/tài liệu
│   │   │   ├── download-file.service.ts              # Tải file báo cáo, hồ sơ PDF
│   │   │   └── file-preview.service.ts               # Xem trước file ảnh/pdf nếu cần
│   │   └── realtime/                                 # Tích hợp realtime nếu có
│   │       ├── websocket-client.ts                   # Kết nối websocket
│   │       └── notification-channel.ts               # Kênh nhận thông báo realtime
│   │
│   ├── shared/                                       # Thành phần dùng chung toàn frontend
│   │   ├── ui/                                       # Component giao diện dùng lại
│   │   │   ├── button.tsx                            # Nút bấm chuẩn
│   │   │   ├── input.tsx                             # Ô nhập liệu chuẩn
│   │   │   ├── select.tsx                            # Dropdown chọn dữ liệu
│   │   │   ├── textarea.tsx                          # Ô nhập nội dung dài
│   │   │   ├── modal.tsx                             # Hộp thoại xác nhận/thao tác
│   │   │   ├── table.tsx                             # Bảng dữ liệu chuẩn
│   │   │   ├── pagination.tsx                        # Phân trang
│   │   │   ├── badge.tsx                             # Nhãn trạng thái
│   │   │   ├── card.tsx                              # Khối hiển thị thông tin
│   │   │   ├── tabs.tsx                              # Chuyển tab
│   │   │   ├── toast.tsx                             # Thông báo nhanh
│   │   │   ├── loading.tsx                           # Trạng thái đang tải
│   │   │   ├── empty-state.tsx                       # Trạng thái không có dữ liệu
│   │   │   └── confirm-dialog.tsx                    # Xác nhận thao tác nguy hiểm
│   │   ├── form/                                     # Thành phần form dùng chung
│   │   │   ├── form-field.tsx                        # Khung trường nhập liệu
│   │   │   ├── form-error.tsx                        # Hiển thị lỗi validate
│   │   │   ├── date-picker.tsx                       # Chọn ngày
│   │   │   ├── file-upload.tsx                       # Upload file chuẩn
│   │   │   └── search-box.tsx                        # Ô tìm kiếm
│   │   ├── hooks/                                    # Hook dùng chung
│   │   │   ├── use-debounce.ts                       # Trì hoãn tìm kiếm/lọc
│   │   │   ├── use-pagination.ts                     # Xử lý phân trang
│   │   │   ├── use-current-user.ts                   # Lấy người dùng hiện tại
│   │   │   ├── use-permission.ts                     # Kiểm tra quyền hiện tại
│   │   │   └── use-confirm.ts                        # Mở hộp thoại xác nhận
│   │   ├── utils/                                    # Hàm tiện ích dùng chung
│   │   │   ├── date.util.ts                          # Format ngày tháng
│   │   │   ├── file.util.ts                          # Format dung lượng file, lấy đuôi file
│   │   │   ├── text.util.ts                          # Rút gọn, chuẩn hóa chuỗi
│   │   │   ├── number.util.ts                        # Format số liệu thống kê
│   │   │   ├── query-param.util.ts                   # Chuyển filter thành query param
│   │   │   └── permission.util.ts                    # Kiểm tra quyền, scope phía giao diện
│   │   ├── constants/                                # Hằng số dùng chung
│   │   │   ├── role.constant.ts                      # Danh sách vai trò frontend dùng để hiển thị/chặn UI
│   │   │   ├── permission.constant.ts                # Danh sách quyền frontend biết để ẩn/hiện nút
│   │   │   ├── scope.constant.ts                     # Danh sách phạm vi dữ liệu
│   │   │   ├── status.constant.ts                    # Trạng thái chung
│   │   │   └── route-name.constant.ts                # Tên route hiển thị trong breadcrumb/menu
│   │   ├── types/                                    # Kiểu dữ liệu dùng chung
│   │   │   ├── option.type.ts                        # Kiểu option cho select
│   │   │   ├── pagination.type.ts                    # Kiểu phân trang
│   │   │   ├── filter.type.ts                        # Kiểu bộ lọc chung
│   │   │   ├── current-user.type.ts                  # Kiểu người dùng hiện tại
│   │   │   └── permission.type.ts                    # Kiểu role, permission, scope
│   │   └── styles/                                   # Style dùng chung
│   │       ├── global.css                            # CSS toàn cục
│   │       ├── theme.css                             # Biến màu, font, spacing
│   │       ├── layout.css                            # Style khung layout
│   │       └── print.css                             # Style khi in/xuất hồ sơ
│   │
│   ├── entities/                                     # Mô hình dữ liệu phía frontend
│   │   ├── nguoi-dung.entity.ts                      # Kiểu người dùng dùng trên giao diện
│   │   ├── sinh-vien.entity.ts                       # Kiểu sinh viên/đoàn viên dùng trên giao diện
│   │   ├── to-chuc.entity.ts                         # Kiểu chi đoàn, liên chi đoàn, học viện
│   │   ├── vai-tro.entity.ts                         # Kiểu vai trò
│   │   ├── quyen.entity.ts                           # Kiểu quyền
│   │   ├── su-kien.entity.ts                         # Kiểu sự kiện/hoạt động
│   │   ├── minh-chung.entity.ts                      # Kiểu minh chứng
│   │   ├── dot-xet.entity.ts                         # Kiểu đợt xét
│   │   ├── danh-hieu.entity.ts                       # Kiểu danh hiệu/huy hiệu số
│   │   └── thong-bao.entity.ts                       # Kiểu thông báo
│   │
│   ├── layouts/                                      # Bố cục màn hình
│   │   ├── auth-layout.tsx                           # Layout đăng nhập, quên mật khẩu
│   │   ├── main-layout.tsx                           # Layout chính sau đăng nhập
│   │   ├── doan-vien-layout.tsx                      # Layout ưu tiên menu của đoàn viên
│   │   ├── can-bo-layout.tsx                         # Layout cho Bí thư/Phó Bí thư/BCH các cấp
│   │   ├── admin-layout.tsx                          # Layout cho quản trị viên hệ thống
│   │   ├── header.tsx                                # Thanh trên cùng, đặt bộ chọn vai trò đang thao tác nếu người dùng có nhiều vai trò
│   │   ├── sidebar.tsx                               # Menu trái theo quyền
│   │   ├── breadcrumb.tsx                            # Đường dẫn vị trí trang
│   │   └── user-menu.tsx                             # Menu tài khoản cá nhân
│   │
│   ├── pages/                                        # Trang hoàn chỉnh gắn với route
│   │   ├── public/                                   # Trang công khai
│   │   │   ├── dang-nhap.page.tsx                    # Trang đăng nhập
│   │   │   ├── quen-mat-khau.page.tsx                # Trang quên mật khẩu
│   │   │   └── tra-cuu-qr.page.tsx                   # Trang tra cứu/xác minh QR công khai nếu có
│   │   ├── dashboard/                                # Trang tổng quan
│   │   │   ├── dashboard.page.tsx                    # Dashboard tự đổi nội dung theo vai trò
│   │   │   └── dashboard-router.tsx                  # Chọn dashboard đoàn viên/cán bộ/admin
│   │   ├── doan-vien/                                # Nhóm trang của đoàn viên
│   │   │   ├── ho-so-cua-toi.page.tsx                # Hồ sơ cá nhân
│   │   │   ├── hoat-dong-cua-toi.page.tsx            # Lịch sử hoạt động
│   │   │   ├── minh-chung-cua-toi.page.tsx           # Minh chứng đã nộp
│   │   │   ├── dang-ky-su-kien.page.tsx              # Đăng ký sự kiện
│   │   │   └── ket-qua-xet.page.tsx                  # Theo dõi kết quả xét tiêu chí/danh hiệu
│   │   ├── quan-ly/                                  # Nhóm trang quản lý nghiệp vụ
│   │   │   ├── sinh-vien.page.tsx                    # Danh sách và hồ sơ sinh viên
│   │   │   ├── su-kien.page.tsx                      # Quản lý sự kiện
│   │   │   ├── minh-chung.page.tsx                   # Duyệt minh chứng
│   │   │   ├── dot-xet.page.tsx                      # Quản lý đợt xét
│   │   │   ├── danh-hieu.page.tsx                    # Quản lý danh hiệu/huy hiệu
│   │   │   └── bao-cao.page.tsx                      # Báo cáo, thống kê
│   │   ├── he-thong/                                 # Nhóm trang quản trị hệ thống
│   │   │   ├── nguoi-dung.page.tsx                   # Quản lý tài khoản
│   │   │   ├── phan-quyen.page.tsx                   # Gán vai trò, quyền, phạm vi
│   │   │   ├── cau-hinh.page.tsx                     # Cấu hình hệ thống
│   │   │   └── nhat-ky.page.tsx                      # Nhật ký thao tác
│   │   └── error/                                    # Trang lỗi
│   │       ├── forbidden.page.tsx                    # Trang 403 thiếu quyền
│   │       ├── not-found.page.tsx                    # Trang 404 không tìm thấy
│   │       └── server-error.page.tsx                 # Trang 500 lỗi hệ thống
│   │
│   ├── features/                                     # Module nghiệp vụ frontend
│   │   ├── xac-thuc/                                 # Đăng nhập, đăng xuất, phiên làm việc
│   │   │   ├── api/                                  # API riêng của xác thực
│   │   │   │   ├── xac-thuc.api.ts                   # Gọi API đăng nhập, đăng xuất, refresh token
│   │   │   │   └── xac-thuc.mapper.ts                # Chuyển DTO backend thành dữ liệu frontend
│   │   │   ├── components/                           # Component riêng của xác thực
│   │   │   │   ├── dang-nhap-form.tsx                # Form đăng nhập
│   │   │   │   └── quen-mat-khau-form.tsx            # Form quên mật khẩu
│   │   │   ├── hooks/                                # Hook riêng của xác thực
│   │   │   │   ├── use-dang-nhap.ts                  # Hook xử lý đăng nhập
│   │   │   │   └── use-dang-xuat.ts                  # Hook xử lý đăng xuất
│   │   │   ├── types/                                # Kiểu dữ liệu xác thực
│   │   │   │   └── xac-thuc.type.ts                  # Kiểu đăng nhập, token, phiên
│   │   │   └── validation/                           # Validate form xác thực
│   │   │       └── dang-nhap.schema.ts               # Schema kiểm tra form đăng nhập
│   │   │
│   │   ├── phan-quyen/                               # Vai trò, quyền, phạm vi
│   │   │   ├── api/                                  # API phân quyền
│   │   │   │   ├── phan-quyen.api.ts                 # Gọi API lấy/gán/thu hồi vai trò
│   │   │   │   └── phan-quyen.mapper.ts              # Chuyển dữ liệu quyền từ backend sang frontend
│   │   │   ├── components/                           # Component phân quyền
│   │   │   │   ├── vai-tro-switcher.tsx             # Ô chọn vai trò đang thao tác khi một người có nhiều vai trò
│   │   │   │   ├── vai-tro-table.tsx                 # Bảng vai trò người dùng
│   │   │   │   ├── gan-vai-tro-modal.tsx             # Modal gán vai trò
│   │   │   │   ├── thu-hoi-vai-tro-modal.tsx         # Modal thu hồi vai trò
│   │   │   │   ├── permission-matrix.tsx             # Ma trận quyền theo vai trò
│   │   │   │   └── scope-selector.tsx                # Chọn phạm vi chi đoàn/liên chi/học viện
│   │   │   ├── hooks/                                # Hook phân quyền
│   │   │   │   ├── use-vai-tro-nguoi-dung.ts         # Lấy toàn bộ vai trò của người dùng
│   │   │   │   ├── use-vai-tro-hien-tai.ts           # Lưu vai trò/phạm vi đang được chọn trên giao diện
│   │   │   │   ├── use-doi-vai-tro.ts                # Đổi vai trò đang thao tác
│   │   │   │   ├── use-quyen-hien-tai.ts             # Lấy quyền theo vai trò đang chọn
│   │   │   │   ├── use-gan-vai-tro.ts                # Gán vai trò
│   │   │   │   ├── use-thu-hoi-vai-tro.ts            # Thu hồi vai trò
│   │   │   │   └── use-permission-matrix.ts          # Lấy ma trận quyền
│   │   │   ├── policies/                             # Rule hiển thị UI theo quyền
│   │   │   │   ├── can-view-menu.policy.ts           # Kiểm tra được xem menu nào
│   │   │   │   ├── can-access-page.policy.ts         # Kiểm tra được vào trang nào
│   │   │   │   └── can-show-action.policy.ts         # Kiểm tra được hiện nút thao tác nào
│   │   │   └── types/                                # Kiểu dữ liệu phân quyền
│   │   │       └── phan-quyen.type.ts                # Kiểu role, permission, scope, assignment
│   │   │
│   │   ├── sinh-vien/                                # Quản lý sinh viên/đoàn viên
│   │   │   ├── api/                                  # API sinh viên
│   │   │   │   ├── sinh-vien.api.ts                  # Gọi API danh sách, chi tiết, cập nhật sinh viên
│   │   │   │   └── sinh-vien.mapper.ts               # Chuyển DTO sinh viên sang view model
│   │   │   ├── components/                           # Component sinh viên
│   │   │   │   ├── sinh-vien-table.tsx               # Bảng danh sách sinh viên
│   │   │   │   ├── sinh-vien-filter.tsx              # Bộ lọc sinh viên
│   │   │   │   ├── sinh-vien-detail-card.tsx         # Thẻ thông tin sinh viên
│   │   │   │   ├── cap-nhat-sinh-vien-form.tsx       # Form cập nhật sinh viên
│   │   │   │   └── lich-su-hoat-dong-panel.tsx       # Lịch sử hoạt động của sinh viên
│   │   │   ├── hooks/                                # Hook sinh viên
│   │   │   │   ├── use-danh-sach-sinh-vien.ts        # Lấy danh sách sinh viên
│   │   │   │   ├── use-chi-tiet-sinh-vien.ts         # Lấy chi tiết sinh viên
│   │   │   │   └── use-cap-nhat-sinh-vien.ts         # Cập nhật sinh viên
│   │   │   └── types/                                # Kiểu dữ liệu sinh viên
│   │   │       └── sinh-vien.type.ts                 # Kiểu filter, form, view model sinh viên
│   │   │
│   │   ├── su-kien/                                  # Sự kiện, hoạt động, check-in
│   │   │   ├── api/                                  # API sự kiện
│   │   │   │   ├── su-kien.api.ts                    # Gọi API sự kiện
│   │   │   │   └── su-kien.mapper.ts                 # Chuyển dữ liệu sự kiện sang view model
│   │   │   ├── components/                           # Component sự kiện
│   │   │   │   ├── su-kien-table.tsx                 # Bảng sự kiện
│   │   │   │   ├── su-kien-filter.tsx                # Bộ lọc sự kiện
│   │   │   │   ├── su-kien-form.tsx                  # Form tạo/sửa sự kiện
│   │   │   │   ├── su-kien-detail.tsx                # Chi tiết sự kiện
│   │   │   │   ├── qr-su-kien-panel.tsx              # Hiển thị QR sự kiện nếu có quyền
│   │   │   │   ├── check-in-table.tsx                # Danh sách check-in
│   │   │   │   └── them-thu-cong-modal.tsx           # Thêm người tham gia thủ công
│   │   │   ├── hooks/                                # Hook sự kiện
│   │   │   │   ├── use-danh-sach-su-kien.ts          # Lấy danh sách sự kiện
│   │   │   │   ├── use-tao-su-kien.ts                # Tạo sự kiện
│   │   │   │   ├── use-cap-nhat-su-kien.ts           # Cập nhật sự kiện
│   │   │   │   ├── use-dang-ky-su-kien.ts            # Đăng ký sự kiện
│   │   │   │   └── use-check-in-su-kien.ts           # Check-in sự kiện
│   │   │   └── types/                                # Kiểu dữ liệu sự kiện
│   │   │       └── su-kien.type.ts                   # Kiểu form, filter, view model sự kiện
│   │   │
│   │   ├── minh-chung/                               # Nộp và duyệt minh chứng
│   │   │   ├── api/                                  # API minh chứng
│   │   │   │   ├── minh-chung.api.ts                 # Gọi API nộp, duyệt, từ chối minh chứng
│   │   │   │   └── minh-chung.mapper.ts              # Chuyển dữ liệu minh chứng sang view model
│   │   │   ├── components/                           # Component minh chứng
│   │   │   │   ├── minh-chung-table.tsx              # Bảng minh chứng
│   │   │   │   ├── minh-chung-filter.tsx             # Bộ lọc minh chứng
│   │   │   │   ├── nop-minh-chung-form.tsx           # Form nộp minh chứng
│   │   │   │   ├── duyet-minh-chung-modal.tsx        # Modal duyệt minh chứng
│   │   │   │   ├── tu-choi-minh-chung-modal.tsx      # Modal từ chối minh chứng
│   │   │   │   └── yeu-cau-bo-sung-modal.tsx         # Modal yêu cầu bổ sung
│   │   │   ├── hooks/                                # Hook minh chứng
│   │   │   │   ├── use-danh-sach-minh-chung.ts       # Lấy danh sách minh chứng
│   │   │   │   ├── use-nop-minh-chung.ts             # Nộp minh chứng
│   │   │   │   ├── use-duyet-minh-chung.ts           # Duyệt minh chứng
│   │   │   │   └── use-tu-choi-minh-chung.ts         # Từ chối minh chứng
│   │   │   └── types/                                # Kiểu dữ liệu minh chứng
│   │   │       └── minh-chung.type.ts                # Kiểu form, filter, trạng thái minh chứng
│   │   │
│   │   ├── dot-xet/                                  # Đợt xét tiêu chí, danh hiệu
│   │   │   ├── api/                                  # API đợt xét
│   │   │   │   ├── dot-xet.api.ts                    # Gọi API đợt xét
│   │   │   │   └── dot-xet.mapper.ts                 # Chuyển dữ liệu đợt xét sang view model
│   │   │   ├── components/                           # Component đợt xét
│   │   │   │   ├── dot-xet-table.tsx                 # Bảng đợt xét
│   │   │   │   ├── dot-xet-form.tsx                  # Form tạo/sửa đợt xét
│   │   │   │   ├── cau-hinh-tieu-chi-panel.tsx       # Cấu hình tiêu chí xét
│   │   │   │   └── ket-qua-xet-table.tsx             # Bảng kết quả xét
│   │   │   ├── hooks/                                # Hook đợt xét
│   │   │   │   ├── use-danh-sach-dot-xet.ts          # Lấy danh sách đợt xét
│   │   │   │   ├── use-tao-dot-xet.ts                # Tạo đợt xét
│   │   │   │   └── use-phe-duyet-dot-xet.ts          # Phê duyệt kết quả đợt xét
│   │   │   └── types/                                # Kiểu dữ liệu đợt xét
│   │   │       └── dot-xet.type.ts                   # Kiểu form, filter, kết quả xét
│   │   │
│   │   ├── bao-cao/                                  # Báo cáo, thống kê, xuất dữ liệu
│   │   │   ├── api/                                  # API báo cáo
│   │   │   │   ├── bao-cao.api.ts                    # Gọi API báo cáo
│   │   │   │   └── bao-cao.mapper.ts                 # Chuyển dữ liệu báo cáo sang biểu đồ/bảng
│   │   │   ├── components/                           # Component báo cáo
│   │   │   │   ├── thong-ke-card.tsx                 # Thẻ số liệu tổng quan
│   │   │   │   ├── bao-cao-filter.tsx                # Bộ lọc báo cáo
│   │   │   │   ├── bieu-do-tham-gia.tsx              # Biểu đồ tham gia hoạt động
│   │   │   │   ├── bieu-do-minh-chung.tsx            # Biểu đồ trạng thái minh chứng
│   │   │   │   └── xuat-bao-cao-panel.tsx            # Xuất Excel/PDF
│   │   │   ├── hooks/                                # Hook báo cáo
│   │   │   │   ├── use-tong-quan-bao-cao.ts          # Lấy thống kê tổng quan
│   │   │   │   └── use-xuat-bao-cao.ts               # Xuất báo cáo
│   │   │   └── types/                                # Kiểu dữ liệu báo cáo
│   │   │       └── bao-cao.type.ts                   # Kiểu filter và số liệu báo cáo
│   │   │
│   │   ├── thong-bao/                                # Thông báo hệ thống
│   │   │   ├── api/                                  # API thông báo
│   │   │   │   └── thong-bao.api.ts                  # Gọi API lấy và đánh dấu thông báo
│   │   │   ├── components/                           # Component thông báo
│   │   │   │   ├── notification-list.tsx             # Danh sách thông báo
│   │   │   │   └── notification-bell.tsx             # Chuông thông báo
│   │   │   ├── hooks/                                # Hook thông báo
│   │   │   │   └── use-thong-bao.ts                  # Lấy và cập nhật thông báo
│   │   │   └── types/                                # Kiểu dữ liệu thông báo
│   │   │       └── thong-bao.type.ts                 # Kiểu thông báo
│   │   │
│   │   └── he-thong/                                 # Cấu hình hệ thống, nhật ký
│   │       ├── api/                                  # API hệ thống
│   │       │   ├── cau-hinh.api.ts                   # Gọi API cấu hình hệ thống
│   │       │   └── nhat-ky.api.ts                    # Gọi API nhật ký thao tác
│   │       ├── components/                           # Component hệ thống
│   │       │   ├── cau-hinh-form.tsx                 # Form cấu hình chung
│   │       │   ├── cau-hinh-quy-trinh-form.tsx       # Form cấu hình quy trình duyệt
│   │       │   ├── nhat-ky-table.tsx                 # Bảng nhật ký thao tác
│   │       │   └── nhat-ky-filter.tsx                # Bộ lọc nhật ký
│   │       ├── hooks/                                # Hook hệ thống
│   │       │   ├── use-cau-hinh-he-thong.ts          # Lấy/cập nhật cấu hình
│   │       │   └── use-nhat-ky-he-thong.ts           # Lấy nhật ký hệ thống
│   │       └── types/                                # Kiểu dữ liệu hệ thống
│   │           └── he-thong.type.ts                  # Kiểu cấu hình và nhật ký
│   │
│   ├── tests/                                        # Test frontend
│   │   ├── setup-test.ts                             # Cấu hình test
│   │   ├── route-permission.test.ts                  # Test chặn route theo quyền
│   │   ├── permission-policy.test.ts                 # Test rule ẩn/hiện nút
│   │   ├── su-kien-form.test.tsx                     # Test form sự kiện
│   │   └── minh-chung-flow.test.tsx                  # Test luồng nộp/duyệt minh chứng
│   │
│   └── mocks/                                        # Mock dữ liệu khi phát triển/test
│       ├── handlers.ts                               # Mock API handler
│       ├── server.ts                                 # Mock server cho test
│       └── data/                                     # Dữ liệu giả
│           ├── nguoi-dung.mock.ts                    # Mock người dùng
│           ├── sinh-vien.mock.ts                     # Mock sinh viên
│           ├── su-kien.mock.ts                       # Mock sự kiện
│           └── minh-chung.mock.ts                    # Mock minh chứng
│
├── .env.example                                      # Mẫu biến môi trường frontend
├── index.html                                        # HTML gốc của Vite
├── package.json                                      # Dependencies frontend
├── tsconfig.json                                     # Cấu hình TypeScript
├── vite.config.ts                                    # Cấu hình Vite
├── tailwind.config.ts                                # Cấu hình Tailwind nếu dùng
├── eslint.config.js                                  # Cấu hình kiểm tra code
└── README.md                                         # Hướng dẫn chạy frontend
```

## 4. Cách Tổ Chức Module Nghiệp Vụ

Mỗi module trong `features` nên có cấu trúc ổn định:

```text
features/ten-module/
├── api/                                              # Gọi API và chuyển đổi dữ liệu từ backend
├── components/                                       # Component riêng của module
├── hooks/                                            # Hook lấy dữ liệu và xử lý thao tác
├── types/                                            # Kiểu dữ liệu riêng của module
├── validation/                                       # Schema validate form nếu có
└── policies/                                         # Rule riêng của module nếu có
```

Ý nghĩa:

- `api` là nơi duy nhất của module được gọi backend.
- `mapper` trong `api` giúp đổi DTO backend sang dữ liệu hiển thị.
- `components` chỉ nhận props và hiển thị giao diện.
- `hooks` điều phối gọi API, loading, lỗi, refetch.
- `types` định nghĩa kiểu dữ liệu frontend, không phụ thuộc trực tiếp schema database.
- `validation` kiểm tra dữ liệu form trước khi gửi lên backend.
- `policies` kiểm tra điều kiện hiển thị nút, tab, hành động theo quyền.

## 5. Quy Hoạch Phân Quyền Phía Frontend

Frontend không quyết định quyền cuối cùng. Backend vẫn là nơi chặn quyền thật. Tuy nhiên frontend cần kiểm tra quyền để:

- ẩn menu người dùng không được xem
- chặn vào trang sai vai trò
- ẩn nút thao tác không được phép
- tránh gửi request sai phạm vi
- hiển thị đúng giao diện theo scope

Vai trò chuẩn dùng trong frontend:

```text
doan_vien                                      # Đoàn viên
bi_thu_chi_doan                                # Bí thư Chi đoàn
pho_bi_thu_chi_doan                            # Phó Bí thư Chi đoàn
bi_thu_lien_chi                                # Bí thư Liên chi đoàn
pho_bi_thu_lien_chi                            # Phó Bí thư Liên chi đoàn
uy_vien_bch_lien_chi                           # Ủy viên BCH Liên chi đoàn
bi_thu_doan_hoc_vien                           # Bí thư Đoàn Học viện
pho_bi_thu_doan_hoc_vien                       # Phó Bí thư Đoàn Học viện
uy_vien_bch_doan_hoc_vien                      # Ủy viên BCH Đoàn Học viện
quan_tri_vien_he_thong                         # Quản trị viên hệ thống
```

Quy tắc quan trọng:

- Một người có thể có nhiều vai trò.
- Menu lấy theo tổng quyền hợp lệ của các vai trò.
- Mỗi vai trò phải kèm phạm vi: bản thân, chi đoàn, liên chi đoàn, học viện hoặc hệ thống.
- Nút thao tác nhạy cảm phải kiểm tra cả `permission` và `scope`.
- Frontend chỉ ẩn/hiện để trải nghiệm tốt hơn, backend vẫn phải kiểm tra lại.

Ví dụ:

```text
Người A là Đoàn viên + Bí thư Chi đoàn
→ vẫn có trang hồ sơ cá nhân
→ có thêm menu quản lý chi đoàn
→ chỉ xem và xử lý dữ liệu trong chi đoàn được gán
→ không tự xem dữ liệu liên chi đoàn khác
```

## 6. Khi Backend Hoặc Database Thay Đổi Thì Sửa Ở Đâu

Nếu backend đổi database:

- Frontend không sửa theo database.
- Backend giữ API hoặc cập nhật DTO.
- Frontend chỉ sửa `api` và `mapper` nếu response API thay đổi.

Nếu backend đổi tên trường:

- Sửa trong `features/*/api/*.mapper.ts`.
- Không sửa từng component một.

Nếu thêm quyền mới:

- Sửa `shared/constants/permission.constant.ts`.
- Sửa `features/phan-quyen`.
- Sửa `permission-route.tsx` nếu quyền đó ảnh hưởng route.
- Sửa `can-show-action.policy.ts` nếu quyền đó ảnh hưởng nút.

Nếu thêm vai trò mới:

- Sửa `shared/constants/role.constant.ts`.
- Sửa menu trong `layouts/sidebar.tsx`.
- Sửa route guard nếu vai trò đó có trang riêng.
- Không sửa toàn bộ page nếu page đang kiểm tra bằng permission thay vì role cứng.

Nếu thêm module mới:

- Tạo thư mục mới trong `features`.
- Tạo page tương ứng trong `pages`.
- Thêm route trong `app/router`.
- Thêm menu nếu người dùng cần truy cập.
- Thêm test quyền nếu module có thao tác nhạy cảm.

## 7. Ghi Chú Khi Đọc Cây

- `app` là khung chạy ứng dụng, không chứa nghiệp vụ chi tiết.
- `services` là tầng kỹ thuật gọi API, upload, token, websocket.
- `shared` là phần dùng chung, không nhét logic riêng của module vào đây.
- `entities` là model cho frontend, không phải bảng database.
- `features` là nơi đặt logic nghiệp vụ theo module.
- `pages` chỉ ghép màn hình và gọi hook, không gọi API trực tiếp.
- `layouts` chỉ dựng khung giao diện, menu và breadcrumb.
- `mappers` là điểm chống vỡ frontend khi backend đổi response.
- `policies` là điểm chống lẫn quyền, chống hiển thị sai nút theo scope.

## 8. Thứ Tự Nên Code Frontend

Nên làm theo thứ tự sau để tránh thiếu và tránh xung đột dữ liệu:

1. Khởi tạo `frontend`, cấu hình TypeScript, router, env, HTTP client.
2. Làm `shared/ui`, `shared/types`, `shared/constants` tối thiểu.
3. Làm `xac-thuc`: đăng nhập, lưu token, refresh token, đăng xuất.
4. Làm `phan-quyen`: current user, role, permission, scope, route guard, menu guard.
5. Làm layout chính: `main-layout`, `sidebar`, `header`, `breadcrumb`.
6. Làm module `sinh-vien` và hồ sơ cá nhân để có dữ liệu người dùng nền.
7. Làm module `su-kien` vì liên quan tạo hoạt động, đăng ký, check-in.
8. Làm module `minh-chung` vì cần hồ sơ sinh viên và quyền duyệt theo phạm vi.
9. Làm module `dot-xet`, `danh-hieu` vì phụ thuộc minh chứng đã duyệt.
10. Làm `bao-cao`, `thong-bao`, `he-thong`, `nhat-ky`.
11. Viết test route quyền, policy quyền và các form quan trọng.
12. Tối ưu giao diện, loading, empty state, responsive, in/xuất hồ sơ.



## 9. Bổ Sung Phần Chọn Vai Trò Đang Thao Tác

Phần này xử lý ở frontend để người có nhiều vai trò không bị nhầm đang thao tác với quyền nào.

Các file cần có trong cây frontend:

```text
frontend/src/features/phan-quyen/                       # Module quyền phía giao diện
├── api/                                                # Gọi API lấy vai trò/quyền hiện tại
│   ├── phan-quyen.api.ts                               # Lấy danh sách vai trò, quyền, phạm vi của người dùng
│   └── phan-quyen.mapper.ts                            # Chuyển dữ liệu quyền từ backend sang frontend
├── components/                                         # Component phân quyền
│   ├── vai-tro-switcher.tsx                            # Ô chọn "Đang thao tác với vai trò nào"
│   ├── vai-tro-table.tsx                               # Bảng vai trò người dùng
│   ├── gan-vai-tro-modal.tsx                           # Modal gán vai trò
│   ├── thu-hoi-vai-tro-modal.tsx                       # Modal thu hồi vai trò
│   ├── permission-matrix.tsx                           # Ma trận quyền theo vai trò
│   └── scope-selector.tsx                              # Chọn phạm vi chi đoàn/liên chi/học viện
├── hooks/                                              # Hook phân quyền
│   ├── use-vai-tro-nguoi-dung.ts                       # Lấy toàn bộ vai trò của người dùng
│   ├── use-vai-tro-hien-tai.ts                         # Lưu vai trò/phạm vi đang được chọn trên giao diện
│   ├── use-doi-vai-tro.ts                              # Đổi từ vai trò này sang vai trò khác
│   ├── use-quyen-hien-tai.ts                           # Lấy quyền ứng với vai trò đang chọn
│   ├── use-gan-vai-tro.ts                              # Gán vai trò
│   └── use-thu-hoi-vai-tro.ts                          # Thu hồi vai trò
├── policies/                                           # Rule hiển thị giao diện theo quyền
│   ├── can-view-menu.policy.ts                         # Kiểm tra được xem menu nào theo vai trò đang chọn
│   ├── can-access-page.policy.ts                       # Kiểm tra được vào trang nào
│   └── can-show-action.policy.ts                       # Kiểm tra được hiện nút thao tác nào
└── types/                                              # Kiểu dữ liệu phân quyền
    └── phan-quyen.type.ts                              # Kiểu role, permission, scope, assignment
```

Component `vai-tro-switcher.tsx` nên được đặt ở:

```text
frontend/src/layouts/header.tsx                         # Header hiển thị vai trò đang thao tác
```

Hoặc:

```text
frontend/src/layouts/user-menu.tsx                      # Menu tài khoản có phần đổi vai trò
```

Luồng giao diện:

1. Người dùng đăng nhập.
2. Frontend gọi API lấy danh sách vai trò hiện có.
3. Nếu chỉ có một vai trò, hệ thống tự chọn vai trò đó.
4. Nếu có nhiều vai trò, header hiện ô chọn vai trò.
5. Người dùng chọn Bí thư Chi đoàn thì menu chỉ hiện việc của Chi đoàn.
6. Người dùng chọn Phó Bí thư Đoàn Học viện thì menu hiện việc cấp Học viện.
7. Khi bấm nút thao tác, frontend gửi request bình thường, backend vẫn kiểm tra quyền thật.

Ví dụ:

```text
Người A có 2 vai trò:
- Bí thư Chi đoàn D21CQCN01-B
- Phó Bí thư Đoàn Học viện PTIT

Header hiển thị:
Đang thao tác với vai trò: [Bí thư Chi đoàn D21CQCN01-B ▼]

Nếu A đổi sang:
[Phó Bí thư Đoàn Học viện PTIT]

Menu và nút bấm đổi theo quyền cấp Học viện.
```
