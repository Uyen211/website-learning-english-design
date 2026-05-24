# MÀN HÌNH: LEVEL LIST PAGE (MÀN HÌNH DANH SÁCH CẤP ĐỘ HỌC)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Level List Page (Màn hình danh sách cấp độ học)
- **Mã use case liên quan:** UC-01a, UC-01b, UC-01c
- **Mã luồng người dùng liên quan:** Flow AD-FL-01, Flow AD-FL-02
- **Vai trò người dùng:** Admin (Quản trị viên)
- **Vị trí trong sitemap:** Trang chủ quản trị $\rightarrow$ AD-01: Level List Page (URL: `/admin/levels`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng màn hình này để xem danh sách toàn bộ các cấp độ học (lộ trình Basic, Intermediate, Advanced) trong hệ thống DiveVerse. Admin có thể thực hiện theo dõi nhanh thông tin quy chiếu điểm thi quốc tế (IELTS/TOEIC) của từng cấp độ, truy cập sâu vào danh sách Unit của cấp độ tương ứng, hoặc kích hoạt các chức năng thêm mới, chỉnh sửa và xóa bỏ cấp độ học.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục cột kép chia tỷ lệ gồm Sidebar cố định bên trái chiếm chiều rộng nhỏ và Vùng nội dung chính cuộn dọc chiếm phần còn lại bên phải.
- **Màu nền chung:** Nền trang chính sử dụng tông màu `{colors.canvas}` (`#F9F7FE`) dịu mát, được phủ lớp dải sương mờ `{gradients.atmosphere-haze}`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Left Navigation Sidebar (Vùng A):** Sidebar điều hướng cố định bên trái, chiều rộng `260px`.
  - **Zone 2: Top Bar & Breadcrumbs (Vùng B):** Thanh dẫn đường dẫn và avatar quản trị viên ở góc trên cùng bên phải.
  - **Zone 3: Content Action Toolbar (Vùng C):** Thanh tiêu đề phân hệ quản trị và nút hành động chính "Thêm cấp độ mới".
  - **Zone 4: Level Cards Grid (Vùng D):** Lưới thẻ hiển thị danh sách các cấp độ học hiện có dưới dạng thẻ lơ lửng.
- **Kích thước tham khảo:**
  - Sidebar: chiều rộng cố định `260px`, viền phải hairline tinh tế `1px solid rgba(155, 93, 224, 0.1)`.
  - Vùng nội dung bên phải: căn giữa tối đa `1200px`, sử dụng lưới 12 cột.
  - Khoảng cách giữa các thẻ cấp độ: `{spacing.lg}` (24px).

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh điều hướng Sidebar quản trị (Navigation Sidebar - Vùng A)
- **Đặc tả Visual:**
  - Nền Sidebar: Kính mờ `{colors.glass}` (`rgba(255, 255, 255, 0.7)`) kết hợp `backdrop-filter: blur(8px)`.
  - Viền phải: `1px solid rgba(155, 93, 224, 0.1)`.
- **Thành phần:**
  - **Logo & Wordmark DiveVerse:**
    - Logo: Sử dụng ảnh Cá Voi Vũ Trụ gốc [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) kích thước `40px x 40px` ở góc trên cùng.
    - Wordmark: Chữ "DiveVerse Admin" dạng `{typography.title-lg}` màu `{colors.text-primary}` (`#1A1A2E`).
  - **Danh sách liên kết điều hướng (Nav Links):**
    - Mỗi dòng liên kết có chiều cao `48px` để tối ưu hóa việc nhấp chuột.
    - *Tab "Cấp độ học" (Active):* Nền chuyển sang `{colors.surface}` (`#FFFFFF`), chữ màu `{colors.primary}` (`#4E56C0`) (weight 600) kèm hiệu ứng tỏa sáng nhẹ `{elevation.glow}`.
    - *Tab "Bài kiểm tra" (Inactive):* Nền trong suốt, chữ màu `{colors.text-secondary}` (`#5A5A7A`). Hover chuyển sang chữ màu `{colors.accent}` (`#D78FEE`).
    - *Tab "Báo cáo học tập" (Inactive):* Tương tự bài kiểm tra.

### 4.2 Thanh Breadcrumbs & Đầu trang (Top Breadcrumbs Bar - Vùng B)
- **Thành phần:**
  - **Breadcrumbs:** Dòng chữ dẫn đường dạng `{typography.caption}` (12px), màu `{colors.text-secondary}`. Hiển thị: *"Admin / Lộ trình học / Danh sách cấp độ"*.
  - **Avatar quản trị viên:** Ảnh đại diện tròn `{rounded.full}` đường kính `36px` ở góc phải. Khi click sẽ xổ dropdown menu "Đăng xuất".

### 4.3 Thanh hành động Toolbar (Content Toolbar - Vùng C)
- **Thành phần:**
  - **Tiêu đề phân hệ:** Dạng chữ `{typography.display-md}` (Manrope, 36px, weight 700, letter-spacing -1px), màu `{colors.text-primary}`. Hiển thị: *"Cấp độ học"*.
  - **Nút "Thêm cấp độ mới":** Style `button-primary` nền `{colors.primary}` (`#4E56C0`), chữ trắng, cao `44px`, bo góc `{rounded.lg}` (16px). Mặc định tỏa sáng `{elevation.active-glow}`. Hover tỏa sáng mạnh `{elevation.hover-glow}`. Bấm vào mở Modal `AD-01-M1`.

### 4.4 Lưới thẻ cấp độ học (Level Cards Grid - Vùng D)
- **Đặc tả Grid:**
  - Hiển thị dạng lưới 3 cột ở màn hình desktop lớn, tự động chuyển về 2 cột ở tablet và 1 cột ở mobile.
- **Thẻ cấp độ học (Level Card Item):**
  - Nền thẻ: `{colors.surface}` (`#FFFFFF`).
  - Bo góc: `{rounded.xl}` (24px).
  - Viền mờ: `1px solid rgba(155, 93, 224, 0.1)`. Padding: `{spacing.lg}` (24px).
  - Hiệu ứng nâng: Mặc định `{elevation.glow}`. Hover tỏa sáng mượt `{elevation.hover-glow}`.
  - **Nội dung thẻ:**
    - **Tên cấp độ học:** Dạng chữ `{typography.title-lg}` (24px, Manrope, weight 700), màu `{colors.text-primary}`. Nhấp vào tên cấp độ để mở màn hình danh sách Unit của cấp độ đó (`AD-02`).
    - **Mô tả ngắn:** Dạng chữ `{typography.body-sm}` (14px, Inter, màu `{colors.text-secondary}`).
    - **Khung điểm mục tiêu (Spec Badges Area):**
      - Hiển thị các badge viên thuốc `{rounded.pill}`, nền nhạt `{colors.light-accent}` (`#FDCFFA`), chữ màu `{colors.primary}`.
      - Các badge gồm: *"IELTS Target: {ielts_score}"*, *"TOEIC Target: {toeic_score}"*, *"Tối đa: {units_count} Units"*.
    - **Bộ nút hành động chân thẻ:**
      - *Nút "Sửa":* Style `button-secondary` nền `{colors.surface}`, viền `1px solid rgba(78, 86, 192, 0.2)`, chữ `{colors.primary}`, cao `44px`, bo góc `{rounded.lg}`. Bấm vào mở Modal sửa `AD-01-M2`.
      - *Nút "Xóa":* Style liên kết văn bản trơn, chữ màu `{colors.error}` (`#EF4444`) (weight 600), cao `44px` (bao gồm padding trong suốt) để đạt touch target. Bấm vào kích hoạt luồng xóa `UC-01c`.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Click vào tên cấp độ học trên thẻ**
  - Hệ thống chuyển hướng Admin sang trang danh sách Unit `/admin/levels/{level_id}/units` (`AD-02`).
- **Hành động: Click nút "Thêm cấp độ mới"**
  - Hiển thị Modal `AD-01-M1` nổi đè lên trên màn hình hiện tại.
- **Hành động: Click nút "Sửa" trên thẻ cấp độ**
  - Hiển thị Modal `AD-01-M2` điền sẵn dữ liệu cũ nổi đè lên trên màn hình hiện tại.
- **Hành động: Click nút "Xóa" trên thẻ cấp độ**
  - Hệ thống tự động kiểm tra điều kiện xóa:
    - *Nếu cấp độ đang có học viên hoạt động:* Báo lỗi dạng Toast đỏ màu `{colors.error}` ở góc trên bên phải: *"Không thể xóa cấp độ này vì đang có [X] học viên hoạt động trên lộ trình!"*.
    - *Nếu cấp độ trống hợp lệ:* Hiển thị Modal xác nhận xóa `AD-01-M3`.

---

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái danh sách trống (Empty State):**
  - Khi chưa có cấp độ học nào được tạo trong cơ sở dữ liệu:
    - Ẩn lưới thẻ. Hiển thị hình ảnh minh họa chú cá voi [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`160px x 160px`) đang bay lơ lửng giữa khoảng không vũ trụ trống rỗng.
    - Dòng chữ thông báo: *"Hệ thống chưa có cấp độ học nào được khởi tạo. Hãy nhấn nút 'Thêm cấp độ mới' để bắt đầu lộ trình!"* dạng `{typography.body-md}` màu `{colors.text-secondary}`.
- **Trạng thái tải trang (Loading State):** Hiển thị 3 thẻ khung xương Skeleton màu xám nhạt `{colors.canvas}` nhấp nháy mờ dịu mắt.
- **Trạng thái lỗi kết nối (Error State):** Hiển thị bảng thông tin lỗi đỏ kèm nút "Tải lại trang" style `button-secondary`.

---

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** Màn hình đăng nhập quản trị viên hoặc click tab "Cấp độ học" ở Sidebar từ các phân hệ khác.
- **Đi đến:**
  - [unit_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/unit_list_page.md) khi click chọn tên một cấp độ.
  - [test_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/test_list_page.md) khi click chọn tab "Bài kiểm tra" trên Sidebar.

---

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Đảm bảo viền phân cách Sidebar và Vùng nội dung chỉ là đường kẻ hairline siêu mờ `rgba(155, 93, 224, 0.1)` để không gian luôn cảm giác thoáng đãng và thanh khiết.
- **KHÔNG ĐƯỢC:** Sử dụng bất kỳ bóng đổ vật lý màu đen hay xám đậm nào. Toàn bộ hiệu ứng chiều sâu bắt buộc dùng dải phát sáng dịu nhẹ `{elevation.glow}` và viền mờ theo định hướng hệ thống Light Mode Universe.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Danh sách Cấp độ (Levels Management Table):** Liên kết với mảng `adminDashboardData.levelsList`. Mỗi cấp độ hiển thị các trường:
  - Tên cấp độ: `{name}`
  - Số lượng Unit hiện có: `{unitsCount}`
  - Số học viên hoạt động: `{activeUsers}`
  - Mục tiêu IELTS: `{ieltsTarget}`
  - Mục tiêu TOEIC: `{toeicTarget}`
