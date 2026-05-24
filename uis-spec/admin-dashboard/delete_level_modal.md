# MÀN HÌNH: DELETE LEVEL CONFIRMATION MODAL (HỘP THOẠI XÁC NHẬN XÓA CẤP ĐỘ HỌC)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Delete Level Confirmation Modal (Hộp thoại xác nhận xóa cấp độ học)
- **Mã use case liên quan:** UC-01c
- **Mã luồng người dùng liên quan:** Flow AD-FL-01 (Quản lý Cấp độ)
- **Vai trò người dùng:** Admin (Quản trị viên)
- **Vị trí trong sitemap:** Trang chủ quản trị $\rightarrow$ AD-01: Level List Page $\rightarrow$ Modal AD-01-M3

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng hộp thoại cảnh báo nổi này để xác nhận quyết định chắc chắn trước khi thực hiện xóa hoàn toàn một cấp độ học (lộ trình học) ra khỏi cơ sở dữ liệu hệ thống DiveVerse.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Hộp thoại nổi lớp phủ cỡ nhỏ căn giữa hoàn toàn (Small Centered Modal Overlay) đè lên giao diện màn hình danh sách cấp độ học `AD-01`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Overlay Backdrop (Vùng A):** Lớp nền tối mờ che phủ toàn bộ màn hình phía sau.
  - **Zone 2: Modal Header & Content (Vùng B):** Tiêu đề cảnh báo nguy hiểm đi kèm biểu tượng và nội dung thông điệp chi tiết.
  - **Zone 3: Modal Actions Footer (Vùng C):** Chân hộp thoại chứa cặp nút bấm Xác nhận xóa / Hủy căn lề phải.
- **Kích thước tham khảo:**
  - Chiều rộng cố định của hộp thoại: `400px`.
  - Chiều cao tự động co giãn theo văn bản cảnh báo.
  - Khoảng cách padding trong modal: `{spacing.lg}` (24px).
  - Khoảng cách dọc giữa các khối: `{spacing.md}` (16px).

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Lớp nền tối mờ (Overlay Backdrop - Vùng A)
- **Đặc tả Visual:**
  - Nền overlay: Tông màu tối `{colors.dark-floor}` (`#1C1B2E`) ở mức `50%` opacity làm backdrop.
  - Hiệu ứng: `backdrop-filter: blur(8px)`.
  - Hành vi: Nhấp chuột ra ngoài vùng hộp thoại sẽ đóng modal tương đương hành động "Hủy".

### 4.2 Thẻ Modal chính & Nội dung cảnh báo (Modal Container & Body - Vùng B)
- **Đặc tả Visual:**
  - Nền hộp thoại: `{colors.surface}` (`#FFFFFF`).
  - Bo góc: `{rounded.xl}` (24px).
  - Viền mờ: `1px solid rgba(239, 68, 68, 0.2)` (viền đỏ nhạt cảnh báo).
  - Hiệu ứng nâng: `{elevation.hover-glow}`.
- **Thành phần bên trong:**
  - **Biểu tượng Cảnh báo:** Biểu tượng thông tin cảnh báo (Lucide `info`) màu `{colors.error}` (`#EF4444`) kích thước `24px x 24px` nằm bên trái tiêu đề.
  - **Tiêu đề cảnh báo:** Dạng chữ `{typography.title-md}` (18px, weight 600), màu `{colors.text-primary}`. Hiển thị: *"Xóa cấp độ học"*.
  - **Thông điệp chi tiết:** Dạng chữ `{typography.body-md}` (16px, weight 400), màu `{colors.text-secondary}`. Hiển thị: *"Bạn có chắc chắn muốn xóa cấp độ này? Hành động này sẽ loại bỏ hoàn toàn lộ trình và các cấu hình liên quan của cấp độ học khỏi hệ thống, đồng thời không thể hoàn tác."*.

### 4.3 Chân nút hành động (Modal Actions Footer - Vùng C)
- **Nút "Xác nhận xóa":**
  - Style `button-primary` nền `{colors.error}` (`#EF4444`), chữ trắng, cao `44px`, bo góc `{rounded.lg}` (16px).
  - Hiệu ứng: `{elevation.active-glow}`. Hover tỏa sáng `{elevation.hover-glow}`.
- **Nút "Hủy":**
  - Style `button-secondary` nền `{colors.surface}`, viền mờ, chữ `{colors.primary}`, cao `44px`, bo góc `{rounded.lg}`.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Click nút "Xác nhận xóa"**
  - Admin click nút Xác nhận $\rightarrow$ Nút chuyển sang trạng thái Loading (hiển thị spinner mờ, khóa click) $\rightarrow$ Gửi yêu cầu API DELETE xóa cấp độ $\rightarrow$ Thành công $\rightarrow$ Đóng Modal $\rightarrow$ Quay lại màn hình `AD-01` $\rightarrow$ Hiện Toast màu xanh lá `{colors.success}`: *"Xóa cấp độ học thành công!"* $\rightarrow$ Tự động tải lại và cập nhật danh sách.
  - **API Xóa cấp độ:** `DELETE /api/levels/{level_id}`
    - Response: `{ "success": true }`
- **Hành động: Click nút "Hủy" hoặc click ngoài vùng Modal**
  - Đóng Modal $\rightarrow$ Quay lại danh sách `AD-01` giữ nguyên dữ liệu.

---

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái lỗi API (Error State):** Nếu máy chủ báo lỗi khi xóa cấp độ $\rightarrow$ Hiển thị thông báo lỗi màu đỏ `{colors.error}` ngay bên dưới thông điệp: *"Lỗi hệ thống. Không thể thực hiện xóa vào lúc này!"*.

---

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [level_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/level_list_page.md) khi click nút "Xóa" trên thẻ cấp độ học trống hợp lệ.
- **Đi đến:** Quay lại [level_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/level_list_page.md) sau khi đóng modal.

---

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Đặt nút Xác nhận xóa bằng tông màu đỏ nổi bật `{colors.error}` cảnh báo nguy hiểm, trong khi nút Hủy sử dụng tông màu trung tính để tránh nhầm lẫn hành động (Nguyên tắc Báo hiệu - Signaling Principle).
- **KHÔNG ĐƯỢC:** Sử dụng bóng đổ đen thô ráp. Việc phân cấp chỉ dựa vào viền mờ màu cảnh báo nhạt và dải phát sáng mờ ảo để giữ trọn vẹn đặc trưng phong cách của DiveVerse.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Xác nhận xóa cấp độ (Level Delete Warning Check):** Sử dụng các trường `{name}` và số học viên đang hoạt động `{activeUsers}` từ mảng `adminDashboardData.levelsList` của cấp độ muốn xóa để hiển thị cảnh báo ràng buộc trên giao diện hộp thoại xác nhận.
