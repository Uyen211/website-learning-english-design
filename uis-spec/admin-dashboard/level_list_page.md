# MÀN HÌNH: LEVEL LIST PAGE (MÀN HÌNH DANH SÁCH CẤP ĐỘ)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Level List Page (Màn hình danh sách cấp độ)
- Mã use case liên quan: UC-01a, UC-01b, UC-01c
- Mã luồng người dùng liên quan: Flow AD-FL-01, Flow AD-FL-02
- Vai trò người dùng: Admin
- Vị trí trong sitemap: Trang chủ quản trị -> AD-01: Level List Page

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng màn hình này để xem danh sách toàn bộ các cấp độ học (lộ trình) trong hệ thống, thực hiện sắp xếp, truy cập danh sách Unit của từng cấp độ, hoặc kích hoạt các chức năng thêm, sửa, xóa cấp độ học.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục cột kép gồm Sidebar cố định bên trái và Vùng nội dung chính cuộn dọc bên phải.
- Các vùng chính trên màn hình:
  - Vùng A: Sidebar điều hướng (Fixed Navigation Sidebar) nằm bên trái.
  - Vùng B: Thanh đầu trang (Header / Breadcrumbs bar) ở trên cùng vùng bên phải.
  - Vùng C: Thanh công cụ nội dung (Content Toolbar) hiển thị tiêu đề và nút hành động.
  - Vùng D: Vùng lưới danh sách các cấp độ học (Level Cards Grid) hiển thị thông tin chi tiết các cấp độ dưới dạng thẻ.
- Kích thước / Grid tham khảo:
  - Sidebar: cố định chiều rộng 260px.
  - Vùng bên phải chiếm phần chiều rộng còn lại, căn giữa tối đa 1280px, sử dụng lưới 12 cột.
  - Khoảng cách các phần tử: spacing-lg (24px) và spacing-xl (32px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)
- **Tên component:** Logo & Wordmark DiveVerse
  - **Loại component tham chiếu từ DESIGN.md:** top-nav brand component
  - **Vị trí:** Vùng A, ở trên cùng của Sidebar
  - **Trạng thái:** Mặc định
  - **Dữ liệu hiển thị / hành vi:** Hiển thị Logo 3D claymation và chữ "DiveVerse Admin" dạng vector màu ink.

- **Tên component:** Danh sách liên kết điều hướng Sidebar
  - **Loại component tham chiếu từ DESIGN.md:** nav-link / category-tab
  - **Vị trí:** Vùng A, phần thân Sidebar
  - **Trạng thái:**
    - Cấp độ học: category-tab-active (nền surface-card #f5f0e0, chữ ink #0a0a0a)
    - Bài kiểm tra: category-tab (trong suốt, chữ muted #6a6a6a)
    - Báo cáo học tập: category-tab (trong suốt, chữ muted #6a6a6a)
  - **Dữ liệu hiển thị / hành vi:** Các liên kết chuyển đổi phân hệ quản trị. Nhấp "Bài kiểm tra" chuyển sang AD-04.

- **Tên component:** Thanh Breadcrumbs
  - **Loại component tham chiếu từ DESIGN.md:** body-sm (màu muted #6a6a6a)
  - **Vị trí:** Vùng B, góc trên bên trái
  - **Trạng thái:** Mặc định
  - **Dữ liệu hiển thị / hành vi:** Hiển thị dòng chữ dẫn đường dạng text-link: "Admin / Lộ trình học / Danh sách cấp độ".

- **Tên component:** Avatar quản trị viên
  - **Loại component tham chiếu từ DESIGN.md:** rounded-full (avatar size 36px)
  - **Vị trí:** Vùng B, góc trên bên phải
  - **Trạng thái:** Mặc định
  - **Dữ liệu hiển thị / hành vi:** Hiển thị ảnh đại diện admin, nhấp vào hiển thị dropdown menu "Đăng xuất".

- **Tên component:** Tiêu đề trang
  - **Loại component tham chiếu từ DESIGN.md:** display-md (Plain Black display typeface, size 40px, weight 500, letter-spacing -1px)
  - **Vị trí:** Vùng C, góc bên trái
  - **Trạng thái:** Mặc định, màu chữ là ink
  - **Dữ liệu hiển thị / hành vi:** Hiển thị tiêu đề "Cấp độ học".

- **Tên component:** Nút thêm cấp độ mới
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (background #0a0a0a, text #ffffff, rounded-md 12px, font Inter 14px/600)
  - **Vị trí:** Vùng C, góc bên phải, thẳng hàng với tiêu đề
  - **Trạng thái:** Mặc định, hover
  - **Dữ liệu hiển thị / hành vi:** Hiển thị text "Thêm cấp độ mới". Nhấp vào để kích hoạt Modal AD-01-M1.

- **Tên component:** Lưới thẻ cấp độ học (Level Cards Grid)
  - **Loại component tham chiếu từ DESIGN.md:** grid 3-up (desktop) / 2-up (tablet)
  - **Vị trí:** Vùng D, trung tâm vùng nội dung
  - **Trạng thái:** Mặc định
  - **Dữ liệu hiển thị / hành vi:** Hiển thị danh sách các thẻ cấp độ học. Mỗi thẻ cấp độ được thiết kế dạng `feature-card-cream` (nền surface-card #f5f0e0, border-radius 24px) chứa các thông tin cụ thể bên dưới.

- **Tên component:** Tên cấp độ trên thẻ
  - **Loại component tham chiếu từ DESIGN.md:** title-lg (font Inter 24px/600, letter-spacing -0.3px)
  - **Vị trí:** Vùng D, nằm ở đầu mỗi thẻ cấp độ
  - **Trạng thái:** Mặc định, màu ink
  - **Dữ liệu hiển thị / hành vi:** Hiển thị tên cấp độ (ví dụ: "Cơ bản (A1 - A2)", "Trung cấp (B1 - B2)"). Admin nhấp vào tên cấp độ để mở màn hình danh sách Unit tương ứng (AD-02).

- **Tên component:** Nội dung mô tả cấp độ
  - **Loại component tham chiếu từ DESIGN.md:** body-md (font Inter 16px, màu body #3a3a3a)
  - **Vị trí:** Vùng D, nằm dưới tên cấp độ trên thẻ
  - **Trạng thái:** Mặc định
  - **Dữ liệu hiển thị / hành vi:** Hiển thị đoạn mô tả ngắn của cấp độ đó.

- **Tên component:** Điểm số và số Unit quy chiếu (Tags)
  - **Loại component tham chiếu từ DESIGN.md:** badge-pill (nền #faf5e8 hoặc canvas, rounded-pill, font caption 13px/500)
  - **Vị trí:** Vùng D, nằm ở giữa thẻ cấp độ
  - **Trạng thái:** Mặc định
  - **Dữ liệu hiển thị / hành vi:** Hiển thị các nhãn điểm mục tiêu như "IELTS Target: 4.5", "TOEIC Target: 450", "Tối đa: 15 Units".

- **Tên component:** Nút Sửa trên thẻ
  - **Loại component tham chiếu từ DESIGN.md:** button-secondary (background #fffaf0, border 1px hairline #e5e5e5, rounded-sm 8px, font Inter 14px/600)
  - **Vị trí:** Vùng D, góc dưới bên trái của mỗi thẻ cấp độ
  - **Trạng thái:** Mặc định, hover
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Sửa". Nhấn vào để mở Modal AD-01-M2 chỉnh sửa cấp độ đó.

- **Tên component:** Nút Xóa trên thẻ
  - **Loại component tham chiếu từ DESIGN.md:** button-text-link / text-link (màu error #ef4444, font Inter 14px/600)
  - **Vị trí:** Vùng D, góc dưới bên phải của mỗi thẻ cấp độ
  - **Trạng thái:** Mặc định, hover
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Xóa". Nhấn vào để kích hoạt luồng xóa cấp độ (UC-01c).

## 5. CHI TIẾT TƯƠNG TÁC
- **Hành động:** Nhấp vào tên một Cấp độ học trên thẻ
  - **Luồng chính:** Admin nhấp chuột vào tên cấp độ -> Chuyển hướng sang màn hình AD-02 (Unit List Page của cấp độ đã chọn).
  - **Dữ liệu gửi lên / nhận về:** Gửi đi ID cấp độ học được chọn.
- **Hành động:** Nhấp nút "Thêm cấp độ mới"
  - **Luồng chính:** Admin nhấp nút -> Hiển thị Modal AD-01-M1 đè lên giao diện hiện tại.
- **Hành động:** Nhấp nút "Sửa" trên thẻ cấp độ
  - **Luồng chính:** Admin nhấp nút -> Hiển thị Modal AD-01-M2 chứa dữ liệu của cấp độ được chọn đè lên giao diện hiện tại.
- **Hành động:** Nhấp nút "Xóa" trên thẻ cấp độ
  - **Luồng chính:** Admin nhấp nút -> Hệ thống kiểm tra điều kiện xóa (UC-01c):
    - Nếu cấp độ đang có học viên học -> Hiển thị thông báo báo lỗi: "Không thể xóa cấp độ này vì đang có [X] người học hoạt động...".
    - Nếu cấp độ trống hợp lệ -> Hiển thị Modal xác nhận xóa AD-01-M3.

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT
- **Trạng thái rỗng (empty state):** Khi CSDL chưa có cấp độ học nào -> Vùng D ẩn lưới thẻ, hiển thị hình ảnh minh họa 3D claymation tối giản kèm dòng chữ "Chưa có cấp độ học nào được tạo. Hãy nhấn nút 'Thêm cấp độ mới' phía trên để bắt đầu." ở chính giữa màn hình.
- **Trạng thái tải (loading state):** Khi đang tải dữ liệu cấp độ học từ máy chủ -> Các thẻ cấp độ được hiển thị dưới dạng khung xương xám mờ (Skeleton Cards) nhấp nháy nhẹ.
- **Trạng thái lỗi (error state):** Khi kết nối máy chủ thất bại -> Vùng D hiển thị thông báo lỗi "Không thể tải danh sách cấp độ học. Vui lòng kiểm tra lại kết nối mạng." kèm theo nút "Tải lại trang" (button-secondary).
- **Trạng thái thành công (success state):** Khi thêm, sửa hoặc xóa cấp độ thành công từ các Modal và quay lại màn hình này -> Hệ thống hiển thị Toast thông báo màu xanh lá (#22c55e) ở góc trên bên phải màn hình: "Thực hiện thành công!".

## 7. THAM CHIẾU LUỒNG
- **Đến từ màn hình nào trước đó?** Từ Admin Login Page (TR-04) sau khi đăng nhập thành công.
- **Sau khi hoàn thành hành động, đi đến màn hình nào?**
  - Chuyển sang màn hình AD-02 (Unit List Page) sau khi nhấp vào một tên cấp độ.
  - Chuyển sang màn hình AD-04 (Test List Page) khi nhấp chọn liên kết bài kiểm tra trên Sidebar.
- **Các màn hình liên quan khác:** Modal AD-01-M1, AD-01-M2, AD-01-M3 hiển thị trực tiếp đè trên màn hình này.

## 8. LƯU Ý THIẾT KẾ
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0) đặc trưng để tạo sự dễ chịu.
- Thiết kế lưới thẻ cấp độ rõ ràng với khoảng cách spacing-lg (24px) giữa các thẻ nhằm giảm tải nhận thức và tối ưu hóa phân cấp thị giác theo Nguyên tắc Báo hiệu (Signaling Principle) bằng cách in đậm tên cấp độ.
- Các nút tương tác "Sửa" và "Xóa" trên thẻ đảm bảo touch target đạt tối thiểu 44x44px bằng cách tăng vùng đệm padding trong suốt xung quanh nút.
- Không sử dụng các đường viền hay bóng đổ đậm. Ranh giới giữa Sidebar và Content Area chỉ là một đường hairline 1px tinh tế (#e5e5e5).



