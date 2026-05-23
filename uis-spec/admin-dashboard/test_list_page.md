# MÀN HÌNH: TEST LIST PAGE (MÀN HÌNH DANH SÁCH BÀI KIỂM TRA)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Test List Page (Màn hình danh sách bài kiểm tra)
- Mã use case liên quan: UC-04a, UC-04b, UC-04c
- Mã luồng người dùng liên quan: Flow AD-FL-04 (Quản lý Bài kiểm tra)
- Vai trò người dùng: Admin (Quản trị viên)
- Vị trí trong sitemap: Trang chủ quản trị -> AD-04: Test List Page (URL: /admin/tests)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng màn hình này để xem danh sách toàn bộ đề kiểm tra trong hệ thống, thực hiện tìm kiếm, lọc đề thi theo loại (Mini-test, Level test, Mock test), và kích hoạt các tính năng tạo đề thi mới, chỉnh sửa đề thi cũ hoặc xóa đề thi.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục cột kép (Sidebar cố định bên trái chiếm 260px và Vùng nội dung chính cuộn dọc bên phải chiếm phần còn lại).
- Các vùng chính trên màn hình:
  - Vùng A: Sidebar điều hướng (Fixed Navigation Sidebar) hiển thị danh mục quản trị.
  - Vùng B: Thanh đầu trang (Header / Breadcrumbs bar) hiển thị đường dẫn thư mục và thông tin tài khoản admin.
  - Vùng C: Thanh công cụ tìm kiếm và bộ lọc (Search and Filter Bar) cùng nút "Tạo đề thi mới".
  - Vùng D: Bảng danh sách đề thi (Data Table) hiển thị thông tin tổng quan của từng đề thi.
- Kích thước / Grid tham khảo:
  - Vùng bên phải chiếm phần chiều rộng còn lại, căn giữa tối đa 1280px.
  - Bảng danh sách chiếm trọn 12 cột, các cột trong bảng được phân bổ khoảng cách đồng đều.
  - Khoảng cách các phần tử: spacing-lg (24px) và spacing-xl (32px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)
- **Tên component:** Danh sách liên kết điều hướng Sidebar
  - **Loại component tham chiếu từ DESIGN.md:** nav-link / category-tab
  - **Vị trí:** Vùng A (Sidebar), danh sách chạy dọc thân Sidebar.
  - **Trạng thái:**
    - Bài kiểm tra: category-tab-active (nền surface-card #f5f0e0, chữ ink #0a0a0a, font Inter weight 600)
    - Cấp độ học: category-tab (trong suốt, chữ muted #6a6a6a)
    - Báo cáo học tập: category-tab (trong suốt, chữ muted #6a6a6a)
  - **Dữ liệu hiển thị / hành vi:** Các liên kết phân hệ quản trị. Nhấp chọn chuyển đổi qua các trang tương ứng.

- **Tên component:** Thanh dẫn Breadcrumbs
  - **Loại component tham chiếu từ DESIGN.md:** body-sm (màu muted #6a6a6a)
  - **Vị trí:** Vùng B (Header), góc trên bên trái.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị dòng chữ: "Admin / Quản lý đề thi / Danh sách bài kiểm tra".

- **Tên component:** Tiêu đề trang
  - **Loại component tham chiếu từ DESIGN.md:** display-md (Plain Black display typeface, font Inter weight 500, size 32px, letter-spacing -1px)
  - **Vị trí:** Vùng C, góc trên bên trái.
  - **Trạng thái:** Mặc định, màu chữ ink (#0a0a0a).
  - **Dữ liệu hiển thị / hành vi:** Hiển thị tiêu đề "Quản lý Đề kiểm tra".

- **Tên component:** Nút "Tạo bài kiểm tra mới"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, rounded-md 12px, height 44px, font Inter size 14px, weight 600)
  - **Vị trí:** Vùng C, góc trên bên phải, cùng hàng với tiêu đề.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị text "Tạo đề thi mới". Nhấp vào để chuyển hướng đến màn hình soạn thảo đề thi AD-04-Form.

- **Tên component:** Thanh tìm kiếm đề kiểm tra (Search Input)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, màu chữ ink #0a0a0a, border 1px hairline #e5e5e5, rounded-md 12px, height 44px, width 320px)
  - **Vị trí:** Vùng C, nằm dưới tiêu đề.
  - **Trạng thái:** Mặc định, focus.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị icon kính lúp màu muted ở góc trái, placeholder hiển thị "Tìm tên đề kiểm tra...". Admin gõ kí tự để lọc danh sách tức thì.

- **Tên component:** Bộ lọc Loại đề thi (Test Type Filter)
  - **Loại component tham chiếu từ DESIGN.md:** dropdown / select (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-md 12px, height 44px, width 180px)
  - **Vị trí:** Vùng C, nằm cạnh thanh tìm kiếm về bên phải.
  - **Trạng thái:** Mặc định, focus.
  - **Dữ liệu hiển thị / hành vi:** Cho phép lọc theo: "Tất cả loại đề", "Mini-test", "Level test", "Mock test".

- **Tên component:** Bộ lọc Cấp độ liên kết (Level Filter)
  - **Loại component tham chiếu từ DESIGN.md:** dropdown / select (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-md 12px, height 44px, width 180px)
  - **Vị trí:** Vùng C, nằm cạnh bộ lọc Loại đề thi về bên phải.
  - **Trạng thái:** Mặc định, focus.
  - **Dữ liệu hiển thị / hành vi:** Cho phép lọc theo các cấp độ liên kết (ví dụ: "Tất cả cấp độ", "Basic (A1-A2)", "Intermediate", "Advanced").

- **Tên component:** Bảng danh sách đề thi (Data Table)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-lg 16px, padding 0)
  - **Vị trí:** Vùng D.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị cấu trúc dạng bảng gồm các cột: Tên đề thi, Loại đề, Cấp độ/Unit liên kết, Thời gian (phút), Thang điểm tối đa, Ngày tạo, Hành động. Mỗi dòng hiển thị thông tin của một đề thi.

- **Tên component:** Nhãn Loại đề thi (Test Type Badge)
  - **Loại component tham chiếu từ DESIGN.md:** badge-pill (nền thay đổi theo loại, rounded-pill, font caption size 12px)
  - **Vị trí:** Vùng D, trong cột "Loại đề" của bảng.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:**
    - Mini-test: Nền brand-peach #ffb084 nhạt, chữ ink.
    - Level test: Nền brand-lavender #b8a4ed nhạt, chữ ink.
    - Mock test: Nền brand-teal #1a3a3a, chữ màu on-primary #ffffff.

- **Tên component:** Nút "Sửa" trên dòng đề thi
  - **Loại component tham chiếu từ DESIGN.md:** button-secondary (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-sm 8px, font Inter size 13px, weight 600, padding 6px x 12px)
  - **Vị trí:** Vùng D, nằm ở cột "Hành động" của mỗi dòng đề thi.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Sửa". Nhấn vào để chuyển hướng đến màn hình chỉnh sửa AD-04-Form với dữ liệu đề thi được nạp sẵn.

- **Tên component:** Nút "Xóa" trên dòng đề thi
  - **Loại component tham chiếu từ DESIGN.md:** button-text-link (màu error #ef4444, font Inter size 13px, weight 600)
  - **Vị trí:** Vùng D, nằm cạnh nút "Sửa" ở cột "Hành động".
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Xóa". Nhấn vào để mở Modal xác nhận xóa AD-04-M1.

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động:** Nhập ký tự vào thanh tìm kiếm hoặc thay đổi giá trị dropdown bộ lọc
  - **Luồng chính:** Admin thay đổi nội dung tìm kiếm/bộ lọc -> Hệ thống tự động gửi yêu cầu lấy danh sách đã lọc -> Bảng dữ liệu Vùng D tự động cập nhật danh sách đề thi tương thích mà không cần load lại trang.
- **Hành động:** Nhấp nút "Tạo đề thi mới"
  - **Luồng chính:** Admin click nút -> Chuyển hướng trình duyệt đến màn hình AD-04-Form (Create / Edit Test Page) ở trạng thái trống.
- **Hành động:** Nhấp nút "Sửa" trên dòng đề thi
  - **Luồng chính:** Admin click nút -> Chuyển hướng trình duyệt đến màn hình AD-04-Form của đề thi được chọn để chỉnh sửa.
- **Hành động:** Nhấp nút "Xóa" trên dòng đề thi
  - **Luồng chính:** Mở Modal xác nhận xóa AD-04-M1 đè lên màn hình hiện tại.

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Khi CSDL chưa có đề thi nào hoặc không tìm thấy kết quả tìm kiếm thích hợp -> Bảng danh sách ẩn đi, thay thế bằng hình ảnh 3D claymation minh họa ở giữa màn hình kèm dòng chữ: "Không tìm thấy bài kiểm tra nào phù hợp. Hãy thử thay đổi bộ lọc hoặc bấm nút 'Tạo đề thi mới'!".
- **Trạng thái tải (loading state):** Khi đang gọi dữ liệu từ máy chủ, các dòng trong bảng hiển thị hiệu ứng skeleton mờ nhấp nháy, các nút bấm bị khóa click.
- **Trạng thái lỗi (error state):** Khi kết nối máy chủ thất bại, bảng danh sách bị ẩn và hiển thị văn bản báo lỗi đỏ: "Không thể tải danh sách đề thi. Vui lòng kiểm tra lại kết nối." kèm nút "Tải lại".
- **Trạng thái thành công (success state):** Khi quay lại màn hình này sau khi thêm/sửa/xóa đề thi thành công, hệ thống hiển thị Toast thông báo xanh lá góc phải màn hình: "Thao tác đề thi thành công!".

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?**
  - Từ màn hình danh sách cấp độ AD-01 sau khi Admin nhấp chọn liên kết "Quản lý đề thi" trên Sidebar.
  - Từ màn hình Login Page sau khi đăng nhập (nếu link mặc định dẫn vào đây).
- **Sau khi hoàn thành hành động, đi đến màn hình nào?**
  - Chuyển sang màn hình AD-04-Form (Create / Edit Test Page) khi nhấn thêm/sửa đề thi.
- **Các màn hình liên quan khác:** Modal AD-04-M1 hiển thị đè lên màn hình này.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0) đặc trưng.
- Bảng dữ liệu được thiết kế dạng `product-mockup-card` không có bóng đổ, viền hairline 1px (#e5e5e5) nhẹ nhàng. Header của bảng được in đậm màu ink (#0a0a0a) bằng font Inter 14px weight 600, các dòng phân tách nhau bằng đường kẻ hairline mảnh.
- Khoảng cách padding trong bảng dữ liệu: spacing-md (16px) cho mỗi dòng để đảm bảo các dòng thông tin thông thoáng và dễ đọc.
- Touch target của các nút bấm trong bảng (Sửa, Xóa) đảm bảo kích thước chuẩn tối thiểu 44px bằng cách tăng padding trong suốt xung quanh nút.
- Màu sắc của các badge phân loại loại đề (Mock test màu teal, Level test màu lavender, Mini-test màu peach) giúp Admin nhận diện trực quan nhanh chóng theo Nguyên tắc Báo hiệu (Signaling Principle) mà không bị quá tải thông tin.



