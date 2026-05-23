# MÀN HÌNH: PERSONAL REVIEW DASHBOARD (BẢNG ĐIỀU KHIỂN TRA CỨU & ÔN TẬP)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Personal Review Dashboard (Màn hình bảng điều khiển tra cứu & ôn tập)
- Mã màn hình: LN-12
- Mã use case liên quan: UC-08 (Tra cứu nhanh và ôn tập lặp lại ngắt quãng SRS)
- Mã luồng người dùng liên quan: Flow LN-FL-09 (Tra cứu nhanh & Ôn tập SRS)
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Dashboard -> Click tab "Tra cứu & Ôn tập" -> Personal Review Dashboard (URL: /review)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này làm trung tâm để quản lý tiến trình ghi nhớ cá nhân, thực hiện tìm kiếm từ vựng/ngữ pháp và kích hoạt phiên ôn tập lặp lại ngắt quãng (SRS) hàng ngày.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục một cột căn giữa kết hợp chia lưới 2 cột không đối xứng (7:5) trên nền canvas sáng ấm (#fffaf0) có Top Sticky Navigation.
- Các vùng chính trên màn hình:
  - Vùng A: Thanh tìm kiếm từ điển ở chính giữa phía trên (Dictionary Search Bar).
  - Vùng B: Thẻ Kích hoạt Ôn tập hàng ngày (SRS Card Container) hiển thị số lượng từ cần ôn và nút ôn tập.
  - Vùng C: Lưới thẻ từ vựng đang ghi nhớ (SRS Memory Cards Grid) hiển thị thống kê độ bền trí nhớ.
- Kích thước / Grid tham khảo:
  - Chiều rộng tối đa của nội dung: 1000px căn giữa.
  - Vùng B và C sử dụng lưới 12 cột (7 cột cho B và 5 cột cho C).
  - Khoảng cách padding trong các thẻ: spacing-lg (24px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)

### PHÂN HỆ BẢNG ĐIỀU KHIỂN ÔN TẬP (PERSONAL REVIEW DASHBOARD - LN-12)
- **Tên component:** Thanh tìm kiếm từ điển (Dictionary Search Bar)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-md 12px, height 44px, width 100%)
  - **Vị trí:** Vùng A.
  - **Trạng thái:** Mặc định, focus.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị icon kính lúp ở góc trái. Placeholder: "Nhập từ vựng hoặc cấu trúc ngữ pháp cần tra cứu...". Gõ ký tự sẽ tự động xổ dropdown danh sách từ gợi ý tương đương bên dưới.

- **Tên component:** Danh sách từ gợi ý (Search Auto-complete Dropdown)
  - **Loại component tham chiếu từ DESIGN.md:** dropdown (nền surface-card #f5f0e0, border 1px hairline #e5e5e5, rounded-md 12px, padding 8px)
  - **Vị trí:** Vùng A, nằm dưới thanh tìm kiếm khi gõ chữ.
  - **Trạng thái:** Ẩn mặc định, hiển thị khi có ký tự tìm kiếm.
  - **Dữ liệu hiển thị / hành vi:** Danh sách các từ gợi ý trùng khớp (ví dụ: "collaborate", "collaboration", "collaborative"). Học viên click vào từ để chuyển hướng sang trang Dictionary / Search Result Page (LN-14).

- **Tên component:** Thẻ kích hoạt ôn tập SRS (SRS Trigger Card)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-peach (nền brand-peach #ffb084, chữ ink #0a0a0a, rounded-xl 24px, padding 32px)
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Mặc định. Có ngọn lửa streak pulsing nhẹ.
  - **Dữ liệu hiển thị / hành vi:** 
    - Tiêu đề: "Ôn tập SRS hàng ngày" (Plain Black 24px).
    - Thống kê: "Hôm nay bạn có **15 từ & cấu trúc** cần ôn tập lại để tránh bị quên.".
    - Nút "Ôn tập ngay" (`button-primary` nền đen, chữ trắng). Nhấn vào sẽ chuyển sang SRS Review Page (LN-13).

- **Tên component:** Biểu đồ độ bền trí nhớ (Memory Strength Widget)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền canvas #fffaf0, rounded-lg 16px, padding 20px)
  - **Vị trí:** Vùng C.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị biểu đồ tròn biểu thị tỷ lệ từ vựng đã chuyển hóa vào bộ nhớ dài hạn (ví dụ: "Bộ nhớ dài hạn: 120 từ - Bộ nhớ ngắn hạn: 45 từ").

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Nhập từ khóa tìm kiếm và click từ gợi ý**
  - **Luồng chính:** Học viên nhập "collab" -> Dropdown gợi ý hiện ra -> Click "collaborate" -> Hệ thống chuyển hướng người học sang trang chi tiết từ điển tại URL `/dictionary/collaborate` (LN-14).
  - **Luồng con / rẽ nhánh (Không tìm thấy từ):** Học viên nhập từ không có trong từ điển -> Dropdown hiển thị dòng cảnh báo: "Không tìm thấy từ vựng hoặc cấu trúc ngữ pháp phù hợp trong từ điển" -> Cho phép học viên sửa từ khóa.
- **Hành động: Click nút "Ôn tập ngay"**
  - **Luồng chính:** Học viên click nút -> Chuyển hướng sang trang `/review/srs` (LN-13) để bắt đầu phiên ôn tập.
- **Hành động: Xem biểu đồ thống kê**
  - Hover vào các phân đoạn của biểu đồ tròn để xem số lượng từ vựng cụ thể theo từng trạng thái ghi nhớ (New, Learning, Review, Mastered).

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Khi hôm nay học viên không có từ nào cần ôn tập -> Thẻ SRS ở Vùng B đổi màu xanh lá success nhẹ, hiển thị text: "Tuyệt vời! Hôm nay bạn đã hoàn thành tất cả mục tiêu ôn tập. Hãy học thêm bài mới!". Nút "Ôn tập ngay" bị disabled.
- **Trạng thái tải (loading state):** Khi đang tải dữ liệu thống kê SRS, hiển thị các khối skeleton mờ.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ Learner Dashboard (LN-01) khi nhấp chọn tab "Tra cứu & Ôn tập" trên Top Nav.
- **Sau khi hoàn thành hành động, đi đến màn hình nào?**
  - Chuyển sang SRS Review Page (LN-13-S1) khi bấm bắt đầu ôn tập.
  - Quay lại Dashboard (LN-01) khi chọn tab Dashboard trên Top Nav.
- **Các màn hình liên quan khác:** SRS Review Page (LN-13-S1).

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0) đặc trưng.
- Thẻ kích hoạt ôn tập sử dụng màu cam đào Peach (`#ffb084`) của Clay.com để báo hiệu hoạt động hàng ngày vô cùng quan trọng, thu hút sự chú ý của người dùng.
- Thẻ xem chi tiết từ điển sử dụng màu nền surface-card (#f5f0e0), viền hairline 1px (#e5e5e5) bo tròn rounded-lg (16px) hoặc rounded-xl (24px) tạo cảm giác tối giản, thoáng mắt.
- Dropdown tìm kiếm nhanh có độ đổ bóng cực thấp, mượt mà giúp tập trung thị giác vào danh sách từ gợi ý.
- Touch target của các nút bấm và ô tìm kiếm tối thiểu 44px.
