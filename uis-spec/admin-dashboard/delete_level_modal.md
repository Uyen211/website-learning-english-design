# MÀN HÌNH: DELETE LEVEL CONFIRMATION MODAL (HỘP THOẠI XÁC NHẬN XÓA CẤP ĐỘ)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Delete Level Confirmation Modal (Hộp thoại xác nhận xóa cấp độ)
- Mã use case liên quan: UC-01c
- Mã luồng người dùng liên quan: Flow AD-FL-01
- Vai trò người dùng: Admin
- Vị trí trong sitemap: Trang chủ quản trị -> AD-01: Level List Page -> Modal AD-01-M3

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng hộp thoại xác nhận này để đưa ra quyết định chắc chắn trước khi thực hiện xóa hoàn toàn một cấp độ học khỏi cơ sở dữ liệu hệ thống.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Hộp thoại lớp phủ loại nhỏ căn giữa (Small Centered Modal Overlay) đè lên màn hình AD-01.
- Các vùng chính trên màn hình:
  - Vùng A: Lớp nền tối mờ (Overlay Backdrop) che phủ toàn bộ màn hình nền AD-01.
  - Vùng B: Tiêu đề cảnh báo và nội dung văn bản xác nhận (Modal Content).
  - Vùng C: Khu vực các nút bấm hành động (Modal Actions Footer) căn lề phải.
- Kích thước / Grid tham khảo:
  - Chiều rộng cố định của hộp thoại: 400px.
  - Chiều cao tự động co giãn theo văn bản cảnh báo.
  - Khoảng cách padding trong modal: spacing-lg (24px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)
- **Tên component:** Lớp nền tối mờ (Backdrop)
  - **Loại component tham chiếu từ DESIGN.md:** overlay / backdrop
  - **Vị trí:** Vùng A, bao phủ toàn màn hình nền phía sau
  - **Trạng thái:** Mặc định
  - **Dữ liệu hiển thị / hành vi:** Nhấp chuột ngoài vùng hộp thoại sẽ thực hiện hành động "Hủy".

- **Tên component:** Tiêu đề cảnh báo
  - **Loại component tham chiếu từ DESIGN.md:** title-md (font Inter 18px/600)
  - **Vị trí:** Vùng B, góc trên bên trái hộp thoại
  - **Trạng thái:** Mặc định, màu chữ ink
  - **Dữ liệu hiển thị / hành vi:** Hiển thị dòng chữ cảnh báo tiêu đề: "Xóa cấp độ học".

- **Tên component:** Nội dung thông điệp cảnh báo
  - **Loại component tham chiếu từ DESIGN.md:** body-md (font Inter 16px/1.55, màu body #3a3a3a)
  - **Vị trí:** Vùng B, nằm dưới tiêu đề
  - **Trạng thái:** Mặc định
  - **Dữ liệu hiển thị / hành vi:** Hiển thị dòng chữ xác nhận: "Bạn có chắc chắn muốn xóa cấp độ này? Hành động này sẽ loại bỏ hoàn toàn lộ trình và không thể hoàn tác.".

- **Tên component:** Nút Xác nhận xóa
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (background #0a0a0a, text #ffffff, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng C, góc dưới bên phải
  - **Trạng thái:** Mặc định, hover, disabled (nếu đang xử lý)
  - **Dữ liệu hiển thị / hành vi:** Hiển thị text "Xác nhận xóa". Nhấp nút sẽ gửi yêu cầu xóa cấp độ khỏi hệ thống.

- **Tên component:** Nút Hủy
  - **Loại component tham chiếu từ DESIGN.md:** button-secondary (background #fffaf0, border 1px hairline #e5e5e5, text #0a0a0a, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng C, nằm bên trái nút Xác nhận xóa
  - **Trạng thái:** Mặc định, hover
  - **Dữ liệu hiển thị / hành vi:** Hiển thị text "Hủy". Nhấn để đóng hộp thoại và giữ nguyên cấp độ học.

## 5. CHI TIẾT TƯƠNG TÁC
- **Hành động:** Nhấn nút "Xác nhận xóa"
  - **Luồng chính:** Admin chọn "Xác nhận xóa" -> Hệ thống gửi yêu cầu xóa cấp độ lên máy chủ -> Xóa thành công khỏi CSDL -> Đóng Modal -> Quay lại màn hình AD-01 (Hiển thị Toast thông báo thành công và tự động tải lại danh sách loại bỏ cấp độ vừa xóa).
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: id của cấp độ học cần xóa (số nguyên/chuỗi ký tự).
    - Nhận về: Trạng thái thành công/thất bại của tác vụ xóa.

- **Hành động:** Nhấn nút "Hủy" hoặc nhấp chuột ra ngoài vùng Modal
  - **Luồng chính:** Hệ thống đóng Modal -> Quay lại màn hình danh sách cấp độ học AD-01 (Giữ nguyên mọi dữ liệu cũ).

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT
- **Trạng thái rỗng (empty state):** Không áp dụng cho màn hình này.
- **Trạng thái tải (loading state):** Khi nhấn "Xác nhận xóa", nút Xác nhận chuyển sang trạng thái loading (text tạm ẩn, xuất hiện spinner, nút bị disabled) để chờ phản hồi từ API xóa của máy chủ.
- **Trạng thái lỗi (error state):** Khi API xóa bị lỗi do sự cố kết nối máy chủ -> Hiển thị dòng chữ báo lỗi nhỏ màu đỏ (#ef4444) "Lỗi hệ thống. Không thể thực hiện xóa vào lúc này." nằm ngay sát phía trên các nút bấm.
- **Trạng thái thành công (success state):** Không hiển thị trên chính Modal (Modal tự động đóng khi thành công).

## 7. THAM CHIẾU LUỒNG
- **Đến từ màn hình nào trước đó?** Từ màn hình danh sách cấp độ học AD-01 sau khi Admin nhấp chuột vào nút "Xóa" trên thẻ cấp độ học hợp lệ (cấp độ không có học viên học hoạt động).
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Chuyển hướng quay lại màn hình danh sách cấp độ học AD-01.
- **Các màn hình liên quan khác:** AD-01.

## 8. LƯU Ý THIẾT KẾ
- Nền hộp thoại sử dụng màu surface-card (#f5f0e0), viền bao quanh được bo tròn góc bo rounded-lg (16px) nhẹ nhàng và sang trọng.
- Spacing giữa tiêu đề, thông điệp và các nút là spacing-lg (24px) tạo bố cục thoáng đãng và có nhịp điệu rõ ràng.
- Các nút hành động được thiết kế rõ ràng về thứ tự phân cấp thị giác theo Nguyên tắc Báo hiệu (Signaling Principle) giúp Admin dễ dàng nhận thấy nút primary đen tuyền để nhấn xác nhận hoặc hủy.
- Touch target của nút đạt tối thiểu 44x44px.



