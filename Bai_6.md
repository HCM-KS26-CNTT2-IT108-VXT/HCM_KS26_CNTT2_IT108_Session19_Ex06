# Bài 6: Ngăn chặn rò rỉ thông tin bí mật trên GitHub

## 1. Pre-push Checklist

Trước khi đẩy mã nguồn lên GitHub, team cần kiểm tra:

- [ ]  Kiểm tra mã nguồn có chứa API Keys, mật khẩu hoặc Token không.
- [ ]  Không ghi trực tiếp thông tin bí mật vào code.
- [ ]  Kiểm tra file `.env` đã được thêm vào `.gitignore`.
- [ ]  Sử dụng công cụ Gitleaks để quét mã nguồn tìm thông tin bí mật.
- [ ]  Kiểm tra lại các file trước khi Push lên GitHub.

## 2. Cấu trúc file an toàn trên GitHub

```text
Ecommerce/
│
├── src/
├── .env.example
├── .gitignore
├── README.md
└── package.json
```

### Nội dung file `.gitignore`

```gitignore
.env
.env.*
!.env.example
node_modules/
```

### Nội dung file `.env.example`

```env
# DEV
DEV_API_URL=
DEV_API_KEY=

# TEST
TEST_API_URL=
TEST_API_KEY=

# PRODUCTION
PROD_API_URL=
PROD_API_KEY=
```

**Lưu ý:** File `.env.example` chỉ chứa tên biến và giá trị mẫu, không chứa API Key thật.

## 3. Bật xác thực hai yếu tố (2FA)

- Mỗi thành viên đăng nhập GitHub.
- Vào Settings → Password and authentication.
- Chọn Enable two-factor authentication.
- Thiết lập xác thực bằng ứng dụng Authenticator.
- Lưu Backup Codes ở nơi an toàn.
- Yêu cầu tất cả thành viên bật 2FA trước khi tham gia repository.

## 4. Báo cáo rủi ro nếu thiếu `.gitignore`


| Rủi ro                       | Hậu quả                             |
| ----------------------------- | ------------------------------------- |
| Đẩy file`.env` lên GitHub  | Lộ API Keys và mật khẩu.          |
| Đẩy thư mục`node_modules` | Làm repository nặng hơn.           |
| Lộ thông tin đăng nhập   | Hacker có thể truy cập hệ thống. |
| Lộ dữ liệu cấu hình      | Ảnh hưởng đến bảo mật dự án. |

**Cách xử lý:** Tạo `.gitignore`, quét mã nguồn trước khi Push và thu hồi, thay mới ngay các API Keys nếu đã bị lộ.
