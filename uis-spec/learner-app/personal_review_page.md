# MÀN HÌNH: PERSONAL REVIEW DASHBOARD (BẢNG ĐIỀU KHIỂN TRA CỨU & ÔN TẬP CÁ NHÂN)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Personal Review Dashboard (Màn hình bảng điều khiển tra cứu & ôn tập cá nhân)
- **Mã màn hình:** LN-12
- **Mã use case liên quan:** UC-08 (Tra cứu nhanh và ôn tập lặp lại ngắt quãng SRS)
- **Mã luồng người dùng liên quan:** Flow LN-FL-09 (Tra cứu nhanh & Ôn tập SRS)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Dashboard $\rightarrow$ Click tab "Tra cứu & Ôn tập" trên Top Nav $\rightarrow$ Personal Review Dashboard (URL: `/review`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này làm trung tâm học tập để quản lý tiến trình ghi nhớ dài hạn cá nhân. Tại đây, người học thực hiện tra cứu nhanh từ vựng/ngữ pháp qua thanh tìm kiếm thông minh có gợi ý tự động (autocomplete), theo dõi biểu đồ thống kê mức độ bền vững của trí nhớ (Memory Strength), và kích hoạt phiên ôn tập lặp lại ngắt quãng (SRS) hàng ngày để gia cố kiến thức trước khi bị quên.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục kết hợp chia lưới 2 cột bất đối xứng tỷ lệ 7:5 trên máy tính (desktop) và tự động xếp chồng 1 cột trên điện thoại (mobile).
- **Màu nền chung:** Nền trang sử dụng `{colors.canvas}` (`#F9F7FE`) dịu nhẹ với dải sương mờ `{gradients.atmosphere-haze}` phủ xung quanh.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Top Navigation Bar (Thanh điều hướng cố định):** Chiều cao 64px, chứa logo, các liên kết chính và avatar.
  - **Zone 2: Dictionary Search Area (Thanh tìm kiếm từ điển - Vùng A):** Trải rộng 100% ở phía trên cùng của khu vực nội dung chính.
  - **Zone 3: Left Panel (Vùng B - chiếm 7 cột):** Chứa Thẻ kích hoạt ôn tập SRS hàng ngày (SRS Trigger Card) và các gợi ý ôn tập chuyên sâu.
  - **Zone 4: Right Panel (Vùng C - chiếm 5 cột):** Chứa Biểu đồ độ bền trí nhớ (Memory Strength Widget) và Sổ tay lỗi sai tóm tắt.
- **Kích thước tham khảo:**
  - Chiều rộng tối đa của container nội dung: `1080px` căn giữa.
  - Khoảng cách giữa các panel: `{spacing.lg}` (24px).
  - Padding trong các card: `{spacing.xl}` (32px) cho card chính, `{spacing.lg}` (24px) cho các card phụ.

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh tìm kiếm từ điển thông minh (Dictionary Search Area - Vùng A)
- **Tên component:** Thanh tìm kiếm từ điển (Dictionary Search Bar)
  - **Đặc tả Visual:**
    - Loại component: `text-input` cao `48px` để tối ưu touch target.
    - Nền: `{colors.surface}` (`#FFFFFF`). Viền mặc định: `1px solid rgba(155, 93, 224, 0.2)`. Bo góc: `{rounded.lg}` (16px).
    - Hiệu ứng: Focus viền đổi sang `{colors.primary}` (`#4E56C0`) với `{elevation.active-glow}`.
    - Icon: Kính lúp (Lucide `search`) màu `{colors.text-secondary}` nằm ở góc trái ô nhập liệu.
    - Placeholder: *"Nhập từ vựng hoặc cấu trúc ngữ pháp cần tra cứu..."*.
  - **Hành vi:** Khi gõ ký tự, hệ thống lập tức gọi API tìm kiếm và hiển thị dropdown danh sách từ gợi ý bên dưới.

- **Tên component:** Danh sách từ gợi ý (Search Auto-complete Dropdown)
  - **Đặc tả Visual:**
    - Nền: `{colors.surface}`. Bo góc: `{rounded.lg}` (16px). Viền: `1px solid rgba(155, 93, 224, 0.15)`.
    - Hiệu ứng: Đổ bóng mờ nhẹ `{elevation.glow}` để nổi lên trên bề mặt trang web.
    - Vị trí: Xổ thẳng đứng ngay dưới thanh tìm kiếm, bao phủ chiều rộng tương tự thanh tìm kiếm.
  - **Dữ liệu hiển thị:**
    - Tối đa 5 từ gợi ý trùng khớp (ví dụ: *collaborate*, *collaboration*, *collaborative*).
    - Mỗi dòng hiển thị từ vựng kèm theo loại từ (dạng `{typography.caption}` màu `{colors.text-secondary}`) ở bên phải.
    - Khi rê chuột (hover) vào dòng, dòng chuyển sang nền màu nhạt `{colors.canvas}` và chữ đổi sang `{colors.primary}`.

### 4.2 Thẻ kích hoạt ôn tập SRS hàng ngày (SRS Trigger Card - Vùng B)
- **Đặc tả Visual:**
  - Nền: Dải chuyển màu tinh vân `{gradients.morning-nebula}` vô cùng bắt mắt để kích thích động lực học tập.
  - Bo góc: `{rounded.xxl}` (32px). Padding: `{spacing.xl}` (32px).
  - Hiệu ứng nâng: Mặc định `{elevation.active-glow}`.
- **Nội dung:**
  - **Mascot nhỏ đi kèm:** Hình ảnh chú cá voi [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`80px x 80px`) nhún nhảy chậm ở góc phải card, bụng phát sáng lung linh.
  - **Tiêu đề:** *"Ôn tập SRS Hàng Ngày"* dạng `{typography.title-lg}` (24px, Manrope, chữ màu `{colors.text-primary}`).
  - **Thống kê tiến trình:** *"Hôm nay bạn có **15 từ & cấu trúc** đã đến hạn ôn tập để đưa vào bộ nhớ dài hạn."* (font `{typography.body-md}`, màu `{colors.text-primary}` đậm).
  - **Icon Streak lửa nhỏ:** Biểu tượng ngọn lửa (Lucide `flame`) nhấp nháy phát sáng nhẹ màu cam báo hiệu chuỗi ngày học hiện tại.
  - **Nút "Ôn tập ngay":** Style `button-primary` nền `{colors.primary}` (`#4E56C0`), chữ trắng, cao `48px`, bo góc `{rounded.lg}` (16px), mặc định tỏa sáng `{elevation.active-glow}`. Hover tỏa sáng mạnh `{elevation.hover-glow}`.

### 4.3 Biểu đồ độ bền trí nhớ (Memory Strength Widget - Vùng C)
- **Đặc tả Visual:**
  - Nền: `{colors.surface}`. Bo góc: `{rounded.xl}` (24px). Viền: `1px solid rgba(155, 93, 224, 0.1)`.
  - Padding: `{spacing.lg}` (24px). Hiệu ứng: `{elevation.glow}`.
- **Nội dung:**
  - **Tiêu đề phụ:** *"Độ bền trí nhớ"* dạng `{typography.title-md}` (18px, weight 600, màu `{colors.text-primary}`).
  - **Biểu đồ tròn độ bền (Memory Pie Chart / Progress Ring):**
    - Sử dụng SVG vòng tròn đồng tâm xếp chồng mô tả các mốc độ bền trí nhớ.
    - Màu sắc phân chia theo trạng thái:
      - *Mastered (Dài hạn - Sắp xếp ngoài cùng):* Màu `{colors.success}` (`#22C55E`).
      - *Review (Đang củng cố):* Màu `{colors.secondary}` (`#9B5DE0`).
      - *Learning (Mới học - Trong cùng):* Màu `{colors.accent}` (`#D78FEE`).
  - **Chú thích số liệu cụ thể:** Hiển thị bên dưới biểu đồ:
    - Mastered (Dài hạn): 120 từ.
    - Review (Củng cố): 45 từ.
    - Learning (Mới học): 15 từ.

### 4.4 Sổ tay lỗi sai nhanh (Error Memory Quick-view)
- **Đặc tả Visual:**
  - Thẻ card phụ nền `{colors.surface}` nằm dưới biểu đồ độ bền, bo góc `{rounded.xl}` (24px), viền mờ, padding `{spacing.lg}` (24px).
- **Nội dung:**
  - Hiển thị danh sách 3 từ vựng gần đây bị học viên tự đánh giá là "Quên mất" nhiều nhất.
  - Mỗi từ có kèm theo nút nhỏ "Luyện lại" (style `button-secondary` cao `32px` để luyện tập nhanh lập tức).

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Nhập từ khóa tra cứu từ điển**
  - Học viên nhập ký tự (ví dụ: *"collab"*) $\rightarrow$ Hiển thị dropdown gợi ý $\rightarrow$ Học viên click chọn từ *"collaborate"* $\rightarrow$ Chuyển hướng màn hình sang trang chi tiết từ điển tại URL `/dictionary/collaborate` (LN-14).
  - **Luồng rẽ nhánh (Không tìm thấy từ):** Học viên nhập từ không tồn tại $\rightarrow$ Dropdown hiển thị dòng chữ màu `{colors.text-secondary}`: *"Không tìm thấy từ vựng phù hợp. Bấm Enter để tìm kiếm nâng cao."*
- **Hành động: Bắt đầu phiên ôn tập**
  - Học viên click nút "Ôn tập ngay" trên SRS Trigger Card $\rightarrow$ Hệ thống chuyển hướng sang màn hình `/review/run` (LN-13-S1).

---

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái hôm nay không có từ cần ôn (Empty State):**
  - Khi số từ cần ôn bằng 0:
    - SRS Trigger Card đổi màu nền sang màu `{colors.success}` nhạt, viền màu `{colors.success}` mờ.
    - Tiêu đề đổi thành: *"Trí nhớ của bạn đang rất tốt!"*.
    - Nội dung đổi thành: *"Tuyệt vời! Bạn đã hoàn thành tất cả các mục tiêu ôn tập của ngày hôm nay. Hãy học thêm bài mới để tích lũy thêm từ vựng nhé!"*.
    - Mascot Cá Voi [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) hiển thị động tác nhào lộn ăn mừng.
    - Nút "Ôn tập ngay" bị disabled và đổi thành chữ *"Đã hoàn thành"*.
- **Trạng thái tải dữ liệu (Loading State):** Hiển thị các hiệu ứng skeleton mờ màu `{colors.canvas}` lướt qua tại vị trí biểu đồ tròn và danh sách từ vựng.

---

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** Bất kỳ trang nào sau khi người học nhấp chọn tab "Tra cứu & Ôn tập" trên thanh điều hướng Top Nav.
- **Đi đến:**
  - [srs_review_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/srs_review_page.md) (khi bấm bắt đầu ôn tập).
  - [dictionary_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/dictionary_page.md) (khi click từ vựng tìm kiếm gợi ý).

---

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Đảm bảo thanh tìm kiếm phản hồi tức thì với độ trễ (debounce) tối đa `300ms` trước khi gọi API để tối ưu hóa hiệu năng máy chủ.
- **KHÔNG ĐƯỢC:** Sử dụng các bóng đổ vật lý màu xám hoặc đen dưới các card. Chỉ sử dụng hiệu ứng `{elevation.glow}` và viền hairline 1px nhẹ nhàng với màu nhạt để tạo chiều sâu tinh tế.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Sổ tay lỗi sai cá nhân (Error Memory List):** Liên kết với mảng `profile.errorMemoryList` (các trường `{word}`, `{ipa}`, `{failCount}`).
- **Lịch sử học tập & Điểm số (Study History Table):** Liên kết với mảng `profile.studyHistory` (các trường `{testName}`, `{score}`, `{date}`, `{result}`, `{detailsUrl}`).
