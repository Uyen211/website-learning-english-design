# MÀN HÌNH: GRAMMAR LEARNING PAGE (MÀN HÌNH HỌC NGỮ PHÁP 7 CHẶNG)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Grammar Learning Page (Màn hình học ngữ pháp 7 chặng)
- **Mã use case liên quan:** UC-05b (Học ngữ pháp quy nạp)
- **Mã luồng người dùng liên quan:** LN-FL-02 (Khám phá Ngữ pháp)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Dashboard $\rightarrow$ Click Unit $\rightarrow$ Unit Detail $\rightarrow$ Click bài học Ngữ pháp (URL: `/units/{unit_id}/lessons/{lesson_id}/grammar`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên trải qua lộ trình học ngữ pháp quy nạp (inductive grammar) tự nhiên gồm 7 chặng khép kín. Hành trình giúp người học tự đúc rút quy tắc từ tình huống thực tế, xây dựng Mental Model về cấu trúc qua các bài tập tương tác, tự đặt câu cá nhân hóa dưới sự hỗ trợ của trợ lý AI và lưu trữ cấu trúc vào Spaced Repetition (SRS - UC-08).

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục thẻ căn giữa linh hoạt (Centered Card Layout). Trong các chặng 1-5, màn hình hiển thị Central Card duy nhất. Ở chặng 6 (Viết câu), màn hình mở rộng sang bố cục 2 cột (Tỉ lệ 7:5 trên Desktop) để hiển thị thêm Bảng Phản hồi AI ở bên phải.
- **Màu nền chung:** Nền trang sử dụng `{colors.canvas}` (`#F9F7FE`) phối dải chuyển màu mờ `{gradients.atmosphere-haze}`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Progress Header (Thanh tiến độ bài học)**
    - Ghim cố định ở sát mép trên. Chiều cao: `64px`. Chứa thanh tiến độ ngang và nút thoát.
  - **Zone 2: Central Card (Thẻ học tập trung tâm)**
    - Kích thước: `760px x 500px` (Rộng hơn trang từ vựng một chút để chứa các câu văn dài). Căn giữa hoàn hảo bằng Flexbox.
  - **Zone 3: ZPD AI Feedback Panel (Bảng phản hồi Cá Voi bên phải)**
    - Rộng `360px`, ghim sát lề phải Vùng B. Trượt mở mượt mà từ phải sang khi học viên nộp câu viết ở chặng 6.
  - **Zone 4: Footer Toolbar (Thanh hành động chân trang)**
    - Nằm ở sát mép dưới Central Card, chứa các nút điều hướng chuyển chặng.

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh điều hướng & Tiến độ bài học (Progress Header)
- **Đặc tả Visual:**
  - Nền: Kính mờ `{colors.glass}` (`rgba(255, 255, 255, 0.7)`), có `backdrop-filter: blur(8px)`.
  - Viền dưới mờ `1px solid rgba(155, 93, 224, 0.1)`. Chiều cao: `64px`.
- **Thành phần:**
  - **Logo & Breadcrumbs:** Logo cá voi chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`36px`) kèm dòng text `{typography.caption}`: *"Unit 2 / Lesson 2 / Học Ngữ pháp"*.
  - **Thanh tiến độ ngang:** Nằm cố định viền sát mép trên thanh Nav. Cao `6px`. Nền `{colors.light-accent}`. Phần hoàn thành chạy màu dải ngân hà `{gradients.galactic-glow}` thể hiện tỷ số (ví dụ: *"Chặng 3 / 7"*).
  - **Nút thoát bài học (Exit Button):** Icon Lucide `x` màu `{colors.text-secondary}`, touch target `44px`. Click vào mở popup xác thực dừng học.

### 4.2 Thẻ học tập trung tâm (Central Card)
- **Đặc tả Visual:**
  - Nền: `{colors.surface}` (`#FFFFFF`). Bo góc: `{rounded.xl}` (24px).
  - Viền: `1px solid rgba(155, 93, 224, 0.1)`.
  - Hiệu ứng nâng: `{elevation.glow}` (Soft glow tím).
  - Padding bên trong: `{spacing.xl}` (32px).
- **Nội dung thay đổi theo 7 chặng học tập (Mapped to UC-05b):**

#### CHẶNG 1: NHẬN DIỆN TÌNH HUỐNG (SITUATIONAL IDENTIFICATION)
- **Phương tiện ngữ cảnh:** Hiển thị video ngắn, hình ảnh minh họa 3D Clay, hoặc mẩu hội thoại ngắn chứa cấu trúc ngữ pháp mục tiêu (ví dụ: cấu trúc câu điều kiện loại 1). *Tuyệt đối không hiển thị tên cấu trúc hay công thức ở chặng này.*
- **Câu hỏi nhận diện:** Một câu hỏi trắc nghiệm khách quan dạng `{typography.body-md}` yêu cầu người học nhận xét trạng thái tình huống đang diễn ra trong ngữ cảnh.
- **Nút hành động:** Nút các lựa chọn đáp án (`button-secondary` style), click chọn đáp án đúng để mở nút *"Tiếp tục"* sang Chặng 2.

#### CHẶNG 2: NHẬN DIỆN KHUÔN MẪU (PATTERN RECOGNITION)
- **Khối ví dụ song song:** Hiển thị 3 câu ví dụ thực tế có cấu trúc ngữ pháp tương tự nhau (ví dụ: 3 câu điều kiện loại 1 khác nhau về từ vựng nhưng đồng điệu cấu trúc).
- **Yêu cầu đúc rút:** Hệ thống yêu cầu học viên tích chọn điểm chung về mặt hình thức giữa 3 câu (ví dụ: phát hiện sự xuất hiện của từ *"If"*, động từ chia ở hiện tại đơn ở vế 1, và *"will"* ở vế 2).

#### CHẶNG 3: ĐÚC RÚT QUY TẮC (RULE EXTRACTION)
- **Cặp câu tương phản (Contrastive Pairs):** Hiển thị cặp câu có sự khác biệt nhỏ về mặt ngữ pháp để làm nổi bật sự khác biệt về sắc thái ý nghĩa (ví dụ: vế dùng *will* so với vế dùng *going to*).
- **Bảng đúc rút quy tắc chính thức:** Hiển thị công thức ngữ pháp dạng trực quan hóa đồ họa, đặt tên cấu trúc và giới thiệu các cấu trúc câu hạt nhân (Grammar Chunks) thường dùng.
- **Mascot hướng dẫn:** Chú cá voi chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`64px`) xuất hiện giải thích quy luật bằng ngôn từ dễ hiểu, thân thiện.

#### CHẶNG 4: THỰC HÀNH NHẬN DIỆN (ACTIVE PRACTICE - BASIC)
- **Focus Mode / Drag & Drop:**
  - Hệ thống ẩn đi các thành phần phụ trong câu, chỉ hiển thị cấu trúc câu hạt nhân (Subject + Verb + Object).
  - Học viên tương tác kéo thả các từ để xây dựng Mental Model về cấu trúc cho đến khi hoàn thành chính xác.
  - Các ô trạm (nodes) tương tác có bo góc `{rounded.md}` (12px), chọn đúng đổi viền màu xanh `{colors.success}` (`#22C55E`), chọn sai viền đỏ `{colors.error}` (`#EF4444`).

#### CHẶNG 5: THỰC HÀNH NÂNG CAO (ACTIVE PRACTICE - INTERMEDIATE/ADVANCED)
- **Active Identification / Sentence Transformation:**
  - Hiển thị bài tập viết lại câu (Sentence Transformation) dựa trên câu gốc có sẵn, yêu cầu viết lại tương đương cấu trúc.
  - Học viên nhập câu viết lại vào ô nhập liệu `{rounded.lg}` (16px), chiều cao `44px` (`input-height`).

#### CHẶNG 6: CHÍNH TẢ CHUNK (DICTATION - GHI NHỚ ÂM THANH)
- **Giao diện:** 
  - Hệ thống phát âm thanh của một chunk ngữ pháp hạt nhân cố định.
  - Học viên nghe và gõ lại chính xác chunk ngữ pháp vào ô nhập liệu Dictation Input.
  - Trạng thái lỗi (Nếu gõ sai quá 3 lần): Hiển thị đáp án đúng chính thức của Admin kèm lời giải thích, bắt buộc gõ lại đúng để đi tiếp.

#### CHẶNG 7: TỰ VIẾT CÂU & TRỢ LÝ AI (PERSONALIZED OUTPUT & ZPD AI FEEDBACK)
- **Khung viết câu ngữ pháp:** 
  - Khung nhập văn bản (Textarea) nền `{colors.surface}`, bo góc `{rounded.xl}` (24px), viền mờ `1px solid rgba(155, 93, 224, 0.2)`.
  - Hướng dẫn của Admin: *"Hãy tự đặt một câu mới sử dụng cấu trúc ngữ pháp vừa học."* dạng `{typography.body-sm}`.
- **Nút "Nộp câu" (CTA):** Nền `{colors.primary}`, chữ trắng, bo góc `{rounded.lg}` (16px), default `{elevation.active-glow}`.
- **Bảng phản hồi AI (Wise Whale AI Feedback Panel - Vùng Zone 3):**
  - Trượt ra từ lề phải màn hình. Đặc tả Visual: Nền kính mờ `{colors.glass}`, bo góc `{rounded.xl}` (24px), hiệu ứng `{elevation.glass}`.
  - Trợ lý Cá Voi Xanh sử dụng ảnh [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`64px`) ở đỉnh Panel, hiển thị các bong bóng chat hướng dẫn gợi mở 3 vòng:
    - *Vòng 1 (Gợi ý loại lỗi):* AI bôi đỏ `{colors.error}` vị trí lỗi cấu trúc/ngữ pháp và phân loại lỗi.
    - *Vòng 2 (Gợi ý cấu trúc):* AI gợi ý công thức viết lại cho đúng.
    - *Vòng 3 (Đáp án mẫu):* Hiển thị câu gợi ý mẫu khuyết cấu trúc ngữ pháp vừa học để học viên điền nốt.

#### CHẶNG 8 (HOÀN THÀNH): HOÀN THÀNH BÀI HỌC (COMPLETION & EXP / SRS)
- **Khối chúc mừng (Completion Card):**
  - Nền: Dải gradient rực rỡ `{gradients.morning-nebula}`. Bo góc `{rounded.xxl}` (32px).
  - Hiệu ứng: Pulsing phát sáng `{elevation.active-glow}` kèm pháo hoa giấy mờ ảo.
  - Mascot Cá Voi Xanh [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`160px`) nhún nhảy chậm.
- **Nội dung phần thưởng:** Hiển thị badge cộng điểm *"EXP +15"* và thông báo *"Cấu trúc ngữ pháp đã được lưu vào danh sách SRS cá nhân!"*.
- **Nút CTA chính:** Nút *"Hoàn thành bài học"* (`button-primary` style) dẫn quay về Unit Detail Page.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Chọn nút "Nộp câu" ở Chặng 7**
  - **Luồng:** Nộp câu $\rightarrow$ Nút chuyển loading $\rightarrow$ AI phân tích dữ liệu $\rightarrow$ Bảng AI bên phải trượt mở $\rightarrow$ AI hiển thị lỗi bôi màu đỏ `{colors.error}` hoặc báo thành công màu xanh `{colors.success}`.
  - **Dữ liệu API gửi đi:** `POST /api/learning/grammar/validate-sentence`
    - Payload: `{ "grammar_id": 12, "sentence": "If I will go, I call you." }`
    - Response: `{ "isValid": false, "errors": [{"text": "will go", "type": "tense-error", "correction": "go"}], "suggestions": "In first conditional, the if-clause uses present simple." }`

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
- **Thông tin bài học (Lesson Header):** Liên kết với `lessons.unit_1[1]` (các trường `{name}`, `{category}`).
- **Hành trình ngữ pháp quy nạp 7 chặng (7-Stage Exercises Data):**
  - Chặng 1: Cặp câu tương phản -> `{lessons.unit_1[1].exercises.stage1_contrastivePairs}` (câu A, câu B, giải thích sắc thái).
  - Chặng 2: Kiểm tra khái niệm -> `{lessons.unit_1[1].exercises.stage2_conceptChecking}` (câu hỏi MCQ kiểm tra hiểu nhanh).
  - Chặng 3: Nhận diện khuôn mẫu -> `{lessons.unit_1[1].exercises.stage3_inductionDiscovery}` (câu ví dụ song song để phát hiện cấu trúc).
  - Chặng 4: Công thức hạt nhân -> `{lessons.unit_1[1].exercises.stage4_focusFormula}` (công thức dạng S + Be + N/Adj, phân tích thành phần).
  - Chặng 5: Nhận diện trong ngữ cảnh -> `{lessons.unit_1[1].exercises.stage5_inputProcessing}` (đoạn văn có các ô chọn thả be).
  - Chặng 6: Viết câu có kiểm soát -> `{lessons.unit_1[1].exercises.stage6_controlledProduction}` (câu hỏi dịch, từ gợi ý, đáp án).
  - Chặng 7: Đặt câu cá nhân hóa ZPD -> `{lessons.unit_1[1].exercises.stage7_zpdWritingFeedback}` (yêu cầu đặt câu, phản hồi gợi ý từ AI).
