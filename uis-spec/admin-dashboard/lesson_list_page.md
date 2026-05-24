# MÀN HÌNH: LESSON LIST PAGE (MÀN HÌNH DANH SÁCH BÀI HỌC THEO UNIT)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Lesson List Page (Màn hình danh sách bài học theo Unit)
- **Mã use case liên quan:** UC-03a, UC-03b, UC-03c
- **Mã luồng người dùng liên quan:** Flow AD-FL-03 (Cấu hình Bài học và Luyện tập)
- **Vai trò người dùng:** Admin (Quản trị viên)
- **Vị trí trong sitemap:** Trang chủ quản trị $\rightarrow$ AD-01: Level List Page $\rightarrow$ Click cấp độ $\rightarrow$ AD-02: Unit List Page $\rightarrow$ Click Unit $\rightarrow$ AD-03: Lesson List Page (URL: `/admin/units/{unit_id}/lessons`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng màn hình này để quản lý danh sách 6 bài học bắt buộc (Từ vựng, Ngữ pháp, Nghe, Nói, Đọc, Viết) trong một Unit cụ thể. Admin có thể xem trạng thái cấu hình của từng bài học (Đã cấu hình / Chưa cấu hình) và kích hoạt các trang cấu hình chi tiết bài tập, hoặc xóa sạch cấu hình bài tập cũ để làm lại từ đầu.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục cột kép gồm Sidebar cố định bên trái (`260px`) và Vùng nội dung chính cuộn dọc bên phải.
- **Màu nền chung:** Nền trang chính sử dụng tông màu `{colors.canvas}` (`#F9F7FE`) phối dải chuyển màu mờ `{gradients.atmosphere-haze}`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Left Navigation Sidebar (Vùng A):** Sidebar điều hướng cố định bên trái.
  - **Zone 2: Header Breadcrumbs Bar (Vùng B):** Thanh dẫn thư mục và thông tin tài khoản admin.
  - **Zone 3: Unit Info Banner (Vùng C):** Banner thông tin Unit hiển thị tên Unit, chủ đề, kỹ năng thi quy chiếu và thống kê tiến độ cấu hình bài học.
  - **Zone 4: Lesson Cards Grid (Vùng D):** Lưới 6 thẻ bài học tương ứng với 6 kỹ năng cốt lõi.
- **Kích thước tham khảo:**
  - Chiều rộng tối đa của vùng nội dung chính bên phải: `1200px`.
  - Lưới bài học: Sử dụng lưới 3 cột ở màn hình desktop (3-up Grid), tự động co về 2 cột ở tablet và 1 cột ở mobile.
  - Khoảng cách giữa các thẻ bài học: `{spacing.lg}` (24px).

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh Breadcrumbs điều hướng đầu trang (Breadcrumbs Header - Vùng B)
- **Breadcrumbs:** Dòng chữ dạng `{typography.caption}` (12px), màu `{colors.text-secondary}`. Hiển thị: *"Admin / Lộ trình học / {Tên Cấp độ} / {Tên Unit} / Danh sách bài học"*.
- Admin có thể click vào các liên kết để quay lại màn hình `AD-01` hoặc danh sách Unit `AD-02`.

### 4.2 Thẻ Banner thông tin Unit (Unit Info Banner - Vùng C)
- **Đặc tả Visual:**
  - Nền banner: `{colors.surface}` (`#FFFFFF`).
  - Bo góc lớn: `{rounded.xxl}` (32px). Padding: `{spacing.xl}` (32px).
  - Viền trái dày `6px` màu chủ đạo `{colors.primary}` (`#4E56C0`) để tạo điểm nhấn chuyên nghiệp.
  - Hiệu ứng nâng: `{elevation.glow}` (soft glow nhẹ).
- **Nội dung:**
  - **Tiêu đề Unit:** Dạng chữ `{typography.title-lg}` (24px, Manrope, weight 700), màu `{colors.text-primary}`. Hiển thị: *"Chi tiết bài học của Unit: {Tên Unit}"*.
  - **Nhãn thông tin bổ trợ:** Hiển thị các badge viên thuốc `{rounded.pill}` nền nhạt `{colors.light-accent}` (`#FDCFFA`), chữ màu `{colors.primary}` ghi: *"Chủ đề: {Chủ đề lớn}"*, *"Kỹ năng thi: {IELTS / TOEIC}"*.
  - **Mascot nhỏ cổ vũ:** Ảnh Cá Voi Vũ Trụ [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`60px x 60px`) lấp ló góc phải banner để mang lại nguồn năng lượng vui tươi.

### 4.3 Lưới thẻ bài học (Lesson Cards Grid - Vùng D)
- **Thẻ bài học (Lesson Card Item):**
  - Nền thẻ: `{colors.surface}` (`#FFFFFF`).
  - Bo góc: `{rounded.xl}` (24px).
  - Viền mờ: `1px solid rgba(155, 93, 224, 0.1)`. Padding: `{spacing.lg}` (24px).
  - Hiệu ứng nâng: Mặc định `{elevation.glow}`. Hover tỏa sáng `{elevation.hover-glow}`.
  - **Thành phần bên trong thẻ:**
    - **Nhãn loại kỹ năng (Category Badge):** Badge viên thuốc `{rounded.pill}` ở góc trái trên, nền nhạt `{colors.light-accent}` (`#FDCFFA`), chữ màu `{colors.primary}`. Hiển thị: *"VOCABULARY"*, *"GRAMMAR"*, *"LISTENING"*, *"SPEAKING"*, *"READING"*, *"WRITING"*.
    - **Nhãn trạng thái cấu hình (Status Badge):**
      - *Đã cấu hình:* Nền nhạt `{colors.success}` ở mức 10% opacity, chữ màu `{colors.success}` (`#22C55E`), ghi *"Đã cấu hình"*.
      - *Chưa cấu hình:* Nền nhạt `{colors.text-secondary}` ở mức 10% opacity, chữ màu `{colors.text-secondary}` (`#5A5A7A`), ghi *"Chưa cấu hình"*.
    - **Tiêu đề bài học:** Dạng chữ `{typography.title-md}` (18px, weight 600, màu `{colors.text-primary}`). Hiển thị tên bài học cụ thể (ví dụ: *"Vocabulary: Greetings & Introductions"*).
    - **Cụm nút điều khiển chân thẻ (chiều cao nút 44px):**
      - *Trường hợp Chưa cấu hình:* Hiển thị 1 nút "Cấu hình bài học" trải rộng 100%. Style `button-primary` nền `{colors.primary}` (`#4E56C0`), chữ trắng, có `{elevation.active-glow}`. Bấm vào chuyển hướng sang trang soạn thảo `AD-03-Form`.
      - *Trường hợp Đã cấu hình:* Hiển thị 2 nút xếp ngang:
        - Nút "Sửa": Style `button-secondary` (rộng 48%), viền mờ, chữ `{colors.primary}`. Bấm vào chuyển hướng sang trang soạn thảo `AD-03-Form` ở chế độ chỉnh sửa.
        - Nút "Xóa cấu hình": Style liên kết văn bản trơn (rộng 48%), chữ màu `{colors.error}` (`#EF4444`) (weight 600). Bấm vào kích hoạt luồng xóa cấu hình `UC-03c`.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Click nút "Cấu hình" hoặc "Sửa"**
  - Hệ thống chuyển hướng Admin sang trang cấu hình bài học tương ứng tại `/admin/lessons/{lesson_id}/configure` (`AD-03-Form`).
- **Hành động: Click nút "Xóa cấu hình"**
  - Hệ thống kiểm tra điều kiện xóa cấu hình:
    - *Nếu bài học đã có học viên học và nộp câu trả lời:* Ngăn chặn xóa, hiển thị Toast cảnh báo màu `{colors.error}`: *"Không thể xóa cấu hình vì bài học đã có tiến trình học tập của học viên được ghi nhận!"*.
    - *Nếu bài học trống hợp lệ:* Hiển thị Modal xác nhận xóa cấu hình `AD-03-M1`.

---

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái tải trang (Loading State):** Lưới hiển thị các thẻ bài học có Skeleton mờ che phủ tiêu đề và nhãn, các nút bấm tạm thời ẩn.
- **Trạng thái thành công (Success State):** Khi xóa cấu hình bài học thành công từ Modal `AD-03-M1` và quay lại màn hình này $\rightarrow$ Hiện Toast màu xanh lá `{colors.success}`: *"Xóa cấu hình bài học thành công!"* $\rightarrow$ Thẻ bài học cập nhật badge thành "Chưa cấu hình" và đổi nút thành "Cấu hình bài học".

---

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [unit_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/unit_list_page.md) sau khi click chọn tên một Unit cụ thể.
- **Đi đến:**
  - [lesson_configuration_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/lesson_configuration_page.md) khi click nút cấu hình hoặc chỉnh sửa.
  - [unit_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/unit_list_page.md) khi click Breadcrumbs "Danh sách Unit".

---

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Đảm bảo lưới thẻ bài học hiển thị rõ ràng, cân xứng, khoảng cách dọc ngang `{spacing.lg}` (24px) giúp giao diện sạch sẽ, thoáng mắt và dễ định vị bài học.
- **KHÔNG ĐƯỢC:** Sử dụng bất cứ bóng đổ đen thô ráp nào. Mọi thẻ bài đều sử dụng hiệu ứng phát sáng mờ `{elevation.glow}` với sắc tím nhạt đặc trưng của DiveVerse.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Danh sách Bài học thuộc Unit (Lessons Management Table):** Liên kết với mảng `adminDashboardData.lessonsList`. Mỗi bài học hiển thị:
  - Tên bài học: `{name}`
  - Thể loại kỹ năng: `{category}` (VOCABULARY, GRAMMAR, LISTENING, etc.)
  - Trạng thái cấu hình: `{status}` (configured / unconfigured)
