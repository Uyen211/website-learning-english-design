# MÀN HÌNH: GRAMMAR LEARNING PAGE (MÀN HÌNH HỌC NGỮ PHÁP tự nhiên)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Grammar Learning Page (Màn hình học ngữ pháp tự nhiên - UC-05b)
- Mã use case liên quan: UC-05b (Học ngữ pháp tự nhiên)
- Mã luồng người dùng liên quan: Flow LN-FL-03 (Học ngữ pháp tự nhiên)
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Dashboard -> Click Unit -> Unit Detail Page -> Click bài học Ngữ pháp -> Grammar Learning Page (URL: /units/{unit_id}/lessons/{lesson_id}/grammar)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này để trải qua hành trình khám phá ngữ pháp tự nhiên 7 chặng đường khám phá (từ làm quen tình huống, nhận diện khuôn mẫu, tự đúc rút quy tắc qua cặp câu tương phản, thực hành nhận diện cấu trúc hạt nhân, gõ chính tả chunk ngữ pháp, đặt câu sản sinh cá nhân hóa có AI Cá Voi Thông Thái sửa lỗi sai, đến khi hoàn thành để lên lịch ôn tập SRS).

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Centered card layout (Bố cục một cột căn giữa hoàn toàn theo cả chiều ngang và dọc) sử dụng nền canvas sáng ấm (#fffaf0), kết hợp thanh tiến độ ngang ở đầu màn hình và bảng điều khiển phụ (Gợi ý từ Cá Voi Thông Thái Panel) trượt mở từ bên phải.
- Các vùng chính trên màn hình:
  - Vùng A: Thanh tiến độ bài học (Progress Header) cố định ở đầu màn hình.
  - Vùng B: Thẻ học tập trung tâm (Central Learning Card Container) hiển thị nội dung của từng giai đoạn học ngữ pháp.
  - Vùng C: Bảng gợi ý từ Cá Voi Cá Voi Thông Thái (Gợi ý từ Cá Voi Thông Thái Panel) xuất hiện dọc bên phải Central Card trong giai đoạn sản sinh câu.
  - Vùng D: Thanh điều hướng chân trang (Footer Action Bar) chứa các nút bấm chuyển tiếp.
- Kích thước / Grid tham khảo:
  - Thẻ học tập trung tâm kích thước cố định: 760px x 500px, góc bo rounded-xl (24px).
  - Vùng C (Bảng Cá Voi) có chiều rộng 360px khi mở rộng bên phải Central Card.
  - Khoảng cách padding trong thẻ học tập: spacing-xl (32px).
  - Sử dụng CSS Flexbox/Grid căn giữa viewport hoàn toàn.

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)

### THÀNH PHẦN CHUNG (PROGRESS HEADER & CONTROLS)
- **Tên component:** Thanh tiến độ bài học (Lesson Progress Bar)
  - **Loại component tham chiếu từ DESIGN.md:** progress-bar (nền surface-strong #ebe6d6, thanh tiến độ xanh success #22c55e, height 8px)
  - **Vị trí:** Vùng A, chạy ngang đầu màn hình.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị số lượng ngữ pháp đã hoàn thành (ví dụ: "Ngữ pháp 1 / 3 - Hoàn thành 33%").

- **Tên component:** Nút đóng bài học (Exit Button)
  - **Loại component tham chiếu từ DESIGN.md:** rounded-full (icon button 36px x 36px, màu muted #6a6a6a)
  - **Vị trí:** Vùng A, góc trên bên phải.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị icon dấu "X" màu ink. Nhấn vào sẽ thoát bài học, hiển thị popup xác nhận trước khi quay lại màn hình LN-02.

---

### GIAI ĐOẠN 1: NHẬN DIỆN TÌNH HUỐNG (SITUATIONAL IDENTIFICATION STAGE)
- **Tên component:** Phương tiện ngữ cảnh (Contextual Video/Image)
  - **Loại component tham chiếu từ DESIGN.md:** hero-illustration-card (nền surface-soft #faf5e8, rounded-lg 16px)
  - **Vị trí:** Vùng B, nằm trên cùng Central Card.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị một video ngắn hoặc hình ảnh 3D claymation minh họa một tình huống giao tiếp (ví dụ: Một người đang vội vã chạy để bắt xe buýt, câu thoại xuất hiện trên đầu: "If I run fast, I will catch the bus."). Tuyệt đối không hiển thị tên cấu trúc ngữ pháp hay công thức.

- **Tên component:** Câu hỏi trắc nghiệm tình huống
  - **Loại component tham chiếu từ DESIGN.md:** title-sm (font Inter weight 600, màu ink #0a0a0a)
  - **Vị trí:** Vùng B, nằm dưới phần hình ảnh.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị câu hỏi: "Tình huống này diễn ra khi nào?" kèm các lựa chọn trắc nghiệm A, B, C dưới dạng nút `button-secondary` xếp dọc. Người dùng nhấp chọn đáp án đúng để mở nút "Tiếp tục".

---

### GIAI ĐOẠN 2: NHẬN DIỆN KHUÔN MẪU (PATTERN RECOGNITION STAGE)
- **Tên component:** Bảng ví dụ khuôn mẫu (Pattern Sentences Box)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền canvas #fffaf0, rounded-lg 16px, border 1px hairline #e5e5e5, padding 20px)
  - **Vị trí:** Vùng B, thân Central Card.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị 3 câu ví dụ có cấu trúc tương tự nhau:
    - 1. *If it rains, we will stay at home.*
    - 2. *If you study hard, you will pass the exam.*
    - 3. *If she arrives early, she will call us.*

- **Tên component:** Câu hỏi nhận diện đặc điểm chung
  - **Loại component tham chiếu từ DESIGN.md:** button-secondary (xếp 3-4 tùy chọn trắc nghiệm)
  - **Vị trí:** Vùng B, dưới bảng ví dụ.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Yêu cầu học viên phát hiện điểm chung về mặt hình thức: "Đặc điểm chung của động từ ở mệnh đề IF trong các câu trên là gì?". Học viên nhấp chọn đáp án đúng (ví dụ: "Chia ở thì Hiện tại đơn") để chuyển sang Giai đoạn 3.

---

### GIAI ĐOẠN 3: ĐỐI CHIẾU & ĐÚC RÚT QUY TẮC (RULE EXTRACTION STAGE)
- **Tên component:** Cặp câu tương phản (Contrastive Pairs Grid)
  - **Loại component tham chiếu từ DESIGN.md:** grid 2-up (hai thẻ nhỏ đặt song song)
  - **Vị trí:** Vùng B, phần trên của Central Card.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị 2 câu có sự tương phản sắc thái ngữ pháp để học viên so sánh:
    - *Thẻ trái:* "If it rains, I will stay home." (Có thể xảy ra ở tương lai).
    - *Thẻ phải:* "If it rained, I would stay home." (Trái thực tế ở hiện tại).

- **Tên component:** Bảng quy tắc & Cấu trúc hạt nhân (Grammar Chunk Box)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền surface-card #f5f0e0, rounded-lg 16px, padding 20px)
  - **Vị trí:** Vùng B, thân Central Card.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** 
    - Hiển thị tên gọi chính thức: "Câu điều kiện loại 1 (Conditional Sentence Type 1)".
    - Hiển thị công thức trực quan: **If + S + V(s/es), S + will/can + V-infinitive**.
    - Các cấu trúc hạt nhân (Grammar Chunks): "If you need help, ...", "If I have time, ...".

---

### GIAI ĐOẠN 4: THỰC HÀNH NHẬN DIỆN (ACTIVE PRACTICE STAGE)
*Màn hình hiển thị hình thức bài tập tương ứng do Admin cấu hình:*

- **Tên component:** Giao diện kéo thả Focus Mode
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (các từ được đặt trong các badge-pill nhỏ bo tròn)
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hệ thống ẩn đi các thành phần phụ, chỉ hiển thị cấu trúc câu hạt nhân (S+V+O). Học viên kéo thả các thẻ từ xáo trộn để xây dựng mô hình tâm trí cấu trúc câu chuẩn.

- **Tên component:** Biểu mẫu Viết lại câu (Sentence Transformation Input)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, height 44px, rounded-md 12px)
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Mặc định, focus, error.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị câu gốc: "She doesn't study hard, so she will fail." và câu gợi ý viết lại: "If she...". Học viên gõ phần còn lại vào ô nhập liệu: "studies hard, she will pass the exam".

---

### GIAI ĐOẠN 5: NGHE GÕ CHUNK NGỮ PHÁP (DICTATION STAGE)
- **Tên component:** Ô nhập Dictation Chunk
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, text ink #0a0a0a, rounded-md 12px, border 1px hairline #e5e5e5, height 44px, font Inter size 16px, căn giữa)
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Mặc định, focus, error (viền đỏ màu error #ef4444).
  - **Dữ liệu hiển thị / hành vi:** Hệ thống phát audio của một chunk ngữ pháp (ví dụ: "If you need help"). Học viên gõ lại chính xác chunk vào ô trống. Nếu gõ sai lần 3 -> Hiển thị hộp đáp án mẫu cưỡng bức bắt buộc gõ lại chính xác để đi tiếp.

---

### GIAI ĐOẠN 6: TỰ VIẾT CÂU CÁ HÂN HÓA & TRỢ LÝ Cá Voi Thông Thái (PERSONALIZED PRODUCTION STAGE)
- **Tên component:** Khung viết câu ngữ pháp
  - **Loại component tham chiếu từ DESIGN.md:** text-area (nền canvas #fffaf0, text ink #0a0a0a, border 1px hairline #e5e5e5, rounded-md 12px, padding 16px, chiều cao 100px)
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Mặc định, focus, error.
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Hãy tự viết một câu mới sử dụng cấu trúc Câu điều kiện loại 1 kể về kế hoạch thực tế của bạn *". Placeholder: "Ví dụ: If I have free time this weekend, I will..."

---

### VÙNG C: BẢNG gợi ý từ Cá Voi Cá Voi Thông Thái (Gợi ý từ Cá Voi Thông Thái PANEL)
- **Tên component:** Bảng điều khiển Cá Voi Thông Thái (Cá Voi Thông Thái Panel Container)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-ochre (nền brand-ochre #e8b94a nhạt, border-left 1px hairline #e5e5e5, padding 20px)
  - **Vị trí:** Vùng C, hiển thị dọc bên phải Central Card khi chuyển sang Giai đoạn 6.
  - **Trạng thái:** Ẩn mặc định, tự động trượt mở ra ở giai đoạn 6 khi có phản hồi lỗi từ AI.
  - **Dữ liệu hiển thị / hành vi:** Chứa tiêu đề "Phân tích ngữ pháp AI", bôi đỏ vị trí lỗi sai của học viên (ví dụ: viết "If I will have time, I go" -> bôi đỏ "will have" và "go"), và đưa ra gợi ý nâng đỡ qua 3 vòng:
    - *Vòng 1:* Báo lỗi cấu trúc (ví dụ: "Mệnh đề IF trong câu điều kiện loại 1 không dùng động từ khuyết thiếu will. Hãy sửa lại!").
    - *Vòng 2:* Gợi ý công thức chi tiết (ví dụ: "Mệnh đề IF chia Hiện tại đơn: If + S + V(s/es). Mệnh đề chính dùng: will + V. Hãy sửa lại câu của bạn!").
    - *Vòng 3:* Khóa ô nhập tự do, hiển thị câu mẫu khuyết của Admin để điền từ (ví dụ: "If I _____ (have) time, I will go. Hãy điền từ chia động từ thích hợp vào chỗ trống!").

---

### GIAI ĐOẠN 7: HOÀN THÀNH BÀI HỌC (LESSON COMPLETION PAGE)
- **Tên component:** Khối chúc mừng hoàn thành (Congratulatory Box)
  - **Loại component tham chiếu từ DESIGN.md:** cta-band-illustrated (nền surface-soft #faf5e8, rounded-xl 24px, padding 40px)
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** 
    - Tiêu đề: "Chúc mừng! Bạn đã làm chủ cấu trúc này!" (display-sm 32px, màu ink #0a0a0a).
    - Cập nhật EXP: "+15 EXP" (badge-pill success).
    - Trạng thái SRS: "Cấu trúc 'Conditional Sentence Type 1' đã được lưu vào lịch ôn tập SRS cá nhân của bạn.".

- **Tên component:** Nút "Hoàn thành bài học"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, height 44px, rounded-md 12px)
  - **Vị trí:** Vùng D.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị text "Hoàn thành & Quay lại". Nhấp chuột để thoát màn hình và quay về Unit Detail Page (LN-02).

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Giai đoạn 5 - Nhập chính tả và click "Kiểm tra"**
  - **Luồng chính:** Học viên nghe audio chunk -> Nhập đúng vào ô nhập liệu -> Click nút "Kiểm tra" -> Hệ thống hiện viền xanh success (#22c55e), phát âm thanh báo đúng -> Central Card tự động chuyển sang Giai đoạn 6 sau 1 giây.
  - **Luồng con / rẽ nhánh:** Học viên gõ sai -> Hệ thống báo đỏ viền ô nhập, phát lại audio -> Học viên gõ lại. Nếu gõ sai lần 3 -> Hiển thị hộp đáp án mẫu cưỡng bức để gõ lại đúng chính tả mới được đi tiếp.
- **Hành động: Giai đoạn 6 - Tự viết câu và click "Nộp câu"**
  - **Luồng chính:** Học viên đặt câu đúng ngữ pháp -> Click "Nộp câu" -> AI phân tích không thấy lỗi -> Nút nộp chuyển sang trạng thái thành công -> Tự động chuyển sang Giai đoạn 7 (Hoàn thành bài học).
  - **Luồng con / rẽ nhánh (Phản hồi Cá Voi Thông Thái):**
    - Học viên viết câu có lỗi -> Click "Nộp câu" -> Nút nộp tắt loading, Cá Voi Thông Thái Panel mở rộng ra bên phải.
    - *Lần sửa 1:* AI bôi đỏ vị trí lỗi trên câu học viên và đưa ra gợi ý gợi mở ở Bảng Cá Voi. Học viên sửa câu -> Bấm nộp lại.
    - *Lần sửa 2:* AI phát hiện vẫn lỗi -> Bôi đỏ lỗi và đưa ra gợi ý công thức trực tiếp ở Bảng Cá Voi. Học viên sửa lại câu chính xác và bấm nộp -> Chuyển sang Giai đoạn 7.
    - *Lần sửa 3 (nếu vẫn sai):* Hệ thống tự động khóa ô đặt câu. Hiển thị câu mẫu của Admin bị khuyết động từ chia. Học viên điền động từ thích hợp vào ô khuyết -> Nhấn xác nhận -> Chuyển sang Giai đoạn 7.
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: `{ "userId": 105, "grammarId": 24, "userSentence": "If it will rain, I will stay home." }`
    - Nhận về: `{ "isValid": false, "errorCount": 1, "errors": [{ "text": "will rain", "index": 7, "suggestion": "rains", "type": "tense_error" }], "hint": "Mệnh đề IF trong câu điều kiện loại 1 không dùng..." }`

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Không áp dụng.
- **Trạng thái tải (loading state):** Khi nhấn "Nộp câu" ở Giai đoạn 6, AI đang phân tích cú pháp câu (khoảng 1-2 giây) -> Nút nộp chuyển sang trạng thái Loading (hiển thị spinner, khóa click), Bảng Cá Voi hiển thị các thanh xương skeleton nhấp nháy.
- **Trạng thái lỗi (error state):** Khi API AI bị mất kết nối mạng -> Hiển thị thông báo đỏ ở chân Bảng Cá Voi: "Lỗi kết nối AI. Chuyển sang chế độ câu mẫu khuyết từ..." để học viên hoàn tất bài học, không bị kẹt lại.
- **Trạng thái thành công (success state):** Giai đoạn 7 chúc mừng hoàn thành bài học, rơi confetti, cộng điểm EXP.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ Unit Detail Page (LN-02) sau khi học viên nhấp chọn bài học Ngữ pháp và bấm nút "Bắt đầu học".
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Chuyển hướng quay trở lại Unit Detail Page (LN-02) khi bấm nút "Hoàn thành bài học" ở Giai đoạn 7.
- **Các màn hình liên quan khác:** LN-02.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0) đặc trưng.
- Hộp chứa biểu mẫu học tập Central Card sử dụng phong cách `feature-card-cream` màu surface-card (#f5f0e0), các nút bấm bo góc rounded-md (12px) màu đen ink hoặc canvas hairline mỏng 1px (#e5e5e5).
- Trong giai đoạn 6, Cá Voi Thông Thái Panel sử dụng màu vàng ấm nhạt của `feature-card-ochre` để tạo sự chú ý vừa phải cho học viên mà không gây cảm giác áp lực khi làm sai câu.
- Theo Nguyên tắc Báo hiệu (Signaling Principle), các ký tự hoặc từ viết sai ngữ pháp được bôi màu đỏ sáng (#ef4444) kết hợp gạch wavy để thu hút tiêu điểm thị giác tức thì giúp học viên tự điều chỉnh lỗi sai.
- Đảm bảo khoảng cách spacing-lg (24px) giữa câu ví dụ và các trường nhập để tránh chật chội. Touch target của các nút bấm và ô nhập là 44px.



