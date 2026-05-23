# MÀN HÌNH: LEARNER LOGIN PAGE (TRANG ĐĂNG NHẬP NGƯỜI HỌC)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Learner Login Page (Trang đăng nhập người học)
- Mã use case liên quan: LN-FL-01 (Xác thực tài khoản người học - Điều kiện ban đầu của tất cả các bài học học viên)
- Mã luồng người dùng liên quan: Flow LN-FL-01 (Xác thực tài khoản người học)
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Login Page (URL: /login)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Người học truy cập màn hình này để đăng nhập vào tài khoản cá nhân của mình trên hệ thống DiveVerse nhằm lưu giữ học bạ, tham gia học các Unit và thực hành các kỹ năng.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Centered card layout (Bố cục một cột căn giữa hoàn toàn theo cả chiều ngang và dọc) trên nền canvas sáng ấm (#fffaf0).
- Các vùng chính trên màn hình:
  - Vùng A: Biểu tượng logo chú bạch tuộc và tiêu đề trang căn giữa.
  - Vùng B: Thẻ biểu mẫu đăng nhập (Login Card Container) chứa các trường nhập liệu, nút bấm đăng nhập và nút đăng nhập bên thứ ba (Google/Facebook).
  - Vùng C: Chân trang tối giản chứa liên kết bản quyền.
- Kích thước / Grid tham khảo:
  - Chiều rộng của thẻ biểu mẫu: 440px.
  - Căn giữa dọc và ngang bằng CSS Flexbox.
  - Khoảng cách padding trong thẻ: 40px.
  - Khoảng cách giữa các trường: spacing-md (16px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)
- **Tên component:** Logo Mascot
  - **Loại component tham chiếu từ DESIGN.md:** 3D claymation mascot / image
  - **Vị trí:** Vùng A, nằm trên cùng, căn giữa.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hình ảnh chú bạch tuộc DiveVerse đang đọc sách. Kích thước 100px x 100px.

- **Tên component:** Tiêu đề trang
  - **Loại component tham chiếu từ DESIGN.md:** display-md (Plain Black display typeface, font Inter weight 500, size 32px, letter-spacing -0.5px)
  - **Vị trí:** Vùng A, cách logo 16px.
  - **Trạng thái:** Mặc định, màu chữ ink (#0a0a0a).
  - **Dữ liệu hiển thị / hành vi:** Dòng chữ "Chào mừng quay lại!".

- **Tên component:** Hộp chứa biểu mẫu (Login Form Card)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền surface-card #f5f0e0, border 1px hairline #e5e5e5, rounded-xl 24px, padding 40px, không đổ bóng)
  - **Vị trí:** Vùng B, trung tâm màn hình.
  - **Trạng thái:** Mặc định.

- **Tên component:** Trường nhập Email (Email Input)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, màu chữ ink #0a0a0a, rounded-md 12px, border 1px hairline #e5e5e5, height 44px)
  - **Vị trí:** Vùng B, trường nhập thứ nhất.
  - **Trạng thái:**
    - Mặc định: viền màu hairline, placeholder "Nhập email của bạn..." màu muted-soft (#9a9a9a).
    - Focus: viền đổi sang màu primary (#0a0a0a) 1.5px.
    - Error: viền đỏ màu error (#ef4444).
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Email *". Bắt buộc nhập.

- **Tên component:** Trường nhập Mật khẩu (Password Input)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, màu chữ ink #0a0a0a, rounded-md 12px, border 1px hairline #e5e5e5, height 44px, ẩn ký tự mật khẩu)
  - **Vị trí:** Vùng B, trường nhập thứ hai.
  - **Trạng thái:** Mặc định, focus, error.
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Mật khẩu *". Placeholder: "••••••••". Tích hợp icon hiển thị/ẩn mật khẩu ở góc phải. Bắt buộc nhập.

- **Tên component:** Liên kết "Quên mật khẩu?" (Forgot Password Link)
  - **Loại component tham chiếu từ DESIGN.md:** button-text-link (màu muted #6a6a6a, font Inter 13px, weight 500)
  - **Vị trí:** Vùng B, nằm dưới trường mật khẩu, căn lề phải.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị text "Quên mật khẩu?". Nhấp chọn để mở luồng lấy lại mật khẩu.

- **Tên component:** Nút "Đăng nhập"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, font Inter size 14px, weight 600, rounded-md 12px, height 44px, width 100%)
  - **Vị trí:** Vùng B, nằm dưới link quên mật khẩu.
  - **Trạng thái:** Mặc định, hover, loading (xoay spinner trắng ở giữa, khóa tương tác).
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Đăng nhập". Click để thực hiện xác thực.

- **Tên component:** Đường phân cách "Hoặc" (Divider)
  - **Loại component tham chiếu từ DESIGN.md:** body-sm (màu muted-soft #9a9a9a)
  - **Vị trí:** Vùng B, nằm dưới nút Đăng nhập.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị một dòng hairline ngang mờ hai bên, ở giữa có chữ "hoặc đăng nhập bằng".

- **Tên component:** Nút Đăng nhập Google (Google Login Button)
  - **Loại component tham chiếu từ DESIGN.md:** button-secondary (nền canvas #fffaf0, border 1px hairline #e5e5e5, chữ ink #0a0a0a, rounded-md 12px, height 44px, width 100%)
  - **Vị trí:** Vùng B, nằm dưới đường phân cách.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị icon Google nhỏ màu sắc và dòng chữ "Tiếp tục với Google". Nhấp chọn để mở popup đăng nhập tài khoản Google.

- **Tên component:** Liên kết "Đăng ký tài khoản" (Switch to Register)
  - **Loại component tham chiếu từ DESIGN.md:** text-link (màu ink #0a0a0a, font Inter 14px, weight 600, có gạch chân)
  - **Vị trí:** Vùng B, dưới cùng của thẻ biểu mẫu.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị dòng chữ: "Chưa có tài khoản? Đăng ký ngay". Nhấp chuột sẽ chuyển hướng đến Register Page (TR-03).

- **Tên component:** Thông báo lỗi biểu mẫu
  - **Loại component tham chiếu từ DESIGN.md:** body-sm (màu error #ef4444)
  - **Vị trí:** Vùng B, hiển thị sát trên nút Đăng nhập khi có lỗi.
  - **Trạng thái:** Ẩn mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị "Email hoặc mật khẩu không chính xác!".

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động:** Điền email, mật khẩu và nhấp nút "Đăng nhập"
  - **Luồng chính:**
    1. Học viên nhập đúng định dạng email và mật khẩu hợp lệ.
    2. Nhấn nút "Đăng nhập".
    3. Nút chuyển sang trạng thái Loading (hiển thị spinner, khóa tương tác).
    4. Hệ thống gửi yêu cầu API POST đến server.
    5. API trả về mã thành công (200 OK) kèm JWT Token.
    6. Hệ thống lưu Token vào LocalStorage.
    7. Hiển thị Toast thông báo đăng nhập thành công màu xanh lá ở góc trên bên phải.
    8. Sau 1.5 giây, hệ thống chuyển hướng sang màn hình LN-01 (Learner Dashboard).
  - **Luồng con / rẽ nhánh:**
    - *Trường hợp thiếu thông tin:* Nếu trường email hoặc mật khẩu bị bỏ trống -> Không gửi API, bôi đỏ viền trường bị thiếu, hiển thị thông báo lỗi "Email và mật khẩu không được để trống!".
    - *Trường hợp email sai định dạng:* Nếu nhập email không có chữ @ hoặc không đúng format -> Bôi đỏ viền ô email, hiển thị lỗi: "Định dạng email không hợp lệ!".
    - *Trường hợp sai thông tin đăng nhập:* Nếu thông tin xác thực sai -> Máy chủ trả về lỗi 401 -> Nút Đăng nhập tắt trạng thái Loading. Viền cả hai trường nhập đổi sang màu đỏ. Hiển thị thông báo lỗi màu đỏ: "Email hoặc mật khẩu không chính xác!".
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: `{ "email": "learner@gmail.com", "password": "learner_password" }`
    - Nhận về: `{ "success": true, "token": "eyJhbGciOi...", "user": { "id": 105, "role": "learner", "name": "Nguyễn Văn A" } }`

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Các trường nhập mặc định hiển thị trống kèm placeholder xám.
- **Trạng thái tải (loading state):** Khi đang gọi API xác thực, nút "Đăng nhập" hiển thị spinner xoay và vô hiệu hóa click, các trường nhập phía trên cũng tạm thời không cho sửa.
- **Trạng thái lỗi (error state):** Khi API thất bại, bôi đỏ viền input và hiển thị nhãn báo lỗi đỏ (#ef4444).
- **Trạng thái thành công (success state):** Hiển thị Toast thông báo xanh lá (#22c55e) ở góc trên bên phải: "Đăng nhập thành công! Đang tải lộ trình học...".

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ Guest Landing Page (TR-01) khi nhấp nút "Đăng nhập", hoặc từ Register Page (TR-03) khi nhấp liên kết "Đăng nhập".
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Chuyển hướng đến Learner Dashboard (LN-01).
- **Các màn hình liên quan khác:** Register Page (TR-03).

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn sử dụng màu canvas sáng ấm (#fffaf0).
- Thẻ biểu mẫu được thiết kế mềm mại bằng góc bo lớn rounded-xl (24px) và màu nền surface-card (#f5f0e0), không có bóng đổ thô cứng, chỉ sử dụng đường hairline mỏng nhẹ 1px (#e5e5e5).
- Nguyên tắc tránh quá tải nhận thức (Coherence Principle): Thiết kế form đăng nhập đơn giản nhất có thể. Các nút đăng nhập mạng xã hội phụ trợ được đặt nhỏ gọn, phân tách rõ ràng bằng đường chia hairline mỏng để không lấn át nút đăng nhập chính.
- Kích thước touch target của tất cả các trường nhập và nút bấm được đặt ở chiều cao 44px, nút Google và các liên kết đảm bảo kích thước dễ nhấp.
