# MÀN HÌNH: VOCABULARY LEARNING PAGE (MÀN HÌNH HỌC TỪ VỰNG 6 BƯỚC)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Vocabulary Learning Page (Màn hình học từ vựng 6 bước)
- **Mã use case liên quan:** UC-05a (Học từ vựng nền tảng)
- **Mã luồng người dùng liên quan:** LN-FL-02 (Khám phá Từ vựng)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Dashboard $\rightarrow$ Click Unit $\rightarrow$ Unit Detail $\rightarrow$ Click bài học Từ vựng (URL: `/units/{unit_id}/lessons/{lesson_id}/vocabulary`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này để trải qua lộ trình học và tiếp thu từ vựng tự nhiên gồm 6 bước khép kín. Hành trình dẫn dắt người học từ suy đoán ý nghĩa qua ngữ cảnh thực tế đến sản sinh câu cá nhân hóa dưới sự hỗ trợ của trợ lý AI Cá Voi Xanh, cuối cùng lưu trữ từ vựng vào thuật toán lặp lại ngắt quãng (SRS - UC-08).

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục thẻ căn giữa linh hoạt (Centered Card Layout). Khi ở các bước 1-4, màn hình chỉ tập trung vào một Central Card duy nhất. Ở bước 5 (Viết câu), màn hình mở rộng sang bố cục 2 cột (Tỉ lệ 7:5 trên Desktop) để hiển thị thêm Bảng Phản hồi AI ở bên phải.
- **Màu nền chung:** Nền trang sử dụng `{colors.canvas}` (`#F9F7FE`) phối dải chuyển màu mờ `{gradients.atmosphere-haze}`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Progress Header (Thanh tiến độ bài học)**
    - Ghim cố định ở sát mép trên. Chiều cao: `nav-height` (64px). Chứa thanh tiến độ ngang và nút thoát.
  - **Zone 2: Central Card (Thẻ học tập trung tâm)**
    - Kích thước: `720px x 480px`. Căn giữa hoàn hảo bằng Flexbox.
  - **Zone 3: ZPD AI Feedback Panel (Bảng phản hồi Cá Voi bên phải)**
    - Rộng `360px`, ghim sát lề phải Vùng B. Trượt mở mượt mà từ phải sang khi học viên nộp câu viết ở bước 5.
  - **Zone 4: Footer Toolbar (Thanh hành động chân trang)**
    - Nằm ở sát mép dưới Central Card, chứa các nút điều hướng chuyển bước.

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh điều hướng & Tiến độ bài học (Progress Header)
- **Đặc tả Visual:**
  - Nền: Kính mờ `{colors.glass}` (`rgba(255, 255, 255, 0.7)`), có `backdrop-filter: blur(8px)`.
  - Viền dưới mờ `1px solid rgba(155, 93, 224, 0.1)`. Chiều cao: `64px`.
- **Thành phần:**
  - **Logo & Breadcrumbs:** Logo cá voi chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`36px`) kèm dòng text `{typography.caption}`: *"Unit 2 / Lesson 1 / Học Từ vựng"*.
  - **Thanh tiến độ ngang (Progress Bar):** Nằm cố định viền sát mép trên thanh Nav. Cao `6px`. Nền `{colors.light-accent}`. Phần hoàn thành chạy màu dải ngân hà `{gradients.galactic-glow}` thể hiện tỷ số (ví dụ: *"Từ 3 / 10"*).
  - **Nút thoát bài học (Exit Button):** Icon Lucide `x` màu `{colors.text-secondary}`, touch target `44px`. Click vào mở popup xác thực dừng học.

### 4.2 Thẻ học tập trung tâm (Central Card)
- **Đặc tả Visual:**
  - Nền: `{colors.surface}` (`#FFFFFF`). Bo góc: `{rounded.xl}` (24px).
  - Viền: `1px solid rgba(155, 93, 224, 0.1)`.
  - Hiệu ứng nâng: `{elevation.glow}` (Soft glow tím).
  - Padding bên trong: `{spacing.xl}` (32px).
- **Nội dung thay đổi theo 6 bước học tập:**

#### BƯỚC 1: LÀM QUEN NGỮ CẢNH (CONTEXTUAL GUESSING)
- **Hộp phát âm thanh (Audio Player Button):** Nút tròn `{rounded.full}` màu `{colors.primary}` (`#4E56C0`) đính icon Lucide `volume-2` màu trắng. Click để phát âm thanh từ mục tiêu (accent bản xứ chuẩn).
- **Vùng hiển thị câu ví dụ:** Hiển thị 3 câu ví dụ thực tế chứa từ mục tiêu. Từ mục tiêu được tô màu đậm `{colors.primary}` dạng `{typography.title-md}`.
- **Nút hành động:** Nút chính *"Xem nghĩa"* (`button-primary` style, default `{elevation.active-glow}`). Click để chuyển sang Bước 2.

#### BƯỚC 2: XEM NGHĨA CHI TIẾT (VOCABULARY DETAIL)
- **Tên từ mục tiêu:** Dạng chữ `{typography.display-sm}` (Manrope, 28px, weight 700) màu `{colors.text-primary}`.
- **Phiên âm IPA:** Kế bên từ mục tiêu, màu `{colors.text-secondary}` dùng `{typography.body-md}` (ví dụ: `/ˌcɑːn.sə.dẽɪ.ʃən/`).
- **Khối định nghĩa:** Một thẻ Card nhỏ, nền `{colors.canvas}`, bo góc `{rounded.lg}` (16px), hiển thị nghĩa tiếng Việt/tiếng Anh, sắc thái từ (Register/Nuance).
- **Bảng Collocations:** Danh sách các từ phối hợp đi kèm được gạch đầu dòng rõ ràng.
- **Mascot hướng dẫn:** Biểu tượng chú cá voi chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`48px x 48px`) xuất hiện ở góc phải Card định nghĩa kèm bóng thoại động viên.

#### BƯỚC 3: THỰC HÀNH NHẬN DIỆN (ACTIVE PRACTICE - BASIC & ADVANCED)
- **Hình thức 1 (Basic - Flashcards & Matching):**
  - Hiển thị các ô thẻ kéo ghép đôi từ vựng với hình ảnh/định nghĩa hoặc thẻ Flashcard lật mặt.
  - Các ô trạm (nodes) tương tác có bo góc `{rounded.md}` (12px), khi chọn đúng đổi viền màu xanh `{colors.success}` (`#22C55E`), chọn sai viền đỏ `{colors.error}` (`#EF4444`).
- **Hình thức 2 (Advanced - Smart Concordance & AI Next-Word Prediction):**
  - Hiển thị câu ngữ cảnh mới khuyết cụm từ collocation mục tiêu.
  - Ô nhập liệu văn bản `{rounded.lg}`, chiều cao `44px`. Học viên phải điền từ/cụm từ thích hợp nhất.

#### BƯỚC 4: NGHE GÕ LẠI CHÍNH TẢ (DICTATION - GHEN NHỚ ÂM THANH)
- **Giao diện:** 
  - Nút phát loa trung tâm lớn. Hệ thống phát tự động âm thanh của từ mục tiêu.
  - Ô nhập chữ chính tả (Dictation Input Box) ở ngay dưới: Căn giữa, cỡ chữ lớn `{typography.title-lg}`, bo góc `{rounded.lg}` (16px).
  - Trạng thái lỗi (Nếu gõ sai): Hộp nhập báo đỏ viền `{colors.error}` kèm âm thanh báo lỗi nhẹ. Lần sai thứ 3: Hiển thị đáp án đúng chính thức của Admin, bắt buộc gõ lại đúng 1 lần để hoàn thành.

#### BƯỚC 5: TỰ VIẾT CÂU & TRỢ LÝ AI (PERSONALIZED PRODUCTION & ZPD AI FEEDBACK)
- **Khung đặt câu cá nhân hóa:** 
  - Khung nhập văn bản lớn (Textarea) nền `{colors.surface}`, bo góc `{rounded.xl}` (24px), viền mờ `1px solid rgba(155, 93, 224, 0.2)`.
  - Hướng dẫn của Admin: *"Hãy tự đặt một câu mới sử dụng từ vựng đã học bám sát bối cảnh đời sống thực tế của bạn."* dạng `{typography.body-sm}`.
- **Nút "Nộp câu" (CTA):** Nền `{colors.primary}`, chữ trắng, bo góc `{rounded.lg}` (16px), default `{elevation.active-glow}`.
- **Bảng phản hồi AI (Wise Whale AI Feedback Panel - Vùng Zone 3):**
  - Trượt ra từ lề phải màn hình. Đặc tả Visual: Nền kính mờ `{colors.glass}`, bo góc `{rounded.xl}` (24px), hiệu ứng `{elevation.glass}`.
  - Trợ lý Cá Voi Xanh sử dụng ảnh [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`64px`) ở đỉnh Panel, hiển thị các bong bóng chat hướng dẫn gợi mở 3 vòng:
    - *Vòng 1 (Gợi ý loại lỗi):* AI bôi đỏ `{colors.error}` vị trí lỗi chính tả/từ loại trong câu của học viên và phân loại lỗi.
    - *Vòng 2 (Gợi ý cấu trúc):* AI đưa ra cấu trúc ngữ pháp gợi ý để viết lại cho đúng ngữ cảnh.
    - *Vòng 3 (Đáp án mẫu):* Hiển thị câu gợi ý mẫu khuyết từ mục tiêu do Admin thiết lập để học viên điền nốt.

#### BƯỚC 6: HOÀN THÀNH BÀI HỌC (COMPLETION & EXP / SRS)
- **Khối chúc mừng (Completion Card):**
  - Nền: Dải gradient rực rỡ `{gradients.morning-nebula}`. Bo góc `{rounded.xxl}` (32px).
  - Hiệu ứng: Pulsing phát sáng `{elevation.active-glow}` kèm hiệu ứng pháo hoa giấy bay mờ ảo.
  - Mascot Cá Voi Xanh [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`160px`) nhún nhảy chậm chúc mừng.
- **Nội dung phần thưởng:** Hiển thịbadge cộng điểm *"EXP +15"* và thông báo *"Từ vựng đã được lưu vào Spaced Repetition (SRS) để ôn tập tiếp theo!"* dạng `{typography.title-md}`.
- **Nút CTA chính:** Nút *"Hoàn thành bài học"* (`button-primary` style) dẫn quay về Unit Detail Page.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Chọn nút "Nộp câu" ở Bước 5**
  - **Luồng:** Nộp câu $\rightarrow$ Nút chuyển loading $\rightarrow$ AI phân tích dữ liệu $\rightarrow$ Bảng AI bên phải trượt mở $\rightarrow$ AI hiển thị lỗi bôi màu đỏ `{colors.error}` hoặc báo thành công màu xanh `{colors.success}`.
  - **Dữ liệu API gửi đi:** `POST /api/learning/vocabulary/validate-sentence`
    - Payload: `{ "word": "consolidate", "sentence": "I want to consolidate my knowledge." }`
    - Response: `{ "isValid": true, "score": 95, "feedback": "Excellent sentence!" }`

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT
- **Trạng thái tải (Loading state):** Hiển thị loading spinner trên nút CTA, các trường nhập liệu tạm thời bị khóa.
- **Trạng thái lỗi (Error state):** Các trường nhập sai hoặc gõ sai chính tả viền đỏ `{colors.error}`.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [unit_detail_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/unit_detail_page.md)
- **Đi đến:** [unit_detail_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/unit_detail_page.md) (sau khi hoàn thành).

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Thiết kế các chuyển động trượt mở (slide-in) của AI Panel cực kỳ mượt mà (`0.3s` `ease-in-out`). Đảm bảo toàn bộ touch target trên di động tối thiểu là `44px`.
- **KHÔNG ĐƯỢC:** Sử dụng màu sắc bên ngoài bộ quy chuẩn tokens. Bóng đổ đen vật lý bị cấm tuyệt đối, chỉ dùng glow màu theo quy chuẩn.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Thông tin bài học (Lesson Header):** Liên kết với `lessons.unit_1[0]` (các trường `{name}`, `{category}`).
- **Luồng bài tập từ vựng 6 bước (6-Step Exercises Data):**
  - Bước 1: Làm quen bối cảnh -> `{lessons.unit_1[0].exercises.step1_contextualGuessing}` (từ mục tiêu, âm thanh, câu bối cảnh).
  - Bước 2: Flashcard học sâu -> `{lessons.unit_1[0].exercises.step2_flashcard}` (phiên âm, định nghĩa, ảnh minh họa, collocation).
  - Bước 3: Trắc nghiệm nhanh -> `{lessons.unit_1[0].exercises.step3_multipleChoice}` (câu hỏi trắc nghiệm đồng nghĩa).
  - Bước 4: Viết chính tả -> `{lessons.unit_1[0].exercises.step4_dictation}` (âm thanh nghe, từ đáp án chính xác).
  - Bước 5: Luyện phát âm -> `{lessons.unit_1[0].exercises.step5_asrPronunciation}` (câu mẫu phát âm, IPA, danh sách âm vị).
  - Bước 6: Đặt câu cá nhân hóa -> `{lessons.unit_1[0].exercises.step6_zpdFeedback}` (hướng dẫn viết câu, phản hồi gợi ý 3 vòng từ AI).
