# MÀN HÌNH: TEST LIST PAGE (MÀN HÌNH DANH SÁCH BÀI KIỂM TRA)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Test List Page (Màn hình danh sách bài kiểm tra)
- **Mã use case liên quan:** UC-04a, UC-04b, UC-04c
- **Mã luồng người dùng liên quan:** Flow AD-FL-04 (Quản lý Bài kiểm tra)
- **Vai trò người dùng:** Admin (Quản trị viên)
- **Vị trí trong sitemap:** Trang chủ quản trị $\rightarrow$ AD-04: Test List Page (URL: `/admin/tests`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng màn hình này để quản lý toàn bộ các bài kiểm tra đánh giá năng lực trong hệ thống DiveVerse. Admin có thể thực hiện tìm kiếm đề thi, lọc danh sách theo thể loại đề (Mini-test, Level test, Mock test) và cấp độ học liên kết, đồng thời kích hoạt các phân hệ soạn thảo đề kiểm tra mới, chỉnh sửa đề kiểm tra cũ, hoặc xóa đề thi.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục cột kép gồm Sidebar cố định bên trái chiếm `260px` và Vùng nội dung chính cuộn dọc bên phải.
- **Màu nền chung:** Nền trang chính sử dụng tông màu `{colors.canvas}` (`#F9F7FE`) phủ sương mờ `{gradients.atmosphere-haze}`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Left Navigation Sidebar (Vùng A):** Sidebar điều hướng cố định bên trái.
  - **Zone 2: Header Breadcrumbs Bar (Vùng B):** Thanh dẫn thư mục và thông tin tài khoản admin.
  - **Zone 3: Search, Filter & Action Bar (Vùng C):** Tiêu đề trang, nút "Tạo đề thi mới", thanh tìm kiếm từ khóa, và hai hộp chọn bộ lọc phân loại.
  - **Zone 4: Tests Data Table (Vùng D):** Bảng dữ liệu lớn hiển thị danh sách các đề kiểm tra trong hệ thống.
- **Kích thước tham khảo:**
  - Chiều rộng tối đa của vùng nội dung chính bên phải: `1200px`.
  - Bảng danh sách chiếm trọn 12 cột, khoảng cách dọc giữa các khối điều khiển: `{spacing.lg}` (24px).

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh điều hướng Sidebar quản trị (Navigation Sidebar - Vùng A)
- **Đặc tả Visual:**
  - Tương tự như đặc tả tại [level_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/level_list_page.md).
  - Tab "Bài kiểm tra" ở trạng thái Active (nền `{colors.surface}`, chữ màu `{colors.primary}`, có `{elevation.glow}`) để biểu thị đang làm việc với phân hệ Quản lý đề thi.

### 4.2 Thanh Breadcrumbs điều hướng (Top Breadcrumbs Bar - Vùng B)
- **Breadcrumbs:** Dòng chữ dạng `{typography.caption}` (12px), màu `{colors.text-secondary}`. Hiển thị: *"Admin / Quản lý đề thi / Danh sách bài kiểm tra"*.

### 4.3 Khu vực tìm kiếm, bộ lọc & hành động (Toolbar Areas - Vùng C)
- **Tiêu đề trang:** Dạng chữ `{typography.display-sm}` (28px, Manrope, weight 700, màu `{colors.text-primary}`). Hiển thị: *"Quản lý Đề kiểm tra"*.
- **Nút "Tạo đề thi mới":** Style `button-primary` nền `{colors.primary}` (`#4E56C0`), chữ trắng, cao `44px`, bo góc `{rounded.lg}` (16px). Mặc định tỏa sáng `{elevation.active-glow}`. Bấm vào chuyển hướng sang trang soạn thảo `AD-04-Form`.
- **Thanh tìm kiếm đề kiểm tra (Search Input):**
  - Loại component: `text-input` cao `44px`, rộng `320px`, bo góc `{rounded.lg}` (16px), nền `{colors.surface}`.
  - Icon: Kính lúp (Lucide `search`) ở góc trái. Placeholder: *"Tìm tên đề kiểm tra..."*.
- **Bộ lọc Loại đề thi (Test Type Filter):**
  - Loại component: Dropdown/Select cao `44px`, rộng `180px`, bo góc `{rounded.lg}` (16px), nền `{colors.surface}`, viền mờ `1px solid rgba(155, 93, 224, 0.2)`.
  - Lựa chọn: *Tất cả loại đề*, *Mini-test*, *Level test*, *Mock test*.
- **Bộ lọc Cấp độ liên kết (Level Filter):**
  - Tương tự dropdown Loại đề thi. Lựa chọn các cấp độ từ `level_built.md`: *Tất cả cấp độ*, *Basic (A1-A2)*, *Intermediate*, *Advanced*.

### 4.4 Bảng danh sách đề thi (Tests Data Table - Vùng D)
- **Đặc tả Visual:**
  - Nền bảng: `{colors.surface}` (`#FFFFFF`).
  - Bo góc: `{rounded.xl}` (24px). Padding: `{spacing.md}` (16px).
  - Viền mờ: `1px solid rgba(155, 93, 224, 0.1)`. Hiệu ứng nâng: `{elevation.glow}`.
- **Thành phần bảng:**
  - Bảng gồm các cột: Tên đề thi, Loại đề, Cấp độ/Unit liên kết, Thời gian (phút), Điểm số tối đa, Ngày tạo, Hành động.
  - Header của bảng: Chữ dạng `{typography.caption}` (12px, weight 600, màu `{colors.text-primary}` đậm), viết hoa, phân tách với dữ liệu bằng một đường hairline siêu mảnh.
  - Mỗi dòng là một đề thi, khoảng cách padding dọc mỗi dòng `16px` để dễ quan sát. Các dòng phân tách nhau bằng đường viền ngang mảnh `1px solid rgba(155, 93, 224, 0.05)`.
  - **Badge Loại đề thi (Test Type Badge):**
    - *Mini-test:* Nền nhạt `{colors.light-accent}` (`#FDCFFA`), chữ màu `{colors.primary}` (`#4E56C0`), tag bo tròn dạng viên thuốc.
    - *Level test:* Nền nhạt `{colors.accent}` (`#D78FEE`) ở mức 15% opacity, chữ màu `{colors.secondary}` (`#9B5DE0`), tag bo tròn.
    - *Mock test:* Nền đậm `{colors.primary}` (`#4E56C0`) ở mức 15% opacity, chữ màu `{colors.primary}`, tag bo tròn.
  - **Bộ nút tương tác cuối dòng (cột Hành động):**
    - *Nút "Sửa":* Style `button-secondary` cao `36px` (padding đảm bảo touch target 44px), viền mờ, chữ `{colors.primary}`. Bấm vào chuyển hướng sang trang soạn thảo `AD-04-Form` ở chế độ chỉnh sửa.
    - *Nút "Xóa":* Style liên kết chữ trơn màu `{colors.error}` (`#EF4444`) (weight 600). Bấm vào mở Modal xác nhận xóa `AD-04-M1`.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Tìm kiếm từ khóa hoặc lọc dropdown**
  - Admin gõ phím hoặc đổi bộ lọc $\rightarrow$ Hệ thống tự động gửi yêu cầu API lấy danh sách đã lọc (áp dụng debounce `300ms` cho ô tìm kiếm) $\rightarrow$ Bảng tự động tải lại thông tin phù hợp mà không cần load lại trang.
- **Hành động: Click nút "Xóa" trên dòng đề thi**
  - Mở Modal xác nhận xóa `AD-04-M1` nổi đè lên trên màn hình hiện tại.

---

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái kết quả trống (Empty State):**
  - Khi không tìm thấy đề kiểm tra nào phù hợp:
    - Ẩn bảng dữ liệu. Hiển thị hình ảnh chú cá voi [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`160px x 160px`) soi kính lúp tìm kiếm trong vũ trụ.
    - Văn bản hiển thị: *"Không tìm thấy đề kiểm tra nào phù hợp. Hãy thử thay đổi bộ lọc hoặc tạo đề thi mới!"* dạng `{typography.body-md}` màu `{colors.text-secondary}`.
- **Trạng thái tải trang (Loading State):** Bảng dữ liệu hiển thị các hiệu ứng dòng Skeleton nhấp nháy xám mờ mượt mà, các nút hành động khóa tương tác click.

---

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** Màn hình danh sách cấp độ `AD-01` sau khi click liên kết "Bài kiểm tra" trên Sidebar, hoặc các trang soạn thảo thi sau khi bấm lưu/hủy.
- **Đi đến:** [create_edit_test_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/create_edit_test_page.md) khi bấm nút tạo mới hoặc chỉnh sửa một đề thi.

---

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Thiết lập độ tương phản hợp lý giữa văn bản header bảng và dữ liệu dòng để giúp Admin dễ dàng dò đọc các bảng dữ liệu có mật độ thông tin cao.
- **KHÔNG ĐƯỢC:** Sử dụng các bóng đổ thô cứng màu đen. Chiều sâu nổi của bảng dữ liệu được tạo bởi viền hairline màu nhạt và hiệu ứng phát sáng nhẹ `{elevation.glow}` để giữ trọn vẹn nét mềm mịn của hệ thống.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Danh sách Đề kiểm tra & Đề thi thử (Tests Management Table):** Liên kết với mảng `adminDashboardData.testsList`. Mỗi đề thi hiển thị:
  - Tên bài thi: `{name}`
  - Dạng bài kiểm tra: `{type}` (Mini-test, Mock test, etc.)
  - Cột mốc liên kết: `{levelUnit}`
  - Thời gian làm bài: `{duration}` phút
  - Trạng thái: `{status}` (active / inactive)
