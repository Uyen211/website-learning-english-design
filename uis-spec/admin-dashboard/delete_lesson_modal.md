# MÀN HÌNH: DELETE LESSON CONFIGURATION CONFIRMATION MODAL (HỘP THOẠI XÁC NHẬN XÓA CẤU HÌNH BÀI HỌC)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Delete Lesson Configuration Confirmation Modal (Hộp thoại xác nhận xóa cấu hình bài học)
- **Mã use case liên quan:** UC-03c
- **Mã luồng người dùng liên quan:** Flow AD-FL-03 (Cấu hình Bài học và Luyện tập)
- **Vai trò người dùng:** Admin (Quản trị viên)
- **Vị trí trong sitemap:** Trang chủ quản trị $\rightarrow$ AD-01 $\rightarrow$ AD-02 $\rightarrow$ AD-03: Lesson List Page $\rightarrow$ Modal AD-03-M1

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng hộp thoại cảnh báo nổi này để đưa ra quyết định chắc chắn trước khi tiến hành xóa sạch toàn bộ nội dung bài giảng, tệp đa phương tiện đã tải lên và câu hỏi luyện tập của một bài học, đưa trạng thái bài học về "Chưa cấu hình" trong hệ thống DiveVerse.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Hộp thoại nổi lớp phủ cỡ nhỏ căn giữa hoàn toàn (Small Centered Modal Overlay) đè lên giao diện màn hình danh sách bài học `AD-03`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Overlay Backdrop (Vùng A):** Lớp nền tối mờ che phủ toàn bộ giao diện phía dưới.
  - **Zone 2: Modal Header & Icon (Vùng B):** Biểu tượng cảnh báo nguy hiểm đi kèm Tiêu đề cảnh báo.
  - **Zone 3: Modal Body Content (Vùng C):** Đoạn thông điệp xác nhận chi tiết.
  - **Zone 4: Modal Actions Footer (Vùng D):** Chân hộp thoại chứa cặp nút Xác nhận xóa / Hủy căn lề phải.
- **Kích thước tham khảo:**
  - Chiều rộng cố định của hộp thoại: `420px`.
  - Chiều cao tự động co giãn theo văn bản cảnh báo.
  - Khoảng cách padding trong modal: `{spacing.lg}` (24px).
  - Khoảng cách dọc giữa các vùng: `{spacing.md}` (16px).

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Lớp nền tối mờ (Overlay Backdrop - Vùng A)
- **Đặc tả Visual:**
  - Nền overlay: Tông màu tối `{colors.dark-floor}` (`#1C1B2E`) ở mức `50%` opacity làm backdrop.
  - Hiệu ứng: `backdrop-filter: blur(8px)`.
  - Hành vi: Nhấp ngoài vùng hộp thoại sẽ đóng modal tương đương hành động "Hủy".

### 4.2 Thẻ Modal chính & Tiêu đề cảnh báo (Modal Container & Header - Vùng B)
- **Đặc tả Visual:**
  - Nền hộp thoại: `{colors.surface}` (`#FFFFFF`).
  - Bo góc: `{rounded.xl}` (24px).
  - Viền mờ: `1px solid rgba(239, 68, 68, 0.2)` (viền đỏ nhạt cảnh báo).
  - Hiệu ứng nâng: `{elevation.hover-glow}`.
- **Thành phần:**
  - **Biểu tượng Cảnh báo:** Biểu tượng thông tin cảnh báo (Lucide `info`) màu `{colors.error}` (`#EF4444`) kích thước `24px x 24px` nằm bên trái tiêu đề.
  - **Tiêu đề cảnh báo:** Dạng chữ `{typography.title-md}` (18px, weight 600), màu `{colors.text-primary}`. Hiển thị: *"Xóa cấu hình bài học"*.

### 4.3 Thân thông điệp chi tiết (Modal Body - Vùng C)
- **Thông điệp chi tiết:**
  - Dạng chữ `{typography.body-md}` (15px, line-height 1.55, màu `{colors.text-secondary}`).
  - Hiển thị: *"Bạn có chắc chắn muốn xóa toàn bộ nội dung cấu hình và các câu hỏi bài tập của bài học này? Hành động này sẽ đưa trạng thái bài học về 'Chưa cấu hình' và không thể hoàn tác."*.

### 4.4 Chân nút hành động (Modal Actions Footer - Vùng D)
- **Nút "Xác nhận xóa":**
  - Style `button-primary` nền `{colors.error}` (`#EF4444`), chữ trắng, cao `44px`, bo góc `{rounded.lg}` (16px).
  - Hiệu ứng: `{elevation.active-glow}`. Hover tỏa sáng `{elevation.hover-glow}`.
- **Nút "Hủy":**
  - Style `button-secondary` nền `{colors.surface}`, viền mờ, chữ `{colors.primary}`, cao `44px`, bo góc `{rounded.lg}`.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Click nút "Xác nhận xóa"**
  - Admin click nút Xác nhận $\rightarrow$ Nút chuyển sang trạng thái Loading (hiển thị spinner mờ, khóa click) $\rightarrow$ Gửi yêu cầu API DELETE xóa cấu hình bài học kèm theo ID bài học $\rightarrow$ Thành công $\rightarrow$ Đóng Modal $\rightarrow$ Quay lại danh sách `AD-03` (Thẻ bài học tự động đổi badge trạng thái sang "Chưa cấu hình" màu xám và nút đổi thành "Cấu hình bài học") $\rightarrow$ Hiện Toast màu xanh lá `{colors.success}`: *"Xóa cấu hình bài học thành công!"*.
  - **API Xóa cấu hình bài học:** `DELETE /api/lessons/{lesson_id}/configuration`
    - Response: `{ "success": true }`
- **Hành động: Click nút "Hủy" hoặc click ngoài vùng Modal**
  - Đóng Modal $\rightarrow$ Quay lại danh sách `AD-03` giữ nguyên mọi dữ liệu cũ.

---

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái lỗi API (Error State):** Nếu máy chủ báo lỗi khi xóa cấu hình $\rightarrow$ Hiển thị dòng chữ báo lỗi đỏ `{colors.error}`: *"Lỗi hệ thống. Không thể xóa cấu hình bài học vào lúc này. Vui lòng thử lại!"* ngay bên trên các nút bấm.

---

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [lesson_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/lesson_list_page.md) khi click nút "Xóa cấu hình" trên thẻ bài học hợp lệ (đã qua kiểm tra chưa có học viên học).
- **Đi đến:** Quay lại [lesson_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/lesson_list_page.md) sau khi đóng modal.

---

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Đặt nút Xác nhận xóa bằng tông màu đỏ nổi bật `{colors.error}` cảnh báo nguy hiểm, trong khi nút Hủy sử dụng tông màu trung tính để tránh nhầm lẫn hành động (Nguyên tắc Báo hiệu - Signaling Principle).
- **KHÔNG ĐƯỢC:** Sử dụng bóng đổ đen thô cứng dưới hộp thoại. Toàn bộ hiệu ứng chiều sâu bắt buộc dùng viền mờ cảnh báo nhạt và dải phát sáng mờ ảo để giữ trọn vẹn đặc trưng phong cách của DiveVerse.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Xác nhận xóa cấu hình bài học (Lesson Delete Warning Check):** Sử dụng các trường `{name}` và `{category}` từ mảng `adminDashboardData.lessonsList` của bài học muốn xóa cấu hình để hiển thị trên giao diện hộp thoại cảnh báo xóa.
