# MÀN HÌNH: LEARNER LOGIN PAGE (TRANG ĐĂNG NHẬP NGƯỜI HỌC)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Learner Login Page (Trang đăng nhập người học)
- **Mã use case liên quan:** LN-FL-01 (Xác thực tài khoản người học - Khởi tạo phiên làm việc học viên)
- **Mã luồng người dùng liên quan:** LN-FL-01 (Xác thực tài khoản người học)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Đăng nhập (URL: `/login`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Cung cấp cổng xác thực an toàn để người học truy cập vào tài khoản của mình trên hệ thống DiveVerse. Việc đăng nhập thành công giúp kích hoạt tiến trình học tập cá nhân, khôi phục lịch sử học bạ, đồng bộ hóa thuật toán ôn tập Spaced Repetition (SRS - UC-08) và theo dõi chuỗi ngày học liên tục (Streak).

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục thẻ căn giữa (Centered Card Layout) dùng CSS Flexbox hoặc Grid để ghim khối biểu mẫu chính xác vào tâm màn hình.
- **Màu nền chung:** Nền trang sử dụng `{colors.canvas}` (`#F9F7FE`) kết hợp phủ dải chuyển màu khí quyển `{gradients.atmosphere-haze}` dạng radial phát ra từ góc trái trên màn hình. Điểm xuyết các chấm sao lấp lánh mờ ảo.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Vùng A: Khu vực Nhận diện thương hiệu (Phía trên thẻ)**
    - Logo DiveVerse thu nhỏ nằm căn giữa cùng Mascot Cá Voi Xanh động viên học viên.
  - **Vùng B: Khối Biểu mẫu Đăng nhập (Trung tâm)**
    - Một thẻ biểu mẫu duy nhất chứa toàn bộ các trường nhập liệu, nút submit và phương thức đăng nhập thay thế.
  - **Vùng C: Chân trang tối giản (Footer)**
    - Chứa thông tin bản quyền và các liên kết pháp lý cơ bản ở góc dưới màn hình.

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thẻ biểu mẫu đăng nhập (Login Card Container)
- **Đặc tả Visual:**
  - Nền: `{colors.surface}` (`#FFFFFF`) tinh khiết.
  - Bo góc: `{rounded.xxl}` (32px).
  - Chiều rộng tối đa: `440px`.
  - Hiệu ứng nâng độ cao: `{elevation.glow}` (Mặc định tỏa ánh sáng tím nhạt bao quanh thẻ).
  - Padding bên trong: `{spacing.xl}` (32px).
  - Viền mờ: `1px solid rgba(155, 93, 224, 0.1)`.

### 4.2 Nhận diện thương hiệu & Mascot (Vùng A)
- **Logo DiveVerse:**
  - Sử dụng hình ảnh cá voi chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png).
  - Kích thước: `80px x 80px`. Căn giữa hoàn hảo phía trên thẻ.
- **Tiêu đề trang:**
  - Kiểu chữ: `{typography.display-sm}` (Manrope, 28px, weight 700, letter-spacing -0.5px).
  - Màu sắc: `{colors.text-primary}` (`#1A1A2E`).
  - Nội dung: *"Chào mừng quay lại!"*
- **Mascot Cá Voi Xanh Vũ Trụ (Bản động viên đăng nhập):**
  - Sử dụng hình ảnh cá voi chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png).
  - Kích thước: `100px` lơ lửng ngay góc trên bên phải của Thẻ biểu mẫu, vây và đuôi cong nhẹ hướng vào biểu mẫu như đang chào đón người học.

### 4.3 Các trường nhập liệu (Input Fields - Vùng B)
- **Trường nhập Email:**
  - Nhãn (Label): *"Email đăng ký *" dùng `{typography.caption}` màu `{colors.text-primary}`.
  - Hộp nhập liệu (Input Box):
    - Bo góc: `{rounded.lg}` (16px).
    - Chiều cao: `input-height` (44px).
    - Nền: `{colors.surface}` (`#FFFFFF`).
    - Viền mặc định: `1px solid rgba(155, 93, 224, 0.2)`.
    - Trạng thái Focus: Viền đổi sang màu `{colors.primary}` (`#4E56C0`), đồng thời có một lớp soft glow tỏa nhẹ xung quanh input.
    - Placeholder: *"Nhập email của bạn..."* dùng `{typography.body-sm}` màu `{colors.text-secondary}`.
- **Trường nhập Mật khẩu:**
  - Nhãn (Label): *"Mật khẩu *" dùng `{typography.caption}`.
  - Hộp nhập liệu: Tương tự trường Email nhưng ẩn ký tự (`type="password"`).
  - Icon chức năng: Đặt icon Lucide `eye` / `eye-off` ở góc phải hộp nhập liệu (Stroke 2px, kích thước 20px, màu `{colors.text-secondary}`) để cho phép học viên hiển thị/ẩn mật khẩu.
- **Liên kết "Quên mật khẩu?":**
  - **Vị trí:** Căn lề phải, ngay dưới trường nhập Mật khẩu.
  - **Đặc tả Visual:** Kiểu chữ `{typography.caption}` (12px, weight 500), màu `{colors.primary}` (`#4E56C0`). Khi hover: đổi màu sang `{colors.accent}` (`#D78FEE`) và có đường gạch chân mờ.

### 4.4 Các nút bấm hành động (Action Buttons - Vùng B)
- **Nút "Đăng nhập" (Primary CTA của Form):**
  - **Đặc tả Visual:** Nền `{colors.primary}` (`#4E56C0`), chữ màu `#FFFFFF`. Bo góc `{rounded.lg}` (16px). Chiều rộng 100% (`width: 100%`). Chiều cao tối thiểu `button-min-height` (44px).
  - **Hiệu ứng:** Mặc định có `{elevation.active-glow}`. Khi hover: kích hoạt `{elevation.hover-glow}` (Hiệu ứng tỏa sáng tím đậm), chuyển động mượt mà trong `0.2s`.
- **Đường phân cách Social Login:**
  - Một đường line nằm ngang nét mảnh màu `rgba(155, 93, 224, 0.15)` cắt đôi nhãn *"hoặc đăng nhập bằng"* ở chính giữa biểu mẫu. Nhãn dùng `{typography.caption}` màu `{colors.text-secondary}`.
- **Nút Đăng nhập bằng Google (Secondary Button):**
  - **Đặc tả Visual:** Nền trắng `{colors.surface}`, chữ màu `{colors.primary}`, viền `1px solid rgba(78, 86, 192, 0.2)`. Bo góc `{rounded.lg}` (16px). Chiều rộng 100%. Chiều cao tối thiểu `44px`.
  - **Icon:** Logo Google đa sắc căn lề trái của văn bản nút.
- **Liên kết chuyển sang trang Đăng ký:**
  - **Vị trí:** Dưới cùng của thẻ biểu mẫu, căn giữa.
  - **Đặc tả Visual:** *"Chưa có tài khoản? Đăng ký ngay"* dùng `{typography.body-sm}` (Inter, 14px). Cụm từ *"Đăng ký ngay"* được tô màu `{colors.primary}` (`#4E56C0`) và in đậm. Khi hover sẽ tỏa sáng mờ và gạch chân.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION FLOWS)
1. **Luồng xác thực thành công:**
   - Người học điền email và mật khẩu hợp lệ $\rightarrow$ Click nút "Đăng nhập".
   - Nút chuyển sang trạng thái Loading (Spinner xoay tròn ở giữa, khóa toàn bộ click).
   - Gửi yêu cầu API xác thực: `POST /api/auth/login` với dữ liệu `{ email, password }`.
   - API trả về thành công: `{ success: true, token: "jwt_token", user: { id, name, email, current_level_id } }`.
   - Hệ thống lưu Token vào LocalStorage, đồng thời lưu thông tin cấp độ hiện tại để định tuyến bài học.
   - Hiển thị Toast chúc mừng màu xanh lá `{colors.success}`: *"Đăng nhập thành công! Chào mừng quay trở lại."*.
   - Chuyển hướng mượt mà (Fade Out/Fade In) sang trang [learner_dashboard.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/learner_dashboard.md).
2. **Luồng xử lý lỗi dữ liệu nhập (Validation & API Errors):**
   - **Lỗi bỏ trống hoặc sai định dạng email:** Kiểm tra tức thì (on-blur), nếu để trống hoặc không đúng cấu hình định dạng email, viền input đổi sang màu đỏ semantic `{colors.error}` (`#EF4444`) và hiển thị text báo lỗi: *"Vui lòng nhập đúng định dạng email"*.
   - **Lỗi mật khẩu để trống:** Viền input mật khẩu báo đỏ, hiển thị: *"Mật khẩu không được để trống"*.
   - **Lỗi sai thông tin từ Server (API báo 401):** Bật một banner thông báo lỗi (Alert) dạng `{rounded.md}` ở đầu thẻ biểu mẫu, nội dung: *"Email hoặc mật khẩu không chính xác. Hãy kiểm tra lại!"*. Biểu mẫu thực hiện hiệu ứng rung nhẹ (`shake`) để báo hiệu trực quan.

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT
- **Trạng thái tải (Loading state):** Nút Đăng nhập chuyển màu xám mờ nhẹ, hiển thị loading spinner, các trường input bị khóa (`disabled`).
- **Trạng thái lỗi (Error state):** Các trường nhập liệu sai bị viền đỏ `{colors.error}` kèm hiệu ứng rung lắc nhẹ để báo hiệu cho người dùng.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [guest_landing_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/guest_landing_page.md).
- **Đi đến:** [learner_dashboard.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/learner_dashboard.md) (Sau khi đăng nhập thành công), hoặc [learner_register_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/learner_register_page.md) (Khi click "Đăng ký ngay").

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Thiết kế form cực kỳ sạch sẽ, căn giữa hoàn hảo. Phải đảm bảo touch target tối thiểu `44px` cho toàn bộ các nút bấm và liên kết để người dùng thao tác dễ dàng trên mọi thiết bị.
- **KHÔNG ĐƯỢC:** Tự ý tạo ra các modal pop-up chen ngang trong quá trình đăng nhập. Các lỗi phải được thông báo dạng văn bản inline hoặc banner cảnh báo nội tuyển ngay trên Thẻ.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Thông báo lỗi đầu vào (Validation Errors):**
  - Định dạng Email không hợp lệ: `{auth.loginErrors.emailInvalid}`
  - Mật khẩu quá ngắn: `{auth.loginErrors.passwordShort}`
  - Sai tài khoản hoặc mật khẩu: `{auth.loginErrors.credentialsIncorrect}`
