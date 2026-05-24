# MÀN HÌNH: PRE-TEST SETUP PAGE (MÀN HÌNH THIẾT LẬP TRƯỚC KHI THI)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Pre-test Setup Page (Màn hình thiết lập trước khi thi)
- **Mã use case liên quan:** UC-07 (Thực hiện bài thi đánh giá năng lực)
- **Mã luồng người dùng liên quan:** LN-FL-04 (Phòng thi - Exam Room)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Dashboard $\rightarrow$ Click Unit $\rightarrow$ Unit Detail Page $\rightarrow$ Click Bài thi $\rightarrow$ Pre-test Setup Page (URL: `/units/{unit_id}/exams/{exam_id}/setup`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Người học sử dụng màn hình này để xem cấu trúc tổng quát của đề thi (số lượng câu hỏi, thời gian quy định, cơ cấu kỹ năng) và cấu hình lựa chọn chế độ làm bài (Tập dượt hoặc Thi thật) trước khi nhấn bắt đầu thực hiện bài thi chính thức.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục một cột căn giữa hoàn toàn (Centered Card Layout) dùng CSS Flexbox để đưa khối nội dung chính vào tâm màn hình.
- **Màu nền chung:** Nền trang sử dụng `{colors.canvas}` (`#F9F7FE`) phối dải chuyển màu mờ `{gradients.atmosphere-haze}`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Top Bar (Thanh điều hướng cố định)**
    - Chiều cao: `nav-height` (64px), ghim cố định ở sát mép trên.
  - **Zone 2: Central Card (Thẻ thiết lập chính)**
    - Kích thước: Rộng tối đa `680px`. Căn giữa dọc và ngang.
  - **Zone 3: Footer Action Box (Nút khởi chạy bài thi)**
    - Nằm ở dưới cùng của thẻ thiết lập chính.

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh điều hướng đầu trang (Learner Top Nav)
- **Đặc tả Visual:**
  - Nền: Kính mờ `{colors.glass}` (`rgba(255, 255, 255, 0.7)`), có `backdrop-filter: blur(8px)`.
  - Chiều cao: `nav-height` (64px). Viền dưới mờ `1px solid rgba(155, 93, 224, 0.1)`.
- **Thành phần:**
  - **Logo DiveVerse:** Sử dụng ảnh cá voi chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) kích thước `36px x 36px` căn lề trái, bên cạnh là chữ "DiveVerse" dạng `{typography.title-lg}`.
  - **Avatar người dùng:** Dạng tròn `{rounded.full}` đường kính `36px`.

### 4.2 Thẻ thiết lập chính (Central Setup Card - Vùng B)
- **Đặc tả Visual:**
  - Nền: `{colors.surface}` (`#FFFFFF`).
  - Bo góc: `{rounded.xxl}` (32px).
  - Hiệu ứng nâng: `{elevation.glow}`. Padding: `{spacing.xl}` (32px).
  - Viền mờ: `1px solid rgba(155, 93, 224, 0.1)`.
- **Nội dung bên trong:**
  - **Thanh dẫn Breadcrumbs:** Dạng chữ `{typography.caption}` (12px), màu `{colors.text-secondary}`. Hiển thị: *"Lộ trình học / Unit 2 / Bài thi cuối khóa"*.
  - **Tiêu đề bài thi:** Dạng chữ `{typography.display-md}` (Manrope, 36px, weight 700, letter-spacing -1px). Màu `{colors.text-primary}`. Hiển thị: *"Mini-exam cuối Unit 2: Everyday Work"*.
  - **Thẻ cấu trúc đề thi (Test Spec Card):**
    - Nền: `{colors.canvas}`. Bo góc: `{rounded.xl}` (24px). Viền mờ `1px solid rgba(155, 93, 224, 0.1)`. Padding: `{spacing.lg}` (24px).
    - Hiển thị các chỉ số chi tiết:
      - *Số lượng:* 40 câu hỏi.
      - *Thời gian làm bài:* 30 phút.
      - *Điểm tối đa:* 100 EXP.
      - *Cấu trúc:* 15 câu Từ vựng, 15 câu Ngữ pháp, 5 câu Đọc hiểu, 5 câu Nghe hiểu (theo `level_built.md`).
      - *Điều kiện qua môn:* Đạt tối thiểu 50 EXP.
    - **Mascot cổ vũ:** Icon Cá Voi chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`64px x 64px`) nhún nhảy chậm bên cạnh thông tin đề thi để tạo cảm giác thân thiện nâng đỡ.

### 4.3 Khung chọn chế độ làm bài (Exam Mode Selector - Vùng C)
Gồm 2 cột hiển thị song song giúp học viên lựa chọn chế độ tương tác theo **UC-07**:
- **Chế độ "Tập dượt" (Practice Mode):**
  - Đặc tả thẻ: Thẻ Card nhỏ nền `{colors.surface}`, bo góc `{rounded.xl}` (24px), viền `1px solid rgba(155, 93, 224, 0.1)`.
  - Trạng thái Active: Viền đổi sang màu chủ đạo `{colors.primary}` (`#4E56C0`) dày 2px và có lớp phát sáng mờ.
  - Nội dung: Tiêu đề *"Tập dượt"* dạng `{typography.title-md}` (weight 600) và mô tả: *"Không giới hạn thời gian, cho phép xem ngay lời giải thích của Admin sau mỗi câu. Điểm số không ghi nhận vào học bạ."*
- **Chế độ "Thi thật" (Real Exam Mode):**
  - Tương tự thẻ Tập dượt.
  - Nội dung: Tiêu đề *"Thi thật"* dạng `{typography.title-md}` (weight 600) và mô tả: *"Có đếm ngược thời gian nghiêm ngặt, tự động nộp bài khi hết giờ. Kết quả được lưu vào học bạ để mở khóa Unit mới."*

### 4.4 Nút hành động "Bắt đầu làm bài" (Start Action Box - Vùng D)
- **Đặc tả Visual:**
  - Nút bấm `button-primary` style, nền `{colors.primary}` (`#4E56C0`), chữ trắng.
  - Bo góc: `{rounded.lg}` (16px). Chiều rộng 100%. Chiều cao: `button-min-height` (44px).
  - Hiệu ứng: Default `{elevation.active-glow}`. Hover tỏa sáng `{elevation.hover-glow}`.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Chọn Chế độ làm bài**
  - Học viên click vào một trong hai thẻ chế độ $\rightarrow$ Thẻ đó chuyển sang trạng thái Active (viền màu `{colors.primary}`, có quầng sáng), thẻ còn lại chuyển về mặc định. Mặc định hệ thống chọn sẵn "Thi thật" để học viên tích lũy học bạ.
- **Hành động: Click nút "Bắt đầu làm bài"**
  - Hệ thống gửi API khởi tạo phiên làm bài thi.
  - **Dữ liệu API:** `POST /api/exams/start`
    - Payload: `{ "examId": 82, "mode": "real_exam" }`
    - Response: `{ "success": true, "sessionToken": "exam_sess_94827" }`
  - Thành công: Chuyển hướng sang giao diện phòng thi tương ứng:
    - Nếu đề thi là Mini-exam hoặc Level test $\rightarrow$ Chuyển sang [unit_level_test_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/unit_level_test_page.md).
    - Nếu đề thi là Mock test thực tế $\rightarrow$ Chuyển sang [mock_test_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/mock_test_page.md).

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT
- **Trạng thái tải (Loading state):** Khi đang gọi API, nút hiển thị spinner và khóa click.
- **Trạng thái lỗi kết nối:** Hiển thị Toast màu đỏ `{colors.error}`: *"Không thể khởi tạo phòng thi. Vui lòng kiểm tra lại kết nối!"*.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [unit_detail_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/unit_detail_page.md) hoặc [learner_dashboard.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/learner_dashboard.md).
- **Đi đến:** [unit_level_test_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/unit_level_test_page.md) hoặc [mock_test_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/mock_test_page.md).

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Đảm bảo bố cục thoáng đãng với khoảng cách dọc `{spacing.lg}` (24px) để giải tỏa căng thẳng tâm lý của học viên trước khi làm bài thi.
- **KHÔNG ĐƯỢC:** Sử dụng bóng đổ đen thô ráp. Việc định vị trạng thái chọn chế độ thi bắt buộc dùng viền `{colors.primary}` và soft glow để giữ đúng đặc trưng của DiveVerse.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Thông tin bài thi đầu vào (Pre-test Info):** Liên kết với đối tượng `tests[0]` (id: `test_pre`), bao gồm các trường `{name}`, `{typeLabel}`, `{duration}`, `{questionsCount}`, `{maxScore}`.
- **Danh sách câu hỏi Pre-test (Questions list):** Mảng `tests[0].questions` (các trường `{text}`, `{options}`, `{correctAnswer}`).
