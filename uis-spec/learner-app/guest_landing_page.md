# MÀN HÌNH: GUEST LANDING PAGE (TRANG CHỦ GIỚI THIỆU)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Guest Landing Page (Trang chủ giới thiệu)
- Mã use case liên quan: N/A (Trang giới thiệu tiếp thị dành cho khách truy cập)
- Mã luồng người dùng liên quan: Flow LN-FL-01 (Xác thực tài khoản người học)
- Vai trò người dùng: Guest (Khách truy cập chưa đăng nhập)
- Vị trí trong sitemap: Trang chủ (URL: /)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Người dùng (Khách vãng lai) truy cập trang này để tìm hiểu về hành trình khám phá tiếng Anh cùng DiveVerse (phương pháp học tự nhiên, luyện tập tương tác và người bạn đồng hành AI Cá Voi) và bắt đầu chuyến du hành của mình.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục cuộn dọc nhiều phân băng (Multi-band Long Scrolling Layout) đặc trưng của Clay.com, sử dụng nền canvas sáng ấm (#fffaf0).
- Các vùng chính trên màn hình:
  - Vùng A: Thanh điều hướng đầu trang (Sticky Header Navbar) cố định.
  - Vùng B: Phân băng khởi hành (Hero Section Grid 7-5) giới thiệu thông điệp chính "Bơi vào vũ trụ ngôn ngữ", kết hợp hình minh họa 3D Chú Cá Voi Xanh bơi giữa các hành tinh kiến thức bên phải.
  - Vùng C: Lưới thẻ "Trạm dừng chân" (Feature Cards Grid 3-up) giới thiệu các tính năng: Học từ vựng tự nhiên, Luyện kỹ năng thực tế, và Người bạn Cá Voi đồng hành.
  - Vùng D: Băng kêu gọi hành động "Sẵn sàng cất cánh" (Illustrated CTA Band).
  - Vùng E: Chân trang (Cream-tinted Footer) chứa thông tin kết nối và hình ảnh mặt trăng đất sét 3D.
- Kích thước / Grid tham khảo:
  - Chiều rộng nội dung tối đa: 1280px căn giữa.
  - Khoảng cách dọc giữa các phân băng: spacing-section (96px).
  - Lưới Vùng C: 3 cột ở desktop, 2 cột ở tablet, 1 cột ở mobile.

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)
- **Tên component:** Thanh điều hướng đầu trang (Header Navbar)
  - **Loại component tham chiếu từ DESIGN.md:** top-nav (cao 64px, nền canvas #fffaf0, border-bottom 1px hairline #e5e5e5)
  - **Vị trí:** Vùng A, ghim cố định ở đầu màn hình.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** 
    - Bên trái: Logo 3D DiveVerse hình Chú Cá Voi Xanh và Wordmark "DiveVerse" màu ink (#0a0a0a).
    - Ở giữa: Danh sách link điều hướng (Khám phá, Lộ trình, Tính năng, Tham gia) dạng `nav-link` (Inter 14px weight 500, màu muted #6a6a6a).
    - Bên phải: Nút "Đăng nhập" (`button-text-link`) và nút "Khám phá ngay" (`button-primary` nền đen, chữ trắng).

- **Tên component:** Tiêu đề Hero (Hero Headline)
  - **Loại component tham chiếu từ DESIGN.md:** display-xl (Plain Black display typeface, font Inter weight 500, size 68px, line-height 1.0, letter-spacing -2.5px)
  - **Vị trí:** Vùng B, nằm bên trái của Hero Section.
  - **Trạng thái:** Mặc định, màu chữ ink (#0a0a0a).
  - **Dữ liệu hiển thị / hành vi:** Dòng chữ: "Bơi vào vũ trụ tiếng Anh theo cách tự nhiên nhất".

- **Tên component:** Đoạn văn mô tả Hero
  - **Loại component tham chiếu từ DESIGN.md:** body-strong (font Inter weight 500, size 18px, line-height 1.55, màu body-strong #1a1a1a)
  - **Vị trí:** Vùng B, nằm dưới tiêu đề Hero.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Dòng chữ: "DiveVerse giúp bạn đắm mình vào ngôn ngữ qua những ngữ cảnh thực tế. Cùng chú Cá Voi Thông Thái khám phá từ vựng, ngữ pháp và luyện nói tương tác mỗi ngày.".

- **Tên component:** Nút CTA Hero "Bắt đầu học ngay"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, font Inter size 14px, weight 600, rounded-md 12px, height 44px, padding 12px x 24px)
  - **Vị trí:** Vùng B, nằm dưới đoạn mô tả Hero.
  - **Trạng thái:** Mặc định, hover (tăng độ sáng nhẹ).
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Bắt đầu học ngay". Nhấp chuột chuyển sang Register Page (TR-03).

- **Tên component:** Ảnh minh họa Hero 3D
  - **Loại component tham chiếu từ DESIGN.md:** hero-illustration-card (nền surface-soft #faf5e8, rounded-xl 24px)
  - **Vị trí:** Vùng B, nằm bên phải của Hero Section.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hình ảnh 3D claymation minh họa một nhân vật đang lướt sóng trên đại dương tri thức chứa đầy các chữ cái và từ vựng tiếng Anh. Kích thước hiển thị: 480px x 420px.

- **Tên component:** Lưới thẻ tính năng (Feature Cards Grid)
  - **Loại component tham chiếu từ DESIGN.md:** grid 3-up
  - **Vị trí:** Vùng C.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị 3 thẻ tính năng nổi bật:
    - *Thẻ 1 - Học từ vựng tự nhiên:* `feature-card-pink` (nền brand-pink #ff4d8b, chữ trắng). Chứa tiêu đề "Học từ vựng 6 giai đoạn" (Plain Black 24px), đoạn mô tả ngắn, hình ảnh mockup UI mini các giai đoạn đoán ngữ cảnh và gõ chính tả dictation.
    - *Thẻ 2 - Luyện nói hội thoại AI:* `feature-card-teal` (nền brand-teal #1a3a3a, chữ trắng). Chứa tiêu đề "Hội thoại giả lập AI" (Plain Black 24px), đoạn mô tả ngắn, hình ảnh minh họa soundwave và chat box tương tác cùng Cá Voi Thông Thái.
    - *Thẻ 3 - Ôn tập lặp lại ngắt quãng:* `feature-card-lavender` (nền brand-lavender #b8a4ed, chữ ink). Chứa tiêu đề "Bộ nhớ dài hạn SRS" (Plain Black 24px), đoạn mô tả ngắn, hình ảnh 3D claymation một chiếc đồng hồ cát phản xạ 10 giây.

- **Tên component:** Băng kêu gọi hành động cuối trang (CTA Illustrated Band)
  - **Loại component tham chiếu từ DESIGN.md:** cta-band-illustrated (nền surface-soft #faf5e8, rounded-xl 24px, padding 80px)
  - **Vị trí:** Vùng D.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:**
    - Tiêu đề "Sẵn sàng chinh phục tiếng Anh?" (display-md 40px, weight 500, màu ink #0a0a0a).
    - Nút CTA lớn "Đăng ký tài khoản miễn phí" (`button-primary` nền đen, chữ trắng).
    - Hình minh họa 3D chú Cá Voi Xanh mascot nhỏ đang đứng cười thân thiện vẫy tay ở góc phải.

- **Tên component:** Chân trang (Footer)
  - **Loại component tham chiếu từ DESIGN.md:** footer (nền surface-soft #faf5e8, text màu body #3a3a3a, padding dọc 80px)
  - **Vị trí:** Vùng E.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** 
    - Hiển thị 4 cột liên kết thông tin (Sản phẩm, Công ty, Tài nguyên, Pháp lý).
    - Dưới cùng hiển thị bản quyền và hình vẽ vector tối giản một ngọn núi đất sét nhấp nhô màu kem nhạt - biểu tượng signature của Clay.com.

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động:** Nhấp vào nút "Bắt đầu học ngay" (Hero CTA) hoặc "Đăng ký tài khoản miễn phí" (Pre-footer CTA)
  - **Luồng chính:** Khách click nút -> Chuyển hướng trình duyệt sang màn hình Register Page (TR-03) để đăng ký tài khoản mới.
- **Hành động:** Nhấp vào nút "Đăng nhập" ở Vùng A
  - **Luồng chính:** Khách click nút -> Chuyển hướng trình duyệt sang màn hình Login Page (TR-02).
- **Hành động:** Di chuột qua các thẻ tính năng ở Vùng C
  - **Luồng chính:** Con trỏ chuột chuyển thành dạng bàn tay. Thẻ hơi nhấc lên nhẹ nhờ hiệu ứng transition css mượt mà (không dùng bóng đổ đậm để giữ phong cách Clay phẳng).

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Không áp dụng cho trang tĩnh.
- **Trạng thái tải (loading state):** Khi trang đang load, ảnh 3D claymation hiển thị một ô xám mờ nhẹ trước khi ảnh tải hoàn tất.
- **Trạng thái lỗi (error state):** Không áp dụng.
- **Trạng thái thành công (success state):** Không áp dụng.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Không có (đây là trang chủ của hệ thống).
- **Sau khi hoàn thành hành động, đi đến màn hình nào?**
  - Chuyển sang Register Page (TR-03) khi bấm đăng ký.
  - Chuyển sang Login Page (TR-02) khi bấm đăng nhập.
- **Các màn hình liên quan khác:** Không có.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Giữ đúng hợp đồng thiết kế của Clay.com: Canvas màu kem ấm `#fffaf0` làm chủ đạo, tuyệt đối không dùng màu xám lạnh.
- Các thẻ feature card ở Vùng C tuân thủ quy tắc xen kẽ màu sắc: Pink -> Teal -> Lavender để tạo nhịp điệu sinh động cho trang. Thẻ Pink và Teal có nền rất đậm nên chữ được lật sang màu trắng (`#ffffff`), thẻ Lavender có nền sáng nên chữ giữ màu đen (`#0a0a0a`).
- Sử dụng font display display-xl ở cỡ chữ cực lớn 68px, chữ đậm trung bình (weight 500), khoảng cách chữ khít nhau (-2.5px) để tạo tính thương hiệu cao cấp.
- Footer sử dụng màu nền ấm `surface-soft` (#faf5e8) thay vì màu đen/xám đậm truyền thống của các trang SaaS khác.
- Đảm bảo touch target của tất cả các liên kết và nút tối thiểu 44x44px.



