# MÀN HÌNH: PROFILE & STATS PAGE (MÀN HÌNH HỒ SƠ CÁ NHÂN, HỌC BẠ & CÀI ĐẶT)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Profile & Stats Page (Màn hình hồ sơ cá nhân, học bạ & cài đặt)
- **Mã use case liên quan:** N/A (Trang thống kê tiến trình học tập và thay đổi cấu hình tài khoản học viên)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Dashboard $\rightarrow$ Click Avatar ở Top Nav $\rightarrow$ Profile & Stats Page (URL: `/profile`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này để quản lý toàn bộ hồ sơ cá nhân, theo dõi các chỉ số học tập tích lũy (streak học tập, điểm EXP, tổng thời gian rèn luyện), xem bảng lịch sử thi đánh giá năng lực kèm liên kết tới trang chi tiết kết quả, ôn tập nhanh danh sách từ vựng hay làm sai (Sổ tay lỗi sai), và cập nhật cấu hình tài khoản (đổi mật khẩu bảo mật).

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục cột kép chia tỷ lệ bất đối xứng 4:8 (Split Column Layout) gồm Sidebar thông tin cá nhân bên trái và Vùng nội dung chi tiết dạng Tab bên phải để tối ưu hóa khả năng đọc và giảm thiểu quá tải nhận thức.
- **Màu nền chung:** Nền trang chính sử dụng tông màu `{colors.canvas}` (`#F9F7FE`) phối hợp dải chuyển màu sương mờ `{gradients.atmosphere-haze}`. Cạnh dưới cùng của trang sử dụng nền tối `{colors.dark-floor}` (`#1C1B2E`) làm footer nghỉ mắt.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Left Profile Sidebar (Vùng A - chiếm 4 cột):** Hiển thị ảnh đại diện dạng tròn, họ tên, email, và thẻ cấp độ học hiện tại.
  - **Zone 2: Content Tab Switcher (Vùng B - chiếm 8 cột, phía trên bên phải):** Thanh chuyển đổi Tab dạng pill.
  - **Zone 3: Tab Content Area (Vùng C & D - chiếm 8 cột, phía dưới bên phải):** Hiển thị động Tab "Thống kê & Học bạ" hoặc Tab "Cài đặt tài khoản".
- **Kích thước tham khảo:**
  - Chiều rộng tối đa của nội dung: `1140px` căn giữa.
  - Khoảng cách giữa hai cột chính: `{spacing.xl}` (32px).
  - Padding trong các thẻ card: `{spacing.lg}` (24px).

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Cột Sidebar Thông Tin Cá Nhân (Left Profile Sidebar - Vùng A)
- **Đặc tả Visual:**
  - Nền Sidebar: `{colors.surface}` (`#FFFFFF`). Bo góc lớn: `{rounded.xl}` (24px).
  - Viền mờ: `1px solid rgba(155, 93, 224, 0.1)`. Padding: `{spacing.lg}` (24px).
  - Hiệu ứng nâng: `{elevation.glow}` (soft glow nhẹ).
- **Thành phần bên trong:**
  - **Ảnh đại diện học viên (Avatar Uploader):**
    - Thiết kế: Dạng tròn hoàn hảo `{rounded.full}` (50%), đường kính `100px`.
    - Hành vi: Khi rê chuột (hover) qua ảnh đại diện, xuất hiện một lớp phủ màu bán trong suốt màu tím `{colors.primary}` ở mức 40% opacity đè lên kèm icon Tải lên nhỏ (Lucide `upload`) màu trắng ở tâm để học viên tải ảnh đại diện mới lên.
  - **Thông tin định danh:**
    - Họ tên: Dạng `{typography.title-lg}` (24px, Manrope, weight 700), màu `{colors.text-primary}`. Ví dụ: *"Nguyễn Văn A"*.
    - Email: Dạng `{typography.body-sm}` (14px, Inter, weight 400), màu `{colors.text-secondary}`. Ví dụ: *"nguyenvana@gmail.com"*.
  - **Badge Cấp độ hiện tại:**
    - Style: Dạng viên thuốc `{rounded.pill}`, nền nhạt `{colors.light-accent}` (`#FDCFFA`), chữ màu `{colors.primary}` (`#4E56C0`).
    - Nội dung: *"Basic (A1 - A2)"* (lấy thông tin từ lộ trình trong `level_built.md`).

### 4.2 Thanh chuyển đổi Tab (Content Tab Switcher - Vùng B)
- **Đặc tả Visual:**
  - Nền thanh tab: `{colors.glass}` (`rgba(255, 255, 255, 0.7)`), bo tròn `{rounded.pill}`, cao `48px`.
  - Có 2 tab: *"Thống kê & Học bạ"* và *"Cài đặt tài khoản"*.
- **Hành vi chuyển đổi:**
  - Tab đang hoạt động (Active): Nền đổi sang `{colors.surface}`, chữ màu `{colors.primary}` (weight 600) kèm hiệu ứng phát sáng nhẹ `{elevation.glow}`.
  - Tab không hoạt động: Nền trong suốt, chữ màu `{colors.text-secondary}`. Hover vào tab sẽ đổi chữ sang màu `{colors.accent}` (`#D78FEE`).

### 4.3 Tab Thống kê & Học bạ (Stats & Report Tab - Vùng C)
*Hiển thị mặc định khi học viên truy cập trang:*
- **Lưới chỉ số tích lũy (Stats Cards Grid):**
  - Gồm 3 thẻ nhỏ xếp ngang song song, bo góc `{rounded.lg}` (16px), nền `{colors.surface}`, viền mờ `1px solid rgba(155, 93, 224, 0.1)`.
  - **Thẻ 1 (Tích lũy EXP):** Hiển thị icon Cúp vàng (Lucide `trophy`) màu `{colors.warning}`, text *"1,250 EXP tích lũy"*.
  - **Thẻ 2 (Chuỗi ngày - Streak):** Hiển thị icon Ngọn lửa (Lucide `flame`) màu `{colors.error}` nhấp nháy, text *"Streak: 12 ngày liên tiếp"*.
  - **Thẻ 3 (Thời gian học):** Hiển thị icon Lịch (Lucide `calendar`) màu `{colors.secondary}`, text *"Học: 24.5 giờ"*.
- **Bảng lịch sử bài thi (Study History Table):**
  - Loại component: `product-mockup-card` nền `{colors.surface}`, bo góc `{rounded.xl}` (24px), viền mờ, padding `{spacing.lg}` (24px).
  - Nội dung: Bảng hiển thị danh sách các bài thi đã làm gồm:
    - *Tên bài thi:* ví dụ *"Mini-exam cuối Unit 4"* hoặc *"IELTS Mock Test 1"*.
    - *Điểm số / Thang điểm:* ví dụ *"85/100 EXP"* hoặc *"6.5 IELTS"*.
    - *Ngày hoàn thành:* ví dụ *"24-05-2026"*.
    - *Kết quả:* Tag đạt màu `{colors.success}` ("Đạt") hoặc tag chưa đạt màu `{colors.error}` ("Chưa đạt").
    - *Liên kết chi tiết:* Chữ màu `{colors.primary}` ghi *"Xem chi tiết"*, bấm vào sẽ chuyển hướng sang trang kết quả thi [test_result_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/test_result_page.md).
- **Sổ tay lỗi sai (Error Memory List):**
  - Loại component: Nền `{colors.surface}`, bo góc `{rounded.xl}` (24px), viền mờ, padding `{spacing.lg}` (24px).
  - Nội dung: Danh sách 5 từ vựng hoặc cấu trúc ngữ pháp bị làm sai nhiều nhất trong các bài thi và luyện tập.
  - Mỗi dòng hiển thị: Từ vựng, phiên âm IPA, số lần làm sai (ví dụ: *Sai 4 lần* dạng chữ đỏ `{colors.error}`).
  - Nút hành động đầu dòng: Nút "Luyện lại nhanh" style `button-secondary` cao `36px` để kích hoạt nhanh phiên ôn tập SRS riêng lẻ cho từ đó.

### 4.4 Tab Thiết lập tài khoản (Settings Tab - Vùng D)
- **Form đổi mật khẩu (Change Password Form):**
  - Thiết kế dạng Vertical Form xếp dọc, bao gồm các trường:
    - *Mật khẩu hiện tại*
    - *Mật khẩu mới*
    - *Nhập lại mật khẩu mới*
  - Mỗi trường nhập liệu là một `text-input` dạng mật khẩu (ẩn chữ), cao `44px`, bo góc `{rounded.lg}` (16px), nền `{colors.canvas}`.
- **Thông báo lỗi xác thực trực quan (Form Validation Errors):**
  - Nếu mật khẩu mới dưới 6 ký tự $\rightarrow$ Trường báo đỏ viền màu `{colors.error}` kèm dòng chữ lỗi đỏ: *"Mật khẩu mới phải đạt tối thiểu 6 ký tự!"*.
  - Nếu nhập lại mật khẩu không trùng khớp $\rightarrow$ Trường nhập lại báo đỏ kèm dòng chữ lỗi: *"Mật khẩu xác nhận không trùng khớp!"*.
- **Nút "Lưu cài đặt":**
  - Style `button-primary` nền `{colors.primary}` (`#4E56C0`), chữ trắng, cao `44px`, bo góc `{rounded.lg}`.
  - Hiệu ứng: `{elevation.active-glow}`. Hover tỏa sáng `{elevation.hover-glow}`.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Click chuyển đổi các Tab điều hướng**
  - Học viên click tab *"Cài đặt tài khoản"* $\rightarrow$ Vùng C (Thống kê) ẩn mượt mà $\rightarrow$ Vùng D (Thiết lập) hiện ra. Thời gian chuyển động (transition) mượt `0.3s ease-in-out`.
- **Hành động: Nộp form đổi mật khẩu**
  - Học viên điền đầy đủ thông tin $\rightarrow$ Bấm "Lưu cài đặt" $\rightarrow$ Nút chuyển sang trạng thái Loading (spinner xoay mờ, khóa click) $\rightarrow$ Gửi API cập nhật $\rightarrow$ Thành công $\rightarrow$ Hiển thị Toast thông báo màu xanh lá `{colors.success}`: *"Đã cập nhật mật khẩu mới thành công!"*.
  - **API Đổi mật khẩu:** `POST /api/user/update-profile`
    - Payload: `{ "oldPassword": "...", "newPassword": "..." }`
    - Response: `{ "success": true }`

---

## 6. CÁC TRẠNG THÁI ĐẶP BIỆT (SPECIAL STATES)
- **Trạng thái Sổ tay lỗi sai trống (Empty State):**
  - Khi học viên chưa có lỗi sai nào ghi nhận trong học bạ $\rightarrow$ Sổ tay lỗi sai hiển thị khối Empty State thiết kế đẹp mắt.
  - Hình ảnh: Chú Cá Voi Vũ Trụ [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`140px x 140px`) đang cười lớn vui vẻ, vây quanh là các ngôi sao lấp lánh.
  - Dòng chữ: *"Tuyệt vời! Sổ tay lỗi sai hiện tại đang trống. Bạn đang làm rất tốt, hãy tiếp tục duy trì phong độ này nhé!"* dạng `{typography.body-md}` màu `{colors.text-secondary}`.
- **Trạng thái tải trang (Loading State):** Khi đang tải dữ liệu lịch sử thi và các chỉ số tích lũy, hiển thị skeleton loading mờ che phủ bảng và lưới chỉ số.

---

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** Bất kỳ trang nào có thanh điều hướng Top Nav sau khi học viên nhấp chuột vào ảnh Avatar đại diện cá nhân ở góc phải và chọn mục *"Hồ sơ & Học bạ"*.
- **Đi đến:**
  - [test_result_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/test_result_page.md) khi học viên bấm vào liên kết "Xem chi tiết" của một kết quả thi trong bảng lịch sử bài thi.
  - [srs_review_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/srs_review_page.md) khi học viên click nút "Luyện lại nhanh" một từ vựng hay sai trong Sổ tay lỗi sai.

---

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Đảm bảo bố cục Split Column 4:8 co giãn tốt trên mọi độ phân giải màn hình. Trên di động, Sidebar sẽ tự động trượt lên trên cùng và thu hẹp chiều cao thành một thẻ ngang nhỏ gọn để nhường đất diễn cho các tab chi tiết bên dưới.
- **KHÔNG ĐƯỢC:** Sử dụng bóng đổ đen đập vào mắt người dùng. Mọi thẻ bài và sidebar đều phải sử dụng hiệu ứng phát sáng mờ `{elevation.glow}` với sắc tím nhạt để tạo bầu không khí vũ trụ sương mờ trong trẻo của DiveVerse.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Hồ sơ cá nhân & Thống kê tích lũy (User Settings & Profile):** Liên kết trực tiếp với đối tượng `profile`, bao gồm:
  - Họ và tên học viên: `{profile.name}`
  - Email cá nhân: `{profile.email}`
  - Cấp độ hiện tại: `{profile.level}`
  - EXP tích lũy: `{profile.stats.exp}`
  - Số ngày học liên tục (Streak): `{profile.stats.streak}`
  - Số giờ học tích lũy: `{profile.stats.studyHours}`
