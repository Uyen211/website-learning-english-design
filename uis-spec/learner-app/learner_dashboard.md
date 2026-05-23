# MÀN HÌNH: LEARNER DASHBOARD (LỘ TRÌNH HỌC TRỰC QUAN DẠNG SƠ ĐỒ CÂY/TRẠM)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Learner Dashboard (Lộ trình học trực quan dạng sơ đồ cây/trạm)
- Mã use case liên quan: UC-05a, UC-05b, UC-06, UC-07, UC-08 (Màn hình điều phối trung tâm cho mọi hoạt động học tập)
- Mã luồng người dùng liên quan: Flow LN-FL-01, LN-FL-02, LN-FL-03, LN-FL-04, LN-FL-05, LN-FL-06, LN-FL-07, LN-FL-08, LN-FL-09 (Điểm xuất phát hành trình)
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Đăng nhập học viên -> Learner Dashboard (URL: /dashboard)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Người học sử dụng màn hình này để theo dõi toàn bộ lộ trình học tiếng Anh được trực quan hóa dưới dạng bản đồ cây/trạm học tập, xem tiến trình cá nhân (điểm EXP, streak ngày học), và nhấp chọn các Unit đã mở khóa để bắt đầu học tập.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục một cột có thanh điều hướng ghim cố định đầu trang (Sticky Top Navbar) và màn hình cuộn dọc vô tận chứa sơ đồ trạm học tập (Vertical Roadmap Path).
- Các vùng chính trên màn hình:
  - Vùng A: Thanh điều hướng đầu trang (Learner Top Nav) chứa Logo, các tab phân hệ ứng dụng (Dashboard, Luyện tập, Thi cử, Ôn tập), và Avatar người dùng.
  - Vùng B: Bảng thông tin cá nhân và tiến trình (Student Progress Widget) ở phía trên bên trái (hoặc dạng thanh nổi ngang) hiển thị cấp độ hiện tại, thanh tiến trình %, tổng điểm EXP và chuỗi ngày streak học tập.
  - Vùng C: Gợi ý bài học tiếp theo (Next Recommendation Card) dạng thẻ nổi bật, nhắc nhở bài học cần học ngay lập tức để giữ streak.
  - Vùng D: Sơ đồ lộ trình học dạng cây/trạm (Visual Roadmap Tree Graph) chạy dọc chính giữa màn hình. Các Unit được vẽ dưới dạng các nút tròn (trạm học) nối với nhau bằng các đường vẽ cong uốn lượn phong cách đất sét 3D.
- Kích thước / Grid tham khảo:
  - Chiều rộng tối đa của Vùng D: 900px, nằm chính giữa màn hình.
  - Vùng B và C được thiết kế như các widget nổi hoặc thanh ngang phía trên sơ đồ lộ trình.
  - Khoảng cách dọc giữa các trạm Unit: 120px để tạo không gian uốn lượn của sơ đồ cây lộ trình.

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)
- **Tên component:** Thanh điều hướng học viên (Learner Top Nav)
  - **Loại component tham chiếu từ DESIGN.md:** top-nav (cao 64px, nền canvas #fffaf0, ghim cố định ở đầu trang, border-bottom 1px hairline #e5e5e5)
  - **Vị trí:** Vùng A.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:**
    - Trái: Logo Chú Cá Voi Xanh Vũ Trụ DiveVerse.
    - Giữa: Các tab chuyến đi: Dashboard (active), Trạm Luyện kỹ năng, Phòng Thi, Kho Ôn tập.
    - Phải: Tổng EXP hiển thị dạng badge icon, và Avatar bo tròn của học viên.

- **Tên component:** Bảng thông tin cá nhân & tiến trình (Student Progress Widget)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền surface-card #f5f0e0, border 1px hairline #e5e5e5, rounded-lg 16px, padding 20px)
  - **Vị trí:** Vùng B, nằm phía trên lộ trình.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:**
    - Cấp độ hiện tại: "Cấp độ: Cơ bản (A1 - A2)".
    - Thanh tiến trình: Progress Bar màu xanh lá success (#22c55e), hiển thị mức hoàn thành cấp độ học (ví dụ: "Đã hoàn thành 45%").
    - Streak học tập: Icon ngọn lửa màu cam đỏ và dòng chữ: "Streak: 7 ngày".

- **Tên component:** Thẻ gợi ý học tập (Next Recommendation Card)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-ochre (nền brand-ochre #e8b94a, chữ ink #0a0a0a, rounded-xl 24px, padding 24px)
  - **Vị trí:** Vùng C, nằm cạnh bảng tiến trình.
  - **Trạng thái:** Mặc định. Có nhịp thở phát sáng nhẹ (pulsing glow) ở viền để thu hút sự chú ý.
  - **Dữ liệu hiển thị / hành vi:** Dòng chữ "BÀI HỌC TIẾP THEO: Unit 2 - Đời sống công sở (Học Từ vựng)". Nút CTA "Vào học ngay" (`button-primary` nền đen, chữ trắng) ở trong thẻ. Nhấn vào sẽ dẫn trực tiếp tới bài học từ vựng của Unit 2.

- **Tên component:** Trạm Unit đã hoàn thành (Completed Unit Node)
  - **Loại component tham chiếu từ DESIGN.md:** rounded-full (trạm tròn đường kính 80px, nền brand-teal #1a3a3a, chữ màu on-primary #ffffff)
  - **Vị trí:** Vùng D, nằm trên đường cong lộ trình.
  - **Trạng thái:** Đã hoàn thành.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị số thứ tự Unit ở giữa trạm (ví dụ: "01"). Phía trên có một vòng tròn icon tích xanh lá nhỏ biểu thị đã hoàn thành. Rê chuột qua thẻ hiển thị popup tóm tắt: "Unit 1: Pronoun Basics - Hoàn thành 100%". Nhấp chuột sẽ chuyển sang màn hình Unit Detail (LN-02).

- **Tên component:** Trạm Unit đang học (Active Unit Node)
  - **Loại component tham chiếu từ DESIGN.md:** rounded-full (trạm tròn đường kính 90px, nền brand-peach #ffb084, chữ ink #0a0a0a, border 3px solid primary #0a0a0a)
  - **Vị trí:** Vùng D, nằm tiếp theo trên lộ trình.
  - **Trạng thái:** Active / Đang học. Có hiệu ứng nhấp nháy phát sáng (pulsing) màu cam đào xung quanh trạm.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị số thứ tự ở giữa (ví dụ: "02"). Nhấp chuột sẽ mở màn hình Unit Detail (LN-02) để tiếp tục học các bài học chưa xong.

- **Tên component:** Trạm Unit chưa mở khóa (Locked Unit Node)
  - **Loại component tham chiếu từ DESIGN.md:** rounded-full (trạm tròn đường kính 80px, nền surface-strong #ebe6d6, chữ màu muted #6a6a6a)
  - **Vị trí:** Vùng D, nằm ở các vị trí phía sau trên lộ trình.
  - **Trạng thái:** Bị khóa.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị một icon chiếc ổ khóa nhỏ ở giữa trạm, số thứ tự mờ đi (ví dụ: "03"). Không thể nhấp chọn.

- **Tên component:** Đường nối lộ trình (Path Connector Lines)
  - **Loại component tham chiếu từ DESIGN.md:** vector line (đường vẽ uốn lượn 3D dẹt dải đất sét)
  - **Vị trí:** Vùng D, kết nối giữa các trạm Unit.
  - **Trạng thái:** 
    - Đã kết nối: Đường nối có màu cam đất sét đậm.
    - Chưa mở khóa: Đường nối mờ màu xám kem nhạt.

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động:** Nhấp vào một Trạm Unit đang học hoặc đã hoàn thành (Active / Completed Node)
  - **Luồng chính:** Học viên click chuột trái vào nút trạm -> Hệ thống chuyển hướng trình duyệt đến màn hình Unit Detail Page (LN-02) tương ứng của Unit đó.
- **Hành động:** Nhấp vào Trạm Unit bị khóa (Locked Node)
  - **Luồng chính:** Học viên click chuột vào nút trạm -> Hệ thống không chuyển trang, trạm phát rung nhẹ (shake animation) và hiển thị tooltip thông báo lỗi mờ màu tối: "Bạn cần hoàn thành Unit trước đó để mở khóa!".
- **Hành động:** Nhấp vào Avatar học viên ở Top Nav
  - **Luồng chính:** Mở menu dropdown nhỏ hiển thị các tùy chọn: "Học bạ cá nhân", "Cài đặt tài khoản", "Đăng xuất". Nhấp chọn "Đăng xuất" sẽ xóa JWT token trong LocalStorage và chuyển về Guest Landing Page (TR-01).

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Không áp dụng cho màn hình lộ trình vì cấu trúc lộ trình các Unit luôn cố định dựa trên thiết lập của Admin.
- **Trạng thái tải (loading state):** Khi đang tải tiến trình học viên từ API, các trạm Unit hiển thị dạng vòng tròn xám nhạt và các liên kết bị khóa click, thanh tiến trình hiển thị skeleton nhấp nháy.
- **Trạng thái lỗi (error state):** Nếu API lộ trình bị lỗi, hiển thị một banner thông báo lỗi màu đỏ ở đầu trang: "Lỗi đồng bộ tiến trình. Vui lòng nhấn F5 để tải lại!".
- **Trạng thái thành công (success state):** Khi học viên vừa hoàn thành toàn bộ bài tập của một Unit và quay lại trang này, hệ thống hiển thị hiệu ứng pháo hoa giấy (confetti) rơi từ trên xuống và trạm Unit vừa học chuyển đổi màu sắc từ peach sang teal cùng icon tích xanh xuất hiện.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ Login Page (TR-02) hoặc Register Page (TR-03) sau khi xác thực thành công.
- **Sau khi hoàn thành hành động, đi đến màn hình nào?**
  - Chuyển sang Unit Detail Page (LN-02) khi click vào một Unit đã mở khóa.
  - Chuyển sang các phân hệ Luyện tập, Thi cử, Ôn tập khi click các tab tương ứng trên Top Nav.
- **Các màn hình liên quan khác:** Unit Detail Page (LN-02).

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0) đặc trưng.
- Sơ đồ trạm lộ trình được thiết kế mềm mại, các trạm tròn Unit bo góc tuyệt đối (`rounded-full`) và sử dụng các màu sắc ấm áp tương phản cao của Clay.com: Unit hoàn thành dùng màu Teal sẫm (#1a3a3a), Unit active dùng màu cam đào Peach (#ffb084), Unit khóa dùng màu xám kem đất sét (#ebe6d6).
- Sử dụng hiệu ứng micro-animation (pulsing) phát sáng nhẹ xung quanh Trạm đang học để kích thích động lực học tập của học viên theo Nguyên tắc Báo hiệu (Signaling Principle).
- Khoảng cách giữa các trạm uốn lượn thưa thớt tạo nhịp điệu dễ thở, giảm áp lực tâm lý cho người học khi nhìn vào toàn bộ lộ trình dài.
- Touch target của các nút trạm đạt tối thiểu 80x80px giúp dễ bấm trên mọi thiết bị di động và máy tính bảng.



