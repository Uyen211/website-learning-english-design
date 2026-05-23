# MÀN HÌNH: ADD / EDIT LEVEL MODAL (HỘP THOẠI THÊM/SỬA CẤP ĐỘ)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Add / Edit Level Modal (Hộp thoại thêm/sửa cấp độ)
- Mã use case liên quan: UC-01a, UC-01b
- Mã luồng người dùng liên quan: Flow AD-FL-01
- Vai trò người dùng: Admin
- Vị trí trong sitemap: Trang chủ quản trị -> AD-01: Level List Page -> Modal AD-01-M1 (Thêm) / AD-01-M2 (Sửa)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng hộp thoại nổi này để nhập thông tin cấp độ học mới hoặc chỉnh sửa dữ liệu của một cấp độ học hiện có và lưu lại vào hệ thống.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Hộp thoại lớp phủ căn giữa (Centered Modal Overlay) đè lên màn hình danh sách cấp độ.
- Các vùng chính trên màn hình:
  - Vùng A: Lớp nền tối mờ (Overlay Backdrop) làm mờ màn hình AD-01 phía dưới.
  - Vùng B: Tiêu đề hộp thoại và nút đóng nhanh (Header của Modal).
  - Vùng C: Thân hộp thoại (Form Body) chứa các trường nhập liệu dạng biểu mẫu 1 cột dọc.
  - Vùng D: Chân hộp thoại (Footer của Modal) chứa nhóm nút hành động lưu/hủy.
- Kích thước / Grid tham khảo:
  - Chiều rộng cố định của hộp thoại: 600px.
  - Chiều cao tự động co giãn theo nội dung form, có thanh cuộn dọc (scrollable body) nếu nội dung quá dài.
  - Khoảng cách padding trong modal: spacing-xl (32px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)
- **Tên component:** Lớp nền tối mờ (Backdrop)
  - **Loại component tham chiếu từ DESIGN.md:** overlay / backdrop (màu tối navy nhạt có độ mờ thấp)
  - **Vị trí:** Vùng A, bao phủ toàn bộ màn hình phía sau
  - **Trạng thái:** Mặc định
  - **Dữ liệu hiển thị / hành vi:** Nhấp chuột ngoài vùng hộp thoại sẽ đóng modal tương đương hành động "Hủy".

- **Tên component:** Tiêu đề hộp thoại
  - **Loại component tham chiếu từ DESIGN.md:** title-lg (font Inter 24px/600, letter-spacing -0.3px)
  - **Vị trí:** Vùng B, góc trên bên trái của hộp thoại
  - **Trạng thái:** Mặc định, màu chữ ink
  - **Dữ liệu hiển thị / hành vi:** Hiển thị "Thêm cấp độ học mới" (đối với Modal AD-01-M1) hoặc "Chỉnh sửa cấp độ học" (đối với Modal AD-01-M2).

- **Tên component:** Trường nhập Tên cấp độ
  - **Loại component tham chiếu từ DESIGN.md:** text-input (background #fffaf0, rounded-md 12px, border 1px hairline #e5e5e5, height 44px)
  - **Vị trí:** Vùng C, trường nhập thứ nhất
  - **Trạng thái:** Mặc định, focus (border primary #0a0a0a), error (border error #ef4444)
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Tên cấp độ *", hiển thị dữ liệu trống hoặc dữ liệu cũ để chỉnh sửa.

- **Tên component:** Trường nhập Mô tả ngắn
  - **Loại component tham chiếu từ DESIGN.md:** text-input (background #fffaf0, rounded-md 12px, border 1px hairline #e5e5e5, height 44px)
  - **Vị trí:** Vùng C, trường nhập thứ hai
  - **Trạng thái:** Mặc định, focus, error
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Mô tả ngắn", hiển thị text mô tả tóm tắt cấp độ.

- **Tên component:** Trường nhập Mô tả chi tiết
  - **Loại component tham chiếu từ DESIGN.md:** text-area / large text input (background #fffaf0, rounded-md 12px, border 1px hairline #e5e5e5, chiều cao tối thiểu 120px)
  - **Vị trí:** Vùng C, trường nhập thứ ba
  - **Trạng thái:** Mặc định, focus, error
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Mô tả chi tiết", trường nhập văn bản lớn cho phép xuống dòng.

- **Tên component:** Trường chọn IELTS target
  - **Loại component tham chiếu từ DESIGN.md:** dropdown / select (background #fffaf0, rounded-md 12px, border 1px hairline #e5e5e5, height 44px)
  - **Vị trí:** Vùng C, trường nhập thứ tư (bên trái nếu chia cột đôi với TOEIC)
  - **Trạng thái:** Mặc định, focus, error
  - **Dữ liệu hiển thị / hành vi:** Nhãn "IELTS Target", danh sách chọn điểm từ "0.0" đến "9.0" (bước nhảy 0.5).

- **Tên component:** Trường nhập TOEIC target
  - **Loại component tham chiếu từ DESIGN.md:** text-input / number input (background #fffaf0, rounded-md 12px, border 1px hairline #e5e5e5, height 44px)
  - **Vị trí:** Vùng C, trường nhập thứ năm (bên phải nếu chia cột đôi)
  - **Trạng thái:** Mặc định, focus, error
  - **Dữ liệu hiển thị / hành vi:** Nhãn "TOEIC Target", ô nhập số từ 0 đến 990.

- **Tên component:** Trường chọn Số lượng Unit tối đa
  - **Loại component tham chiếu từ DESIGN.md:** dropdown / select (background #fffaf0, rounded-md 12px, border 1px hairline #e5e5e5, height 44px)
  - **Vị trí:** Vùng C, trường nhập cuối cùng
  - **Trạng thái:** Mặc định, focus, error
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Số lượng Unit tối đa", danh sách chọn số từ 1 đến 50.

- **Tên component:** Nút Lưu / Lưu thay đổi
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (background #0a0a0a, text #ffffff, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng D, góc dưới bên phải
  - **Trạng thái:** Mặc định, hover, disabled (nếu đang lưu), loading
  - **Dữ liệu hiển thị / hành vi:** Hiển thị "Lưu" (Modal thêm) hoặc "Lưu thay đổi" (Modal sửa). Nhấn để gửi dữ liệu lưu trữ.

- **Tên component:** Nút Hủy
  - **Loại component tham chiếu từ DESIGN.md:** button-secondary (background #fffaf0, border 1px hairline #e5e5e5, text #0a0a0a, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng D, nằm cạnh nút Lưu về bên trái
  - **Trạng thái:** Mặc định, hover
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Hủy". Nhấn để đóng hộp thoại và hủy bỏ các thông tin vừa nhập.

- **Tên component:** Thông báo lỗi bối cảnh (Error Labels)
  - **Loại component tham chiếu từ DESIGN.md:** body-sm (màu error #ef4444)
  - **Vị trí:** Vùng C, xuất hiện động ngay bên dưới viền đỏ của trường nhập liệu bị lỗi tương ứng
  - **Trạng thái:** Ẩn mặc định
  - **Dữ liệu hiển thị / hành vi:** Hiển thị nội dung lỗi như "Tên cấp độ không được để trống", "Tên cấp độ đã tồn tại", hoặc "Điểm số quy chiếu không hợp lệ".

## 5. CHI TIẾT TƯƠNG TÁC
- **Hành động:** Nhập liệu và nhấn nút "Lưu" hoặc "Lưu thay đổi"
  - **Luồng chính:** Admin nhập đầy đủ thông tin bắt buộc -> Nhấn "Lưu" -> Hệ thống kiểm tra dữ liệu đầu vào hợp lệ -> Đóng Modal -> Lưu thông tin vào CSDL -> Hiển thị Toast thông báo thành công tại AD-01 và cập nhật danh sách.
  - **Luồng con / rẽ nhánh:**
    - Nếu Tên cấp độ bỏ trống (Rẽ nhánh E-1) -> Hệ thống không đóng Modal, bôi đỏ viền trường Tên cấp độ, hiển thị thông báo lỗi: "Tên cấp độ không được để trống" ngay bên dưới.
    - Nếu Tên cấp độ trùng lặp với cấp độ đã có (Rẽ nhánh E-2) -> Hệ thống bôi đỏ trường Tên cấp độ, hiển thị thông báo lỗi: "Tên cấp độ đã tồn tại trong hệ thống".
    - Nếu khung điểm mục tiêu không hợp lệ (Rẽ nhánh E-3) -> Hệ thống bôi đỏ trường IELTS hoặc TOEIC mục tiêu, hiển thị thông báo lỗi: "Điểm số quy chiếu IELTS (0.0-9.0) hoặc TOEIC (0-990) không hợp lệ".
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: id (chỉ áp dụng đối với Modal sửa), name (chuỗi ký tự), shortDescription (chuỗi ký tự), detailDescription (chuỗi ký tự), ieltsTarget (số thực), toeicTarget (số nguyên), maxUnits (số nguyên).
    - Nhận về: Trạng thái thành công/thất bại, ID cấp độ mới tạo hoặc thông tin cấp độ được cập nhật.

- **Hành động:** Nhấn nút "Hủy" hoặc nhấp chuột ngoài vùng Modal
  - **Luồng chính:** Hệ thống hủy bỏ toàn bộ dữ liệu vừa nhập/sửa đổi -> Đóng Modal -> Quay lại màn hình AD-01 (dữ liệu danh sách cấp độ giữ nguyên).

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT
- **Trạng thái rỗng (empty state):** Đối với Modal thêm mới, các trường nhập liệu mặc định trống hoặc hiển thị các placeholder mờ. Đối với Modal sửa, các trường được tự động điền sẵn dữ liệu lấy từ cấp độ học đã chọn.
- **Trạng thái tải (loading state):** Khi nhấn "Lưu", nút Lưu chuyển sang trạng thái loading và tạm khóa tương tác để tránh Admin click đúp gửi hai yêu cầu trùng lặp lên máy chủ.
- **Trạng thái lỗi (error state):** Khi xảy ra lỗi dữ liệu đầu vào -> Hộp thoại bôi đỏ viền các trường bị lỗi và hiển thị nhãn lỗi màu đỏ (#ef4444).
- **Trạng thái thành công (success state):** Không hiển thị trên chính Modal (Modal tự động đóng khi thành công).

## 7. THAM CHIẾU LUỒNG
- **Đến từ màn hình nào trước đó?** Từ màn hình danh sách cấp độ học AD-01 (sau khi nhấn nút "Thêm cấp độ mới" hoặc nút "Sửa").
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Đóng Modal và quay trở lại màn hình danh sách cấp độ học AD-01.
- **Các màn hình liên quan khác:** AD-01.

## 8. LƯU Ý THIẾT KẾ
- Nền hộp thoại sử dụng màu surface-card (#f5f0e0), viền bao quanh được bo tròn lớn góc bo rounded-lg (16px) hoặc rounded-xl (24px) để tạo cảm giác thân thiện giống thiết kế Clay.
- Theo Nguyên tắc Báo hiệu (Signaling Principle), các nhãn lỗi có màu đỏ sáng (#ef4444) nổi bật trên nền vàng ấm giúp Admin dễ nhận biết lỗi sai mà không bị nhầm lẫn.
- Khoảng cách giữa các trường nhập liệu là spacing-md (16px) đảm bảo không gian thoáng mát cho mắt và tránh gây quá tải nhận thức cho người dùng.
- Chiều cao các nút hành động là 44px đạt touch target chuẩn mực.
