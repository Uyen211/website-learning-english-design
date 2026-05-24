# MÀN HÌNH: UNIT DETAIL PAGE (MÀN HÌNH CHI TIẾT UNIT, DANH SÁCH BÀI HỌC)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Unit Detail Page (Màn hình chi tiết Unit, danh sách bài học)
- **Mã use case liên quan:** UC-05a, UC-05b, UC-06a, UC-06b, UC-06c, UC-06d, UC-07
- **Mã luồng người dùng liên quan:** LN-FL-02, LN-FL-03, LN-FL-04, LN-FL-05 (Màn hình điều phối bài học của từng Unit)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Dashboard $\rightarrow$ Click Unit $\rightarrow$ Unit Detail Page (URL: `/units/{unit_id}`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Người học sử dụng màn hình này để quản lý và truy cập các bài học thành phần trong một Unit (bao gồm 6 bài học kỹ năng: Từ vựng, Ngữ pháp, Nghe, Nói, Đọc, Viết) và thực hiện Bài thi cuối Unit (Mini-exam) sau khi đã tích lũy đủ điều kiện kiến thức.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục danh sách một cột căn giữa (Centered Single Column Layout) rộng tối đa `960px` để người học tập trung cao độ, không bị xao nhãng.
- **Màu nền chung:** Nền trang sử dụng `{colors.canvas}` (`#F9F7FE`) với họa tiết sao mờ tinh tế.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Top Bar (Thanh điều hướng cố định)**
    - Chiều cao: `nav-height` (64px). Ghim cố định đầu trang. Chứa logo cá voi chính và avatar người dùng.
  - **Zone 2: Unit Banner (Banner tiêu đề Unit)**
    - Một thẻ Card lớn nằm ngang trên cùng, chứa tên chủ đề Unit, thanh dẫn đường (Breadcrumbs) và tiến độ tổng của Unit.
  - **Zone 3: Lesson Cards List (Danh sách bài học kỹ năng)**
    - Dàn trang xếp dọc gồm 6 thẻ bài học, ngăn cách nhau bởi khoảng cách `{spacing.md}` (16px).
  - **Zone 4: Mini-Exam Block (Khối bài kiểm tra kết khóa)**
    - Nằm ở cuối danh sách bài học, hiển thị rõ ràng trạng thái Khóa/Mở khóa dựa trên tiến độ học tập.

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh điều hướng đầu trang (Learner Top Nav)
- **Đặc tả Visual:**
  - Nền: Kính mờ `{colors.glass}` (`rgba(255, 255, 255, 0.7)`), có thuộc tính `backdrop-filter: blur(8px)`.
  - Chiều cao: `nav-height` (64px). Viền dưới mờ `1px solid rgba(155, 93, 224, 0.1)`.
- **Các phần tử:**
  - **Logo DiveVerse:** Sử dụng ảnh cá voi chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) kích thước `36px x 36px` căn lề trái kết hợp chữ "DiveVerse" dạng `{typography.title-lg}`.
  - **Avatar người dùng:** Dạng tròn `{rounded.full}` đường kính `36px`.

### 4.2 Banner tiêu đề Unit (Unit Banner Card)
- **Đặc tả Visual:**
  - Nền: Dải màu mượt mà `{gradients.morning-nebula}` (`linear-gradient(135deg, #FDCFFA 0%, #D78FEE 50%, #9B5DE0 100%)`).
  - Bo góc: `{rounded.xxl}` (32px).
  - Hiệu ứng: `{elevation.active-glow}`. Padding: `{spacing.xl}` (32px).
- **Các phần tử bên trong:**
  - **Thanh dẫn Breadcrumbs:** Dạng chữ `{typography.caption}` (12px), màu `{colors.text-primary}`. Hiển thị: *"Lộ trình học / Unit 2: Đời sống công sở"*.
  - **Tiêu đề Unit:** Dạng chữ `{typography.display-sm}` (Manrope, 28px, weight 700). Màu `{colors.text-primary}`.
  - **Mô tả ngắn:** Dạng chữ `{typography.body-md}`. Nội dung: *"Chủ đề từ vựng văn phòng, collocation công sở và ngữ pháp câu điều kiện loại 1."*
  - **Thanh tiến độ Unit (Progress Bar):** Cao 8px. Nền `{colors.surface}` (`rgba(255, 255, 255, 0.4)`), phần hoàn thành dùng màu `{colors.primary}` (`#4E56C0`) để tạo sự tương phản mạnh mẽ.
  - **Mascot Hướng dẫn viên:** Đặt một icon Cá Voi phụ dùng ảnh [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) kích thước `64px x 64px` lơ lửng ở góc phải Banner, đóng vai trò như người đồng hành hướng dẫn bài học cho học viên.

### 4.3 Các thẻ bài học kỹ năng (Lesson Cards - Mapped to UC-05/UC-06)
- **Đặc tả Visual chung của mỗi thẻ:**
  - Nền: `{colors.surface}` (`#FFFFFF`). Bo góc: `{rounded.xl}` (24px). Viền: `1px solid rgba(155, 93, 224, 0.1)`.
  - Hiệu ứng: Soft glow `{elevation.glow}`. Padding: `{spacing.lg}` (24px).
- **Nội dung và Luồng đi chi tiết của từng thẻ bài học:**
  - **Thẻ 1: Bài học Từ vựng nền tảng (UC-05a)**
    - Icon kỹ năng: Lucide `sparkles` màu `{colors.secondary}`.
    - Tiêu đề: *"Từ vựng: Workplace Collocations"*
    - Trạng thái nút:
      - *Chưa học:* Nút *"Bắt đầu"* (`button-primary` style) $\rightarrow$ Dẫn vào [vocabulary_learning_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/vocabulary_learning_page.md) để học 6 giai đoạn (Contextual Guessing -> Flashcards -> Dictation -> ZPD AI Feedback).
      - *Đang học:* Nút *"Tiếp tục"* (Hiển thị mốc tiến độ ví dụ: *"Đang ở bước 3/6"*).
      - *Hoàn thành:* Icon check xanh lá `{colors.success}` + Nút *"Luyện tập lại"* (`button-secondary` style).
  - **Thẻ 2: Bài học Ngữ pháp quy nạp (UC-05b)**
    - Icon kỹ năng: Lucide `book-open`.
    - Tiêu đề: *"Ngữ pháp: Câu điều kiện loại 1"*
    - Trạng thái nút: Bắt đầu / Tiếp tục / Luyện tập lại $\rightarrow$ Dẫn vào [grammar_learning_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/grammar_learning_page.md) học qua tình huống quy nạp (Situational Identification -> Pattern Recognition -> Rule Extraction -> Focus Mode -> Chunk Dictation -> Production).
  - **Thẻ 3: Bài luyện Nghe (UC-06a)**
    - Icon kỹ năng: Lucide `headphones`.
    - Tiêu đề: *"Luyện nghe: Office Gossip (Interactive Story)"*
    - Trạng thái nút: Bắt đầu / Luyện tập lại $\rightarrow$ Dẫn vào phòng luyện nghe tích hợp (Interactive Story đoạn ngắn hoặc Shadowing ghi âm nói đuổi khớp âm).
  - **Thẻ 4: Bài luyện Nói (UC-06b)**
    - Icon kỹ năng: Lucide `mic`.
    - Tiêu đề: *"Luyện nói: Phỏng vấn xin việc (AI Role-play)"*
    - Trạng thái nút: Bắt đầu / Luyện tập lại $\rightarrow$ Dẫn vào màn hình luyện nói ASR phát âm hoặc đàm thoại giả lập với giám khảo AI tối thiểu 4 lượt thoại.
  - **Thẻ 5: Bài luyện Đọc (UC-06c)**
    - Icon kỹ năng: Lucide `file-text`.
    - Tiêu đề: *"Luyện đọc: Đọc email công việc"*
    - Trạng thái nút: Bắt đầu / Luyện tập lại $\rightarrow$ Dẫn vào màn hình đọc hiểu thông thường hoặc đọc báo thực tế (News-based) tra từ tại chỗ.
  - **Thẻ 6: Bài luyện Viết (UC-06d)**
    - Icon kỹ năng: Lucide `pen-tool`.
    - Tiêu đề: *"Luyện viết: Phản hồi Email khách hàng (Scaffolded ZPD)"*
    - Trạng thái nút: Bắt đầu / Luyện tập lại $\rightarrow$ Dẫn vào khung viết gợi ý 3 vòng (loại lỗi -> cấu trúc viết lại -> giải thích chi tiết) hoặc chấm luận AI theo 4 tiêu chí quốc tế.

### 4.4 Khối bài kiểm tra kết khóa (Mini-Exam Card - UC-07)
- **Đặc tả Visual:**
  - Nền: `{colors.surface}`. Bo góc `{rounded.xxl}` (32px). Padding: `{spacing.xl}` (32px).
- **Trạng thái cấu hình (theo UC-07):**
  - **Trạng thái Khóa (Mặc định khi chưa học xong cả 6 bài kỹ năng):**
    - Độ đục (Opacity) toàn thẻ giảm xuống `60%`.
    - Ở giữa hiển thị icon ổ khóa mờ (icon `lock`).
    - Banner cảnh báo: *"Vui lòng hoàn thành đầy đủ 6 bài học kỹ năng phía trên để mở khóa bài kiểm tra này!"*.
    - Các nút thiết lập và nút bấm CTA *"Luyện thi ngay"* bị vô hiệu hóa (`disabled`).
  - **Trạng thái Mở khóa (Khi hoàn thành toàn bộ 6 bài học):**
    - Thẻ bừng sáng, viền đổi sang dải gradient `{gradients.galactic-glow}` và tỏa quầng sáng `{elevation.active-glow}`.
    - **Mascot cổ vũ:** Xuất hiện một biểu tượng chú Cá Voi chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) kích thước `48px x 48px` đính kèm các hạt sao phát sáng lấp lánh để thu hút học viên vào làm bài.
    - **Cấu hình lựa chọn chế độ làm bài (UC-07):**
      - Hiển thị 2 ô chọn (Radio Buttons) hoặc Tab Toggle:
        - **Chế độ Tập dượt:** Không giới hạn thời gian làm bài, cho phép xem lời giải thích chi tiết của Admin ngay lập tức.
        - **Chế độ Thi thật:** Bắt đầu đếm ngược thời gian nghiêm ngặt, tự động khóa câu trả lời khi hết giờ.
      - Hiển thị cấu trúc đề thi: *"Số lượng: 30 câu hỏi | Thời gian: 45 phút | Kỹ năng tích hợp: Từ vựng, Ngữ pháp, Nghe, Đọc"*.
    - **Nút CTA hành động ("Bắt đầu thi"):** Kích hoạt ở trạng thái `button-primary` với màu `{colors.primary}`, có hover glow mạnh. Dẫn chuyển tiếp đến [pre_test_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/pre_test_page.md).

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Click vào nút Bắt đầu / Tiếp tục / Luyện tập lại trên thẻ bài học**
  - Chuyển hướng mượt mà (Fade Out/Fade In trong `0.3s`) đến trang học tập kỹ năng tương ứng (ví dụ: [vocabulary_learning_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/vocabulary_learning_page.md)).
- **Hành động: Click vào nút Bắt đầu thi (khi đã mở khóa)**
  - Hệ thống ghi nhận chế độ làm bài được chọn ("Tập dượt" hoặc "Thi thật").
  - Chuyển hướng đến màn hình chuẩn bị thi: [pre_test_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/pre_test_page.md).

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT
- **Trạng thái tải (Loading state):** Toàn bộ danh sách thẻ hiển thị Skeleton Loader màu tím mờ, có hiệu ứng xung nhịp quét sáng mịn.
- **Trạng thái hiển thị Responsive:**
  - **Mobile:** Thẻ bài học chuyển từ cấu trúc hàng ngang (2 cột trái-phải) sang xếp dọc 1 cột (Tiêu đề trên, Nút CTA dưới rộng 100%).

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [learner_dashboard.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/learner_dashboard.md).
- **Đi đến:** Các trang bài học kỹ năng cụ thể (`vocabulary_learning_page.md`, v.v.) và [pre_test_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/pre_test_page.md).

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Sử dụng tệp ảnh gốc [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) cho logo thanh Nav ghim cố định và các icon Mascot hướng dẫn trong Banner để đảm bảo tính nhất quán của hệ thống DiveVerse.
- **KHÔNG ĐƯỢC:** Thiết kế các nút bấm có touch target nhỏ hơn `44px`. Đảm bảo các thẻ bài học có khoảng cách thở rộng rãi, tuân thủ nghiêm ngặt hệ thống Spacing.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Thông tin chi tiết Unit (Unit Info Header):** Ánh xạ từ `levels[0].units[0]` (đối với Unit 1), bao gồm các trường `{sequence}`, `{name}`, `{theme}`, `{vocabularyTopic}`, `{grammarTopic}`, `{targetSkill}`.
- **Danh sách bài học của Unit (Lessons List Grid):** Liên kết với mảng `lessons.unit_1` (các trường `{id}`, `{category}`, `{name}`, `{status}`).
