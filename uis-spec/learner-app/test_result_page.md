# MÀN HÌNH: TEST RESULT PAGE (MÀN HÌNH KẾT QUẢ BÀI THI)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Test Result Page (Màn hình kết quả bài thi)
- **Mã use case liên quan:** UC-07 (Thực hiện bài thi đánh giá năng lực)
- **Mã luồng người dùng liên quan:** LN-FL-04 (Phòng thi - Exam Room)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Dashboard $\rightarrow$ Unit Detail $\rightarrow$ Pre-test Setup $\rightarrow$ Phòng thi (LN-10) $\rightarrow$ Test Result Page (URL: `/exams/results/{result_id}`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Người học sử dụng màn hình này để đánh giá chi tiết năng lực của mình sau khi nộp bài thi. Màn hình hiển thị điểm số tổng hợp, ước lượng Band điểm IELTS / điểm TOEIC tương ứng, biểu đồ năng lực kỹ năng, đáp án đúng/sai kèm lời giải thích của Admin và đề xuất định hướng ôn tập các lỗ hổng kiến thức.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục một cột dọc kết hợp chia lưới linh hoạt (Flex Grid Layout) có chiều rộng nội dung tối đa `1000px` căn giữa.
- **Màu nền chung:** Nền trang sử dụng `{colors.canvas}` (`#F9F7FE`) phối dải chuyển màu mờ `{gradients.atmosphere-haze}`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Score Overview Banner (Banner điểm số tổng hợp)**
    - Nằm to ở đầu trang, hiển thị kết quả Đạt/Chưa đạt và điểm thưởng.
  - **Zone 2: Skills & Recommendations Grid (Lưới năng lực & Đề xuất ôn tập)**
    - Chia đôi tỷ lệ 6:6 bằng CSS Grid 12 cột. Trái: Biểu đồ năng lực; Phải: Card đề xuất ôn tập.
  - **Zone 3: Question Review List (Danh sách câu hỏi & Đáp án chi tiết)**
    - Xếp dọc các câu hỏi đề thi, hỗ trợ tab lọc câu trả lời đúng/sai.
  - **Zone 4: Footer Action Button (Nút thoát kết quả)**
    - Nằm ở dưới cùng trang kết quả.

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Banner tổng hợp điểm số (Score Overview Banner - Vùng A)
- **Đặc tả Visual:**
  - Nền: Thẻ Card lớn nền `{colors.surface}` (`#FFFFFF`) kết hợp viền sáng rực rỡ từ dải gradient `{gradients.galactic-glow}`.
  - Bo góc: `{rounded.xl}` (24px).
  - Hiệu ứng: `{elevation.active-glow}`. Padding: `{spacing.xl}` (32px). Căn giữa.
  - **Pháo hoa chúc mừng (Confetti):** Tự động kích hoạt rơi pháo hoa giấy mờ ảo trên màn hình nếu học viên đạt điểm đỗ bài thi.
- **Nội dung hiển thị:**
  - Định vị điểm thi: Ước lượng Band điểm IELTS hoặc điểm TOEIC (ví dụ: *"IELTS Band ước lượng: 6.5"* hoặc *"TOEIC ước lượng: 620"*).
  - Điểm số thô tích lũy: *"85 / 100 EXP (+100 EXP thưởng)"*.
  - Nhãn trạng thái đỗ/trượt: Badge màu xanh lá `{colors.success}` (`#22C55E`) ghi *"ĐẠT YÊU CẦU"* hoặc badge màu đỏ `{colors.error}` (`#EF4444`) ghi *"CHƯA ĐẠT YÊU CẦU"*.

### 4.2 Biểu đồ năng lực & Thẻ đề xuất ôn tập (Vùng B)
- **Biểu đồ năng lực kỹ năng (Left Column):**
  - Thẻ nền `{colors.surface}`. Bo góc `{rounded.xl}` (24px), padding `{spacing.lg}` (24px).
  - Hiển thị biểu đồ hình cột hoặc tròn mô tả điểm số của các kỹ năng (Nghe, Nói, Đọc, Viết) giúp người học nhận diện điểm mạnh, điểm yếu.
- **Thẻ đề xuất ôn tập (Right Column):**
  - Nền: `{colors.light-accent}` (`#FDCFFA`) mờ ảo. Bo góc `{rounded.xl}` (24px). Padding `{spacing.lg}`.
  - Tiêu đề: *"Đề xuất ôn tập từ Cá Voi Xanh"* dạng `{typography.title-md}`.
  - Nội dung đề xuất: Liệt kê các chủ điểm bài học mà học viên làm sai nhiều (ví dụ: *"Cần cải thiện: Câu điều kiện loại 1 (Ngữ pháp), Workplace Collocations (Từ vựng)"*). Nhấp vào tên bài học sẽ dẫn thẳng tới trang học tương ứng (ví dụ: [grammar_learning_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/grammar_learning_page.md)).

### 4.3 Danh sách xem lại đáp án câu hỏi (Question Review List - Vùng C)
- **Thanh lọc câu hỏi (Review Filters):**
  - Các tab dạng viên thuốc `{rounded.pill}`: *"Tất cả câu"*, *"Câu đúng"*, *"Câu sai"*. Click để lọc danh sách câu hỏi bên dưới.
- **Thẻ xem lại câu hỏi (Question Review Card):**
  - Nền: `{colors.surface}` (`#FFFFFF`). Bo góc `{rounded.xl}` (24px). Padding `{spacing.lg}`. Viền mờ.
  - Hiển thị: Đề bài câu hỏi, đáp án học viên chọn (gắn màu đỏ `{colors.error}` kèm dấu nhân nếu làm sai; gắn màu xanh `{colors.success}` kèm tích xanh nếu làm đúng), đáp án chính xác của đề thi.
- **Khối lời giải thích của Admin (Admin's Explanation Box):**
  - Nằm dưới mỗi câu hỏi.
  - Nền: `{colors.canvas}`. Bo góc: `{rounded.md}` (12px). Border-left 3px solid `{colors.primary}` (`#4E56C0`). Padding: `{spacing.md}` (16px).
  - Nội dung: *"Lời giải thích từ giáo viên:"* dạng `{typography.body-md}` (weight 600) và đoạn văn giải nghĩa chi tiết cấu trúc từ vựng/ngữ pháp liên quan.
- **Đánh giá AI cho phần nói & viết (AI Review Panel):**
  - Xuất hiện dưới các câu hỏi tự luận. Hiển thị chi tiết lỗi chính tả/ngữ pháp bôi đỏ gạch wavy kèm theo tiêu chí chấm điểm chi tiết của Cá Voi AI.

### 4.4 Nút hành động "Quay lại Dashboard" (Vùng D)
- **Đặc tả Visual:**
  - Nút bấm lớn căn giữa trang. Nền `{colors.primary}` (`#4E56C0`), chữ trắng.
  - Bo góc: `{rounded.lg}` (16px). Chiều rộng `320px`. Chiều cao: `button-min-height` (44px).
  - Hiệu ứng: Default `{elevation.active-glow}`, hover `{elevation.hover-glow}`.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Click chuyển đổi tab bộ lọc câu hỏi**
  - Học viên click tab "Câu sai" $\rightarrow$ Danh sách Vùng C ẩn các câu làm đúng, chỉ hiển thị các câu làm sai để học viên tập trung ôn tập $\rightarrow$ Click tab "Tất cả" hiển thị đầy đủ.
- **Hành động: Click vào bài học được đề xuất ôn tập ở Vùng B**
  - Chuyển hướng trực tiếp sang trang học của bài học đó (ví dụ: [grammar_learning_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/grammar_learning_page.md)) để củng cố lại kiến thức.
- **Hành động: Nhấp nút "Quay lại Dashboard"**
  - Hệ thống kiểm tra kết quả thi, nếu đạt điểm đỗ $\rightarrow$ Tự động cập nhật mở khóa bài học/Unit tiếp theo trên cơ sở dữ liệu $\rightarrow$ Chuyển hướng quay lại màn hình [learner_dashboard.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/learner_dashboard.md).

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT
- **Trạng thái tải (Loading state):** Hiển thị skeleton mờ nhấp nháy trên toàn bộ trang trong lúc đang truy vấn dữ liệu điểm thi từ máy chủ.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [unit_level_test_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/unit_level_test_page.md) hoặc [mock_test_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/mock_test_page.md).
- **Đi đến:** [learner_dashboard.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/learner_dashboard.md).

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Sử dụng tệp ảnh gốc [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) làm logo ghim cố định ở đầu thanh Nav để đồng nhất nhận diện thương hiệu.
- **KHÔNG ĐƯỢC:** Sử dụng màu sắc bên ngoài bộ quy chuẩn tokens. Bôi đỏ đúng mã `{colors.error}` cho các câu trả lời sai và xanh lá `{colors.success}` cho câu trả lời đúng.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Thông tin kết quả thi (Test Result Header):** Liên kết với đối tượng `testResult`, bao gồm:
  - Tên bài thi: `{testResult.testName}`
  - Điểm số tích lũy: `{testResult.score}`
  - Số câu đúng: `{testResult.correctCount}`
  - Số câu sai: `{testResult.incorrectCount}`
  - Thời gian làm bài: `{testResult.timeSpent}`
  - CEFR quy đổi tương đương: `{testResult.cefrEquivalent}`
- **Biểu đồ phân tích kỹ năng (Skills Chart):** Liên kết với đối tượng `{testResult.skillsBreakdown}` (kết quả phần trăm của listening, reading, writing, speaking).
- **Danh sách chi tiết câu sai (Incorrect Answers Details):** Liên kết với mảng `testResult.incorrectDetails` (gồm `{questionText}`, `{userAnswer}`, `{correctAnswer}`, và `{explanation}`).
