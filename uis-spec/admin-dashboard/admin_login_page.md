# MÀN HÌNH: ADMIN LOGIN PAGE (TRANG ĐĂNG NHẬP QUẢN TRỊ)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Admin Login Page (Trang đăng nhập quản trị)
- Mã use case liên quan: UC-01a, UC-01b, UC-01c, UC-02a, UC-02b, UC-02c, UC-02d, UC-03a, UC-03b, UC-03c, UC-04a, UC-04b, UC-04c (Tất cả use case của Admin đều yêu cầu điều kiện đăng nhập này)
- Mã luồng người dùng liên quan: Flow AD-FL-01 (Phân hệ xác thực & quản trị)
- Vai trò người dùng: Admin (Quản trị viên hệ thống)
- Vị trí trong sitemap: Trang chủ quản trị -> Đăng nhập admin (URL: /admin/login)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Người dùng (Quản trị viên) truy cập màn hình này để thực hiện đăng nhập vào hệ thống quản trị DiveVerse bằng tài khoản admin đã được cấp. Đăng nhập thành công sẽ cấp quyền truy cập để quản lý Cấp độ học, Unit, Bài học, Bài tập và Đề kiểm tra.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Centered card layout (Bố cục một cột căn giữa hoàn toàn theo cả hai chiều ngang và dọc) trên nền canvas sáng ấm (#fffaf0).
- Các vùng chính trên màn hình:
  - Vùng A: Khu vực thương hiệu phía trên gồm biểu tượng mascot dạng 3D claymation đặc trưng và tiêu đề lớn "DiveVerse Admin" màu ink.
  - Vùng B: Thẻ biểu mẫu đăng nhập trung tâm (Login Card Container) dạng hình chữ nhật đứng, bo tròn các góc rất lớn (rounded-xl, 24px) chứa các trường nhập liệu tài khoản, mật khẩu, thông báo lỗi và nút đăng nhập.
  - Vùng C: Chân trang tối giản (Minimal Footer) hiển thị dòng thông tin bản quyền nhỏ màu nhạt ở dưới cùng màn hình.
- Kích thước / Grid tham khảo:
  - Thẻ biểu mẫu có chiều rộng cố định 440px, tự động căn giữa toàn màn hình (viewport centering) bằng CSS Flexbox.
  - Khoảng cách padding bên trong thẻ biểu mẫu: 40px cho cả 4 cạnh để tạo khoảng trống thoáng đãng cho mắt.
  - Khoảng cách dọc giữa logo, thẻ biểu mẫu và footer là spacing-xl (32px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)
- **Tên component:** Logo Mascot DiveVerse
  - **Loại component tham chiếu từ DESIGN.md:** 3D claymation illustration / image
  - **Vị trí:** Vùng A, nằm trên cùng, căn giữa ngang.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hình ảnh một chú Cá Voi Xanh hoạt hình 3D màu cam đất sét (ochre) đang đeo tai nghe học tiếng Anh. Kích thước hình ảnh: 120px x 120px. Không thể nhấp chọn.

- **Tên component:** Tiêu đề trang
  - **Loại component tham chiếu từ DESIGN.md:** display-md (Plain Black display typeface, font Inter với weight 500, size 36px, line-height 1.1, letter-spacing -1.5px)
  - **Vị trí:** Vùng A, nằm ngay dưới Logo Mascot, cách logo 16px (spacing-md).
  - **Trạng thái:** Mặc định, màu chữ ink (#0a0a0a).
  - **Dữ liệu hiển thị / hành vi:** Dòng chữ "DiveVerse Admin".

- **Tên component:** Thẻ biểu mẫu (Login Card Container)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền surface-card #f5f0e0, border 1px hairline #e5e5e5, rounded-xl 24px, padding 40px, không có đổ bóng để giữ tính chất phẳng tối giản)
  - **Vị trí:** Vùng B, nằm chính giữa màn hình.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hộp chứa toàn bộ các trường tương tác nhập liệu.

- **Tên component:** Trường nhập tài khoản
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, màu chữ ink #0a0a0a, font Inter size 15px, rounded-md 12px, border 1px hairline #e5e5e5, height 44px, padding 12px x 16px)
  - **Vị trí:** Vùng B, nằm ở hàng đầu tiên trong thẻ biểu mẫu.
  - **Trạng thái:** 
    - Mặc định: viền màu hairline (#e5e5e5), placeholder hiển thị "Tên đăng nhập hoặc email..." màu muted-soft (#9a9a9a).
    - Focus (nhấp chuột vào): viền đổi sang màu primary (#0a0a0a) với độ dày 1.5px, nhãn đầu vào đứng yên.
    - Error: viền đỏ màu error (#ef4444) khi có lỗi.
  - **Dữ liệu hiển thị / hành vi:** Phía trên ô nhập có nhãn nhỏ (label) màu ink: "Tài khoản đăng nhập" (font Inter weight 600, size 13px, khoảng cách đến ô nhập 8px).

- **Tên component:** Trường nhập mật khẩu
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, màu chữ ink #0a0a0a, font Inter size 15px, rounded-md 12px, border 1px hairline #e5e5e5, height 44px, padding 12px x 16px, ký tự nhập vào tự động ẩn dạng dấu chấm tròn)
  - **Vị trí:** Vùng B, nằm dưới trường nhập tài khoản, cách trường tài khoản 20px.
  - **Trạng thái:**
    - Mặc định: viền màu hairline (#e5e5e5), placeholder hiển thị "••••••••" màu muted-soft (#9a9a9a).
    - Focus: viền đổi sang màu primary (#0a0a0a).
    - Error: viền đỏ màu error (#ef4444).
  - **Dữ liệu hiển thị / hành vi:** Phía trên ô nhập có nhãn nhỏ màu ink: "Mật khẩu" (font Inter weight 600, size 13px, khoảng cách đến ô nhập 8px). Tích hợp nút icon "Hiển thị/Ẩn mật khẩu" (eye icon) màu muted (#6a6a6a) ở góc phải trong ô nhập để chuyển đổi xem mật khẩu dạng text thường (kích thước icon 20px, touch target 44px).

- **Tên component:** Thông báo lỗi chung của biểu mẫu
  - **Loại component tham chiếu từ DESIGN.md:** body-sm (màu error #ef4444, font Inter weight 500, size 14px)
  - **Vị trí:** Vùng B, nằm dưới trường nhập mật khẩu và trên nút đăng nhập, cách mỗi bên 12px.
  - **Trạng thái:** Ẩn mặc định, chỉ hiển thị khi nhận phản hồi thất bại từ máy chủ hoặc lỗi trống trường thông tin.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị thông báo "Tài khoản hoặc mật khẩu không chính xác!" hoặc "Vui lòng nhập đầy đủ tài khoản và mật khẩu!".

- **Tên component:** Nút Đăng nhập
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, font Inter size 14px, weight 600, rounded-md 12px, height 44px, width 100% của card)
  - **Vị trí:** Vùng B, nằm ở dưới cùng trong thẻ biểu mẫu.
  - **Trạng thái:**
    - Mặc định: nền đen, chữ trắng.
    - Hover: nền chuyển sang màu xám đen đậm hoặc nâng sáng nhẹ (opacity 0.95), con trỏ chuột dạng bàn tay (pointer).
    - Loading: chữ ẩn đi, ở giữa xuất hiện một spinner xoay vòng tròn màu trắng (#ffffff), vô hiệu hóa mọi thao tác bấm chuột.
  - **Dữ liệu hiển thị / hành vi:** Văn bản hiển thị "Đăng nhập hệ thống". Nhấp vào để bắt đầu quá trình xác thực.

- **Tên component:** Bản quyền Footer
  - **Loại component tham chiếu từ DESIGN.md:** body-sm (màu muted-soft #9a9a9a, font Inter size 12px)
  - **Vị trí:** Vùng C, nằm sát cạnh đáy màn hình.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị text "© 2026 DiveVerse. All rights reserved. Admin Console v1.0".

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động:** Nhập thông tin và nhấp chuột vào nút "Đăng nhập hệ thống" (hoặc nhấn phím Enter khi đang focus vào bất kỳ ô nhập liệu nào)
  - **Luồng chính:**
    1. Admin nhập tài khoản và mật khẩu hợp lệ.
    2. Nhấn nút "Đăng nhập hệ thống".
    3. Nút chuyển sang trạng thái Loading (hiển thị spinner, khóa click). Viền các trường nhập giữ nguyên hairline.
    4. Hệ thống gửi yêu cầu API POST đến server.
    5. API trả về mã thành công (200 OK) kèm JWT Token.
    6. Hệ thống lưu Token vào LocalStorage.
    7. Hiển thị Toast thông báo thành công màu xanh lá ở góc trên bên phải màn hình: "Đăng nhập thành công! Đang chuyển hướng..."
    8. Sau 1.5 giây, hệ thống chuyển hướng sang màn hình AD-01 (Level List Page).
  - **Luồng con / rẽ nhánh:**
    - *Trường hợp thiếu thông tin:* Nếu trường tài khoản hoặc mật khẩu bị bỏ trống khi nhấn đăng nhập -> Hệ thống không gửi API. Viền của trường bị thiếu đổi sang màu đỏ (#ef4444). Hiển thị dòng chữ báo lỗi màu đỏ ngay dưới ô nhập mật khẩu: "Vui lòng nhập đầy đủ thông tin tài khoản và mật khẩu".
    - *Trường hợp sai tài khoản/mật khẩu:* Nếu thông tin xác thực sai -> Máy chủ phản hồi lỗi 401 Unauthorized -> Nút Đăng nhập tắt trạng thái Loading, trở về mặc định. Viền cả hai trường tài khoản và mật khẩu đổi sang màu đỏ (#ef4444). Hiển thị thông báo lỗi màu đỏ ở vùng chỉ định: "Tài khoản hoặc mật khẩu không chính xác!".
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi (Payload): `{ "username": "admin_user", "password": "secure_password_123" }`
    - Nhận về (Response): `{ "success": true, "token": "eyJhbGciOi...", "user": { "id": 1, "role": "admin", "name": "System Administrator" } }`

- **Hành động:** Nhấp vào icon "Hiển thị/Ẩn mật khẩu" (hình con mắt)
  - **Luồng chính:** Học viên/Admin nhấp chuột vào icon -> Thuộc tính type của trường mật khẩu đổi từ "password" sang "text" -> Các ký tự dấu chấm tròn đổi thành văn bản hiển thị rõ -> Icon chuyển sang trạng thái gạch chéo mắt. Nhấp lại lần nữa sẽ đổi type về "password" và ẩn ký tự.

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Không áp dụng cho màn hình này. Các trường nhập mặc định hiển thị trống kèm placeholder xám nhạt.
- **Trạng thái tải (loading state):** Khi đang gọi API xác thực, nút "Đăng nhập hệ thống" đổi sang màu đen mờ, ẩn chữ và quay spinner trắng, vô hiệu hóa nhập liệu của 2 trường phía trên.
- **Trạng thái lỗi (error state):** Khi API thất bại hoặc mất kết nối -> Viền input đổi sang màu đỏ (#ef4444) và hiển thị thông báo lỗi màu đỏ ngay phía dưới form để người dùng sửa lại.
- **Trạng thái thành công (success state):** Khi API thành công, hiển thị Toast thông báo xanh lá (#22c55e) có kích thước 320px x 64px ở góc trên bên phải, chứa icon tích xanh và dòng chữ "Thao tác thành công. Chào mừng quay trở lại!".

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Không có màn hình trước đó trong hệ thống (đây là điểm truy cập đầu tiên khi Admin truy cập đường dẫn quản trị).
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Chuyển hướng trực tiếp đến màn hình AD-01 (Level List Page).
- **Các màn hình liên quan khác:** Không có.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0) đặc trưng để tách biệt hẳn với các hệ thống quản trị dạng xám/xanh lạnh thông thường.
- Thẻ biểu mẫu được thiết kế mềm mại bằng góc bo lớn rounded-xl (24px) và màu nền surface-card (#f5f0e0), không dùng bóng đổ thô cứng, chỉ sử dụng đường hairline mỏng nhẹ 1px (#e5e5e5) làm ranh giới.
- Typography: Tiêu đề sử dụng font chữ Inter mô phỏng Plain Black với kích thước lớn 36px, chữ đậm trung bình (weight 500), khoảng cách chữ hẹp (-1.5px) để tạo điểm nhấn thương hiệu vui nhộn nhưng chuyên nghiệp.
- Nguyên tắc tránh quá tải nhận thức (Coherence Principle): Loại bỏ hoàn toàn mọi liên kết không cần thiết như "Quên mật khẩu" hay "Đăng ký" khỏi màn hình Admin Login. Chỉ giữ đúng một mục tiêu duy nhất là đăng nhập tài khoản admin.
- Kích thước touch target của tất cả các trường nhập và nút bấm được khóa cứng ở chiều cao 44px, đảm bảo click chính xác 100% trên mọi thiết bị.
�i (error state):** Khi thông tin đăng nhập sai hoặc mất kết nối máy chủ -> Hiển thị text báo lỗi màu đỏ (#ef4444) sát trên nút bấm và bôi đỏ viền input.
- **Trạng thái thành công (success state):** Sau khi xác thực thành công -> Xuất hiện toast thông báo xanh lá (#22c55e) ở góc trên bên phải màn hình: "Đăng nhập thành công! Đang chuyển hướng..." trước khi chuyển trang.

## 7. THAM CHIẾU LUỒNG
- **Đến từ màn hình nào trước đó?** Không có (đây là trang khởi đầu khi truy cập URL admin).
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Đi đến màn hình AD-01 (Level List Page) của Admin Portal.
- **Các màn hình liên quan khác:** Không có.

## 8. LƯU Ý THIẾT KẾ
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0) đặc trưng của Clay.com.
- Thẻ biểu mẫu được thiết kế mềm mại bằng góc bo lớn rounded-xl (24px) và màu nền surface-card (#f5f0e0), không có bóng đổ thô để giữ đúng tinh thần phẳng tối giản.
- Đảm bảo khoảng cách spacing-md (16px) giữa các trường nhập liệu và spacing-lg (24px) giữa mật khẩu và nút bấm.
- Touch target của nút đăng nhập đạt kích thước chuẩn tối thiểu 44px về chiều cao để dễ bấm trên thiết bị di động/máy tính bảng.



