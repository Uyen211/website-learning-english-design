# MÀN HÌNH: PROFILE & STATS PAGE (MÀN HÌNH HỒ SƠ CÁ NHÂN, HỌC BẠ & CÀI ĐẶT)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Profile & Stats Page (Màn hình hồ sơ cá nhân, học bạ & cài đặt)
- Mã use case liên quan: N/A (Trang thống kê tiến trình học tập và thay đổi cấu hình tài khoản học viên)
- Mã luồng người dùng liên quan: Phân hệ hồ sơ và quản lý tài khoản cá nhân của học viên
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Dashboard -> Click Avatar -> Profile & Stats Page (URL: /profile)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này để xem thông tin hồ sơ cá nhân, theo dõi các thống kê học tập (streak, EXP, bài thi đã hoàn thành), truy cập danh sách từ vựng hay sai (Sổ tay lỗi sai), và thay đổi các thiết lập tài khoản như mật khẩu hay thông báo.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục cột kép chia tỷ lệ không đối xứng 4:8 (Split Column Layout) gồm Sidebar thông tin cá nhân bên trái và Vùng nội dung chi tiết dạng Tab bên phải.
- Các vùng chính trên màn hình:
  - Vùng A: Sidebar thông tin cá nhân (Profile Widget Sidebar) hiển thị ảnh đại diện, họ tên, email, và cấp độ hiện tại.
  - Vùng B: Thanh chuyển đổi Tab nội dung bên phải (Content Tab Switcher).
  - Vùng C: Vùng nội dung Tab Thống kê & Học bạ (Stats & Report Tab) hiển thị chỉ số EXP, biểu đồ, lịch sử thi và Sổ tay lỗi sai.
  - Vùng D: Vùng nội dung Tab Thiết lập tài khoản (Settings Tab) hiển thị form đổi mật khẩu và cấu hình nhận thông báo.
- Kích thước / Grid tham khảo:
  - Chiều rộng tối đa của nội dung: 1200px căn giữa.
  - Sidebar bên trái chiếm 4 cột, vùng tab bên phải chiếm 8 cột trên lưới 12-column.
  - Khoảng cách padding trong các thẻ: spacing-lg (24px).
  - Khoảng cách dọc giữa các phần: spacing-xl (32px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)

### FIXED SIDEBAR (VÙNG A)
- **Tên component:** Ảnh đại diện học viên (Avatar Uploader)
  - **Loại component tham chiếu từ DESIGN.md:** rounded-full (ảnh tròn đường kính 100px)
  - **Vị trí:** Vùng A, trên cùng Sidebar.
  - **Trạng thái:** Mặc định. Khi rê chuột qua hiển thị icon máy ảnh đè lên để tải ảnh mới.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị ảnh đại diện hiện tại của học viên.

- **Tên component:** Thông tin định danh & Cấp độ
  - **Loại component tham chiếu từ DESIGN.md:** title-md (font Inter 18px, weight 600, màu ink #0a0a0a)
  - **Vị trí:** Vùng A, dưới avatar.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** 
    - Họ tên: "Nguyễn Văn A".
    - Email: "nguyenvana@gmail.com".
    - Badge Cấp độ: `badge-pill` màu brand-peach (#ffb084) ghi "Cơ bản (A1 - A2)".

---

### TABS & CONTENT AREA (VÙNG B, C & D)
- **Tên component:** Thanh Tab điều hướng (Tab Switcher)
  - **Loại component tham chiếu từ DESIGN.md:** category-tab / tab-bar (nền canvas #fffaf0, rounded-lg)
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hai tab: "Thống kê & Học bạ" (active, nền surface-card #f5f0e0), "Cài đặt tài khoản" (trong suốt). Học viên click tab để chuyển đổi nội dung hiển thị Vùng C hoặc Vùng D.

#### 1. TAB THỐNG KÊ & HỌC BẠ (VÙNG C)
- **Tên component:** Thẻ chỉ số tích lũy (Stats Cards Grid)
  - **Loại component tham chiếu từ DESIGN.md:** grid 3-up (3 thẻ nhỏ song song)
  - **Vị trí:** Vùng C, trên cùng.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** 
    - Thẻ 1 (Ochre): Icon cúp vàng, hiển thị "1,250 EXP tích lũy".
    - Thẻ 2 (Peach): Icon ngọn lửa, hiển thị "Streak: 12 ngày học liên tiếp".
    - Thẻ 3 (Lavender): Icon đồng hồ, hiển thị "Thời gian học: 24.5 giờ".

- **Tên component:** Lịch sử bài thi (Study History Table)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền canvas #fffaf0, rounded-lg 16px, padding 20px)
  - **Vị trí:** Vùng C, ở giữa.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Bảng hiển thị danh sách các bài thi đã làm gồm: Tên bài thi, Thang điểm, Ngày thi, Kết quả (Đạt/Chưa đạt), và liên kết "Xem chi tiết" dẫn sang Test Result Page (LN-11).

- **Tên component:** Sổ tay lỗi sai (Error Memory list)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền surface-card #f5f0e0, border 1px hairline #e5e5e5, rounded-lg 16px, padding 20px)
  - **Vị trí:** Vùng C, dưới cùng.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Danh sách các từ vựng hoặc cấu trúc ngữ pháp hay bị làm sai nhiều lần trong quá trình học và làm bài thi. Đầu mỗi dòng có nút "Luyện lại nhanh" để mở phiên ôn tập SRS riêng cho từ đó.

#### 2. TAB THIẾT LẬP TÀI KHOẢN (VÙNG D)
- **Tên component:** Form đổi mật khẩu (Change Password Form)
  - **Loại component tham chiếu từ DESIGN.md:** vertical form (các trường xếp dọc)
  - **Vị trí:** Vùng D.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Các trường nhập liệu: "Mật khẩu hiện tại", "Mật khẩu mới", "Nhập lại mật khẩu mới" dạng `text-input` (nền canvas #fffaf0, height 44px, bo góc rounded-md 12px, 1px hairline).

- **Tên component:** Nút "Lưu cài đặt"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, height 44px, rounded-md 12px)
  - **Vị trí:** Vùng D, dưới cùng form.
  - **Trạng thái:** Mặc định, hover, loading.
  - **Dữ liệu hiển thị / hành vi:** Nhấp chuột để gửi yêu cầu lưu thay đổi mật khẩu và thiết lập tài khoản.

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Click chuyển đổi các Tab điều hướng ở Vùng B**
  - **Luồng chính:** Học viên click tab "Cài đặt tài khoản" -> Vùng C (Thống kê) ẩn đi -> Vùng D (Thiết lập) hiển thị mượt mà. Click lại tab "Thống kê" -> Vùng D ẩn, Vùng C hiện.
- **Hành động: Điền form đổi mật khẩu và click "Lưu cài đặt"**
  - **Luồng chính:**
    1. Học viên điền đầy đủ mật khẩu cũ, mật khẩu mới (>=6 ký tự) và xác nhận trùng khớp.
    2. Click nút "Lưu cài đặt".
    3. Nút hiển thị Loading -> Gửi yêu cầu API POST cập nhật mật khẩu.
    4. API cập nhật thành công.
    5. Hiển thị Toast thông báo thành công màu xanh lá ở góc trên bên phải: "Cập nhật tài khoản thành công!".
  - **Luồng con / rẽ nhánh (Thông tin sai lệch):** Điền thiếu hoặc mật khẩu nhập lại không khớp -> Báo đỏ viền ô nhập bị lỗi, hiển thị text đỏ: "Mật khẩu xác nhận không trùng khớp!".
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: `POST /api/user/update-profile` (payload: `{ "oldPassword": "...", "newPassword": "..." }`)
    - Nhận về: `{ "success": true }`

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Khi Sổ tay lỗi sai trống -> Hiển thị hình vẽ 3D mascot Cá Voi Xanh nhỏ cười lớn kèm dòng chữ: "Sổ tay lỗi sai trống! Bạn đang làm rất tốt, hãy tiếp tục phát huy!".
- **Trạng thái tải (loading state):** Khi đang lưu cài đặt tài khoản, nút Lưu hiển thị spinner và khóa click.
- **Trạng thái lỗi (error state):** API đổi mật khẩu báo sai mật khẩu hiện tại -> Báo đỏ viền ô mật khẩu hiện tại và hiện text lỗi đỏ: "Mật khẩu hiện tại không chính xác!".

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ Learner Dashboard (LN-01) hoặc bất kỳ trang nào có Top Nav sau khi học viên nhấp chọn Avatar cá nhân và chọn mục "Hồ sơ & Học bạ".
- **Sau khi hoàn thành hành động, đi đến màn hình nào?**
  - Chuyển sang Test Result Page (LN-11) khi bấm xem chi tiết một kết quả thi trong bảng lịch sử thi.
  - Quay trở lại Dashboard (LN-01) khi click tab Dashboard ở Top Nav.
- **Các màn hình liên quan khác:** LN-11, LN-01.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0) đặc trưng.
- Bố cục bất đối xứng 4:8 giúp phân bổ thông tin hợp lý: cột bên trái thể hiện nhanh chân dung học viên, cột bên phải dành cho các dữ liệu bảng biểu và biểu mẫu dài (tránh gây mỏi mắt, quá tải nhận thức).
- Lưới thẻ Stats Cards Grid dùng các màu sắc thương hiệu của Clay: Ochre (#e8b94a), Peach (#ffb084), Lavender (#b8a4ed) nhạt để làm nổi bật các chỉ số cột mốc học tập.
- Các trường nhập liệu và nút bấm có chiều cao 44px đạt chuẩn touch target.
- Viền hairline 1px (#e5e5e5) nhẹ nhàng ngăn cách giữa các khối.



