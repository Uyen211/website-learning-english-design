# MÀN HÌNH: GUEST LANDING PAGE (TRANG CHỦ GIỚI THIỆU)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Guest Landing Page (Trang chủ giới thiệu)
- **Mã use case liên quan:** N/A (Trang tiếp thị giới thiệu sản phẩm cho khách truy cập)
- **Mã luồng người dùng liên quan:** LN-FL-01 (Xác thực tài khoản người học)
- **Vai trò người dùng:** Guest (Khách vãng lai chưa đăng nhập)
- **Vị trí trong sitemap:** Trang chủ (URL: `/`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Giới thiệu phương pháp học tiếng Anh đột phá của DiveVerse (quy nạp tự nhiên, hỗ trợ AI cá nhân hóa theo ZPD) và cấu trúc 3 cấp độ học tập (Basic A1-A2, Intermediate B1-B2, Advanced C1-C2) ánh xạ trực tiếp chuẩn điểm thi quốc tế (IELTS từ 3.0 đến 9.0; TOEIC từ 100 đến 990). Từ đó, thuyết phục và dẫn dắt người dùng đăng nhập hoặc đăng ký tài khoản mới để bắt đầu lộ trình học tập.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục cuộn dọc nhiều phân vùng (Multi-section Vertical Scrolling Layout) có chiều rộng nội dung tối đa là `1200px` (`max-content-width`).
- **Màu sắc nền tảng:** Nền trang tổng thể sử dụng `{colors.canvas}` (`#F9F7FE`). Nền điểm xuyết các chòm sao vector mờ nét mảnh `0.5px` và các chấm sao ngẫu nhiên `1-3px` phát sáng để tạo không gian vũ trụ ánh sáng bồng bềnh.
- **Khoảng cách dọc giữa các phân vùng:** `{spacing.section}` (96px).
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Top Bar (Thanh điều hướng cố định)**
    - Chiều cao cố định: `nav-height` (64px). Ghim cố định ở đầu màn hình khi cuộn.
  - **Zone 2: Hero Section (Khu vực thu hút chính)**
    - Lưới chia 2 cột (Desktop 7:5, chuyển thành 1 cột dọc trên Mobile). Nền phủ lớp radial gradient `{gradients.atmosphere-haze}`.
  - **Zone 3: Lộ trình & Thang điểm quốc tế (Level & Target Mapping Grid)**
    - Lưới 3 cột giới thiệu cấu trúc 3 cấp độ học tập dựa theo `level_built.md`.
  - **Zone 4: Quy trình học tập 6 giai đoạn (6-Stage Learning Process Showcase)**
    - Vùng bố cục ngang trực quan hóa các bước học từ vựng/ngữ pháp (UC-05a, UC-05b) giúp người dùng hiểu phương pháp học của hệ thống.
  - **Zone 5: CTA Band (Thẻ kêu gọi hành động cuối trang)**
    - Một thẻ card lớn nằm ngang căn giữa, nền dải màu `{gradients.morning-nebula}`.
  - **Zone 6: Footer (Chân trang dark mode thư giãn)**
    - Sử dụng nền tối màu `{colors.dark-floor}` (`#1C1B2E`) làm điểm dừng nghỉ cho mắt.

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh điều hướng đầu trang (Top Navigation)
- **Cấu trúc & Định vị:** Vùng 1, ghim cố định (`position: sticky; top: 0; z-index: 100`).
- **Đặc tả Visual:**
  - Nền: Kính mờ `{colors.glass}` (`rgba(255, 255, 255, 0.7)`), thuộc tính `backdrop-filter: blur(8px)`.
  - Viền dưới: `1px solid rgba(155, 93, 224, 0.1)`. Chiều cao: `64px`.
- **Các phần tử bên trong:**
  - **Logo DiveVerse:** Sử dụng tệp ảnh cá voi chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) kích thước `36px x 36px` căn lề trái, bên cạnh là chữ "DiveVerse" dạng `{typography.title-lg}` (Inter, 24px, weight 600, màu `{colors.text-primary}`).
  - **Liên kết điều hướng:** Gồm các nút "Khám phá", "Lộ trình", "Cấp độ", "Tính năng". Font `{typography.body-md}`, màu `{colors.text-secondary}` (`#5A5A7A`). Di chuột qua sẽ đổi màu sang `{colors.primary}` (`#4E56C0`) kèm vạch kẻ chân mờ.
  - **Nút "Đăng nhập":** Kiểu chữ `{typography.button}`, màu `{colors.primary}`. Touch target tối thiểu `44px`.
  - **Nút "Đăng ký du hành" (Primary CTA):** Nền `{colors.primary}` (`#4E56C0`), chữ trắng. Bo góc `{rounded.lg}` (16px). Chiều cao tối thiểu `44px`. Có `{elevation.active-glow}` mặc định, di chuột qua kích hoạt `{elevation.hover-glow}`.

### 4.2 Khu vực Hero (Hero Section)
- **Đặc tả Visual:** Vùng 2. Nền phủ dải màu radial `{gradients.atmosphere-haze}` mượt mà.
- **Các phần tử bên trong:**
  - **Tiêu đề Hero (Hero Headline):**
    - Kiểu chữ: `{typography.display-xl}` (Manrope, 64px, weight 700, letter-spacing -2px).
    - Màu sắc: `{colors.text-primary}`.
    - Nội dung: *"Bơi vào vũ trụ ngôn ngữ theo cách tự nhiên nhất"*
  - **Đoạn mô tả phụ:**
    - Kiểu chữ: `{typography.body-md}` (Inter, 16px, line-height 1.6). Màu `{colors.text-secondary}`.
    - Nội dung: *"Đắm mình vào Anh ngữ thông qua ngữ cảnh thực tế. Cấu trúc lộ trình học tương tác chuẩn quốc tế kết hợp trợ lý AI sửa lỗi 2 vòng giúp bạn tự tin đạt mốc IELTS 3.0 - 9.0 và TOEIC 100 - 990."*
  - **Nút hành động chính (Hero Primary CTA - "Bắt đầu học ngay"):**
    - Kiểu: Nút lớn độc tôn, bo góc `{rounded.lg}` (16px), nền `{colors.primary}` (`#4E56C0`), chữ trắng.
    - Hiệu ứng: Default `{elevation.active-glow}`, hover `{elevation.hover-glow}` (tỏa quầng sáng tím rực rỡ `box-shadow: 0 0 32px rgba(215, 143, 238, 0.4)`), tự động phóng to nhẹ `scale(1.02)` trong `0.2s`.
  - **Mascot Cosmic Blue Whale (Phiên bản Hero):**
    - **Hình ảnh:** Sử dụng hình ảnh cá voi chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png).
    - **Kích thước:** Chiều rộng `160px`.
    - **Vị trí:** Cột bên phải, lơ lửng chuyển động nhún nhảy chậm (`floating keyframe`). Bụng chú cá voi phát sáng màu hồng nhạt `{colors.light-accent}`.

### 4.3 Phân vùng Cấp độ & Thang điểm quốc tế (Level Mapping Grid)
- **Cấu trúc & Định vị:** Vùng 3. Thiết kế lưới 3 cột ngang tương ứng với 3 cấp độ học tập chi tiết trong `level_built.md`.
- **Đặc tả Visual của mỗi thẻ cấp độ (Level Cards):**
  - Nền: `{colors.surface}` (`#FFFFFF`), bo góc `{rounded.xl}` (24px), viền mờ `1px solid rgba(155, 93, 224, 0.1)`, nâng độ cao bằng `{elevation.glow}`. Hover nâng card nhẹ lên và viền đổi màu sang `{colors.accent}`.
- **Nội dung hiển thị chi tiết (theo level_built.md):**
  - **Cột 1: Cấp độ Basic (A1 - A2)**
    - Tên cấp độ: *"Cấp độ Basic (A1-A2) - Giao tiếp sinh tồn"*
    - Thang điểm mục tiêu: **IELTS Target: 3.0 - 3.5 | TOEIC Target: 100 - 540**.
    - Cấu trúc: 25 Units (100 Lessons) | Tích lũy ~2,000 từ vựng.
    - Chủ điểm chính: Chào hỏi, thói quen hàng ngày, quá khứ đơn (Past Simple), dự định tương lai (Will vs Going to), động từ khuyết thiếu cơ bản (Can, Should).
  - **Cột 2: Cấp độ Intermediate (B1 - B2)**
    - Tên cấp độ: *"Cấp độ Intermediate (B1-B2) - Làm việc độc lập"*
    - Thang điểm mục tiêu: **IELTS Target: 5.5 - 6.5 | TOEIC Target: 550 - 940**.
    - Cấu trúc: 35 Units (140 Lessons) | Tích lũy ~6,000 từ vựng.
    - Chủ điểm chính: Phrasal verbs, câu bị động, câu điều kiện loại 1, 2, 3 và hỗn hợp, mệnh đề quan hệ, reported speech, câu chẻ (Cleft sentences).
  - **Cột 3: Cấp độ Advanced (C1 - C2)**
    - Tên cấp độ: *"Cấp độ Advanced (C1-C2) - Chuyên gia học thuật"*
    - Thang điểm mục tiêu: **IELTS Target: 7.5 - 9.0 | TOEIC Target: 945 - 990**.
    - Cấu trúc: 40 Units (160 Lessons) | Tích lũy ~10,000+ từ vựng & Collocations học thuật.
    - Chủ điểm chính: Đảo ngữ nâng cao, danh từ hóa (Nominalisation), rào đón ngôn từ (Hedging language), tư duy phản biện sâu, ngôn ngữ học, vật lý lượng tử đơn giản.

### 4.4 Quy trình học tập 6 giai đoạn (6-Stage Process Showcase)
- **Cấu trúc & Định vị:** Vùng 4. Bố cục chuỗi nằm ngang thể hiện hành trình học quy nạp tự nhiên (UC-05a, UC-05b):
  1. *Làm quen ngữ cảnh (Contextual Guessing):* Đọc ví dụ, nghe âm thanh bản xứ để đoán nghĩa.
  2. *Giải mã chi tiết (Explicit Decoding):* Xem IPA, định nghĩa, collocations, sắc thái từ (Register/Nuance).
  3. *Thực hành tương tác (Active Practice):* Flashcard SRS kéo thả, Collocation Prediction.
  4. *Ghi nhớ vận động (Dictation):* Nghe và gõ lại để khắc sâu trí nhớ âm thanh.
  5. *Tự sản sinh câu (Personalized Production):* Tự đặt câu bám sát đời sống thực tế cá nhân.
  6. *Sửa lỗi bằng AI (ZPD AI Feedback):* Trợ lý AI phân tích, chỉ ra lỗi và hướng dẫn sửa lại qua 2 vòng gợi ý.

### 4.5 Thẻ kêu gọi hành động cuối trang (CTA Band)
- **Đặc tả Visual:** Vùng 5.
  - Nền: Dải gradient `{gradients.morning-nebula}`. Bo góc `{rounded.xxl}` (32px).
  - Hiệu ứng phát sáng: `{elevation.hover-glow}`. Padding: `{spacing.xxl}` (48px).
- **Nội dung:**
  - Tiêu đề: *"Sẵn sàng đắm mình vào vũ trụ tiếng Anh?"* dạng `{typography.display-md}`.
  - Phụ đề: *"Cá Voi Xanh đang đợi bạn ở trạm hành trình tiếp theo."*
  - **Mascot:** Sử dụng hình ảnh cá voi chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) kích thước `180px` nhún nhảy chậm bên cạnh tên lửa nhỏ cách điệu vector mờ.
  - Nút bấm: *"Đăng ký du hành ngay"* nền trắng `{colors.surface}`, chữ màu `{colors.primary}`, bo góc `{rounded.lg}` (16px), có soft glow.

### 4.6 Chân trang (Footer)
- **Đặc tả Visual:** Vùng 6, chân trang tối màu `{colors.dark-floor}` (`#1C1B2E`) điểm xuyết tinh vân mờ.
- **Nội dung:** Các liên kết sản phẩm, điều khoản, logo thu nhỏ và dòng bản quyền.

---

## 5. CHI TIẾT TƯƠNG TÁC & CHUYỂN TRANG
- **Hành động: Click vào bất kỳ nút Đăng ký / Bắt đầu ngay**
  - Chuyển hướng mượt mà (Fade Out/Fade In trong `0.3s`) đến [learner_register_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/learner_register_page.md).
- **Hành động: Click vào nút Đăng nhập**
  - Chuyển hướng mượt mà đến [learner_login_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/learner_login_page.md).
- **Hành động: Di chuột (Hover) qua các thẻ cấp độ (Level Cards)**
  - Thẻ tịnh tiến lên trên `translateY(-4px)` nhẹ nhàng, tăng độ rộng phát sáng của viền từ `{elevation.glow}` lên `{elevation.hover-glow}`.

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT
- **Trạng thái tải trang (Loading State):** Hiển thị màn hình chờ màu `{colors.canvas}` với một chú Cá Voi Xanh nhỏ xoay tròn phát sáng.
- **Trạng thái hiển thị Responsive:**
  - **Mobile:** Menu trên Nav chuyển thành nút hamburger mở panel trượt kính mờ (`{elevation.glass}`) từ bên phải sang. Lưới cấp độ chuyển thành dạng vuốt ngang (carousel slide) tiện lợi.

## 7. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Sử dụng tối đa các mã biến token (ví dụ: `var(--color-primary)`) thay vì nhập trực tiếp mã màu hex. Đảm bảo khoảng trắng xung quanh các card lớn cực kỳ rộng rãi.
- **KHÔNG ĐƯỢC:** Sử dụng đổ bóng xám/đen vật lý. Mọi đổ bóng bắt buộc phải đổi sang dạng dải màu phát sáng (glow) sắc tím/hồng nhạt có độ đục (alpha) thấp như quy chuẩn của hệ thống DiveVerse.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Thống kê hệ thống (Stats Counters):** Liên kết với danh sách `landingPage.stats` (các cặp `{value}` và `{label}`).
- **Các tính năng nổi bật (Features Showcase):** Liên kết với danh sách `landingPage.features` (các trường `{title}`, `{desc}`, `{icon}`).
- **Nhận xét từ học viên (Testimonials):** Liên kết với danh sách `landingPage.testimonials` (các trường `{name}`, `{role}`, `{quote}`, `{avatar}`).
- **Danh mục các Cấp độ (Levels mapping):** Liên kết với mảng `levels` chứa thông tin của `level_basic`, `level_intermediate` và `level_advanced` (các trường `{name}`, `{shortDescription}`, `{ieltsTarget}`, `{toeicTarget}`, `{maxUnits}`).
