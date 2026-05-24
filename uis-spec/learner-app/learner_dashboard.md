# MÀN HÌNH: LEARNER DASHBOARD (LỘ TRÌNH HỌC TRỰC QUAN DẠNG SƠ ĐỒ CÂY/TRẠM)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Learner Dashboard (Lộ trình học trực quan dạng sơ đồ cây/trạm)
- **Mã use case liên quan:** UC-05a, UC-05b, UC-06, UC-07, UC-08 (Màn hình điều phối trung tâm cho mọi hoạt động học tập)
- **Mã luồng người dùng liên quan:** LN-FL-01, LN-FL-02, LN-FL-03, LN-FL-04, LN-FL-05 (Điểm xuất phát hành trình)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Đăng nhập $\rightarrow$ Learner Dashboard (URL: `/dashboard`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Người học sử dụng màn hình này làm trung tâm định hướng hành trình học tập. Màn hình giúp theo dõi lộ trình tiếng Anh trực quan dựa trên 3 Cấp độ học tập (Basic A1-A2, Intermediate B1-B2, Advanced C1-C2) tương ứng các trạm Unit (theo `level_built.md`), quản lý tiến độ cá nhân (Streak, EXP, mục tiêu ngày), truy cập nhanh vào bài học gợi ý tiếp theo và phòng ôn tập Spaced Repetition (SRS - UC-08).

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục một cột có thanh điều hướng ghim cố định đầu trang (Sticky Top Navbar) và màn hình cuộn dọc chứa sơ đồ trạm học tập (Vertical Roadmap Path).
- **Màu nền chung:** Nền trang sử dụng `{colors.canvas}` (`#F9F7FE`) kết hợp với dải màu chuyển tiếp khí quyển `{gradients.atmosphere-haze}` tĩnh ở phía sau khu vực Hero/Lộ trình.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Top Bar (Thanh điều hướng cố định)**
    - Chiều cao: `nav-height` (64px). Chứa logo cá voi chính, các tab chuyển phân hệ học tập, và avatar góc phải.
  - **Zone 2: Student Progress Snapshot (Widget thống kê nhanh)**
    - Bố cục: Nằm ngang ngay dưới Top Bar. Hiển thị Level hiện tại (Basic/Intermediate/Advanced), thanh tiến độ %, chuỗi ngày học liên tục (Streak), và EXP mục tiêu ngày.
  - **Zone 3: Next Lesson Hero Card (Thẻ gợi ý học tập nổi bật - Khu vực Vàng)**
    - Chiều rộng: 100% container, nằm ngay trên lộ trình học để kéo 100% sự tập trung vào nút học tiếp.
  - **Zone 4: Roadmap Path (Sơ đồ lộ trình dạng trạm thiên hà uốn lượn)**
    - Một sơ đồ chạy dọc hình zigzag (zitzac) ở trung tâm màn hình (rộng tối đa 900px), các trạm là các "hành tinh" (Unit) nối với nhau bằng các "quỹ đạo" nét đứt.
  - **Zone 5: Spaced Repetition Panel (Hàng đợi Ôn tập SRS cấp bách)**
    - Bảng danh sách các từ vựng/ngữ pháp đến hạn cần ôn tập (theo thuật toán SRS - UC-08), thúc đẩy người học duy trì trí nhớ dài hạn.

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh điều hướng học viên (Learner Top Nav)
- **Đặc tả Visual:**
  - Nền: Kính mờ `{colors.glass}` (`rgba(255, 255, 255, 0.7)`), có thuộc tính `backdrop-filter: blur(8px)`.
  - Chiều cao: `nav-height` (64px). Viền dưới mờ `1px solid rgba(155, 93, 224, 0.1)`.
- **Các phần tử bên trong:**
  - **Logo DiveVerse:** Sử dụng tệp ảnh cá voi chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) kích thước `36px x 36px` căn lề trái, bên cạnh là chữ "DiveVerse" dạng `{typography.title-lg}`.
  - **Danh sách Tab điều hướng:** Dashboard (Tab active có vạch kẻ `{colors.primary}` dày 3px phía dưới), Luyện tập, Thi cử, Ôn tập. Font chữ `{typography.body-md}`, màu `{colors.text-secondary}`.
  - **Avatar người dùng:** Dạng tròn `{rounded.full}` đường kính `36px`, có viền sáng mờ ảo của `{colors.accent}`. Khi nhấp chuột mở menu dropdown trượt kính mờ.

### 4.2 Bảng thông tin tiến trình (Student Progress Widget)
- **Đặc tả Visual:**
  - Nền: `{colors.surface}` (`#FFFFFF`). Bo góc `{rounded.xl}` (24px).
  - Hiệu ứng: Soft glow `{elevation.glow}`. Padding: `{spacing.lg}` (24px).
- **Nội dung hiển thị động (theo Cấp độ đang học - level_built.md):**
  - **Cấp độ học hiện tại:** Tên cấp độ (ví dụ: *"Cấp độ 2: Intermediate (B1 - B2)"*), kèm badge mục tiêu *"IELTS 5.5 - 6.5"* hoặc *"TOEIC 550 - 940"*.
  - **Streak ngày học:** Icon `flame` (Màu cam sáng `{colors.warning}`) nhấp nháy động chậm, kế bên là dòng chữ *"Streak: 12 ngày"* dạng `{typography.title-md}`.
  - **Thống kê mục tiêu ngày (Daily Goal):** Dòng chữ *"Hôm nay: 15 / 20 XP"* (UX Maslow - Kích thích gắn kết).
  - **Thanh tiến độ cấp độ:** Hiển thị mức hoàn thành (ví dụ: *"15 / 35 Units đã xong - 42%"*). Dưới là thanh `progress-bar` cao 8px, nền `{colors.light-accent}` (`#FDCFFA`), phần hoàn thành dùng dải Gradient `{gradients.morning-nebula}`.

### 4.3 Thẻ gợi ý học tập tiếp theo (Next Lesson Hero Card)
- **Đặc tả Visual:**
  - Nền: `{colors.surface}` (`#FFFFFF`) kết hợp viền sáng rực rỡ từ dải gradient `{gradients.galactic-glow}`.
  - Bo góc: `{rounded.xxl}` (32px).
  - Hiệu ứng: `{elevation.active-glow}`. Padding: `{spacing.xl}` (32px).
- **Nội dung bên trong:**
  - Tiêu đề phụ: *"BÀI HỌC TIẾP THEO"* dùng `{typography.caption}` in hoa, màu `{colors.text-secondary}`.
  - Tiêu đề chính (Bài học chưa hoàn thành gần nhất): *"Unit 2 - Bài 2: Gia đình & Bạn bè (Sở hữu cách)"* (ví dụ của Cấp độ Basic).
  - **Nút CTA Độc tôn ("Vào học ngay"):** Nền `{colors.primary}` (`#4E56C0`), chữ trắng. Bo góc `{rounded.lg}` (16px). Chiều cao tối thiểu `button-min-height` (44px). Default có `{elevation.active-glow}`, hover đổi sang `{elevation.hover-glow}`.
  - **Mascot Icon đại diện:** Sử dụng ảnh cá voi chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) kích thước `48px x 48px` lơ lửng ở góc phải thẻ.

### 4.4 Sơ đồ trạm lộ trình học tập (Roadmap Path Grid)
- **Đặc tả đường dẫn (Path Connector Lines):**
  - Các đường nối zigzag đứt đoạn kết nối các trạm. Trạm đã học xong: đường nối bừng sáng tím đậm. Trạm chưa mở: đường nối mờ xám.
- **Dữ liệu trạm Unit (Ánh xạ từ level_built.md):**
  - Sơ đồ tải danh sách Unit tương ứng với cấp độ hiện tại của người học (Cấp 1: 25 Units, Cấp 2: 35 Units, Cấp 3: 40 Units).
  - Mỗi trạm hiển thị: Số thứ tự Unit ở giữa hành tinh, Tiêu đề Unit ở dưới (ví dụ: *"Unit 1: Greetings & Introductions"*, *"Unit 2: Family & Friends"*).
- **Trạng thái Trạm Unit (Mapped from USE_CASES.md):**
  - **Trạm đã hoàn thành (Completed Unit Node):**
    - Kích thước: `80px`. Nền `{colors.primary}` (`#4E56C0`). Đính kèm một huy hiệu check xanh `{colors.success}` ở góc. Rê chuột (hover) hiển thị tooltip: *"Đạt điểm qua môn: 95/100 EXP"* (UC-07).
  - **Trạm đang học (Active Unit Node):**
    - Kích thước: `90px` (Tạo điểm nhấn lớn nhất). Nền `{colors.surface}`, viền dày 3px màu `{colors.primary}`, nhấp nháy phát sáng liên tục `{elevation.active-glow}`.
    - **Mascot định vị:** Đặt một icon cá voi mini dùng ảnh [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) kích thước `24px x 24px` nằm lơ lửng ngay phía trên trạm để báo hiệu *"Bạn đang ở đây"*.
  - **Trạm bị khóa (Locked Unit Node - Locked Transparency):**
    - Kích thước: `80px`. Nền mờ, hiển thị ổ khóa `lock`.
    - **Quy tắc minh bạch khóa (Non-Negotiable Rule 4):** Hiển thị rõ điều kiện mở khóa mờ bên dưới (ví dụ: *"Cần hoàn thành Unit 1"*).

### 4.5 Hàng đợi ôn tập SRS (Review Queue Panel - UC-08)
- **Đặc tả Visual:**
  - Nền: `{colors.surface}`. Bo góc `{rounded.xl}`. Viền mờ `1px solid rgba(155, 93, 224, 0.1)`. Padding: `{spacing.lg}`.
- **Nội dung hoạt động (theo UC-08):**
  - Tiêu đề: *"ĐẾN HẠN ÔN TẬP (5 Mục)"* dạng `{typography.title-md}`.
  - Hiển thị số lượng từ vựng/ngữ pháp đang ở điểm chuẩn bị quên theo thuật toán SRS.
  - Ví dụ:
    - *Collocation "daily routine" - Trễ hạn 2 ngày.*
    - *Grammar "Present Simple" - Đến hạn hôm nay.*
  - **Nút CTA phụ ("Bắt đầu ôn tập"):** Kích hoạt luồng ôn tập lặp lại ngắt quãng đếm ngược 10s (UC-08).

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Click vào Trạm đang học hoặc Trạm đã hoàn thành**
  - Chuyển hướng mượt mà (Fade Out/Fade In trong `0.3s`) đưa học viên đến trang chi tiết bài học của Unit tương ứng: [unit_detail_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/unit_detail_page.md).
- **Hành động: Click vào Trạm bị khóa**
  - Trạm thực hiện hiệu ứng rung lắc nhẹ (`shake`), hiển thị tooltip đỏ mờ: *"Bạn cần hoàn thành Unit trước đó để mở khóa!"* và tự động ẩn sau 2s.
- **Hành động: Click vào Avatar**
  - Dropdown kính mờ `{colors.glass}` xổ xuống hiển thị liên kết Profile/Settings và Logout.

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT
- **Trạng thái tải (Loading state):** Các hành tinh trạm học tập và các widget tiến trình hiển thị Skeleton Loader màu tím mờ, có hiệu ứng xung nhịp quét sáng mịn.
- **Trạng thái thành công mở khóa Unit mới:** Hiển thị hiệu ứng pháo hoa giấy mờ ảo và trạm Unit vừa hoàn thành đổi màu sang tím đậm, đường nối tiếp theo bừng sáng.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [learner_login_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/learner_login_page.md), [learner_register_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/learner_register_page.md).
- **Đi đến:** [unit_detail_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/unit_detail_page.md) (Sau khi chọn trạm).

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Đảm bảo khoảng cách dọc giữa các trạm Unit rộng rãi (`120px`) để sơ đồ cây không bị chật chội. Sử dụng ảnh [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) làm logo ghim cố định ở đầu thanh điều hướng để đồng nhất nhận diện thương hiệu.
- **KHÔNG ĐƯỢC:** Để hiển thị bóng đổ đen bên dưới các trạm hành tinh. Độ cao (Elevation) của các trạm phải được thể hiện hoàn toàn bằng kích thước nút và quầng sáng phát quang (glow) màu tím/vàng nhạt.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Thông tin & Thống kê học viên (Student Profile):**
  - Họ và tên học viên: `{profile.name}`
  - Lộ trình cấp độ hiện tại: `{profile.level}`
  - Điểm tích lũy EXP: `{profile.stats.exp}`
  - Chuỗi ngày học (Streak): `{profile.stats.streak}`
  - Mục tiêu EXP trong ngày: `{profile.stats.goalXP}`
- **Bài học gợi ý tiếp theo (Next Lesson Card):** Liên kết với thông tin bài học chưa hoàn thành đầu tiên của Unit hiện tại (ví dụ: `lessons.unit_1[0]`).
- **Sơ đồ lộ trình (Roadmap Nodes):** Ánh xạ từ danh sách `levels[0].units` (ví dụ các trạm Unit 1, Unit 2, Unit 3, Unit 4).
- **Hàng đợi ôn tập SRS (Review Queue Panel):** Liên kết với danh sách `srsReviewQueue` (hiển thị số lượng từ đến hạn và danh sách rút gọn).
