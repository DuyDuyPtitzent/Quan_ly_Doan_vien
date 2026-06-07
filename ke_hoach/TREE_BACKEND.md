# Cây Backend Và Giải Thích Theo Tầng

## 1. Mục Đích

Tài liệu này chỉ mô tả backend. Mục tiêu là để:

- Dễ đọc cấu trúc.
- Dễ sửa từng phần mà không đụng lan sang chỗ khác.
- Dễ thay database, storage hoặc cách tích hợp sau này.
- Dễ phân biệt phần giao diện API, phần xử lý nghiệp vụ, phần luật cốt lõi và phần hạ tầng.

## 2. Ý Nghĩa Từng Tầng

### `presentation`
Tầng nhận request từ frontend, kiểm tra dữ liệu đầu vào, gọi tầng xử lý nghiệp vụ và trả response.

### `application`
Tầng này điều phối:

- kiểm tra quyền
- gọi repository lấy dữ liệu
- gọi domain xử lý luật
- lưu kết quả
- gửi thông báo nếu cần

### `domain`
Là tầng chứa luật nghiệp vụ cốt lõi, không phụ thuộc database, không phụ thuộc HTTP.

### `infrastructure`
Tầng làm việc với công nghệ cụ thể như Prisma, PostgreSQL, Redis, MinIO, email và queue.

Nguyên tắc:

- Nếu đổi database thì chỉ đổi ở `infrastructure`.
- Không đẩy luật nghiệp vụ vào controller.
- Không để domain phụ thuộc vào Prisma hay HTTP.

## 3. Cây Backend

```text
backend/                                             # Toàn bộ backend của hệ thống
├── src/                                             # Mã nguồn backend chính
│   ├── main.ts                                       # Điểm khởi động ứng dụng NestJS
│   ├── app.module.ts                                 # Module gốc, gom các module lớn của hệ thống
│   │
│   ├── config/                                       # Cấu hình hệ thống theo môi trường
│   │   ├── app.config.ts                             # Cấu hình tên app, port, prefix API
│   │   ├── database.config.ts                        # Cấu hình kết nối cơ sở dữ liệu
│   │   ├── jwt.config.ts                              # Cấu hình token đăng nhập
│   │   ├── storage.config.ts                          # Cấu hình lưu file: local, MinIO, S3
│   │   ├── mail.config.ts                             # Cấu hình email thông báo
│   │   └── env.validation.ts                          # Kiểm tra biến môi trường
│   │
│   ├── common/                                       # Thành phần dùng chung cho toàn backend
│   │   ├── constants/                                # Hằng số dùng chung của hệ thống
│   │   │   ├── role.constant.ts                      # Danh sách vai trò chuẩn
│   │   │   ├── permission.constant.ts                # Danh sách quyền chuẩn
│   │   │   ├── scope.constant.ts                    # Danh sách phạm vi truy cập
│   │   │   ├── status.constant.ts                   # Danh sách trạng thái chung
│   │   │   └── error-code.constant.ts               # Mã lỗi chuẩn của hệ thống
│   │   ├── decorators/                               # Decorator tự viết
│   │   │   ├── current-user.decorator.ts            # Lấy người dùng hiện tại từ request
│   │   │   ├── public.decorator.ts                  # Đánh dấu API không cần đăng nhập
│   │   │   ├── require-permission.decorator.ts      # Gắn quyền cần có cho API
│   │   │   └── require-role.decorator.ts            # Gắn vai trò cần có cho API
│   │   ├── guards/                                   # Guard bảo vệ API
│   │   │   ├── jwt-auth.guard.ts                     # Kiểm tra token đăng nhập
│   │   │   ├── permission.guard.ts                   # Kiểm tra người dùng có quyền hay không
│   │   │   └── scope.guard.ts                        # Kiểm tra có nằm trong phạm vi dữ liệu hay không
│   │   ├── filters/                                  # Bắt lỗi tập trung
│   │   │   └── http-exception.filter.ts              # Chuẩn hóa lỗi trả về client
│   │   ├── interceptors/                             # Can thiệp request/response
│   │   │   ├── response.interceptor.ts               # Chuẩn hóa response API
│   │   │   └── audit-log.interceptor.ts              # Ghi log thao tác quan trọng
│   │   ├── pipes/                                    # Validate dữ liệu đầu vào
│   │   │   └── validation.pipe.ts                    # Kiểm tra DTO trước khi vào service
│   │   ├── utils/                                    # Hàm tiện ích dùng chung
│   │   │   ├── pagination.util.ts                    # Xử lý phân trang
│   │   │   ├── date.util.ts                          # Xử lý ngày tháng
│   │   │   ├── slug.util.ts                          # Tạo slug hoặc mã định danh
│   │   │   ├── hash.util.ts                          # Hash mật khẩu hoặc file
│   │   │   └── file.util.ts                          # Xử lý tên file, đuôi file, dung lượng
│   │   └── types/                                    # Kiểu dữ liệu dùng chung
│   │       ├── current-user.type.ts                  # Kiểu người dùng hiện tại sau khi giải mã token
│   │       ├── pagination.type.ts                    # Kiểu phân trang
│   │       └── scope.type.ts                         # Kiểu phạm vi dữ liệu
│   │
│   ├── infrastructure/                               # Hạ tầng kỹ thuật của hệ thống
│   │   ├── database/                                 # Tầng làm việc với cơ sở dữ liệu
│   │   │   ├── prisma.module.ts                      # Khai báo module Prisma
│   │   │   ├── prisma.service.ts                     # Cung cấp PrismaClient
│   │   │   └── transaction.service.ts                # Xử lý transaction khi thao tác nhiều bảng
│   │   ├── storage/                                  # Tầng lưu trữ file
│   │   │   ├── storage.interface.ts                  # Interface để đổi local/MinIO/S3 không phá code khác
│   │   │   ├── local-storage.service.ts              # Lưu file trên máy chủ
│   │   │   └── minio-storage.service.ts              # Lưu file bằng MinIO
│   │   ├── mail/                                     # Gửi email
│   │   ├── queue/                                    # Xử lý tác vụ nền nếu cần
│   │   └── integrations/                              # Tích hợp với hệ thống ngoài nếu có
│   │
│   ├── modules/                                      # Các module nghiệp vụ chính
│   │   ├── xac-thuc/                                 # Đăng nhập, đăng xuất, làm mới token
│   │   │   ├── xac-thuc.module.ts                    # Module xác thực
│   │   │   ├── xac-thuc.controller.ts                # API đăng nhập và xác thực
│   │   │   ├── xac-thuc.service.ts                   # Xử lý nghiệp vụ đăng nhập
│   │   │   └── dto/                                  # Dữ liệu đầu vào của xác thực
│   │   │       ├── dang-nhap.dto.ts                  # DTO đăng nhập
│   │   │       ├── lam-moi-token.dto.ts              # DTO làm mới token
│   │   │       └── xac-thuc-otp.dto.ts               # DTO xác thực OTP
│   │   │
│   │   ├── nguoi-dung/                               # Quản lý tài khoản người dùng
│   │   │   ├── nguoi-dung.module.ts                  # Module người dùng
│   │   │   ├── nguoi-dung.controller.ts              # API quản lý người dùng
│   │   │   ├── nguoi-dung.service.ts                 # Xử lý tạo, sửa, khóa tài khoản
│   │   │   ├── mat-khau.service.ts                   # Đổi mật khẩu, quên mật khẩu
│   │   │   └── dto/                                  # Dữ liệu đầu vào của người dùng
│   │   │       ├── tao-nguoi-dung.dto.ts             # DTO tạo tài khoản
│   │   │       ├── cap-nhat-nguoi-dung.dto.ts        # DTO cập nhật tài khoản
│   │   │       ├── doi-mat-khau.dto.ts               # DTO đổi mật khẩu
│   │   │       └── loc-nguoi-dung.dto.ts             # DTO lọc danh sách người dùng
│   │   │
│   │   ├── phan-quyen/                               # Vai trò, quyền, phạm vi và phân công nhiều vai trò
│   │   │   ├── phan-quyen.module.ts                  # Module phân quyền
│   │   │   ├── phan-quyen.controller.ts              # API cấp quyền, thu hồi quyền, lấy quyền hiện tại
│   │   │   ├── phan-quyen.service.ts                 # Điều phối logic phân quyền chung
│   │   │   ├── phan-cong-vai-tro.service.ts          # Xử lý một người có nhiều vai trò theo từng phạm vi
│   │   │   ├── quyen-hien-tai.service.ts             # Tính quyền hiện tại sau đăng nhập để frontend biết người dùng có vai trò nào
│   │   │   ├── domain/                               # Luật nghiệp vụ phân quyền
│   │   │   │   ├── vai-tro.enum.ts                   # Danh sách vai trò chuẩn
│   │   │   │   ├── quyen.enum.ts                     # Danh sách quyền chuẩn
│   │   │   │   ├── pham-vi.enum.ts                   # Danh sách phạm vi chuẩn
│   │   │   │   ├── phan-cong-vai-tro.entity.ts       # Mô hình user + vai trò + phạm vi + thời hạn + quyết định
│   │   │   │   ├── phan-quyen.policy.ts              # Luật kiểm tra ai được làm hành động nào trong phạm vi nào
│   │   │   │   ├── tong-hop-quyen.policy.ts          # Gộp quyền từ nhiều vai trò đang còn hiệu lực
│   │   │   │   └── vai-tro-nguoi-dung.repository.ts  # Interface lấy và lưu vai trò người dùng
│   │   │   └── dto/                                  # Dữ liệu đầu vào/đầu ra của phân quyền
│   │   │       ├── gan-vai-tro.dto.ts                # DTO gán vai trò
│   │   │       ├── thu-hoi-vai-tro.dto.ts            # DTO thu hồi vai trò
│   │   │       ├── cap-nhat-pham-vi.dto.ts           # DTO cập nhật phạm vi
│   │   │       └── quyen-hien-tai.dto.ts             # DTO trả về danh sách vai trò/quyền/phạm vi hiện tại cho frontend
│   │   │
│   │   ├── to-chuc/                                  # Cây tổ chức: trường, khoa, lớp, chi đoàn, liên chi
│   │   │   ├── to-chuc.module.ts                     # Module tổ chức
│   │   │   ├── to-chuc.controller.ts                 # API quản lý tổ chức
│   │   │   ├── to-chuc.service.ts                    # Xử lý nghiệp vụ tổ chức
│   │   │   └── dto/                                  # Dữ liệu đầu vào của tổ chức
│   │   │       ├── tao-to-chuc.dto.ts                # DTO tạo đơn vị
│   │   │       └── cap-nhat-to-chuc.dto.ts           # DTO cập nhật đơn vị
│   │   │
│   │   ├── sinh-vien/                                # Quản lý sinh viên và đoàn viên
│   │   │   ├── sinh-vien.module.ts                   # Module sinh viên
│   │   │   ├── sinh-vien.controller.ts               # API quản lý sinh viên
│   │   │   ├── sinh-vien.service.ts                  # Xử lý nghiệp vụ sinh viên
│   │   │   └── dto/                                  # Dữ liệu đầu vào của sinh viên
│   │   │       ├── tao-sinh-vien.dto.ts              # DTO tạo sinh viên
│   │   │       └── cap-nhat-sinh-vien.dto.ts         # DTO cập nhật sinh viên
│   │   │
│   │   ├── su-kien/                                  # Tạo và quản lý sự kiện
│   │   │   ├── su-kien.module.ts                     # Module sự kiện
│   │   │   ├── su-kien.controller.ts                 # API tạo, sửa, xem, công bố sự kiện
│   │   │   ├── su-kien.service.ts                    # Điều phối nghiệp vụ sự kiện
│   │   │   ├── domain/                               # Luật nghiệp vụ sự kiện
│   │   │   │   ├── su-kien.entity.ts                 # Mô hình sự kiện
│   │   │   │   ├── trang-thai-su-kien.enum.ts        # Trạng thái sự kiện
│   │   │   │   ├── su-kien.policy.ts                 # Luật ai được tạo, sửa, xem sự kiện
│   │   │   │   └── su-kien.repository.ts             # Interface lưu và lấy sự kiện
│   │   │   └── dto/                                  # Dữ liệu đầu vào của sự kiện
│   │   │       ├── tao-su-kien.dto.ts                # DTO tạo sự kiện
│   │   │       ├── cap-nhat-su-kien.dto.ts           # DTO cập nhật sự kiện
│   │   │       └── check-in.dto.ts                   # DTO check-in
│   │   │
│   │   ├── minh-chung/                               # Nộp và duyệt minh chứng
│   │   │   ├── minh-chung.module.ts                  # Module minh chứng
│   │   │   ├── minh-chung.controller.ts              # API nộp và xử lý minh chứng
│   │   │   ├── minh-chung.service.ts                 # Điều phối nghiệp vụ minh chứng
│   │   │   ├── domain/                               # Luật nghiệp vụ minh chứng
│   │   │   │   ├── minh-chung.entity.ts              # Mô hình minh chứng
│   │   │   │   ├── trang-thai-minh-chung.enum.ts     # Trạng thái minh chứng
│   │   │   │   ├── minh-chung.policy.ts              # Luật duyệt và giới hạn sửa minh chứng
│   │   │   │   └── minh-chung.repository.ts          # Interface lưu và lấy minh chứng
│   │   │   └── dto/                                  # Dữ liệu đầu vào của minh chứng
│   │   │       ├── nop-minh-chung.dto.ts             # DTO nộp minh chứng
│   │   │       ├── nop-minh-chung-tu-khai.dto.ts     # DTO nộp minh chứng tự khai báo
│   │   │       ├── phe-duyet-minh-chung.dto.ts       # DTO duyệt minh chứng
│   │   │       ├── tu-choi-minh-chung.dto.ts         # DTO từ chối minh chứng
│   │   │       └── yeu-cau-bo-sung.dto.ts             # DTO yêu cầu bổ sung
│   │   │
│   │   ├── dot-xet/                                  # Đợt xét danh hiệu và tổng hợp minh chứng
│   │   │   ├── dot-xet.module.ts                     # Module đợt xét
│   │   │   ├── dot-xet.controller.ts                 # API tạo, mở, khóa đợt xét
│   │   │   ├── dot-xet.service.ts                    # Điều phối đợt xét
│   │   │   ├── domain/                               # Luật nghiệp vụ đợt xét
│   │   │   │   ├── dot-xet.entity.ts                 # Mô hình đợt xét
│   │   │   │   ├── trang-thai-dot-xet.enum.ts        # Trạng thái đợt xét
│   │   │   │   ├── dot-xet.policy.ts                 # Luật xét và khóa đợt xét
│   │   │   │   └── dot-xet.repository.ts             # Interface lưu và lấy đợt xét
│   │   │   └── dto/                                  # Dữ liệu đầu vào của đợt xét
│   │   │       ├── tao-dot-xet.dto.ts                # DTO tạo đợt xét
│   │   │       ├── dang-ky-dot-xet.dto.ts            # DTO đăng ký đợt xét
│   │   │       └── phe-duyet-dot-xet.dto.ts          # DTO duyệt đợt xét
│   │   │
│   │   ├── danh-hieu/                                # Danh hiệu và huy hiệu số
│   │   │   ├── danh-hieu.module.ts                   # Module danh hiệu
│   │   │   ├── danh-hieu.controller.ts               # API cấp và xem danh hiệu
│   │   │   ├── danh-hieu.service.ts                  # Điều phối nghiệp vụ danh hiệu
│   │   │   └── dto/                                  # Dữ liệu đầu vào của danh hiệu
│   │   │       ├── tao-danh-hieu.dto.ts              # DTO tạo loại danh hiệu
│   │   │       ├── cap-danh-hieu.dto.ts              # DTO cấp danh hiệu
│   │   │       └── loc-danh-hieu.dto.ts              # DTO lọc danh hiệu
│   │   │
│   │   ├── chuong-trinh/                             # Chương trình Đảng, Đoàn, Nhà nước
│   │   │   ├── chuong-trinh.module.ts                # Module chương trình
│   │   │   ├── chuong-trinh.controller.ts            # API quản lý chương trình
│   │   │   ├── chuong-trinh.service.ts               # Điều phối nghiệp vụ chương trình
│   │   │   └── dto/                                  # Dữ liệu đầu vào của chương trình
│   │   │       ├── tao-chuong-trinh.dto.ts           # DTO tạo chương trình
│   │   │       ├── dang-ky-chuong-trinh.dto.ts       # DTO đăng ký chương trình
│   │   │       └── phe-duyet-chuong-trinh.dto.ts     # DTO duyệt chương trình
│   │   │
│   │   ├── bao-cao/                                  # Báo cáo, thống kê, xuất dữ liệu
│   │   │   ├── bao-cao.module.ts                     # Module báo cáo
│   │   │   ├── bao-cao.controller.ts                 # API báo cáo
│   │   │   ├── bao-cao.service.ts                    # Điều phối báo cáo
│   │   │   ├── xuat-excel.service.ts                 # Xuất Excel
│   │   │   ├── xuat-pdf.service.ts                   # Xuất PDF
│   │   │   └── dto/                                  # Dữ liệu đầu vào của báo cáo
│   │   │       ├── loc-bao-cao.dto.ts                # DTO lọc báo cáo
│   │   │       └── xuat-bao-cao.dto.ts               # DTO xuất báo cáo
│   │   │
│   │   ├── tep-tin/                                  # Upload và quản lý file
│   │   │   ├── tep-tin.module.ts                     # Module file
│   │   │   ├── tep-tin.controller.ts                 # API upload và tải file
│   │   │   ├── tep-tin.service.ts                    # Điều phối nghiệp vụ file
│   │   │   └── dto/                                  # Dữ liệu đầu vào của file
│   │   │       └── upload-file.dto.ts                # DTO upload file
│   │   │
│   │   ├── thong-bao/                                # Thông báo hệ thống
│   │   │   ├── thong-bao.module.ts                   # Module thông báo
│   │   │   ├── thong-bao.controller.ts               # API xem và đánh dấu thông báo
│   │   │   ├── thong-bao.service.ts                  # Điều phối nghiệp vụ thông báo
│   │   │   └── dto/                                  # Dữ liệu đầu vào của thông báo
│   │   │       └── tao-thong-bao.dto.ts              # DTO tạo thông báo
│   │   │
│   │   ├── cau-hinh-he-thong/                        # Cấu hình hệ thống theo từng trường
│   │   │   ├── cau-hinh-he-thong.module.ts           # Module cấu hình hệ thống
│   │   │   ├── cau-hinh-he-thong.controller.ts       # API cấu hình hệ thống
│   │   │   ├── cau-hinh-he-thong.service.ts          # Điều phối cấu hình chung
│   │   │   ├── cau-hinh-truong.service.ts            # Cấu hình thông tin trường
│   │   │   ├── cau-hinh-quy-trinh.service.ts         # Cấu hình quy trình duyệt
│   │   │   └── cau-hinh-mau-bieu.service.ts          # Cấu hình mẫu biểu
│   │   │
│   │   ├── nhat-ky-he-thong/                         # Audit log của toàn hệ thống
│   │   │   ├── nhat-ky-he-thong.module.ts            # Module nhật ký
│   │   │   ├── nhat-ky-he-thong.controller.ts        # API xem log
│   │   │   ├── nhat-ky-he-thong.service.ts           # Ghi và truy vấn log
│   │   │   └── dto/                                  # Dữ liệu đầu vào của log
│   │   │       └── loc-nhat-ky.dto.ts                # DTO lọc log
│   │   │
│   │   └── jobs/                                     # Tác vụ chạy nền
│   │       ├── het-han-vai-tro.job.ts                # Tự thu hồi vai trò khi hết nhiệm kỳ
│   │       ├── khoa-dot-xet.job.ts                   # Tự khóa đợt xét khi hết hạn
│   │       ├── nhac-han-duyet-minh-chung.job.ts      # Nhắc cán bộ duyệt minh chứng
│   │       └── gui-thong-bao.job.ts                  # Gửi thông báo định kỳ
│   │
│   ├── prisma/                                       # Khai báo dữ liệu với Prisma
│   │   ├── schema.prisma                             # Khai báo toàn bộ model cơ sở dữ liệu
│   │   ├── seed.ts                                   # Chạy seed dữ liệu gốc
│   │   └── seeds/                                    # Các file seed riêng cho từng nhóm dữ liệu
│   │       ├── seed-roles.ts                         # Seed vai trò mặc định
│   │       ├── seed-permissions.ts                   # Seed quyền mặc định
│   │       ├── seed-role-permissions.ts              # Seed gán quyền cho vai trò
│   │       ├── seed-nhom-ky-nang.ts                  # Seed 6 nhóm kỹ năng
│   │       ├── seed-tieu-chi-5-tot.ts                # Seed 5 tiêu chí Sinh viên 5 tốt
│   │       └── seed-truong-ptit.ts                   # Seed thông tin PTIT ban đầu
│   │
│   └── uploads/                                      # File upload lưu tạm hoặc lưu local
│       ├── minh-chung/                               # File minh chứng
│       ├── avatar/                                   # Ảnh đại diện
│       ├── bao-cao/                                  # File báo cáo xuất ra
│       └── ho-so-xuat/                               # File hồ sơ PDF xuất ra
│
├── test/                                             # Test backend
│   ├── auth.e2e-spec.ts                              # Test xác thực
│   ├── minh-chung.e2e-spec.ts                        # Test nộp và duyệt minh chứng
│   └── su-kien.e2e-spec.ts                           # Test sự kiện
│
├── docker-compose.yml                                # Chạy PostgreSQL, Redis, MinIO bằng Docker
├── Dockerfile                                        # Đóng gói backend thành image
├── .env.example                                      # Mẫu biến môi trường
├── package.json                                      # Danh sách dependencies backend
├── tsconfig.json                                     # Cấu hình TypeScript
└── README.md                                         # Hướng dẫn chạy backend
```

## 4. Ghi Chú Khi Đọc Cây

- `presentation` chỉ nhận request và trả response.
- `application` chỉ điều phối nghiệp vụ.
- `domain` giữ luật cốt lõi.
- `infrastructure` thay đổi khi đổi công nghệ.
- `modules/phan-quyen` là module quan trọng nhất để chặn lọt scope giữa các đơn vị.
- Mỗi module nghiệp vụ nên có `controller`, `service`, `domain`, `dto` để dễ chia việc và dễ bảo trì.
- Nếu thay cơ sở dữ liệu hoặc storage, ưu tiên sửa ở `infrastructure` trước, không sửa lan sang toàn bộ module.


## 5. Bổ Sung Phần Một Người Có Nhiều Vai Trò

Phần này xử lý ở module:

```text
backend/src/modules/phan-quyen/
```

Khi một người vừa là Bí thư Chi đoàn, vừa là Phó Bí thư Đoàn Học viện, hệ thống không tạo tài khoản mới và không ép người đó chỉ dùng một vai trò. Hệ thống lưu nhiều dòng phân công vai trò cho cùng một người dùng.

Các file cần có trong cây backend:

```text
backend/src/modules/phan-quyen/                         # Module quản lý vai trò, quyền và phạm vi
├── phan-quyen.module.ts                                # Gom toàn bộ xử lý phân quyền
├── phan-quyen.controller.ts                            # API gán vai trò, thu hồi vai trò, lấy quyền hiện tại
├── phan-quyen.service.ts                               # Điều phối nghiệp vụ phân quyền
├── phan-cong-vai-tro.service.ts                        # Xử lý một người có nhiều vai trò theo từng phạm vi
├── quyen-hien-tai.service.ts                           # Tính tổng quyền hợp lệ của người dùng sau khi đăng nhập
├── domain/                                             # Luật nghiệp vụ phân quyền
│   ├── vai-tro.enum.ts                                 # Danh sách vai trò chuẩn
│   ├── quyen.enum.ts                                   # Danh sách quyền chuẩn
│   ├── pham-vi.enum.ts                                 # Danh sách phạm vi: bản thân, chi đoàn, liên chi, học viện, hệ thống
│   ├── phan-cong-vai-tro.entity.ts                     # Mô hình user + vai trò + phạm vi + thời hạn + quyết định
│   ├── phan-quyen.policy.ts                            # Kiểm tra người dùng có quyền làm hành động trong phạm vi đó không
│   ├── tong-hop-quyen.policy.ts                        # Gộp quyền từ nhiều vai trò đang còn hiệu lực
│   └── vai-tro-nguoi-dung.repository.ts                # Interface lấy/lưu vai trò người dùng
└── dto/                                                # Dữ liệu đầu vào/đầu ra của phân quyền
    ├── gan-vai-tro.dto.ts                              # Dữ liệu gán vai trò cho người dùng
    ├── thu-hoi-vai-tro.dto.ts                          # Dữ liệu thu hồi vai trò
    ├── cap-nhat-pham-vi.dto.ts                         # Dữ liệu cập nhật phạm vi vai trò
    └── quyen-hien-tai.dto.ts                           # Dữ liệu trả về danh sách vai trò/quyền hiện tại sau đăng nhập
```

Luồng xử lý:

1. Người dùng đăng nhập.
2. Backend lấy tất cả phân công vai trò còn hiệu lực của người đó.
3. `quyen-hien-tai.service.ts` trả về danh sách vai trò, quyền và phạm vi cho frontend.
4. Khi người dùng thao tác, API gửi hành động và phạm vi cần xử lý.
5. `phan-quyen.policy.ts` kiểm tra có vai trò nào của người đó có đúng quyền và đúng phạm vi không.
6. Nếu có thì cho thao tác, nếu không thì trả lỗi 403.

Ví dụ:

```text
Người A có 2 phân công:
- Bí thư Chi đoàn, phạm vi Chi đoàn D21CQCN01-B
- Phó Bí thư Đoàn Học viện, phạm vi Học viện PTIT

A tạo sự kiện cho D21CQCN01-B
→ dùng quyền Bí thư Chi đoàn.

A cấu hình tiêu chí cấp Học viện
→ dùng quyền Phó Bí thư Đoàn Học viện.

A tạo sự kiện cho Chi đoàn khác
→ không được, vì sai phạm vi.
```
