# MÀN HÌNH: REGISTER PAGE (TRANG ĐĂNG KÝ NGƯỜI HỌC)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Register Page (Trang đăng ký người học)
- **Mã use case liên quan:** LN-FL-01 (Xác thực tài khoản người học - Khởi tạo tài khoản học viên)
- **Mã luồng người dùng liên quan:** LN-FL-01 (Xác thực tài khoản người học)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Đăng ký (URL: `/register`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Cung cấp biểu mẫu đăng ký để người dùng mới tạo tài khoản học tập cá nhân trên hệ thống DiveVerse. Việc tạo tài khoản giúp người dùng bắt đầu lộ trình học từ vựng/ngữ pháp (UC-05a, UC-05b), lưu trữ tiến độ cá nhân, và thiết lập cấp độ mục tiêu đầu ra (IELTS/TOEIC).

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục thẻ căn giữa (Centered Card Layout) dùng CSS Flexbox hoặc Grid để ghim khối biểu mẫu chính xác vào trung tâm của màn hình.
- **Màu nền chung:** Nền trang sử dụng `{colors.canvas}` (`#F9F7FE`) kết hợp phủ dải chuyển màu khí quyển `{gradients.atmosphere-haze}` dạng radial phát ra từ góc trái trên màn hình. Điểm xuyết các chấm sao lấp lánh mờ ảo.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Vùng A: Khu vực Nhận diện thương hiệu (Phía trên thẻ)**
    - Logo DiveVerse thu nhỏ nằm căn giữa cùng Mascot Cá Voi Xanh động viên học viên mới.
  - **Vùng B: Khối Biểu mẫu Đăng ký (Trung tâm)**
    - Một thẻ biểu mẫu chứa các trường thông tin đăng ký cơ bản, nút submit, và liên kết đăng nhập.
  - **Vùng C: Chân trang tối giản (Footer)**
    - Chứa thông tin bản quyền và các liên kết pháp lý cơ bản ở góc dưới màn hình.

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thẻ biểu mẫu đăng ký (Register Card Container)
- **Đặc tả Visual:**
  - Nền: `{colors.surface}` (`#FFFFFF`) tinh khiết.
  - Bo góc: `{rounded.xxl}` (32px).
  - Chiều rộng tối đa: `460px` (Rộng hơn trang đăng nhập một chút để dàn đều các trường).
  - Hiệu ứng nâng độ cao: `{elevation.glow}` (Tỏa ánh sáng tím nhạt bao quanh thẻ).
  - Padding bên trong: `{spacing.xl}` (32px).
  - Viền mờ: `1px solid rgba(155, 93, 224, 0.1)`.

### 4.2 Nhận diện thương hiệu & Mascot (Vùng A)
- **Logo DiveVerse:**
  - Sử dụng hình ảnh cá voi chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png).
  - Kích thước: `80px x 80px`. Căn giữa hoàn hảo phía trên thẻ.
- **Tiêu đề trang:**
  - Kiểu chữ: `{typography.display-sm}` (Manrope, 28px, weight 700, letter-spacing -0.5px).
  - Màu sắc: `{colors.text-primary}` (`#1A1A2E`).
  - Nội dung: *"Bắt đầu chuyến du hành!"*
- **Mascot Cá Voi Xanh Vũ Trụ (Bản khởi hành):**
  - Sử dụng hình ảnh cá voi chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png).
  - Kích thước: `100px` lơ lửng ngay góc trên bên phải của Thẻ biểu mẫu. Bụng chú cá voi phát quang hồng nhẹ, bên cạnh có hình ảnh một ngôi sao nhỏ lấp lánh (dùng icon `star` trong thư viện), tạo cảm giác phấn khởi khởi đầu hành trình mới.

### 4.3 Các trường nhập liệu (Input Fields - Vùng B)
- **Trường nhập Họ và tên (Full Name Input):**
  - Nhãn (Label): *"Họ và tên *" dùng `{typography.caption}` màu `{colors.text-primary}`.
  - Hộp nhập liệu:
    - Bo góc: `{rounded.lg}` (16px).
    - Chiều cao: `input-height` (44px).
    - Viền mặc định: `1px solid rgba(155, 93, 224, 0.2)`.
    - Trạng thái Focus: Viền đổi sang màu `{colors.primary}` (`#4E56C0`), kèm theo lớp soft glow nhẹ.
    - Placeholder: *"Ví dụ: Nguyễn Văn A..."* dùng `{typography.body-sm}` màu `{colors.text-secondary}`.
- **Trường nhập Email (Email Input):**
  - Nhãn (Label): *"Email *" dùng `{typography.caption}`.
  - Hộp nhập liệu: Tương tự trường Họ và tên.
  - Placeholder: *"Nhập email đăng ký của bạn..."*.
- **Trường nhập Mật khẩu (Password Input):**
  - Nhãn (Label): *"Mật khẩu (Tối thiểu 8 ký tự) *" dùng `{typography.caption}`.
  - Hộp nhập liệu: Tương tự nhưng ẩn ký tự (`type="password"`).
  - Icon chức năng: Icon Lucide `eye` / `eye-off` ở góc phải để hiển thị/ẩn mật khẩu.
  - Placeholder: *"••••••••"*.
- **Trường Nhập lại mật khẩu (Confirm Password Input):**
  - Nhãn (Label): *"Nhập lại mật khẩu *" dùng `{typography.caption}`.
  - Hộp nhập liệu: Tương tự trường mật khẩu.
  - Placeholder: *"••••••••"*.

### 4.4 Các nút bấm hành động (Action Buttons - Vùng B)
- **Nút "Đăng ký" (Primary CTA của Form):**
  - **Đặc tả Visual:** Nền `{colors.primary}` (`#4E56C0`), chữ màu `#FFFFFF`. Bo góc `{rounded.lg}` (16px). Chiều rộng 100%. Chiều cao tối thiểu `button-min-height` (44px).
  - **Hiệu ứng:** Mặc định có `{elevation.active-glow}`. Khi hover: kích hoạt `{elevation.hover-glow}` (Hiệu ứng tỏa sáng tím đậm), chuyển động mượt mà trong `0.2s`.
  - **Nội dung:** *"Tạo tài khoản miễn phí"*.
- **Đường phân cách Social Signup:**
  - Một đường line nằm ngang nét mảnh màu `rgba(155, 93, 224, 0.15)` cắt đôi nhãn *"hoặc đăng ký bằng"* ở chính giữa biểu mẫu. Nhãn dùng `{typography.caption}` màu `{colors.text-secondary}`.
- **Nút Đăng ký bằng Google (Secondary Button):**
  - **Đặc tả Visual:** Nền trắng `{colors.surface}`, chữ màu `{colors.primary}`, viền `1px solid rgba(78, 86, 192, 0.2)`. Bo góc `{rounded.lg}` (16px). Chiều rộng 100%. Chiều cao tối thiểu `44px`.
  - **Icon:** Logo Google đa sắc căn lề trái của văn bản nút.
- **Liên kết chuyển sang trang Đăng nhập:**
  - **Vị trí:** Dưới cùng của thẻ biểu mẫu, căn giữa.
  - **Đặc tả Visual:** *"Đã có tài khoản? Đăng nhập ngay"* dùng `{typography.body-sm}` (Inter, 14px). Cụm từ *"Đăng nhập ngay"* được tô màu `{colors.primary}` (`#4E56C0`) và in đậm. Khi hover sẽ tỏa sáng mờ và gạch chân.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION FLOWS)
1. **Luồng đăng ký thành công:**
   - Người học nhập đầy đủ và hợp lệ các trường thông tin $\rightarrow$ Click nút "Tạo tài khoản miễn phí".
   - Nút chuyển sang trạng thái Loading (Spinner xoay tròn, khóa tương tác).
   - Gửi yêu cầu API đăng ký tài khoản: `POST /api/auth/register` với thông tin `{ name, email, password }`.
   - API trả về thành công: `{ success: true, token: "jwt_token", user: { id, name, email } }`.
   - Hệ thống tự động lưu Token xác thực vào LocalStorage.
   - Hiển thị Toast chúc mừng màu xanh lá `{colors.success}`: *"Đăng ký tài khoản thành công! Bắt đầu du hành vũ trụ."*
   - Chuyển hướng sang trang [learner_dashboard.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/learner_dashboard.md).
2. **Luồng xử lý lỗi nhập liệu (Validation & Server Errors):**
   - **Họ và tên để trống:** Hiển thị lỗi *"Vui lòng nhập họ và tên của bạn"*.
   - **Email trống/Sai cấu pháp:** Hiển thị lỗi *"Địa chỉ email không hợp lệ"*.
   - **Mật khẩu dưới 8 ký tự:** Hiển thị lỗi *"Mật khẩu phải dài tối thiểu 8 ký tự"*.
   - **Mật khẩu nhập lại không khớp:** Đổi viền trường Xác nhận mật khẩu sang màu đỏ `{colors.error}` và báo lỗi *"Mật khẩu xác nhận không khớp!"*.
   - **Lỗi Email đã tồn tại (API trả về lỗi 409):** Hiển thị banner Alert màu nền hồng nhạt, viền đỏ `{colors.error}` ở đầu thẻ biểu mẫu: *"Email này đã được đăng ký trước đó. Vui lòng đăng nhập hoặc dùng email khác!"*.

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT
- **Trạng thái tải (Loading state):** Nút Đăng ký vô hiệu hóa, hiển thị spinner. Toàn bộ các trường input bị khóa (`disabled`).
- **Trạng thái lỗi (Error state):** Các trường lỗi được viền màu đỏ semantic `{colors.error}` kèm hiệu ứng rung lắc nhẹ để báo hiệu cho người dùng.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [guest_landing_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/guest_landing_page.md), hoặc [learner_login_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/learner_login_page.md).
- **Đi đến:** [learner_dashboard.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/learner_dashboard.md) (Sau khi đăng ký thành công).

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Đảm bảo tất cả các input field có độ nhạy tương tác cao (hiệu ứng focus mềm mại trong `0.2s`). Giữ khoảng cách giữa các trường đồng đều ở mức `{spacing.md}` (16px).
- **KHÔNG ĐƯỢC:** Để xảy ra tình trạng tràn màn hình ở các thiết bị di động nhỏ. Trực quan hóa cấu trúc form theo luồng cuộn đơn khi màn hình hẹp lại.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Thông báo lỗi đăng ký (Validation Errors):**
  - Email đã được đăng ký: `{auth.registerErrors.emailTaken}`
  - Mật khẩu không khớp: `{auth.registerErrors.passwordMismatch}`
  - Mật khẩu quá yếu: `{auth.registerErrors.weakPassword}`
