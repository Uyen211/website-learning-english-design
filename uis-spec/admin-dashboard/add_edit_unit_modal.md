# MÀN HÌNH: ADD / EDIT UNIT MODAL (HỘP THOẠI THÊM/SỬA UNIT)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Add / Edit Unit Modal (Hộp thoại thêm/sửa Unit)
- **Mã use case liên quan:** UC-02a, UC-02b
- **Mã luồng người dùng liên quan:** Flow AD-FL-02 (Quản lý Unit)
- **Vai trò người dùng:** Admin (Quản trị viên)
- **Vị trí trong sitemap:** Trang chủ quản trị $\rightarrow$ AD-01: Level List Page $\rightarrow$ Click tên cấp độ $\rightarrow$ AD-02: Unit List Page $\rightarrow$ Modal AD-02-M1 (Thêm mới) / AD-02-M2 (Chỉnh sửa)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng hộp thoại nổi đè lên màn hình này để nhập thông tin cấu hình cho một Unit mới (ví dụ: *Greetings, Family, Daily Routines* theo `level_built.md`) thuộc một Cấp độ học cụ thể, hoặc chỉnh sửa thông tin của một Unit hiện có.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Hộp thoại lớp phủ nổi căn giữa (Centered Modal Overlay) đè lên giao diện màn hình danh sách Unit `AD-02`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Overlay Backdrop (Vùng A):** Lớp nền tối mờ che phủ toàn bộ màn hình phía dưới.
  - **Zone 2: Modal Header (Vùng B):** Tiêu đề hộp thoại và nút đóng (X).
  - **Zone 3: Form Body (Vùng C):** Thân hộp thoại chứa các trường nhập liệu sắp xếp dọc một cột.
  - **Zone 4: Modal Actions Footer (Vùng D):** Chân hộp thoại chứa cặp nút Lưu/Hủy căn lề phải.
- **Kích thước tham khảo:**
  - Chiều rộng cố định của hộp thoại: `560px`.
  - Chiều cao tự động co giãn theo form nhập liệu.
  - Khoảng cách padding trong modal: `{spacing.xl}` (32px).
  - Khoảng cách dọc giữa các trường nhập liệu: `{spacing.md}` (16px).

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Lớp nền tối mờ (Overlay Backdrop - Vùng A)
- **Đặc tả Visual:**
  - Nền overlay: Tông màu tối `{colors.dark-floor}` (`#1C1B2E`) ở mức `50%` opacity làm backdrop.
  - Hiệu ứng: `backdrop-filter: blur(8px)` kính mờ xuyên thấu.
  - Hành vi: Nhấp chuột ra ngoài vùng hộp thoại sẽ đóng modal tương đương hành động "Hủy".

### 4.2 Thẻ Modal chính & Tiêu đề (Modal Container & Header - Vùng B)
- **Đặc tả Visual:**
  - Nền hộp thoại: `{colors.surface}` (`#FFFFFF`).
  - Bo góc lớn: `{rounded.xl}` (24px).
  - Viền mờ: `1px solid rgba(155, 93, 224, 0.15)`.
  - Hiệu ứng nâng: `{elevation.hover-glow}` (glow phát quang mạnh).
- **Tiêu đề:**
  - Dạng chữ `{typography.title-lg}` (22px, weight 600, màu `{colors.text-primary}`).
  - Hiển thị: *"Thêm Unit mới"* (đối với Modal thêm) hoặc *"Chỉnh sửa Unit"* (đối với Modal sửa).

### 4.3 Thân biểu mẫu nhập liệu (Form Body - Vùng C)
Các trường nhập liệu đều dạng `text-input`, chiều cao `44px`, bo góc `{rounded.lg}` (16px). Viền mặc định `1px solid rgba(155, 93, 224, 0.2)`. Focus viền đổi sang màu `{colors.primary}` (`#4E56C0`) kèm `{elevation.active-glow}`.
- **Trường Số thứ tự Unit (read-only):**
  - Đặc tả: Nền nhạt `{colors.light-accent}` (`#FDCFFA`) ở mức 15% opacity, chữ màu `{colors.text-secondary}`. Con trỏ dạng blocked.
  - Nội dung: Tự động hiển thị sequence (ví dụ: *"05"* đối với tạo mới, hoặc sequence hiện tại của Unit đối với chỉnh sửa).
- **Trường nhập Tên Unit:** Nhãn *"Tên Unit *"* (dấu sao đỏ bắt buộc). Nền `{colors.canvas}` (`#F9F7FE`). Placeholder: *"Ví dụ: Greetings & Introductions..."*.
- **Trường nhập Chủ đề lớn:** Nhãn *"Chủ đề lớn *"* (bắt buộc). Nền `{colors.canvas}`. Placeholder: *"Ví dụ: Greetings / Everyday Work..."*.
- **Trường nhập Chủ điểm từ vựng:** Nhãn *"Chủ điểm từ vựng"*. Placeholder: *"Ví dụ: Chào hỏi, nghề nghiệp..."*.
- **Trường nhập Chủ điểm ngữ pháp:** Nhãn *"Chủ điểm ngữ pháp"*. Placeholder: *"Ví dụ: Present Simple / Passive Voice..."*.
- **Trường chọn Kỹ năng thi áp dụng:**
  - Loại: Dropdown/Select cao `44px`. Nhãn *"Kỹ năng thi áp dụng"*. Lựa chọn: *"IELTS"* hoặc *"TOEIC"*.

### 4.4 Chân nút hành động (Modal Actions Footer - Vùng D)
- **Nút "Lưu" / "Lưu thay đổi":**
  - Style `button-primary` nền `{colors.primary}` (`#4E56C0`), chữ trắng, cao `44px`, bo góc `{rounded.lg}` (16px).
  - Hiệu ứng: `{elevation.active-glow}`. Hover tỏa sáng mạnh `{elevation.hover-glow}`.
- **Nút "Hủy":**
  - Style `button-secondary` nền `{colors.surface}`, viền mờ, chữ `{colors.primary}`, cao `44px`, bo góc `{rounded.lg}`.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Click nút "Lưu" hoặc "Lưu thay đổi"**
  - Admin click nút Lưu $\rightarrow$ Hệ thống kiểm tra dữ liệu:
    - *Nhánh thiếu Tên Unit hoặc Chủ đề lớn (Rẽ nhánh E-1):* Bôi đỏ viền ô nhập bị lỗi màu `{colors.error}` (`#EF4444`) kèm dòng chữ lỗi đỏ: *"Tên Unit và Chủ đề lớn không được để trống!"* ngay dưới trường.
    - *Nhánh hợp lệ:* Nút Lưu hiển thị Loading (xoay spinner mờ, khóa click) $\rightarrow$ Gọi API lưu trữ dữ liệu $\rightarrow$ Thành công $\rightarrow$ Đóng Modal $\rightarrow$ Quay về màn danh sách `AD-02` $\rightarrow$ Hiện Toast màu xanh lá `{colors.success}`: *"Lưu thông tin Unit thành công!"* $\rightarrow$ Tự động làm mới danh sách Unit.
  - **API Lưu Unit:** `POST /api/units/save`
    - Payload: `{ "id": 12 (nếu là sửa), "name": "Greetings", "theme": "Daily Life", "vocabularyTopic": "Greetings", "grammarTopic": "Present Simple", "targetSkill": "IELTS" }`
    - Response: `{ "success": true }`

---

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái khởi tạo (Empty / Fill State):** Ở Modal thêm mới, các trường nhập mặc định trống kèm placeholder. Ở Modal chỉnh sửa, hệ thống tự động điền sẵn các giá trị cấu hình cũ của Unit được chọn vào form.
- **Trạng thái tải (Loading State):** Khi bấm nút Lưu, nút chuyển sang loading và vô hiệu hóa click để tránh gửi trùng lặp.

---

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [unit_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/unit_list_page.md) sau khi click "Thêm Unit mới" hoặc click "Sửa" trên thẻ Unit.
- **Đi đến:** Quay lại [unit_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/unit_list_page.md) sau khi đóng modal.

---

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Thiết kế khoảng cách dọc giữa các trường nhập liệu cân đối `{spacing.md}` (16px) và các nhãn lỗi đỏ rõ ràng để Admin dễ quan sát và sửa đổi.
- **KHÔNG ĐƯỢC:** Sử dụng bóng đổ xám đen thô ráp. Chỉ sử dụng hiệu ứng phát sáng mờ `{elevation.hover-glow}` với màu nhạt để tạo cảm giác hộp thoại đang lơ lửng bồng bềnh trong vũ trụ của DiveVerse.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Biểu mẫu chỉnh sửa Unit (Unit Add/Edit Form Fields):** Liên kết với các trường dữ liệu của Unit được chọn trong mảng `levels[0].units[0]` để điền sẵn thông tin: `{sequence}`, `{name}`, `{theme}`, `{vocabularyTopic}`, `{grammarTopic}`, `{targetSkill}`.
