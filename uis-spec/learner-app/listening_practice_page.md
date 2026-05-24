# MÀN HÌNH: LISTENING PRACTICE PAGE (MÀN HÌNH LUYỆN NGHE)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Listening Practice Page (Màn hình luyện nghe)
- **Mã use case liên quan:** UC-06a (Luyện nghe)
- **Mã luồng người dùng liên quan:** Flow LN-FL-03 (Trạm luyện Kỹ năng - Nghe)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Dashboard $\rightarrow$ Click Unit $\rightarrow$ Unit Detail $\rightarrow$ Click Luyện Nghe (URL: `/units/{unit_id}/lessons/{lesson_id}/listening`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên rèn luyện kỹ năng nghe hiểu qua 3 chế độ tương tác phong phú: Nghe truyện tương tác (Interactive Stories), Trắc nghiệm nghe hiểu đa giọng điệu (Quiz), và Luyện nói đuổi (Shadowing). Học xong, học viên xem chấm điểm tự động, lời giải thích chi tiết của Admin và trò chuyện giải đáp trực tiếp với trợ lý AI Cá Voi Xanh.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục cột kép linh hoạt (Split View Layout). 
  - *Khi làm bài:* Vùng tương tác chính ở giữa rộng `800px` căn giữa.
  - *Khi xem kết quả:* Chia tỷ lệ 7:5 trên Desktop. Cột trái (`720px`) hiển thị transcript và đáp án chi tiết. Cột phải (`380px`) hiển thị Bảng chat Cá Voi Hỏi Đáp (Side AI Chat Panel).
- **Màu nền chung:** Nền trang sử dụng `{colors.canvas}` (`#F9F7FE`) phối dải chuyển màu mờ `{gradients.atmosphere-haze}`.

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh tiến độ nghe (Progress Header)
- **Đặc tả Visual:**
  - Nền: Kính mờ `{colors.glass}` (`rgba(255, 255, 255, 0.7)`), có `backdrop-filter: blur(8px)`.
  - Chiều cao: `nav-height` (64px). Viền dưới mờ `1px solid rgba(155, 93, 224, 0.1)`.
- **Thành phần:**
  - **Thanh tiến trình ngang:** Nằm sát cạnh đỉnh Nav. Cao `6px`. Nền `{colors.light-accent}`. Phần hoàn thành chạy dải gradient `{gradients.morning-nebula}` hiển thị tiến độ (ví dụ: *"Đoạn 2 / 5"* hoặc *"Câu hỏi 4 / 10"*).
  - **Nút thoát bài học (Exit Button):** Icon Lucide `x` màu `{colors.text-secondary}`. Click để thoát về Unit Detail Page sau khi xác nhận.

### 4.2 Vùng tương tác luyện nghe chính (Central Listening Player - Vùng B)
Nội dung thay đổi linh hoạt theo 3 chế độ luyện nghe do Admin cấu hình:

#### CHẾ ĐỘ 1: INTERACTIVE STORIES (NGHE TRUYỆN TƯƠNG TÁC)
- **Trình phát phân đoạn truyện (Audio Player Segment):** 
  - Nút tròn `{rounded.full}` màu `{colors.primary}` (`#4E56C0`) đính icon Lucide `play` / `pause`.
  - Phát âm thanh đoạn truyện ngắn (20-30s). *Học viên bắt buộc phải nghe hết phân đoạn, trình phát tự động dừng ở cuối phân đoạn.*
- **Câu hỏi mở khóa đoạn (Unlocking Question Card):**
  - Nền: `{colors.surface}` (`#FFFFFF`). Bo góc: `{rounded.xl}` (24px). Viền mờ `1px solid rgba(155, 93, 224, 0.1)`. Padding: `{spacing.lg}` (24px).
  - Xuất hiện động ngay dưới nút player sau khi âm thanh kết thúc.
  - Chứa câu hỏi trắc nghiệm hoặc kéo thả từ để kiểm tra thông tin vừa nghe. Học viên phải chọn đáp án đúng để mở khóa nghe tiếp phân đoạn truyện sau.

#### CHẾ ĐỘ 2: AUDIO COMPREHENSION QUIZ (TRẮC NGHIỆM NGHE HIỂU)
- **Bảng điều khiển Audio (Audio Controls Dashboard):**
  - Nền: `{colors.surface}`. Bo góc: `{rounded.xl}`. Viền mờ, padding `{spacing.lg}`.
  - Chứa: Nút Play/Pause, thanh tua âm thanh (seeker bar), và dropdown chọn Tốc độ phát (0.75x, 1.0x, 1.25x, 1.5x), dropdown chọn Accent phát âm (UK Accent / US Accent / Australian Accent - Mapped to UC-06a).
- **Lưới câu hỏi nghe hiểu (Quiz Sheet):**
  - Xếp dọc bên dưới player. Chứa danh sách câu hỏi trắc nghiệm A, B, C, D hoặc điền khuyết dựa theo nội dung bài nghe dài (Basic 1-2 phút, Intermediate 3-5 phút, Advanced 5-15 phút).

#### CHẾ ĐỘ 3: SHADOWING (LUYỆN NÓI ĐUỔI KÉM TIMESTAMPS)
- **Danh sách câu thoại (Transcript Timed Lines):**
  - Danh sách xếp dọc, câu thoại đang phát sẽ sáng nhẹ màu `{colors.light-accent}`.
  - Hiển thị transcript tiếng Anh chia nhỏ theo câu thoại có timestamp (ví dụ: *"00:12 - 00:15: I am working on the database."*).
- **Nút Micro ghi âm nói đuổi (Microphone Shadowing Button):**
  - Căn phải cuối mỗi dòng thoại. Nút tròn `{rounded.full}` đường kính `48px`, nền `{colors.primary}`, chữ trắng.
  - Nhấp để thu âm giọng nói của người học nói đuổi theo câu thoại đó. Khi ghi âm, nút hiển thị sóng âm soundwave màu đỏ `{colors.error}` nhấp nháy.
- **Kết quả chấm phát âm (Word-by-word Coloring):**
  - Hiển thị đè lên văn bản câu thoại sau khi AI phân tích.
  - Từ phát âm đúng: màu xanh lá `{colors.success}` (`#22C55E`).
  - Từ phát âm sai: màu đỏ `{colors.error}` (`#EF4444`) kèm gạch wavy. Di chuột vào hiện bảng gợi ý IPA đúng và lời khuyên của Admin.

### 4.3 Trang kết quả & Hỏi AI (Result Showcase - Zone 3 & 4)
Xuất hiện sau khi học viên bấm nút "Nộp bài":
- **Bảng tổng hợp kết quả (Listening Result Card - Vùng B):**
  - Nền: `{colors.surface}`. Bo góc `{rounded.xl}`. Padding `{spacing.xl}` (32px).
  - Hiển thị tổng số câu trả lời đúng (ví dụ: *"Điểm số: 8 / 10 câu đúng (+10 EXP)"*). Hiển thị lại toàn bộ câu hỏi kèm tích xanh `{colors.success}` cho câu đúng, dấu nhân đỏ `{colors.error}` cho câu sai cùng đáp án và lời giải thích chi tiết của Admin.
- **Nút "Lưu từ vựng" nhanh (Quick Save to SRS):**
  - Kế bên các từ mới được bôi đậm trong transcript. Dạng badge-pill bo góc `{rounded.pill}`. Nhấp để đưa từ vựng đó vào danh sách ôn tập SRS cá nhân (UC-08).
- **Khung chat Người bạn Cá Voi (Cá Voi Thông Thái Side Chat Panel - Vùng C):**
  - Trượt ra từ lề phải màn hình. Đặc tả Visual: Nền kính mờ `{colors.glass}`, bo góc `{rounded.xl}` (24px), hiệu ứng `{elevation.glass}`.
  - Trợ lý Cá Voi Xanh [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`64px`) hiển thị bong bóng chat hỗ trợ giải đáp từ vựng/ngữ pháp xuất hiện trong bài nghe. Học viên gõ câu hỏi vào ô input cao `44px` ở dưới cùng panel.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Trả lời trắc nghiệm mở khóa (Interactive Stories)**
  - Học viên nghe hết đoạn audio $\rightarrow$ Audio dừng, câu hỏi xuất hiện $\rightarrow$ Chọn đáp án đúng $\rightarrow$ Bấm "Tiếp tục" $\rightarrow$ Mở khóa đoạn tiếp theo và tự động phát audio đoạn kế tiếp.
  - Chọn sai $\rightarrow$ Báo đỏ viền câu hỏi `{colors.error}`, hiện nút "Nghe lại đoạn này".
- **Hành động: Gửi câu hỏi chat với Cá Voi Xanh AI**
  - Học viên nhập câu hỏi vào ô chat (ví dụ: *"Giải thích cấu trúc 'had gone' trong bài nghe"*), click nút gửi.
  - AI nhận dữ liệu ngữ cảnh bài nghe từ Server, phân tích và trả về câu trả lời giải thích chi tiết trong bong bóng chat sau `2 giây`.
  - **Dữ liệu API:** `POST /api/listening/dialogue` với payload `{ "userId": 105, "lessonId": 24, "userQuestion": "..." }`.

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT
- **Trạng thái tải (Loading state):** Khi đang tải dữ liệu âm thanh hoặc gửi file ghi âm Shadowing lên máy chủ $\rightarrow$ Nút micro hoặc player hiển thị spinner xoay mờ, tạm khóa click.
- **Trạng thái lỗi (Error state):** Khi API AI bị ngắt kết nối trong khung chat $\rightarrow$ Chatbox hiển thị thông báo: *"Người bạn Cá Voi tạm thời mất kết nối. Bạn có thể xem lời giải thích chi tiết của Admin phía dưới!"*.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [unit_detail_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/unit_detail_page.md).
- **Đi đến:** [unit_detail_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/unit_detail_page.md) (khi click "Hoàn thành bài học").

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Sử dụng tệp ảnh gốc [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) làm logo ghim cố định ở đầu Nav và avatar Cá Voi hướng dẫn trong panel chat để đảm bảo nhất quán nhận diện.
- **KHÔNG ĐƯỢC:** Sử dụng đổ bóng xám/đen vật lý. Tránh quá tải nhận thức bằng cách giữ khoảng trắng rộng rãi `{spacing.lg}` (24px) xung quanh các ô câu hỏi.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Thông tin bài học (Lesson Header):** Liên kết với `lessons.unit_1[2]` (các trường `{name}`, `{audioUrl}`).
- **Các dạng luyện tập Nghe tương tác (Listening Activities):**
  - Interactive Stories: `{lessons.unit_1[2].exercises.interactiveStory}` (truyện ngắn, audio phân đoạn và câu hỏi đi kèm).
  - Trắc nghiệm nghe hiểu: `{lessons.unit_1[2].exercises.comprehensionQuiz}` (các câu hỏi MCQ nghe hiểu).
  - Shadowing (nói đuổi): `{lessons.unit_1[2].exercises.shadowing}` (transcript chia câu thoại kèm mốc thời gian).
