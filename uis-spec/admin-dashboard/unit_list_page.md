# MÀN HÌNH: UNIT LIST PAGE (MÀN HÌNH DANH SÁCH UNIT THEO CẤP ĐỘ)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Unit List Page (Màn hình danh sách Unit theo cấp độ)
- Mã use case liên quan: UC-02a, UC-02b, UC-02c, UC-02d
- Mã luồng người dùng liên quan: Flow AD-FL-02 (Quản lý Unit)
- Vai trò người dùng: Admin (Quản trị viên)
- Vị trí trong sitemap: Trang chủ quản trị -> AD-01: Level List Page -> Click tên cấp độ -> AD-02: Unit List Page (URL: /admin/levels/{level_id}/units)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng màn hình này để xem danh sách toàn bộ các Unit thuộc một Cấp độ học cụ thể, thay đổi thứ tự sắp xếp của các Unit bằng cách kéo thả trực quan, và kích hoạt các hộp thoại thêm, sửa, xóa các Unit trong cấp độ này.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục cột kép (Sidebar cố định bên trái chiếm 260px và Vùng nội dung chính cuộn dọc bên phải chiếm phần còn lại).
- Các vùng chính trên màn hình:
  - Vùng A: Sidebar điều hướng (Fixed Navigation Sidebar) hiển thị danh mục quản trị.
  - Vùng B: Thanh đầu trang (Header / Breadcrumbs bar) hiển thị đường dẫn thư mục và thông tin tài khoản admin.
  - Vùng C: Thanh công cụ nội dung (Content Toolbar) gồm tiêu đề Cấp độ học hiện tại, nút "Thêm Unit mới" và nút "Lưu thứ tự" (khi có thay đổi sắp xếp).
  - Vùng D: Danh sách các thẻ Unit dạng danh sách cuộn dọc (Drag-and-Drop Sortable List). Mỗi thẻ Unit chứa các thông tin của Unit đó.
- Kích thước / Grid tham khảo:
  - Max-width của vùng nội dung chính bên phải: 1200px.
  - Danh sách Unit được xếp dọc theo một cột 12-column, mỗi thẻ Unit chiếm trọn 12 cột để có chiều rộng tối đa, khoảng cách dọc giữa các thẻ: spacing-md (16px).
  - Khoảng cách padding bao quanh nội dung chính: spacing-xl (32px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)
- **Tên component:** Danh sách liên kết điều hướng Sidebar
  - **Loại component tham chiếu từ DESIGN.md:** nav-link / category-tab
  - **Vị trí:** Vùng A (Sidebar), danh sách chạy dọc thân Sidebar.
  - **Trạng thái:**
    - Cấp độ học: category-tab-active (nền surface-card #f5f0e0, chữ ink #0a0a0a, font Inter weight 600) để thể hiện đang làm việc với Cấp độ & Unit.
    - Bài kiểm tra: category-tab (trong suốt, chữ muted #6a6a6a)
    - Báo cáo học tập: category-tab (trong suốt, chữ muted #6a6a6a)
  - **Dữ liệu hiển thị / hành vi:** Các nút bấm chuyển đổi phân hệ. Nhấp chuột vào sẽ chuyển trang.

- **Tên component:** Thanh dẫn Breadcrumbs
  - **Loại component tham chiếu từ DESIGN.md:** body-sm (màu muted #6a6a6a)
  - **Vị trí:** Vùng B (Header), góc trên bên trái.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị dòng văn bản dạng liên kết: "Admin / Lộ trình học / Cấp độ: {Tên Cấp độ đã chọn} / Danh sách Unit". Người học/Admin có thể nhấp vào "Lộ trình học" để quay lại AD-01.

- **Tên component:** Tiêu đề cấp độ học hiện tại
  - **Loại component tham chiếu từ DESIGN.md:** display-md (Plain Black display typeface, font Inter weight 500, size 32px, letter-spacing -1px)
  - **Vị trí:** Vùng C, góc bên trái thanh công cụ.
  - **Trạng thái:** Mặc định, màu ink (#0a0a0a).
  - **Dữ liệu hiển thị / hành vi:** Hiển thị tên cấp độ học đang xem danh sách Unit (ví dụ: "Cấp độ: Cơ bản (A1 - A2)").

- **Tên component:** Nút "Thêm Unit mới"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, font Inter size 14px, weight 600, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng C, góc bên phải thanh công cụ.
  - **Trạng thái:** Mặc định, hover, active.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị text "+ Thêm Unit mới". Nhấp chuột sẽ hiển thị Modal AD-02-M1.

- **Tên component:** Nút "Lưu thứ tự"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, font Inter size 14px, weight 600, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng C, nằm cạnh nút "Thêm Unit mới" về bên trái.
  - **Trạng thái:**
    - Ẩn mặc định khi thứ tự danh sách chưa thay đổi.
    - Hiển thị khi Admin thực hiện thao tác kéo thả thay đổi vị trí ít nhất một Unit.
    - Hover: sáng nhẹ.
    - Loading: xoay spinner trắng, vô hiệu hóa nút.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị text "Lưu thứ tự mới". Nhấp vào để lưu vị trí Unit mới vào cơ sở dữ liệu.

- **Tên component:** Nút "Hủy thay đổi"
  - **Loại component tham chiếu từ DESIGN.md:** button-secondary (nền canvas #fffaf0, border 1px hairline #e5e5e5, chữ ink #0a0a0a, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng C, nằm cạnh nút "Lưu thứ tự" về bên trái.
  - **Trạng thái:** Ẩn mặc định, chỉ hiển thị khi có thay đổi thứ tự kéo thả.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị text "Hủy thay đổi". Nhấp chuột để phục hồi danh sách về thứ tự ban đầu.

- **Tên component:** Danh sách thẻ Unit (Drag-and-Drop)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-lg 16px, padding 20px)
  - **Vị trí:** Vùng D.
  - **Trạng thái:** Mặc định. Có thể kéo thả từng thẻ lên xuống.
  - **Dữ liệu hiển thị / hành vi:** Mỗi dòng là một thẻ Unit có thể kéo thả. Đầu thẻ có icon grip 6 chấm biểu thị tính năng kéo thả. Thẻ hiển thị các thông tin: Số thứ tự Unit, Tên Unit, Chủ đề lớn, Chủ điểm từ vựng, Chủ điểm ngữ pháp, Kỹ năng thi.

- **Tên component:** Số thứ tự Unit (Unit Number Badge)
  - **Loại component tham chiếu từ DESIGN.md:** badge-pill (nền #f5f0e0, chữ ink #0a0a0a, font caption size 13px, weight 600, rounded-pill)
  - **Vị trí:** Vùng D, góc trên bên trái trong mỗi thẻ Unit.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị dạng "Unit 01", "Unit 02", v.v.

- **Tên component:** Tên Unit & Chủ đề
  - **Loại component tham chiếu từ DESIGN.md:** title-md (font Inter 18px, weight 600, màu ink #0a0a0a)
  - **Vị trí:** Vùng D, ở phần giữa thẻ Unit.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị dạng "Tên Unit: {Tên} - Chủ đề: {Chủ đề lớn}". Nhấp vào tên Unit sẽ chuyển hướng sang màn hình AD-03 (Lesson List Page của Unit đó).

- **Tên component:** Các thẻ thông tin bổ trợ (Info Badges)
  - **Loại component tham chiếu từ DESIGN.md:** badge-pill (nền canvas #fffaf0, border 1px hairline #e5e5e5, font Inter 13px, màu body #3a3a3a)
  - **Vị trí:** Vùng D, nằm dưới tên Unit.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị các nhãn: "Từ vựng: {Chủ điểm}", "Ngữ pháp: {Chủ điểm}", "Kỹ năng kiểm tra: {IELTS / TOEIC}".

- **Tên component:** Nút "Sửa" trên thẻ Unit
  - **Loại component tham chiếu từ DESIGN.md:** button-secondary (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-sm 8px, font Inter size 13px, weight 600, padding 8px x 12px)
  - **Vị trí:** Vùng D, góc dưới bên phải thẻ Unit.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Sửa". Nhấn vào để mở Modal sửa Unit AD-02-M2.

- **Tên component:** Nút "Xóa" trên thẻ Unit
  - **Loại component tham chiếu từ DESIGN.md:** button-text-link (màu error #ef4444, font Inter size 13px, weight 600)
  - **Vị trí:** Vùng D, cạnh nút "Sửa" về bên phải.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Xóa". Nhấn vào để kích hoạt luồng xóa Unit (UC-02c).

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động:** Kéo thả thẻ Unit thay đổi thứ tự
  - **Luồng chính:** Admin click giữ chuột trái vào icon grip ở đầu thẻ Unit -> Kéo di chuyển thẻ lên trên hoặc xuống dưới -> Nhả chuột tại vị trí mới. Các thẻ Unit tự động hoán đổi vị trí trực quan. Số thứ tự hiển thị của các Unit tự động cập nhật tạm thời (ví dụ: Unit kéo từ thứ 3 lên thứ 1 sẽ đổi badge thành Unit 01, các thẻ khác tụt số thứ tự). Nút "Lưu thứ tự" và nút "Hủy thay đổi" xuất hiện ở Vùng C.
- **Hành động:** Nhấp nút "Lưu thứ tự"
  - **Luồng chính:** Admin click nút -> Hệ thống gửi API POST chứa danh sách các ID Unit kèm số thứ tự mới -> Thành công -> Hiển thị Toast thông báo thành công màu xanh lá -> Tải lại danh sách Unit theo thứ tự mới. Nút "Lưu thứ tự" và "Hủy thay đổi" ẩn đi.
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: `[ { "id": 12, "sequence": 1 }, { "id": 10, "sequence": 2 }, ... ]`
    - Nhận về: `{ "success": true }`
- **Hành động:** Nhấp nút "Hủy thay đổi"
  - **Luồng chính:** Admin click nút -> Hệ thống khôi phục vị trí các thẻ Unit về đúng trạng thái ban đầu trước khi kéo thả. Nút "Lưu thứ tự" và "Hủy thay đổi" ẩn đi.
- **Hành động:** Nhấp vào tên Unit hoặc chủ đề
  - **Luồng chính:** Admin nhấp chuột -> Chuyển hướng sang màn hình AD-03 (Lesson List Page của Unit đó).
- **Hành động:** Nhấp nút "Thêm Unit mới"
  - **Luồng chính:** Hiển thị Modal AD-02-M1 chồng lên màn hình hiện tại.
- **Hành động:** Nhấp nút "Sửa" trên thẻ Unit
  - **Luồng chính:** Hiển thị Modal AD-02-M2 chứa thông tin cũ chồng lên màn hình hiện tại.
- **Hành động:** Nhấp nút "Xóa" trên thẻ Unit
  - **Luồng chính:** Hệ thống kiểm tra điều kiện xóa (Unit đã có học viên học hoặc làm bài kiểm tra):
    - *Nhánh có học viên hoạt động:* Báo lỗi dạng Toast hoặc cảnh báo đỏ: "Không thể xóa Unit vì hiện đang có tiến trình học tập của học viên được ghi nhận". Không mở Modal xóa.
    - *Nhánh Unit hợp lệ:* Hiển thị Modal xác nhận xóa AD-02-M3.

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Khi cấp độ chưa có Unit nào, hiển thị hình ảnh 3D claymation minh họa ở trung tâm vùng D kèm văn bản: "Cấp độ học này chưa có Unit nào. Hãy nhấn nút 'Thêm Unit mới' phía trên để bắt đầu xây dựng nội dung học tập."
- **Trạng thái tải (loading state):** Khi đang tải danh sách Unit, các thẻ được thay thế bằng các khung xương Skeleton nhấp nháy xám nhẹ.
- **Trạng thái lỗi (error state):** Khi mất kết nối API, vùng D hiển thị thông báo lỗi "Không thể tải danh sách Unit. Vui lòng kiểm tra kết nối mạng." kèm nút "Thử lại".
- **Trạng thái thành công (success state):** Sau khi thực hiện lưu thứ tự thành công, hiển thị Toast thông báo xanh lá ở góc trên bên phải: "Cập nhật thứ tự các Unit thành công!".

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ màn hình AD-01 (Level List Page) sau khi Admin click vào tên của một Cấp độ.
- **Sau khi hoàn thành hành động, đi đến màn hình nào?**
  - Đi đến màn hình AD-03 (Lesson List Page) sau khi nhấp vào tên một Unit.
  - Đi đến màn hình AD-01 (Level List Page) sau khi click vào Breadcrumbs "Lộ trình học".
- **Các màn hình liên quan khác:** Modal AD-02-M1, Modal AD-02-M2, Modal AD-02-M3 hiển thị đè lên màn hình này.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0).
- Các thẻ Unit sử dụng kiểu dáng `product-mockup-card` với viền hairline mỏng 1px (#e5e5e5) màu nhạt, bo tròn góc rounded-lg (16px), không đổ bóng để giữ tính tối giản. Khi rê chuột qua thẻ (hover), viền thẻ đổi màu xám sẫm nhẹ và con trỏ chuột đổi sang dạng di chuyển (grab icon).
- Khoảng cách dọc giữa các thẻ Unit là spacing-md (16px) đảm bảo tính trực quan và dễ dàng thao tác kéo thả mà không bị kích nhầm.
- Touch target của các nút hành động (Sửa, Xóa) được tăng vùng đệm tối thiểu 44x44px. Nút Xóa có màu đỏ thương hiệu (#ef4444) để báo hiệu hành động nguy hiểm theo Nguyên tắc Báo hiệu (Signaling Principle).
