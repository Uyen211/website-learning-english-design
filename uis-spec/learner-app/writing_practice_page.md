# MÀN HÌNH: WRITING PRACTICE PAGE (MÀN HÌNH LUYỆN VIẾT)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Writing Practice Page (Màn hình luyện viết)
- **Mã use case liên quan:** UC-06d (Luyện viết)
- **Mã luồng người dùng liên quan:** Flow LN-FL-03 (Trạm luyện Kỹ năng - Viết)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Dashboard $\rightarrow$ Click Unit $\rightarrow$ Unit Detail $\rightarrow$ Click Luyện Viết (URL: `/units/{unit_id}/lessons/{lesson_id}/writing`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này để nâng cao kỹ năng viết tiếng Anh qua 3 hình thức: Viết câu cơ bản (ghép từ/điền khuyết), Viết ngắn Cá Voi Xanh 3 vòng gợi ý (ZPD), và Viết luận lớn chuẩn hóa quốc tế (IELTS/TOEIC) có AI chấm chữa và phản hồi chi tiết theo 4 tiêu chí.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục cột kép chia tỷ lệ 6:6 (Split Column Layout) cho màn hình viết luận và viết Cá Voi; Bố cục 1 cột căn giữa cho viết câu cơ bản.
- **Màu nền chung:** Nền trang sử dụng `{colors.canvas}` (`#F9F7FE`) phối dải chuyển màu mờ `{gradients.atmosphere-haze}`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Progress Header (Thanh dẫn Breadcrumbs và tiến độ ở đầu trang)**
    - Ghim cố định ở sát mép trên. Chiều cao: `64px`.
  - **Zone 2: Left Prompt Panel (Vùng đề bài và gợi ý bên trái)**
    - Chứa đề bài viết, các gợi ý cấu trúc, hoặc bảng hướng dẫn của Cá Voi Xanh.
  - **Zone 3: Right Editor Panel (Vùng soạn thảo bên phải)**
    - Khung nhập văn bản lớn và bộ đếm từ.
  - **Zone 4: Blank Essay Warning Modal (Hộp thoại báo lỗi bài viết trống)**
    - Một cửa sổ overlay kính mờ nổi đè lên màn hình khi nộp bài viết trống.
  - **Zone 5: AI Writing Evaluation View (Bảng kết quả chấm thi AI)**
    - Thay thế vùng soạn thảo khi nộp bài thành công.

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh tiến trình viết (Progress Header)
- **Đặc tả Visual:**
  - Nền: Kính mờ `{colors.glass}` (`rgba(255, 255, 255, 0.7)`), có `backdrop-filter: blur(8px)`.
  - Chiều cao: `nav-height` (64px). Viền dưới mờ `1px solid rgba(155, 93, 224, 0.1)`.
- **Thành phần:**
  - **Thanh tiến trình ngang:** Nằm sát cạnh đỉnh Nav. Cao `6px`. Nền `{colors.light-accent}`. Phần hoàn thành chạy màu dải ngân hà `{gradients.galactic-glow}` thể hiện tiến độ (ví dụ: *"Bài viết 1 / 2"*).
  - **Nút thoát bài học (Exit Button):** Icon Lucide `x` màu `{colors.text-secondary}`. Click để thoát về Unit Detail Page.

### 4.2 Phân hệ soạn thảo chi tiết (VÙNG B & C)
Nội dung thay đổi theo 3 chế độ luyện viết do Admin cấu hình:

#### CHẾ ĐỘ 1: BASIC WRITING (VIẾT CÂU CƠ BẢN - GHÉP CÂU)
- **Khu vực kéo ghép câu (Word Ordering Interface - Vùng C):**
  - Bố cục 1 cột dọc căn giữa. Nền thẻ `{colors.surface}` (`#FFFFFF`). Bo góc `{rounded.xl}` (24px).
  - Hiển thị các thẻ từ bị xáo trộn (ví dụ: *"will / rains / stay / at / If / home / it / we"*). Học viên kéo thả sắp xếp lại thành câu hoàn chỉnh: *"If it rains, we will stay at home."*.
  - Các thẻ từ có bo góc `{rounded.md}` (12px) dễ gắp kéo.

#### CHẾ ĐỘ 2: SCAFFOLDED WRITING (VIẾT GỢI Ý 3 VÒNG ZPD - CÁ VOI XANH)
- **Đề viết ngắn & Khung cấu trúc (Vùng B - cột trái):**
  - Nền thẻ `{colors.surface}`, padding `{spacing.lg}`.
  - Hiển thị đề bài viết ngắn (ví dụ: *"Viết câu trả lời email xin nghỉ phép"*) kèm theo các gợi ý cấu trúc đích cần sử dụng.
- **Khung Cá Voi gợi ý 3 vòng (3-Tier Hint Box - Vùng B):**
  - Xuất hiện động ngay dưới đề bài khi học viên nộp bài viết bị lỗi.
  - Nền kính mờ `{colors.glass}`, bo góc `{rounded.xl}` (24px), hiệu ứng `{elevation.glass}`.
  - Mascot Cá Voi Xanh [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`48px`) hiển thị gợi mở theo 3 vòng (UC-06d):
    - *Vòng 1:* Chỉ bôi đỏ `{colors.error}` vị trí lỗi chính tả/từ loại lỗi và phân loại lỗi.
    - *Vòng 2:* Gợi ý quy luật ngữ pháp và từ vựng viết lại câu.
    - *Vòng 3:* Hiển thị câu gợi ý mẫu của Admin khuyết từ để học viên điền nốt.
- **Ô soạn thảo (Writing Input - Vùng C - cột phải):**
  - Khung nhập văn bản lớn (Textarea), nền `{colors.surface}`, bo góc `{rounded.xl}` (24px). Viền mặc định `1px solid rgba(155, 93, 224, 0.2)`.

#### CHẾ ĐỘ 3: ESSAY WRITING (VIẾT LUẬN CHUẨN HÓA QUỐC TẾ)
- **Đề viết luận lớn (Essay Prompt Box - Vùng B):**
  - Nền `{colors.surface}`. Bo góc `{rounded.xl}` (24px).
  - Hiển thị đề thi viết luận chính thức (ví dụ: đề IELTS Writing Task 2).
- **Khung soạn luận lớn (Essay Editor Area - Vùng C):**
  - Khung soạn thảo văn bản lớn (Textarea), nền `{colors.surface}`, bo góc `{rounded.xl}` (24px), chiều cao tối thiểu `350px`.
  - **Quy tắc thi cử nghiêm ngặt (USE_CASES.md - UC-06d):** Vô hiệu hóa toàn bộ các công cụ tự động sửa chính tả/ngữ pháp mặc định của trình duyệt để kiểm tra thực lực học viên.
  - Bộ đếm từ ở góc dưới phải: *"Số từ: {X} words"* dạng `{typography.body-sm}` màu `{colors.text-secondary}`.

### 4.3 Trang kết quả viết chấm AI (AI Writing Evaluation View - Vùng E)
Xuất hiện thay thế vùng soạn thảo khi nộp bài thành công:
- **Bảng điểm AI & Đánh giá chi tiết (AI Evaluation Panel):**
  - Nền `{colors.surface}`. Bo góc `{rounded.xxl}` (32px). Padding `{spacing.xl}` (32px).
  - Hiển thị tổng điểm hoặc ước lượng Band điểm IELTS (ví dụ: *"IELTS Band: 6.5"*).
  - Hiển thị điểm chi tiết theo 4 tiêu chí chuẩn quốc tế dạng biểu đồ:
    - **Lexical Resource** (Vốn từ vựng).
    - **Grammatical Range & Accuracy** (Ngữ pháp chính xác).
    - **Coherence & Cohesion** (Tính liên kết mạch lạc).
    - **Task Achievement** (Khả năng hoàn thành nhiệm vụ).
  - Bản viết của học viên được hiển thị lại, bôi đỏ các lỗi sai chính tả/ngữ pháp kèm popup bong bóng gợi ý sửa lỗi khi click vào.
  - Hiển thị bài viết mẫu tối ưu của Admin và lời giải thích chi tiết.

### 4.4 Hộp thoại cảnh báo bài viết trống (Blank Essay Warning Modal - Vùng D)
- **Cấu trúc & Định vị:** Overlay kính mờ `{colors.glass}`, ở giữa chứa card cảnh báo nền `{colors.surface}` bo tròn `{rounded.xl}`.
- **Nội dung:** Tiêu đề màu đỏ `{colors.error}`: *"Bài viết trống!"*. Dòng mô tả: *"Bạn chưa nhập bất kỳ nội dung nào vào khung soạn thảo. Vui lòng hoàn thành bài viết trước khi nộp!"*. Nút bấm "Đóng cảnh báo" (`button-primary` style).

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Nhấp nút "Nộp bài"**
  - Học viên nhập nội dung hợp lệ $\rightarrow$ Click "Nộp bài" $\rightarrow$ Nút chuyển sang trạng thái Loading (hiển thị màng mờ mỏng báo *"AI đang phân tích bài luận theo 4 tiêu chí..."*) $\rightarrow$ Chuyển vùng soạn thảo sang hiển thị trang kết quả chấm thi AI Vùng E và Toast xanh lá báo nộp bài thành công.
  - **Dữ liệu API:** `POST /api/writing/evaluate` gửi payload `{ "essayText": "I agree with this..." }`
    - Response: `{ "success": true, "bandScore": 6.5, "lexical": 6.0, "grammar": 7.0, "coherence": 6.5, "taskAch": 6.5, "corrections": [{"text": "agree", "index": 8, "errorType": "spelling", "correction": "agree"}], "modelEssay": "..." }`

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT
- **Trạng thái tải (Loading state):** Khi nộp bài luận lớn (AI chấm trong 3-5 giây), hiển thị màng mờ mỏng thông báo tiến trình phân tích.
- **Trạng thái lỗi kết nối:** Khi API AI bị ngắt kết nối $\rightarrow$ hiển thị thông báo: *"Lỗi kết nối AI. Bài viết của bạn đã được ghi nhận. Hệ thống sẽ chấm điểm sau!"*.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [unit_detail_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/unit_detail_page.md).
- **Đi đến:** [unit_detail_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/unit_detail_page.md) (khi click "Hoàn thành bài viết").

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Thiết kế Split screen chia đôi 50/50 ở desktop giúp đối chiếu đề bài và khung soạn thảo trực quan. Sử dụng ảnh gốc [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) làm logo ghim cố định ở đầu thanh Nav.
- **KHÔNG ĐƯỢC:** Để hiển thị bóng đổ đen bên dưới các thẻ. Các lỗi sai chính tả trong bài viết sau khi chấm được bôi đỏ đậm kèm gạch wavy dưới từ, lỗi dùng từ sai sắc thái bôi màu vàng `{colors.warning}`, lỗi ngữ pháp bôi màu tím nhạt `{colors.accent}` để học viên phân biệt rõ rệt từng nhóm lỗi.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Thông tin bài học (Lesson Header):** Liên kết với `lessons.unit_1[5]` (các trường `{name}`).
- **Đề bài viết luận & Chỉ dẫn (Writing Prompt):** `{lessons.unit_1[5].exercises.writingPrompt}` (tiêu đề, yêu cầu đề bài).
- **Gợi ý viết 3 vòng ZPD (ZPD Hints):** `{lessons.unit_1[5].exercises.zpdHints}` (các gợi ý về ngữ pháp, từ vựng và cấu trúc tương đương).
- **Hệ thống đánh giá AI (AI Rubrics & Score):** `{lessons.unit_1[5].exercises.aiAssessment.rubrics}` (danh mục tiêu chí đánh giá và trọng số điểm).
