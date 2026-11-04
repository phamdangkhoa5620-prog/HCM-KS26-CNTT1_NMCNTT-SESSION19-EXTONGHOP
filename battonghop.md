## PHẦN 1 – NHẬN DIỆN RỦI RO

### 1\. Nhận diện hai tình huống

* **Tình huống 1 – Typosquatting:** Website `githuh-security.com` giả mạo `github.com`, yêu cầu nhập mật khẩu để mở khóa tài khoản.
* **Tình huống 2 – Malware Crack:** Phần mềm Photoshop crack yêu cầu tắt Windows Defender, có nguy cơ cài mã độc vào máy tính.

### 2\. Quy tắc 5 KHÔNG

1. Không bấm vào đường link lạ.
2. Không cung cấp mật khẩu hoặc OTP.
3. Không tải phần mềm crack.
4. Không tắt Windows Defender.
5. Không mở tệp đính kèm không rõ nguồn gốc.

### 3\. Quy trình cấp cứu 4 bước

1. **Ngắt kết nối:** Tắt Wi-Fi, rút dây mạng.
2. **Đổi mật khẩu:** Sử dụng thiết bị sạch để đổi mật khẩu.
3. **Revoke Token:** Thu hồi Token, Session và quyền truy cập đáng ngờ.
4. **Làm sạch:** Quét mã độc hoặc cài lại Windows.

## PHẦN 2 – PASSWORD MANAGER

### 1\. Rủi ro dùng chung mật khẩu

* Nếu email bị lộ, hacker có thể thử mật khẩu đó trên GitHub và Vercel.
* Kiểu tấn công: **Credential Stuffing**.

### 2\. Zero-Knowledge Architecture

* Dữ liệu được mã hóa trên thiết bị người dùng.
* Máy chủ Bitwarden chỉ lưu dữ liệu đã mã hóa.
* Hacker khó đọc dữ liệu nếu không có khóa giải mã.

### 3\. Cấu hình Password Generator

* Độ dài: 20 ký tự.
* Chữ hoa: Bật.
* Chữ thường: Bật.
* Chữ số: Bật.
* Ký tự đặc biệt: Bật.
* Tạo 3 mật khẩu riêng biệt cho GitHub, Vercel và Email nhóm.

## PHẦN 3 – KÍCH HOẠT 2FA GITHUB

### 1\. Vì sao chọn Authenticator App?

SMS OTP có 2 nhược điểm:

* Có nguy cơ bị chiếm SIM (**SIM Swapping**).
* Phụ thuộc sóng điện thoại và nhà mạng.

Authenticator App sử dụng TOTP tạo mã 6 số theo thời gian, không cần mạng di động để tạo mã.

### 2\. Các bước kích hoạt Google Authenticator

1. Đăng nhập GitHub.
2. Vào Settings → Password and authentication.
3. Chọn Enable two-factor authentication.
4. Chọn Authenticator App.
5. Mở Google Authenticator và quét mã QR.
6. Nhập mã OTP 6 số để xác nhận.
7. Lưu 10 mã khôi phục.

### 3\. Lưu mã khôi phục

* **Nên:** Lưu trong Bitwarden hoặc in ra và cất ở nơi an toàn.
* **Không nên:** Lưu công khai trên GitHub hoặc gửi qua Messenger/Zalo.

## PHẦN 4 – BẢO VỆ SECRETS

### 1\. Hai Secrets bị hardcode

* `API\_KEY = "sk-proj-abc123456789"`
* `DB\_PASSWORD = "SmartCampus@2026"`

### 2\. Code `config.js` sau khi sửa

```javascript
const API\_KEY = process.env.API\_KEY;
const DB\_PASSWORD = process.env.DB\_PASSWORD;

function connectDatabase() {
  return connect(DB\_PASSWORD);
}
```

### 3\. Nội dung các file

**File `.env` (chứa giá trị thật):**

```env
API\_KEY=GIA\_TRI\_THAT
DB\_PASSWORD=MAT\_KHAU\_THAT
```

**File `.gitignore`:**

```gitignore
.env
.env.\*
!.env.example
node\_modules/
```

**File `.env.example` (chỉ chứa tên biến):**

```env
API\_KEY=
DB\_PASSWORD=
```

### 4\. Quy tắc 4 bước kiểm tra trước khi Push

1. Kiểm tra code, không hardcode Secrets.
2. Kiểm tra `.env` đã được thêm vào `.gitignore`.
3. Kiểm tra lịch sử Git, tránh để lộ Secrets trong commit cũ.
4. Kiểm tra lần cuối trước khi `git push`.

**Lệnh kiểm tra:**

```bash
git status
git diff --cached
git check-ignore -v .env
```

