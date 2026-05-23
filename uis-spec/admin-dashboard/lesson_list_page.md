# MÀN HÌNH: LESSON LIST PAGE (MÀN HÌNH DANH SÁCH BÀI HỌC THEO UNIT)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Lesson List Page (Màn hình danh sách bài học theo Unit)
- Mã use case liên quan: UC-03a, UC-03b, UC-03c
- Mã luồng người dùng liên quan: Flow AD-FL-03 (Cấu hình Bài học và Luyện tập)
- Vai trò người dùng: Admin (Quản trị viên)
- Vị trí trong sitemap: Trang chủ quản trị -> AD-01: Level List Page -> Click cấp độ -> AD-02: Unit List Page -> Click Unit -> AD-03: Lesson List Page (URL: /admin/units/{unit_id}/lessons)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng màn hình này để quản lý danh sách các bài học (Từ vựng, Ngữ pháp, Nghe, Nói, Đọc, Viết) trong một Unit cụ thể, xem trạng thái cấu hình của từng bài học và kích hoạt thao tác cấu hình mới, chỉnh sửa hoặc xóa bỏ cấu hình bài tập của bài học đó.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục cột kép (Sidebar cố định bên trái chiếm 260px và Vùng nội dung chính cuộn dọc bên phải chiếm phần còn lại).
- Các vùng chính trên màn hình:
  - Vùng A: Sidebar điều hướng (Fixed Navigation Sidebar) hiển thị danh mục quản trị.
  - Vùng B: Thanh đầu trang (Header / Breadcrumbs bar) hiển thị đường dẫn thư mục và thông tin tài khoản admin.
  - Vùng C: Thanh thông tin Unit (Unit Info Banner) hiển thị Tên Unit, Chủ đề lớn và các thống kê tóm tắt.
  - Vùng D: Lưới danh sách các Bài học (Lesson Grid Layout) hiển thị thông tin và trạng thái cấu hình bài học dưới dạng các thẻ.
- Kích thước / Grid tham khảo:
  - Vùng nội dung chính có chiều rộng tối đa 1280px.
  - Lưới bài học sử dụng lưới 3 cột ở màn hình desktop (3-up Grid), tự động co về 2 cột ở tablet và 1 cột ở mobile.
  - Khoảng cách spacing-lg (24px) giữa các phần tử lưới.

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)
- **Tên component:** Thanh dẫn Breadcrumbs
  - **Loại component tham chiếu từ DESIGN.md:** body-sm (màu muted #6a6a6a)
  - **Vị trí:** Vùng B (Header), góc trên bên trái.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị dòng chữ: "Admin / Lộ trình học / {Tên Cấp độ} / {Tên Unit} / Danh sách bài học". Admin có thể click vào các liên kết để quay lại màn hình AD-01 hoặc AD-02.

- **Tên component:** Thẻ Banner thông tin Unit
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-ochre (nền brand-ochre #e8b94a, chữ màu ink #0a0a0a, rounded-xl 24px, padding 32px)
  - **Vị trí:** Vùng C.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị Tiêu đề "Chi tiết bài học của Unit: {Tên Unit}" (Plain Black, size 24px, weight 500), kèm các tag nhỏ màu canvas ghi: "Chủ đề: {Chủ đề lớn}" và "Kỹ năng: {IELTS / TOEIC}".

- **Tên component:** Lưới thẻ Bài học (Lesson Cards Grid)
  - **Loại component tham chiếu từ DESIGN.md:** grid 3-up (desktop)
  - **Vị trí:** Vùng D.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Chứa 6 thẻ tương đương 6 bài học bắt buộc trong mỗi Unit: Từ vựng, Ngữ pháp, Luyện nghe, Luyện nói, Luyện đọc, Luyện viết.

- **Tên component:** Thẻ bài học (Lesson Card Item)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền surface-card #f5f0e0, border 1px hairline #e5e5e5, rounded-xl 24px, padding 24px)
  - **Vị trí:** Vùng D, nằm trong lưới.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Mỗi thẻ bài học hiển thị:
    - Loại kỹ năng (dưới dạng Badge: Từ vựng, Ngữ pháp, Nghe, Nói, Đọc, Viết).
    - Tên bài học do admin cấu hình hoặc mặc định (ví dụ: "Vocabulary: Everyday Objects").
    - Trạng thái cấu hình (Badge: "Đã cấu hình" màu success hoặc "Chưa cấu hình" màu muted).
    - Bộ nút hành động nằm dưới cùng của thẻ bài học.

- **Tên component:** Nhãn kỹ năng (Lesson Category Badge)
  - **Loại component tham chiếu từ DESIGN.md:** badge-pill (nền canvas #fffaf0, rounded-pill, font caption size 13px, weight 600)
  - **Vị trí:** Vùng D, góc trên bên trái trong mỗi thẻ bài học.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị văn bản: "VOCABULARY", "GRAMMAR", "LISTENING", "SPEAKING", "READING", hoặc "WRITING".

- **Tên component:** Nhãn trạng thái cấu hình (Configuration Status Badge)
  - **Loại component tham chiếu từ DESIGN.md:** badge-pill (nền thay đổi theo trạng thái, rounded-pill, font caption size 12px)
  - **Vị trí:** Vùng D, góc trên bên phải trong mỗi thẻ bài học.
  - **Trạng thái:**
    - Trạng thái đã cấu hình: nền success nhẹ, chữ success sẫm (#22c55e), text "Đã cấu hình".
    - Trạng thái chưa cấu hình: nền surface-strong #ebe6d6, chữ muted #6a6a6a, text "Chưa cấu hình".

- **Tên component:** Tiêu đề bài học trên thẻ
  - **Loại component tham chiếu từ DESIGN.md:** title-md (font Inter 18px, weight 600, màu ink #0a0a0a)
  - **Vị trí:** Vùng D, ở giữa thẻ bài học.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị tên bài học (ví dụ: "Bài học từ vựng Unit 1" hoặc "Luyện đọc hiểu đoạn văn ngắn").

- **Tên component:** Nút "Cấu hình" (dành cho bài chưa cấu hình)
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, rounded-md 12px, height 44px, width 100%)
  - **Vị trí:** Vùng D, ở đáy thẻ bài học chưa cấu hình.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị text "Cấu hình bài học". Nhấp vào để chuyển hướng đến màn hình soạn thảo cấu hình AD-03-Form.

- **Tên component:** Nút "Sửa cấu hình" (dành cho bài đã cấu hình)
  - **Loại component tham chiếu từ DESIGN.md:** button-secondary (nền canvas #fffaf0, border 1px hairline #e5e5e5, chữ ink #0a0a0a, rounded-md 12px, height 44px, width 48% của vùng chứa nút)
  - **Vị trí:** Vùng D, góc dưới bên trái thẻ bài học đã cấu hình.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Sửa". Nhấn vào để chuyển hướng đến màn hình chỉnh sửa AD-03-Form với các dữ liệu cũ đã được tải sẵn.

- **Tên component:** Nút "Xóa cấu hình" (dành cho bài đã cấu hình)
  - **Loại component tham chiếu từ DESIGN.md:** button-text-link (màu error #ef4444, font Inter 14px, weight 600, padding dọc đảm bảo touch target 44px)
  - **Vị trí:** Vùng D, góc dưới bên phải thẻ bài học đã cấu hình.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Xóa cấu hình". Nhấn vào để kích hoạt luồng xóa cấu hình bài học (UC-03c).

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động:** Nhấp nút "Cấu hình" hoặc "Sửa cấu hình"
  - **Luồng chính:** Admin nhấp chuột vào nút -> Chuyển hướng trình duyệt đến màn hình AD-03-Form (Lesson Configuration Page) của bài học đã chọn.
- **Hành động:** Nhấp nút "Xóa cấu hình"
  - **Luồng chính:** Hệ thống kiểm tra điều kiện xóa (Bài học này đã có dữ liệu làm bài và điểm số của học viên hay chưa):
    - *Nhánh bài học đã có học viên học:* Hệ thống ngăn chặn xóa và hiển thị cảnh báo lỗi Toast màu đỏ: "Không thể xóa cấu hình vì bài học đã có tiến trình học tập của học viên".
    - *Nhánh bài học trống hợp lệ:* Xuất hiện Modal xác nhận xóa cấu hình AD-03-M1 đè lên giao diện hiện tại.

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Không áp dụng trực tiếp cho danh sách này vì số lượng thẻ bài học cố định là 6 kỹ năng/bài học nền tảng bắt buộc theo kiến trúc chương trình.
- **Trạng thái tải (loading state):** Khi tải trạng thái của các bài học từ máy chủ, các thẻ bài học hiển thị Skeleton xám mờ và các nút bấm bị ẩn đi.
- **Trạng thái lỗi (error state):** Khi mất kết nối API, lưới bài học ẩn đi và hiển thị dòng chữ thông báo lỗi "Không thể tải danh sách bài học. Vui lòng kiểm tra lại đường truyền." kèm nút "Tải lại".
- **Trạng thái thành công (success state):** Khi xóa cấu hình bài học thành công và quay lại trang này, hiển thị Toast thông báo xanh lá góc phải màn hình: "Xóa cấu hình bài học thành công!". Trạng thái thẻ chuyển về "Chưa cấu hình" và nút chuyển thành "Cấu hình bài học".

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ màn hình AD-02 (Unit List Page) sau khi Admin click vào tên một Unit cụ thể.
- **Sau khi hoàn thành hành động, đi đến màn hình nào?**
  - Đi đến màn hình AD-03-Form (Lesson Configuration Page) để viết bài học.
  - Quay lại màn hình AD-02 (Unit List Page) khi click vào Breadcrumbs "Danh sách Unit".
- **Các màn hình liên quan khác:** Modal AD-03-M1 hiển thị trực tiếp đè trên màn hình này.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0) đặc trưng của Clay.com.
- Các thẻ bài học được thiết kế bằng phong cách `feature-card-cream` có góc bo rất lớn rounded-xl (24px) và nền surface-card (#f5f0e0), tạo cảm giác mập mạp và đồng điệu với logo 3D đất sét của hệ thống.
- Khoảng cách thưa spacing-lg (24px) giữa các thẻ bài học đảm bảo sự thoáng mát về thị giác, giảm cảm giác áp lực khi quản trị lượng nội dung khổng lồ.
- Touch target của tất cả các nút hành động (Cấu hình, Sửa, Xóa) đảm bảo kích thước tối thiểu 44x44px. Nút "Xóa cấu hình" hiển thị màu đỏ (#ef4444) dạng chữ trơn không nền để biểu thị mức độ nghiêm trọng nhưng không làm loãng tiêu điểm thị giác chính.
