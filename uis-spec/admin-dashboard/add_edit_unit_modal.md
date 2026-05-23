# MÀN HÌNH: ADD / EDIT UNIT MODAL (HỘP THOẠI THÊM/SỬA UNIT)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Add / Edit Unit Modal (Hộp thoại thêm/sửa Unit)
- Mã use case liên quan: UC-02a, UC-02b
- Mã luồng người dùng liên quan: Flow AD-FL-02 (Quản lý Unit)
- Vai trò người dùng: Admin (Quản trị viên)
- Vị trí trong sitemap: Trang chủ quản trị -> AD-01: Level List Page -> Click tên cấp độ -> AD-02: Unit List Page -> Modal AD-02-M1 (Thêm) / AD-02-M2 (Sửa)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng hộp thoại nổi này để nhập thông tin thiết lập cho một Unit mới trong cấp độ học, hoặc chỉnh sửa thông tin của một Unit hiện có.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Hộp thoại lớp phủ căn giữa (Centered Modal Overlay) đè lên màn hình danh sách Unit AD-02.
- Các vùng chính trên màn hình:
  - Vùng A: Lớp nền tối mờ (Overlay Backdrop) che phủ và làm mờ màn hình AD-02 phía sau.
  - Vùng B: Tiêu đề hộp thoại và nút hủy nhanh (Header của Modal).
  - Vùng C: Thân hộp thoại (Form Body) chứa các trường nhập liệu dạng biểu mẫu dọc 1 cột.
  - Vùng D: Chân hộp thoại (Footer của Modal) chứa nhóm nút hành động lưu và hủy.
- Kích thước / Grid tham khảo:
  - Chiều rộng cố định của hộp thoại: 560px.
  - Chiều cao tự động co giãn theo nội dung form.
  - Khoảng cách padding trong modal: spacing-xl (32px).
  - Các trường nhập liệu được xếp dọc, khoảng cách giữa các trường: spacing-md (16px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)
- **Tên component:** Lớp nền tối mờ (Backdrop)
  - **Loại component tham chiếu từ DESIGN.md:** overlay / backdrop (màu tối navy nhạt có độ mờ thấp)
  - **Vị trí:** Vùng A, che phủ toàn màn hình.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Nhấp chuột ra ngoài vùng modal sẽ đóng modal tương tự nút "Hủy".

- **Tên component:** Tiêu đề hộp thoại
  - **Loại component tham chiếu từ DESIGN.md:** title-lg (font Inter size 22px, weight 600, màu ink #0a0a0a)
  - **Vị trí:** Vùng B, góc trên bên trái của hộp thoại.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị "Thêm Unit mới" (đối với Modal AD-02-M1) hoặc "Chỉnh sửa Unit" (đối với Modal AD-02-M2).

- **Tên component:** Trường Số thứ tự Unit (Unit Sequence)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền surface-strong #ebe6d6, màu chữ muted #6a6a6a, border 1px hairline #e5e5e5, rounded-md 12px, height 44px, chế độ read-only)
  - **Vị trí:** Vùng C, trường nhập liệu đầu tiên.
  - **Trạng thái:** Disabled / Read-only (không thể chỉnh sửa, con trỏ chuột dạng blocked).
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Số thứ tự Unit". Tự động hiển thị số thứ tự tăng dần tiếp theo (ví dụ: "03" đối với thêm mới) hoặc số thứ tự hiện tại của Unit đó đối với chỉnh sửa.

- **Tên component:** Trường nhập Tên Unit (Unit Name)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, màu chữ ink #0a0a0a, border 1px hairline #e5e5e5, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng C, trường nhập thứ hai.
  - **Trạng thái:** 
    - Mặc định: viền màu hairline, placeholder hiển thị "Ví dụ: Unit 1: Pronoun Basics..." màu muted-soft (#9a9a9a).
    - Focus: viền đổi sang màu primary (#0a0a0a) 1.5px.
    - Error: viền đỏ màu error (#ef4444).
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Tên Unit *". Đây là trường bắt buộc.

- **Tên component:** Trường nhập Chủ đề lớn (Major Theme)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, màu chữ ink #0a0a0a, border 1px hairline #e5e5e5, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng C, trường nhập thứ ba.
  - **Trạng thái:** Mặc định, focus, error.
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Chủ đề lớn *". Placeholder: "Ví dụ: Đời sống thường ngày / Giao tiếp công sở...". Đây là trường bắt buộc.

- **Tên component:** Trường nhập Chủ điểm từ vựng (Vocabulary Topic)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, màu chữ ink #0a0a0a, border 1px hairline #e5e5e5, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng C, trường nhập thứ tư.
  - **Trạng thái:** Mặc định, focus.
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Chủ điểm từ vựng". Placeholder: "Ví dụ: Family / Work / Food...". Trường không bắt buộc.

- **Tên component:** Trường nhập Chủ điểm ngữ pháp (Grammar Topic)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, màu chữ ink #0a0a0a, border 1px hairline #e5e5e5, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng C, trường nhập thứ năm.
  - **Trạng thái:** Mặc định, focus.
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Chủ điểm ngữ pháp". Placeholder: "Ví dụ: Present Simple / Passive Voice...". Trường không bắt buộc.

- **Tên component:** Trường chọn Kỹ năng thi (Test Skill Target)
  - **Loại component tham chiếu từ DESIGN.md:** dropdown / select (nền canvas #fffaf0, màu chữ ink #0a0a0a, border 1px hairline #e5e5e5, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng C, trường nhập thứ sáu.
  - **Trạng thái:** Mặc định, focus.
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Kỹ năng thi áp dụng". Cho phép chọn một trong hai tùy chọn: "IELTS" hoặc "TOEIC".

- **Tên component:** Nút "Lưu" / "Lưu thay đổi"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, font Inter size 14px, weight 600, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng D, góc dưới bên phải.
  - **Trạng thái:**
    - Mặc định: nền đen, chữ trắng.
    - Hover: nền chuyển sang xám đen sẫm.
    - Loading: xoay spinner trắng ở giữa, vô hiệu hóa nút bấm.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị "Lưu" (Modal thêm) hoặc "Lưu thay đổi" (Modal sửa). Nhấn để gửi dữ liệu về hệ thống.

- **Tên component:** Nút "Hủy"
  - **Loại component tham chiếu từ DESIGN.md:** button-secondary (nền canvas #fffaf0, border 1px hairline #e5e5e5, chữ ink #0a0a0a, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng D, nằm cạnh nút Lưu về bên trái.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Hủy". Nhấn để đóng modal, bỏ qua dữ liệu đang nhập.

- **Tên component:** Nhãn thông báo lỗi (Error Message)
  - **Loại component tham chiếu từ DESIGN.md:** body-sm (màu error #ef4444, font Inter weight 500, size 13px)
  - **Vị trí:** Vùng C, hiển thị dưới viền đỏ của trường bị lỗi.
  - **Trạng thái:** Ẩn mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị thông điệp "Tên Unit và Chủ đề lớn không được để trống!".

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động:** Nhấp chuột vào nút "Lưu" hoặc "Lưu thay đổi"
  - **Luồng chính:**
    1. Admin điền đầy đủ các trường Tên Unit và Chủ đề lớn.
    2. Click nút "Lưu".
    3. Nút Lưu kích hoạt trạng thái Loading.
    4. Hệ thống thực hiện gửi yêu cầu lưu qua API.
    5. API phản hồi thành công.
    6. Đóng Modal.
    7. Màn hình AD-02 hiển thị Toast thông báo thành công và tự động tải lại danh sách Unit hiển thị thông tin mới.
  - **Luồng con / rẽ nhánh:**
    - *Trường hợp thiếu Tên Unit hoặc Chủ đề lớn:* Hệ thống ngăn chặn nộp form, giữ nguyên Modal. Bôi đỏ viền trường bị thiếu (#ef4444) và hiển thị thông báo lỗi "Tên Unit và Chủ đề lớn không được để trống" ngay bên dưới trường tương ứng.
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: ` { "id": 12 (chỉ đối với sửa), "name": "Unit 1: Pronouns", "theme": "Daily Life", "vocabularyTopic": "Family", "grammarTopic": "Personal Pronouns", "targetSkill": "IELTS" }`
    - Nhận về: `{ "success": true, "data": { "id": 12, ... } }`
- **Hành động:** Nhấp nút "Hủy" hoặc nhấp ngoài vùng Modal
  - **Luồng chính:** Hệ thống đóng Modal -> Quay lại màn hình AD-02 -> Mọi dữ liệu đang nhập dở bị hủy bỏ, danh sách Unit giữ nguyên.

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Đối với Modal thêm mới, các trường nhập liệu (trừ Số thứ tự) để trống và hiển thị placeholder xám. Đối với Modal sửa, các trường được điền sẵn dữ liệu lấy từ Unit được chọn.
- **Trạng thái tải (loading state):** Khi đang gửi dữ liệu lên máy chủ, nút Lưu chuyển sang trạng thái Loading (hiển thị spinner xoay và vô hiệu hóa click) để tránh nộp form hai lần.
- **Trạng thái lỗi (error state):** Khi API báo lỗi dữ liệu đầu vào hoặc lỗi kết nối, viền ô nhập bị lỗi chuyển sang màu đỏ và hiển thị text thông báo lỗi đỏ (#ef4444) để người dùng sửa đổi.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ màn hình danh sách Unit AD-02 sau khi Admin click nút "Thêm Unit mới" hoặc nút "Sửa" trên thẻ Unit.
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Đóng Modal và quay trở lại màn hình AD-02.
- **Các màn hình liên quan khác:** AD-02.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền hộp thoại sử dụng màu surface-card (#f5f0e0), viền bao quanh được bo tròn góc bo lớn rounded-lg (16px) hoặc rounded-xl (24px) để tạo cảm giác mềm mại thân thiện giống thiết kế Clay.
- Theo Nguyên tắc Báo hiệu (Signaling Principle), các nhãn lỗi có màu đỏ sáng (#ef4444) nổi bật trên nền vàng ấm giúp Admin dễ nhận biết lỗi sai mà không bị nhầm lẫn.
- Khoảng cách giữa các trường nhập liệu là spacing-md (16px) đảm bảo không gian thoáng và tránh gây quá tải nhận thức cho người dùng.
- Chiều cao các nút hành động là 44px đạt touch target chuẩn mực.



