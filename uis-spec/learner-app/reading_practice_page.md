# MÀN HÌNH: READING PRACTICE PAGE (MÀN HÌNH LUYỆN ĐỌC)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Reading Practice Page (Màn hình luyện đọc)
- **Mã use case liên quan:** UC-06c (Luyện đọc)
- **Mã luồng người dùng liên quan:** Flow LN-FL-03 (Trạm luyện Kỹ năng - Đọc)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Dashboard $\rightarrow$ Click Unit $\rightarrow$ Unit Detail $\rightarrow$ Click Luyện Đọc (URL: `/units/{unit_id}/lessons/{lesson_id}/reading`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên rèn luyện kỹ năng đọc hiểu qua hai hình thức: Đọc hiểu văn bản thông thường (Reading Comprehension) và Đọc báo chí thực tế (News-based Learning) kết hợp tính năng bôi đen tra từ điển nhanh tại chỗ và bảng chat Cá Voi Hỏi Đáp để giải đáp các cấu trúc ngữ pháp khó.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục chia đôi màn hình (Split Screen 50/50 Layout) để học viên vừa đối chiếu văn bản vừa làm bài tập mà không cần cuộn trang lên xuống liên tục.
- **Màu nền chung:** Nền trang sử dụng `{colors.canvas}` (`#F9F7FE`) phối dải chuyển màu mờ `{gradients.atmosphere-haze}`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Progress Header (Thanh dẫn Breadcrumbs và tiến độ ở đầu trang)**
    - Ghim cố định ở sát mép trên. Chiều cao: `64px`.
  - **Zone 2: Left Passage Panel (Cột hiển thị bài đọc bên trái)**
    - Chiếm 50% màn hình desktop, hỗ trợ cuộn dọc độc lập. Cho phép bôi đen văn bản để tra cứu.
  - **Zone 3: Right Question Panel (Cột hiển thị bài tập bên phải)**
    - Chiếm 50% màn hình, chứa các câu hỏi tương tác.
  - **Zone 4: Popup Dictionary Tooltip (Cửa sổ tra từ điển nhanh)**
    - Hiển thị nổi đè lên tại vị trí bôi đen văn bản ở Vùng B.
  - **Zone 5: ZPD AI Feedback Panel (Bảng chat Cá Voi giải thích bên phải)**
    - Trượt mở rộng chiếm 360px bên phải màn hình khi học viên xem trang kết quả.

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh tiến trình đọc (Progress Header)
- **Đặc tả Visual:**
  - Nền: Kính mờ `{colors.glass}` (`rgba(255, 255, 255, 0.7)`), có `backdrop-filter: blur(8px)`.
  - Chiều cao: `nav-height` (64px). Viền dưới mờ `1px solid rgba(155, 93, 224, 0.1)`.
- **Thành phần:**
  - **Thanh tiến trình ngang:** Nằm sát cạnh đỉnh Nav. Cao `6px`. Nền `{colors.light-accent}`. Phần hoàn thành chạy màu dải ngân hà `{gradients.galactic-glow}` thể hiện tỷ lệ hoàn thành (ví dụ: *"Câu hỏi 3 / 8"*).
  - **Nút thoát bài học (Exit Button):** Icon Lucide `x` màu `{colors.text-secondary}`. Click để thoát về Unit Detail Page.

### 4.2 Cột hiển thị bài đọc bên trái (Left Passage Panel - Vùng B)
Nội dung thay đổi theo 2 chế độ luyện đọc:

#### CHẾ ĐỘ 1: READING COMPREHENSION (ĐỌC HIỂU THÔNG THƯỜNG)
- **Đặc tả Visual:**
  - Nền: `{colors.surface}` (`#FFFFFF`). Bo góc: `{rounded.xl}` (24px). Viền mờ `1px solid rgba(155, 93, 224, 0.1)`. Padding: `{spacing.lg}` (24px). Có thanh cuộn dọc.
  - Văn bản: Font chữ `{typography.body-md}` (Inter, 16px, line-height 1.6), màu `{colors.text-primary}` để tránh mỏi mắt.
  - Độ dài bài đọc: Basic 500 từ, Intermediate 1500 từ (theo `level_built.md`).
- **Tương tác tra từ:** Học viên bôi đen hoặc double-click vào một từ/cụm từ mới để mở Popup tra từ điển nhanh. Các từ đã lưu vào SRS sẽ được highlight màu hồng nhạt `{colors.light-accent}` trong văn bản để biểu thị trạng thái đã lưu.

#### CHẾ ĐỘ 2: NEWS-BASED LEARNING (ĐỌC BÁO CHÍ THỰC TẾ - DÀNH CHO ADVANCED)
- **Bài báo gốc tự động lọc từ nhiễu (Filtered News Article):** 
  - Hệ thống tự động làm mờ nhẹ hoặc thay thế các từ vựng quá phức tạp ngoài cấp độ học (nhiễu) bằng từ đồng nghĩa tương ứng.
  - Hình ảnh minh họa 3D Claymation phong cách DiveVerse được nhúng ở đầu bài viết.
- **Tra cứu từ học thuật nâng cao:** Hỗ trợ bôi đen tra cứu các cụm Collocations/Idioms học thuật lớn.

### 4.3 Cột hiển thị bài tập bên phải (Right Question Panel - Vùng C)
- **Đặc tả Visual:**
  - Nền: `{colors.surface}` (`#FFFFFF`). Bo góc: `{rounded.xl}` (24px).
  - Viền mờ, padding `{spacing.lg}`. Có thanh cuộn dọc độc lập.
- **Nội dung bài tập:**
  - Chứa danh sách câu hỏi trắc nghiệm A, B, C, D hoặc điền khuyết dựa trên nội dung bài đọc.
  - Các ô trắc nghiệm có touch target tối thiểu `44px` (`button-min-height`). Chọn đáp án đổi viền sang màu `{colors.primary}`.

### 4.4 Cửa sổ tra từ điển nhanh (Popup Dictionary Tooltip - Vùng D)
- **Đặc tả Visual:**
  - Nền: Kính mờ `{colors.glass}`, bo góc `{rounded.md}` (12px), viền mảnh `1px solid rgba(155, 93, 224, 0.2)`. Padding: `{spacing.md}` (16px).
- **Nội dung:**
  - Tiêu đề: Từ vựng và phiên âm IPA (ví dụ: *"Fascinating /ˈfæs.ən.eɪ.tɪŋ/"*).
  - Nghĩa ngắn: *"Hấp dẫn, lôi cuốn"*.
  - **Nút "Lưu vào SRS":** Nút nhỏ nền `{colors.primary}`, chữ trắng, bo góc `{rounded.lg}`. Click để đưa từ vào SRS cá nhân.

### 4.5 Bảng kết quả & Hỏi AI (Reading Result Showcase - Zone 5)
Xuất hiện ở cột phải sau khi nộp bài:
- **Bảng tổng hợp kết quả (Reading Result Table):**
  - Chấm điểm tự động, hiển thị số câu đúng/sai. Câu trả lời đúng của học viên bôi màu xanh `{colors.success}`, câu sai bôi đỏ `{colors.error}` kèm đáp án đúng chính thức và lời giải thích chi tiết của Admin.
- **Khung chat Người bạn Cá Voi (Cá Voi Thông Thái Side Chat Panel):**
  - Trượt ra từ lề phải màn hình. Đặc tả Visual: Nền kính mờ `{colors.glass}`, bo góc `{rounded.xl}` (24px), hiệu ứng `{elevation.glass}`.
  - Trợ lý Cá Voi Xanh [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`64px`) hiển thị bong bóng chat hỗ trợ giải đáp từ vựng/ngữ pháp xuất hiện trong bài đọc. Học viên gõ câu hỏi vào ô input cao `44px` ở dưới cùng panel.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Bôi đen một từ mới trong bài đọc để tra cứu**
  - Học viên bôi đen từ "fascinating" ở Vùng B $\rightarrow$ Popup Dictionary Tooltip Vùng D tự động hiển thị nổi $\rightarrow$ Học viên xem nghĩa $\rightarrow$ Click nút "Lưu từ" $\rightarrow$ Từ được đưa vào SRS $\rightarrow$ Popup đóng lại khi click ra ngoài.
- **Hành động: Click nộp bài đọc ở Vùng D**
  - Học viên hoàn thành tất cả câu hỏi $\rightarrow$ Click "Nộp bài" $\rightarrow$ Hệ thống chấm điểm $\rightarrow$ Chuyển Vùng C sang hiển thị trang kết quả chi tiết $\rightarrow$ Toast thông báo thành công xanh lá $\rightarrow$ Cá Voi Thông Thái Chat Panel mở rộng ở Vùng E.
  - **Dữ liệu API:** `POST /api/reading/evaluate`
    - Payload: `{ "userId": 105, "lessonId": 26, "answers": { "q1": "A", "q2": "collaborate" } }`
    - Response: `{ "score": 90, "correctCount": 9, "totalCount": 10, "details": { "q1": { "isCorrect": true, "correctAnswer": "A", "explanation": "..." } } }`

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT
- **Trạng thái tải (Loading state):** Vùng B và Vùng C hiển thị các khối xám nhấp nháy skeleton.
- **Trạng thái lỗi mạng:** Hiển thị text cảnh báo đỏ `{colors.error}`: *"Lỗi tải bài đọc. Vui lòng nhấn nút thử lại!"*.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [unit_detail_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/unit_detail_page.md).
- **Đi đến:** [unit_detail_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/unit_detail_page.md) (khi click "Hoàn thành bài đọc").

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Đảm bảo tỉ lệ chia đôi 50/50 ở desktop giúp đối chiếu văn bản trực quan. Sử dụng tệp ảnh gốc [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) làm logo ghim cố định ở đầu thanh Nav.
- **KHÔNG ĐƯỢC:** Sử dụng bóng đổ đen thô ráp bên dưới popup từ điển. Popup từ điển nhanh được thiết kế bo tròn nhẹ `{rounded.md}` (12px) trên nền kính mờ, không dùng bóng đổ đen thô ráp mà chỉ có viền hairline tinh tế.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Thông tin bài học (Lesson Header):** Liên kết với `lessons.unit_1[4]` (các trường `{name}`).
- **Đoạn văn đọc & Từ điển tra nhanh (Passage View):** `{lessons.unit_1[4].exercises.passage}` (tiêu đề, nội dung bài đọc và các chú thích giải nghĩa từ vựng).
- **Bộ câu hỏi đọc hiểu (Reading Quiz):** `{lessons.unit_1[4].exercises.comprehensionQuiz}` (danh sách câu hỏi đọc hiểu trắc nghiệm).
