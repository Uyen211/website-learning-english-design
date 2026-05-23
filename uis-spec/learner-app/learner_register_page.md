# MÀN HÌNH: REGISTER PAGE (TRANG ĐĂNG KÝ NGƯỜI HỌC)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Register Page (Trang đăng ký người học)
- Mã use case liên quan: LN-FL-01 (Xác thực tài khoản người học)
- Mã luồng người dùng liên quan: Flow LN-FL-01 (Xác thực tài khoản người học)
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Register Page (URL: /register)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Người dùng (học viên mới) truy cập màn hình này để đăng ký một tài khoản cá nhân mới trên hệ thống DiveVerse bằng cách điền thông tin họ tên, email và mật khẩu.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Centered card layout (Bố cục một cột căn giữa hoàn toàn theo cả chiều ngang và dọc) trên nền canvas sáng ấm (#fffaf0).
- Các vùng chính trên màn hình:
  - Vùng A: Biểu tượng logo DiveVerse và tiêu đề trang căn giữa.
  - Vùng B: Thẻ biểu mẫu đăng ký (Register Card Container) chứa các trường nhập liệu, nút bấm đăng ký và nút đăng ký nhanh qua mạng xã hội.
  - Vùng C: Chân trang tối giản chứa thông tin bản quyền.
- Kích thước / Grid tham khảo:
  - Chiều rộng của thẻ biểu mẫu: 440px.
  - Thẻ căn giữa toàn màn hình bằng CSS Flexbox.
  - Khoảng cách padding trong thẻ: 40px.
  - Khoảng cách dọc giữa các trường: spacing-md (16px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)
- **Tên component:** Logo Mascot
  - **Loại component tham chiếu từ DESIGN.md:** 3D claymation mascot / image
  - **Vị trí:** Vùng A, nằm trên cùng, căn giữa.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hình ảnh chú bạch tuộc DiveVerse đang đội mũ cử nhân. Kích thước 100px x 100px.

- **Tên component:** Tiêu đề trang
  - **Loại component tham chiếu từ DESIGN.md:** display-md (Plain Black display typeface, font Inter weight 500, size 32px, letter-spacing -0.5px)
  - **Vị trí:** Vùng A, cách logo 16px.
  - **Trạng thái:** Mặc định, màu chữ ink (#0a0a0a).
  - **Dữ liệu hiển thị / hành vi:** Dòng chữ "Bắt đầu học ngay!".

- **Tên component:** Hộp chứa biểu mẫu (Register Form Card)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền surface-card #f5f0e0, border 1px hairline #e5e5e5, rounded-xl 24px, padding 40px, không đổ bóng)
  - **Vị trí:** Vùng B, trung tâm màn hình.
  - **Trạng thái:** Mặc định.

- **Tên component:** Trường nhập Họ và tên (Full Name Input)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, màu chữ ink #0a0a0a, rounded-md 12px, border 1px hairline #e5e5e5, height 44px)
  - **Vị trí:** Vùng B, trường nhập thứ nhất.
  - **Trạng thái:**
    - Mặc định: viền màu hairline, placeholder "Ví dụ: Nguyễn Văn A..." màu muted-soft (#9a9a9a).
    - Focus: viền đổi sang màu primary (#0a0a0a) 1.5px.
    - Error: viền đỏ màu error (#ef4444).
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Họ và tên *". Bắt buộc nhập.

- **Tên component:** Trường nhập Email (Email Input)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, màu chữ ink #0a0a0a, rounded-md 12px, border 1px hairline #e5e5e5, height 44px)
  - **Vị trí:** Vùng B, trường nhập thứ hai.
  - **Trạng thái:** Mặc định, focus, error.
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Email *". Placeholder "Nhập email đăng ký...". Bắt buộc nhập.

- **Tên component:** Trường nhập Mật khẩu (Password Input)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, màu chữ ink #0a0a0a, rounded-md 12px, border 1px hairline #e5e5e5, height 44px, ẩn ký tự mật khẩu)
  - **Vị trí:** Vùng B, trường nhập thứ ba.
  - **Trạng thái:** Mặc định, focus, error.
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Mật khẩu *". Placeholder "Tối thiểu 6 ký tự...". Bắt buộc nhập.

- **Tên component:** Trường Nhập lại mật khẩu (Confirm Password Input)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, màu chữ ink #0a0a0a, rounded-md 12px, border 1px hairline #e5e5e5, height 44px, ẩn ký tự mật khẩu)
  - **Vị trí:** Vùng B, trường nhập thứ tư.
  - **Trạng thái:** Mặc định, focus, error.
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Nhập lại mật khẩu *". Placeholder "••••••••". Bắt buộc nhập.

- **Tên component:** Nút "Đăng ký"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, font Inter size 14px, weight 600, rounded-md 12px, height 44px, width 100%)
  - **Vị trí:** Vùng B, nằm dưới các trường nhập liệu.
  - **Trạng thái:** Mặc định, hover, loading.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Đăng ký tài khoản". Nhấp vào để gửi yêu cầu đăng ký mới.

- **Tên component:** Đường phân cách "Hoặc" (Divider)
  - **Loại component tham chiếu từ DESIGN.md:** body-sm (màu muted-soft #9a9a9a)
  - **Vị trí:** Vùng B, nằm dưới nút Đăng ký.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị dòng hairline ngang, ở giữa có chữ "hoặc".

- **Tên component:** Nút Đăng ký nhanh bằng Google (Google Signup Button)
  - **Loại component tham chiếu từ DESIGN.md:** button-secondary (nền canvas #fffaf0, border 1px hairline #e5e5e5, chữ ink #0a0a0a, rounded-md 12px, height 44px, width 100%)
  - **Vị trí:** Vùng B, nằm dưới đường phân cách.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị logo Google màu sắc và chữ "Đăng ký bằng Google".

- **Tên component:** Liên kết "Đăng nhập" (Switch to Login)
  - **Loại component tham chiếu từ DESIGN.md:** text-link (màu ink #0a0a0a, font Inter 14px, weight 600, có gạch chân)
  - **Vị trí:** Vùng B, dưới cùng của thẻ biểu mẫu.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị dòng chữ: "Đã có tài khoản? Đăng nhập ngay". Nhấp chuột sẽ chuyển hướng đến Login Page (TR-02).

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động:** Điền đầy đủ thông tin và nhấp nút "Đăng ký tài khoản"
  - **Luồng chính:**
    1. Học viên nhập đầy đủ thông tin vào các trường (Tên, Email đúng định dạng, Mật khẩu >= 6 ký tự, Nhập lại mật khẩu khớp nhau).
    2. Click nút "Đăng ký tài khoản".
    3. Nút chuyển sang trạng thái Loading (hiển thị spinner xoay và khóa click).
    4. Hệ thống gửi yêu cầu API POST tạo tài khoản mới lên máy chủ.
    5. API tạo tài khoản thành công và tự động đăng nhập, trả về token xác thực (JWT).
    6. Hệ thống lưu Token vào LocalStorage.
    7. Hiển thị Toast thông báo đăng ký thành công màu xanh lá ở góc trên bên phải.
    8. Chuyển hướng sang màn hình học tập chính LN-01 (Learner Dashboard).
  - **Luồng con / rẽ nhánh:**
    - *Trường hợp thiếu thông tin:* Ô nhập bị thiếu bôi đỏ viền, hiển thị lỗi: "Thông tin này là bắt buộc và không được để trống!".
    - *Trường hợp mật khẩu quá ngắn:* Mật khẩu dưới 6 ký tự -> Bôi đỏ viền mật khẩu, báo lỗi: "Mật khẩu phải chứa ít nhất 6 ký tự!".
    - *Trường hợp mật khẩu nhập lại không khớp:* Trường nhập lại mật khẩu bôi đỏ viền, hiển thị thông báo lỗi: "Mật khẩu xác nhận không khớp!".
    - *Trường hợp email đã tồn tại:* Máy chủ trả lỗi 409 Conflict -> Nút Đăng ký đóng Loading, bôi đỏ ô Email, hiển thị lỗi: "Email này đã được sử dụng trong hệ thống!".
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: `{ "name": "Nguyễn Văn A", "email": "learner@gmail.com", "password": "secure_password" }`
    - Nhận về: `{ "success": true, "token": "eyJhbGciOi...", "user": { "id": 105, "role": "learner", "name": "Nguyễn Văn A" } }`

- **Hành động:** Nhấp nút "Đăng ký bằng Google"
  - **Luồng chính:** Nhấp chọn -> Mở popup xác thực tài khoản Google của bên thứ ba -> Thành công -> Hệ thống tự động tạo tài khoản theo thông tin Google và chuyển sang LN-01.

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Các trường nhập mặc định hiển thị trống kèm placeholder xám.
- **Trạng thái tải (loading state):** Khi đang gửi dữ liệu lên server, nút Đăng ký hiển thị spinner xoay và khóa tương tác click.
- **Trạng thái lỗi (error state):** Khi API thất bại, bôi đỏ viền input và hiển thị nhãn báo lỗi đỏ (#ef4444).
- **Trạng thái thành công (success state):** Hiển thị Toast thông báo xanh lá (#22c55e) ở góc trên bên phải: "Tạo tài khoản thành công! Đang khởi tạo lộ trình học tập...".

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ Guest Landing Page (TR-01) khi nhấp nút "Bắt đầu học ngay", hoặc từ Login Page (TR-02) khi nhấp chọn liên kết "Đăng ký ngay".
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Chuyển hướng trực tiếp đến Learner Dashboard (LN-01).
- **Các màn hình liên quan khác:** Login Page (TR-02).

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn sử dụng màu canvas sáng ấm (#fffaf0).
- Thẻ biểu mẫu được thiết kế bằng phong cách `feature-card-cream` có góc bo rất lớn rounded-xl (24px) và màu nền surface-card (#f5f0e0), viền hairline mỏng 1px (#e5e5e5).
- Khoảng cách dọc giữa các trường nhập liệu là spacing-md (16px) đảm bảo tính thoáng mát, dễ nhìn, tránh quá tải nhận thức cho học viên mới.
- Chiều cao các trường nhập và nút bấm là 44px, đạt touch target chuẩn mực.
