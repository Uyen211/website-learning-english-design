# MÀN HÌNH: DELETE TEST CONFIRMATION MODAL (HỘP THOẠI XÁC NHẬN XÓA BÀI KI KIỂM TRA)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Delete Test Confirmation Modal (Hộp thoại xác nhận xóa bài kiểm tra)
- Mã use case liên quan: UC-04c (Một phần của tác vụ quản lý đề kiểm tra)
- Mã luồng người dùng liên quan: Flow AD-FL-04 (Quản lý Bài kiểm tra)
- Vai trò người dùng: Admin (Quản trị viên)
- Vị trí trong sitemap: Trang chủ quản trị -> AD-04: Test List Page -> Modal AD-04-M1

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng hộp thoại xác nhận nổi này để đưa ra quyết định chắc chắn trước khi xóa hoàn toàn một đề kiểm tra (Mini-test / Level test / Mock test) khỏi cơ sở dữ liệu hệ thống.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Hộp thoại nổi cảnh báo cỡ nhỏ căn giữa (Small Centered Modal Overlay) đè lên màn hình danh sách bài kiểm tra AD-04.
- Các vùng chính trên màn hình:
  - Vùng A: Lớp nền tối mờ (Overlay Backdrop) bao phủ màn hình phía sau.
  - Vùng B: Tiêu đề cảnh báo nguy hiểm (Modal Header).
  - Vùng C: Đoạn thông điệp xác nhận chi tiết (Modal Body Content).
  - Vùng D: Các nút bấm hành động (Modal Actions Footer) căn lề phải.
- Kích thước / Grid tham khảo:
  - Chiều rộng cố định của hộp thoại: 420px.
  - Chiều cao tự động co giãn theo nội dung cảnh báo.
  - Khoảng cách padding trong modal: spacing-lg (24px).
  - Khoảng cách dọc giữa các vùng: spacing-md (16px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)
- **Tên component:** Lớp nền tối mờ (Backdrop)
  - **Loại component tham chiếu từ DESIGN.md:** overlay / backdrop (màu tối navy nhạt có độ mờ thấp)
  - **Vị trí:** Vùng A, bao phủ toàn màn hình nền.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Nhấp chuột ngoài vùng hộp thoại sẽ đóng modal tương đương hành động "Hủy".

- **Tên component:** Tiêu đề cảnh báo
  - **Loại component tham chiếu từ DESIGN.md:** title-md (font Inter size 18px, weight 600, màu ink #0a0a0a)
  - **Vị trí:** Vùng B, góc trên bên trái hộp thoại.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị một icon cảnh báo chấm than tam giác màu đỏ (#ef4444) kích thước 24px x 24px đứng trước tiêu đề: "Xóa bài kiểm tra".

- **Tên component:** Thông điệp cảnh báo xóa
  - **Loại component tham chiếu từ DESIGN.md:** body-md (font Inter size 15px, line-height 1.55, màu body #3a3a3a)
  - **Vị trí:** Vùng C, ở trung tâm hộp thoại.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị dòng chữ: "Bạn có chắc chắn muốn xóa bài kiểm tra này khỏi hệ thống? Hành động này sẽ loại bỏ hoàn toàn đề thi và không thể hoàn tác. Các kết quả học bạ cũ của học viên vẫn được lưu giữ.".

- **Tên component:** Nút "Xác nhận xóa"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, font Inter size 14px, weight 600, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng D, góc dưới bên phải.
  - **Trạng thái:**
    - Mặc định: nền đen, chữ trắng.
    - Hover: nền chuyển sang xám đen sẫm.
    - Loading: xoay spinner trắng ở giữa, vô hiệu hóa nút bấm.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Xác nhận xóa". Nhấp chuột để gửi yêu cầu xóa bài kiểm tra lên máy chủ.

- **Tên component:** Nút "Hủy"
  - **Loại component tham chiếu từ DESIGN.md:** button-secondary (nền canvas #fffaf0, border 1px hairline #e5e5e5, chữ ink #0a0a0a, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng D, nằm bên trái nút Xác nhận xóa.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Hủy". Nhấn để đóng hộp thoại và giữ nguyên đề kiểm tra.

- **Tên component:** Thông báo lỗi hệ thống (Error Message)
  - **Loại component tham chiếu từ DESIGN.md:** body-sm (màu error #ef4444)
  - **Vị trí:** Vùng C, hiển thị phía trên nhóm nút nếu API xóa thất bại.
  - **Trạng thái:** Ẩn mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị văn bản "Lỗi hệ thống. Không thể xóa đề thi lúc này. Vui lòng thử lại!".

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động:** Nhấp nút "Xác nhận xóa"
  - **Luồng chính:**
    1. Admin click nút "Xác nhận xóa".
    2. Nút chuyển sang trạng thái Loading (hiển thị spinner và vô hiệu hóa click).
    3. Hệ thống gửi yêu cầu API DELETE xóa bài kiểm tra kèm theo ID đề kiểm tra được chọn.
    4. Máy chủ thực hiện xóa đề kiểm tra trong cơ sở dữ liệu.
    5. API trả về phản hồi thành công.
    6. Đóng Modal.
    7. Quay lại màn hình AD-04 (danh sách đề thi được tải lại tự động, loại bỏ dòng đề thi vừa xóa và hiển thị thông tin cập nhật).
    8. Hiển thị Toast thông báo thành công màu xanh lá ở góc trên bên phải: "Xóa bài kiểm tra thành công!".
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: `DELETE /api/tests/{test_id}`
    - Nhận về: `{ "success": true }`
- **Hành động:** Nhấp nút "Hủy" hoặc nhấp chuột ra ngoài vùng Modal
  - **Luồng chính:** Hệ thống đóng Modal -> Quay lại màn hình AD-04 -> Mọi dữ liệu cũ giữ nguyên.

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Không áp dụng cho màn hình này.
- **Trạng thái tải (loading state):** Khi đang gửi yêu cầu xóa lên máy chủ, nút "Xác nhận xóa" chuyển sang trạng thái Loading và bị vô hiệu hóa click để tránh gửi lặp.
- **Trạng thái lỗi (error state):** Khi API xóa bị lỗi do sự cố kết nối máy chủ -> Hiển thị thông báo lỗi màu đỏ sát trên nút bấm để người dùng thử lại hoặc thoát.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ màn hình danh sách bài kiểm tra AD-04 sau khi Admin nhấp chuột vào nút "Xóa" trên dòng đề kiểm tra.
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Đóng Modal và quay trở lại màn hình AD-04.
- **Các màn hình liên quan khác:** AD-04.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền hộp thoại sử dụng màu surface-card (#f5f0e0), viền bo tròn góc bo rounded-lg (16px) nhẹ nhàng, không có bóng đổ thô cứng để tạo tính đồng nhất với phong cách Clay.com.
- Khoảng cách các vùng được thiết lập thưa thớt spacing-lg (24px) để giảm áp lực nhận thức cho người dùng khi đối diện với các tác vụ hủy hoại dữ liệu.
- Theo Nguyên tắc Báo hiệu (Signaling Principle), nút Xác nhận xóa là nút primary màu đen, trong khi nút Hủy là nút secondary có màu canvas kem ấm để thu hút sự chú ý của Admin vào đúng hành động mong muốn.
- Touch target của tất cả các nút được giữ ở mức 44px để tránh nhấn lệch.



