# MÀN HÌNH: ADD / EDIT LEVEL MODAL (HỘP THOẠI THÊM/SỬA CẤP ĐỘ HỌC)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Add / Edit Level Modal (Hộp thoại thêm/sửa cấp độ học)
- **Mã use case liên quan:** UC-01a, UC-01b
- **Mã luồng người dùng liên quan:** Flow AD-FL-01 (Quản lý Cấp độ)
- **Vai trò người dùng:** Admin (Quản trị viên)
- **Vị trí trong sitemap:** Trang chủ quản trị $\rightarrow$ AD-01: Level List Page $\rightarrow$ Modal AD-01-M1 (Thêm mới) / AD-01-M2 (Chỉnh sửa)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng hộp thoại nổi đè lên màn hình này để nhập thông tin thiết lập cho một cấp độ học mới (lộ trình mới), hoặc chỉnh sửa các thông số hiện tại của một cấp độ học đã tồn tại trong hệ thống.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Hộp thoại lớp phủ căn giữa hoàn toàn (Centered Modal Overlay) đè lên giao diện màn hình danh sách cấp độ học `AD-01`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Overlay Backdrop (Vùng A):** Lớp nền tối mờ che phủ toàn màn hình phía sau.
  - **Zone 2: Modal Header (Vùng B):** Tiêu đề hộp thoại và nút đóng nhanh (X) ở góc phải trên.
  - **Zone 3: Form Body (Vùng C):** Thân hộp thoại chứa biểu mẫu nhập liệu các trường dọc một cột.
  - **Zone 4: Modal Actions Footer (Vùng D):** Chân hộp thoại chứa cặp nút Lưu/Hủy căn lề phải.
- **Kích thước tham khảo:**
  - Chiều rộng cố định của hộp thoại: `600px`.
  - Chiều cao tự động co giãn theo nội dung, có hỗ trợ thanh cuộn dọc (scrollable body) nếu màn hình nhỏ.
  - Khoảng cách padding trong modal: `{spacing.xl}` (32px).
  - Khoảng cách dọc giữa các trường nhập liệu: `{spacing.md}` (16px).

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Lớp nền tối mờ (Overlay Backdrop - Vùng A)
- **Đặc tả Visual:**
  - Nền overlay: Tông màu tối `{colors.dark-floor}` (`#1C1B2E`) ở mức `50%` opacity làm backdrop.
  - Hiệu ứng: `backdrop-filter: blur(8px)` để tạo cảm giác kính mờ xuyên thấu các vì sao lấp lánh của màn hình bên dưới.
  - Hành vi: Nhấp chuột ra ngoài vùng hộp thoại sẽ đóng modal tương tự nút "Hủy".

### 4.2 Thẻ Modal chính & Tiêu đề (Modal Container & Header - Vùng B)
- **Đặc tả Visual:**
  - Nền hộp thoại: `{colors.surface}` (`#FFFFFF`).
  - Bo góc lớn: `{rounded.xl}` (24px).
  - Viền mờ: `1px solid rgba(155, 93, 224, 0.15)`.
  - Hiệu ứng nâng: `{elevation.hover-glow}` (glow phát quang mạnh).
- **Tiêu đề:**
  - Dạng chữ `{typography.title-lg}` (24px, Manrope, weight 700), màu `{colors.text-primary}`.
  - Hiển thị: *"Thêm cấp độ học mới"* (đối với Modal thêm) hoặc *"Chỉnh sửa cấp độ học"* (đối với Modal sửa).

### 4.3 Thân biểu mẫu nhập liệu (Form Body - Vùng C)
Các trường nhập liệu đều dạng `text-input`, chiều cao `44px`, bo góc `{rounded.lg}` (16px), nền `{colors.canvas}` (`#F9F7FE`). Viền mặc định `1px solid rgba(155, 93, 224, 0.2)`. Focus viền đổi sang màu `{colors.primary}` (`#4E56C0`) kèm `{elevation.active-glow}`.
- **Trường nhập Tên cấp độ:** Nhãn *"Tên cấp độ *"* (dấu sao đỏ bắt buộc). Placeholder: *"Ví dụ: Cơ bản (A1 - A2)..."*.
- **Trường nhập Mô tả ngắn:** Nhãn *"Mô tả ngắn"*. Placeholder: *"Ví dụ: Dành cho người học bắt đầu từ con số không..."*.
- **Trường nhập Mô tả chi tiết:** Dạng `text-area` nhập liệu văn bản lớn, chiều cao tối thiểu `120px`. Nhãn *"Mô tả chi tiết"*.
- **Trường chọn IELTS Target:** Dropdown/Select cao `44px`. Lựa chọn điểm từ "0.0" đến "9.0" (bước nhảy 0.5).
- **Trường nhập TOEIC Target:** Trường nhập số (number input) cao `44px`, giới hạn số từ 0 đến 990.
- **Trường chọn Số lượng Unit tối đa:** Dropdown/Select cao `44px`. Lựa chọn số từ 1 đến 50.

### 4.4 Chân nút hành động (Modal Actions Footer - Vùng D)
- **Nút "Lưu" / "Lưu thay đổi":**
  - Style `button-primary` nền `{colors.primary}` (`#4E56C0`), chữ trắng, cao `44px`, bo góc `{rounded.lg}` (16px).
  - Hiệu ứng: `{elevation.active-glow}`. Hover tỏa sáng mạnh `{elevation.hover-glow}`.
- **Nút "Hủy":**
  - Style `button-secondary` nền `{colors.surface}`, viền mờ, chữ `{colors.primary}`, cao `44px`, bo góc `{rounded.lg}`.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Nhập liệu và click "Lưu" hoặc "Lưu thay đổi"**
  - Admin điền thông tin và click nút Lưu $\rightarrow$ Hệ thống kiểm tra dữ liệu:
    - *Nhánh thiếu Tên cấp độ (Rẽ nhánh E-1):* Bôi đỏ viền ô nhập Tên cấp độ màu `{colors.error}` (`#EF4444`) kèm dòng chữ lỗi đỏ: *"Tên cấp độ không được để trống!"* ngay dưới trường.
    - *Nhánh Tên cấp độ bị trùng (Rẽ nhánh E-2):* Bôi đỏ viền ô nhập, hiện chữ lỗi đỏ: *"Tên cấp độ đã tồn tại trên hệ thống!"*.
    - *Nhánh điểm số quy chiếu không hợp lệ (Rẽ nhánh E-3):* Bôi đỏ trường tương ứng, hiện chữ lỗi: *"Điểm số IELTS (0.0-9.0) hoặc TOEIC (0-990) không hợp lệ!"*.
    - *Nhánh hợp lệ:* Nút Lưu chuyển sang trạng thái Loading (hiển thị spinner mờ, khóa click) $\rightarrow$ Gọi API lưu trữ dữ liệu $\rightarrow$ Thành công $\rightarrow$ Tự động đóng Modal $\rightarrow$ Quay về màn hình danh sách `AD-01` $\rightarrow$ Hiện Toast màu xanh lá `{colors.success}`: *"Lưu thông tin cấp độ học thành công!"* $\rightarrow$ Tự động làm mới danh sách cấp độ hiển thị.
  - **API Lưu cấp độ học:** `POST /api/levels/save`
    - Payload: `{ "id": 1 (nếu là sửa), "name": "Basic", "shortDescription": "...", "ieltsTarget": 3.5, "toeicTarget": 350, "maxUnits": 25 }`
    - Response: `{ "success": true }`

---

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái khởi tạo (Empty / Fill State):** Ở Modal thêm mới, các trường hiển thị trống kèm placeholder xám mờ. Ở Modal chỉnh sửa, hệ thống tự động điền sẵn dữ liệu cũ của cấp độ học được chọn vào các trường tương ứng.
- **Trạng thái tải (Loading State):** Khi bấm Lưu, nút Lưu chuyển sang loading và vô hiệu hóa click để tránh gửi lặp yêu cầu lên server.

---

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [level_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/level_list_page.md) sau khi click "Thêm cấp độ mới" hoặc click "Sửa" trên thẻ cấp độ.
- **Đi đến:** Quay lại [level_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/level_list_page.md) sau khi đóng modal.

---

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Thiết kế khoảng cách giữa các trường nhập liệu cân đối `{spacing.md}` (16px), các nhãn thông báo lỗi đỏ `{colors.error}` có font chữ nhỏ dễ nhìn để Admin nhanh chóng sửa lỗi.
- **KHÔNG ĐƯỢC:** Sử dụng bóng đổ đen thô cứng dưới hộp thoại. Chỉ sử dụng hiệu ứng phát sáng mờ `{elevation.hover-glow}` với màu nhạt để tạo cảm giác hộp thoại đang trôi nổi nhẹ nhàng trên vũ trụ sương mờ của DiveVerse.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Biểu mẫu chỉnh sửa Cấp độ (Level Add/Edit Form Fields):** Liên kết với các trường dữ liệu của cấp độ được chọn trong mảng `levels` (ví dụ: `levels[0]` cho cấp độ Basic) để điền sẵn thông tin: `{name}`, `{shortDescription}`, `{detailDescription}`, `{ieltsTarget}`, `{toeicTarget}`, `{maxUnits}`.
