# MÀN HÌNH: UNIT LIST PAGE (MÀN HÌNH DANH SÁCH UNIT THEO CẤP ĐỘ)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Unit List Page (Màn hình danh sách Unit theo cấp độ)
- **Mã use case liên quan:** UC-02a, UC-02b, UC-02c, UC-02d
- **Mã luồng người dùng liên quan:** Flow AD-FL-02 (Quản lý Unit)
- **Vai trò người dùng:** Admin (Quản trị viên)
- **Vị trí trong sitemap:** Trang chủ quản trị $\rightarrow$ AD-01: Level List Page $\rightarrow$ Click tên cấp độ $\rightarrow$ AD-02: Unit List Page (URL: `/admin/levels/{level_id}/units`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng màn hình này để quản lý danh sách toàn bộ các Unit thuộc một Cấp độ học cụ thể. Admin có thể kéo thả trực quan để thay đổi thứ tự giảng dạy của các Unit, lưu lại cấu hình thứ tự mới vào cơ sở dữ liệu, hoặc kích hoạt các hộp thoại nổi để thêm mới, sửa và xóa các Unit trong lộ trình này.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục cột kép gồm Sidebar cố định bên trái chiếm `260px` và Vùng nội dung chính cuộn dọc bên phải chiếm phần còn lại.
- **Màu nền chung:** Nền trang chính sử dụng tông màu `{colors.canvas}` (`#F9F7FE`) phủ sương mờ `{gradients.atmosphere-haze}`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Left Navigation Sidebar (Vùng A):** Sidebar điều hướng cố định bên trái.
  - **Zone 2: Header Breadcrumbs Bar (Vùng B):** Thanh dẫn thư mục và thông tin tài khoản admin.
  - **Zone 3: Toolbar & Drag Control (Vùng C):** Tiêu đề cấp độ học hiện tại, nút "+ Thêm Unit mới", cùng cặp nút "Lưu thứ tự" & "Hủy thay đổi" hiển thị động.
  - **Zone 4: Drag-and-Drop Sortable Unit List (Vùng D):** Danh sách các Unit xếp dọc có hỗ trợ kéo thả thay đổi vị trí.
- **Kích thước tham khảo:**
  - Chiều rộng tối đa của vùng nội dung chính bên phải: `1200px`.
  - Các thẻ Unit chiếm trọn 12 cột lưới để tối ưu không gian hiển thị thông tin ngang.
  - Khoảng cách dọc giữa các thẻ Unit: `{spacing.md}` (16px).

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh điều hướng Sidebar quản trị (Navigation Sidebar - Vùng A)
- **Đặc tả Visual:**
  - Tương tự như đặc tả tại [level_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/level_list_page.md).
  - Tab "Cấp độ học" ở trạng thái Active (nền `{colors.surface}`, chữ màu `{colors.primary}`, có `{elevation.glow}`) để biểu thị đang thao tác sâu trong phân hệ Cấp độ & Unit.

### 4.2 Thanh Breadcrumbs điều hướng (Top Breadcrumbs Bar - Vùng B)
- **Thành phần:**
  - **Breadcrumbs:** Dòng chữ dạng `{typography.caption}` (12px), màu `{colors.text-secondary}`. Hiển thị: *"Admin / Lộ trình học / Cấp độ: {Tên Cấp độ đã chọn} / Danh sách Unit"*.
  - Admin có thể click vào liên kết "Lộ trình học" để nhanh chóng quay trở lại màn hình danh sách cấp độ `AD-01`.

### 4.3 Thanh hành động Toolbar (Content Toolbar - Vùng C)
- **Thành phần:**
  - **Tiêu đề cấp độ học hiện tại:** Dạng chữ `{typography.display-sm}` (28px, Manrope, weight 700, màu `{colors.text-primary}`). Hiển thị: *"Cấp độ: {Tên cấp độ}"* (ví dụ: *Cấp độ: Cơ bản (A1 - A2)*).
  - **Cụm nút hành động sắp xếp và thêm mới:**
    - **Nút "Lưu thứ tự mới":** Style `button-primary` nền `{colors.primary}`, chữ trắng, cao `44px`, bo góc `{rounded.lg}`. Ẩn mặc định, chỉ hiển thị khi có sự kiện kéo thả hoán đổi vị trí Unit.
    - **Nút "Hủy thay đổi":** Style `button-secondary` nền `{colors.surface}`, viền mờ, chữ `{colors.primary}`, cao `44px`, bo góc `{rounded.lg}`. Ẩn mặc định, chỉ hiển thị khi có thay đổi thứ tự kéo thả.
    - **Nút "+ Thêm Unit mới":** Style `button-primary` nền `{colors.primary}` (`#4E56C0`), chữ trắng, cao `44px`, bo góc `{rounded.lg}`. Mặc định tỏa sáng `{elevation.active-glow}`. Bấm vào mở Modal `AD-02-M1`.

### 4.4 Danh sách thẻ Unit hỗ trợ kéo thả (Sortable Unit List - Vùng D)
- **Thẻ bài học Unit (Unit Card Item):**
  - Nền thẻ: `{colors.surface}` (`#FFFFFF`).
  - Bo góc: `{rounded.xl}` (24px).
  - Viền mờ: `1px solid rgba(155, 93, 224, 0.1)`. Padding: `{spacing.lg}` (24px).
  - Hiệu ứng nâng: Mặc định `{elevation.glow}`. Hover viền đổi sang màu `{colors.primary}` nhẹ và có con trỏ dạng grab.
  - **Thành phần bên trong thẻ:**
    - **Icon grip kéo thả:** Icon 6 dấu chấm (Lucide `grip-vertical`) nằm ở đầu ngoài cùng bên trái thẻ, màu `{colors.text-secondary}`.
    - **Nhãn số thứ tự Unit:** Badge viên thuốc `{rounded.pill}`, nền nhạt `{colors.light-accent}` (`#FDCFFA`), chữ màu `{colors.primary}`. Hiển thị dạng: *"Unit 01"*, *"Unit 02"*.
    - **Tên Unit & Chủ đề lớn:**
      - Dạng chữ `{typography.title-md}` (18px, weight 600, màu `{colors.text-primary}`). Nhấp vào tên Unit để mở màn hình danh sách bài học của Unit đó (`AD-03`).
      - Ví dụ: *"Tên Unit: Greetings & Introductions — Chủ đề: Greetings"* (theo `level_built.md`).
    - **Cụm nhãn thông tin phụ (Info Badges Area):**
      - Xếp hàng ngang dưới tên Unit gồm các badge nhỏ nền `{colors.canvas}` (`#F9F7FE`), viền mờ, chữ màu `{colors.text-secondary}`:
        - *"Từ vựng: Chào hỏi & Quốc tịch"*
        - *"Ngữ pháp: To be (Present)"*
        - *"Kỹ năng thi: IELTS"*
    - **Nút tương tác cuối thẻ:**
      - *Nút "Sửa":* Style `button-secondary` cao `40px` (có padding đảm bảo touch target 44px), viền mờ, chữ `{colors.primary}`. Bấm vào mở Modal sửa `AD-02-M2`.
      - *Nút "Xóa":* Style liên kết chữ trơn màu `{colors.error}` (`#EF4444`) (weight 600). Bấm vào kích hoạt luồng xóa `UC-02c`.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Kéo thả thẻ Unit thay đổi thứ tự**
  - Admin giữ chuột trái vào icon grip $\rightarrow$ Kéo thẻ di chuyển $\rightarrow$ Nhả chuột $\rightarrow$ Các thẻ tự động hoán đổi vị trí mượt mà, số thứ tự trên badge tự động cập nhật lại tạm thời $\rightarrow$ Xuất hiện cặp nút "Lưu thứ tự mới" & "Hủy thay đổi" ở Vùng C.
- **Hành động: Click nút "Lưu thứ tự mới"**
  - Hệ thống gửi API POST danh sách thứ tự mới lên server.
  - **API Cập nhật thứ tự:** `POST /api/units/reorder`
    - Payload: `[ { "id": 12, "sequence": 1 }, { "id": 15, "sequence": 2 } ]`
    - Response: `{ "success": true }`
  - Thành công: Đóng trạng thái chỉnh sửa, ẩn các nút Lưu/Hủy, hiện Toast màu xanh lá `{colors.success}`: *"Cập nhật thứ tự các Unit thành công!"*.
- **Hành động: Click nút "Xóa" trên thẻ Unit**
  - Hệ thống kiểm tra điều kiện xóa:
    - *Nếu Unit đã có học viên học hoặc làm bài kiểm tra:* Ngăn chặn xóa, hiện cảnh báo đỏ màu `{colors.error}`: *"Không thể xóa Unit vì hiện đang có tiến trình học tập của học viên được ghi nhận!"*.
    - *Nếu Unit trống hợp lệ:* Hiển thị Modal xác nhận xóa `AD-02-M3`.

---

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái danh sách trống (Empty State):**
  - Khi chưa có Unit nào được tạo cho cấp độ học này:
    - Ẩn danh sách. Hiển thị hình ảnh chú cá voi [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`160px x 160px`) lơ lửng ngơ ngác giữa các vì sao mờ.
    - Văn bản hiển thị: *"Cấp độ này chưa có Unit nào được khởi tạo. Hãy nhấn nút 'Thêm Unit mới' phía trên để bắt đầu xây dựng nội dung!"* dạng `{typography.body-md}` màu `{colors.text-secondary}`.
- **Trạng thái tải trang (Loading State):** Hiển thị các khối Skeleton nhấp nháy mờ dịu mắt thay thế các thẻ Unit.

---

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** Màn hình danh sách cấp độ [level_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/level_list_page.md) sau khi click chọn tên một cấp độ.
- **Đi đến:**
  - [lesson_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/lesson_list_page.md) khi click vào tên một Unit.
  - [level_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/level_list_page.md) khi click Breadcrumbs "Lộ trình học".

---

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Thiết lập hiệu ứng chuyển cảnh kéo thả mượt mà (sử dụng các thư viện như React-Beautiful-DnD hoặc tương đương) kèm theo bóng phát sáng `{elevation.active-glow}` xung quanh thẻ khi đang kéo để tạo phản hồi thị giác tốt.
- **KHÔNG ĐƯỢC:** Sử dụng bóng đổ đen thô ráp. Việc phân cấp chỉ dựa vào viền mờ hairline và dải phát sáng mờ ảo để giữ nguyên hồn thương hiệu DiveVerse.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Danh sách Unit thuộc Cấp độ (Units Management Table):** Liên kết với mảng `adminDashboardData.unitsList`. Mỗi Unit hiển thị:
  - Số thứ tự Unit: `{sequence}`
  - Tên Unit: `{name}`
  - Mã Cấp độ cha: `{levelId}`
  - Số lượng bài học: `{lessonsCount}`
  - Trạng thái hoạt động: `{status}` (active / inactive)
