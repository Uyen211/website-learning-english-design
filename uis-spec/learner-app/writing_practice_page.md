# MÀN HÌNH: WRITING PRACTICE PAGE (MÀN HÌNH LUYỆN VIẾT)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Writing Practice Page (Màn hình luyện viết)
- Mã use case liên quan: UC-06d (Luyện viết)
- Mã luồng người dùng liên quan: Flow LN-FL-07 (Luyện tập kỹ năng Viết)
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Dashboard -> Click Unit -> Unit Detail Page -> Click bài học Luyện Viết -> Writing Practice Page (URL: /units/{unit_id}/lessons/{lesson_id}/writing)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này để nâng cao kỹ năng viết qua 3 hình thức: Viết cơ bản (ghép từ/điền khuyết), Viết ngắn ZPD 3 vòng gợi ý, và Viết luận lớn chuẩn hóa quốc tế (IELTS/TOEIC) có AI chấm chữa chi tiết theo 4 tiêu chí.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục cột kép chia tỷ lệ 6:6 (Split Column Layout) cho màn hình viết luận và viết ZPD; Bố cục 1 cột căn giữa cho viết cơ bản.
- Các vùng chính trên màn hình:
  - Vùng A: Thanh dẫn Breadcrumbs và tiến độ ở đầu trang.
  - Vùng B: Vùng Đề bài và Gợi ý bên trái (Left Prompt Panel) chứa đề bài viết, gợi ý hoặc bảng phản hồi ZPD.
  - Vùng C: Vùng Soạn thảo bài viết bên phải (Right Editor Panel) chứa khung nhập liệu văn bản lớn và bộ đếm từ.
  - Vùng D: Hộp thoại báo lỗi bài viết trống (Blank Essay Warning Modal - LN-08-M1).
  - Vùng E: Bảng kết quả chấm thi AI (AI Writing Evaluation View) hiển thị thay thế khi nộp bài thành công.
- Kích thước / Grid tham khảo:
  - Vùng B (Đề bài/Gợi ý) và Vùng C (Soạn thảo) chiếm tỷ lệ 50/50 ở desktop.
  - Khung soạn thảo văn bản lớn có chiều cao tối thiểu 350px.
  - Khoảng cách padding trong các vùng: spacing-lg (24px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)

### THÀNH PHẦN CHUNG (PROGRESS HEADER)
- **Tên component:** Thanh tiến trình viết (Writing Progress Bar)
  - **Loại component tham chiếu từ DESIGN.md:** progress-bar (nền surface-strong #ebe6d6, thanh tiến độ xanh success #22c55e, height 8px)
  - **Vị trí:** Vùng A.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị vị trí phần bài viết đang thực hiện (ví dụ: "Bài viết 1 / 2").

---

### PHÂN HỆ SOẠN THẢO CHI TIẾT (VÙNG B & C)

#### 1. BASIC WRITING MODE (GIAO DIỆN VIẾT CƠ BẢN)
- **Tên component:** Khu vực kéo ghép câu (Word Ordering Interface)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền surface-card #f5f0e0, padding 20px)
  - **Vị trí:** Vùng C (Bố cục 1 cột dọc căn giữa).
  - **Trạng thái:** Mặc định. Các thẻ từ có thể kéo thả.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị các thẻ từ bị xáo trộn (ví dụ: "will / rains / stay / at / If / home / it / we"). Học viên kéo thả sắp xếp lại thành câu hoàn chỉnh: "If it rains, we will stay at home."

#### 2. SCAFFOLDED ZPD WRITING MODE (GIAO DIỆN VIẾT GỢI Ý 3 VÒNG ZPD)
- **Tên component:** Đề viết ngắn & Khung cấu trúc
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền canvas #fffaf0, padding 20px)
  - **Vị trí:** Vùng B (cột trái).
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị đề bài viết ngắn (ví dụ: "Viết câu trả lời email xin nghỉ phép") kèm theo các gợi ý cấu trúc đích cần sử dụng.

- **Tên component:** Khung ZPD gợi ý 3 vòng (3-Tier Hint Box)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-ochre (nền brand-ochre #e8b94a nhạt, rounded-lg 16px, padding 16px)
  - **Vị trí:** Vùng B, xuất hiện dưới đề bài khi học viên nộp bài viết bị lỗi.
  - **Trạng thái:** Xuất hiện động.
  - **Dữ liệu hiển thị / hành vi:**
    - *Vòng 1:* Chỉ bôi đỏ vị trí lỗi chính tả/từ loại, đưa ra loại lỗi (ví dụ: "Lỗi chính tả ở từ 'recieve'.").
    - *Vòng 2:* Đưa ra gợi ý quy luật ngữ pháp/từ vựng (ví dụ: "Hãy nhớ quy tắc viết: i đứng trước e trừ sau c. Nhận lại viết là receive.").
    - *Vòng 3:* Hiển thị câu gợi ý mẫu của Admin khuyết từ để học viên điền từ hoàn thành.

- **Tên component:** Ô soạn thảo ZPD (ZPD Writing Input)
  - **Loại component tham chiếu từ DESIGN.md:** text-area (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-md 12px, padding 16px)
  - **Vị trí:** Vùng C (cột phải).
  - **Trạng thái:** Mặc định, focus, error.

#### 3. ESSAY WRITING MODE (GIAO DIỆN VIẾT LUẬN CHUẨN HÓA)
- **Tên component:** Đề viết luận lớn (Essay Prompt Box)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền surface-card #f5f0e0, padding 24px)
  - **Vị trí:** Vùng B (cột trái).
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị đề thi viết luận chính thức (ví dụ: IELTS Writing Task 2 về chủ đề giáo dục).

- **Tên component:** Khung soạn luận lớn (Essay Editor Area)
  - **Loại component tham chiếu từ DESIGN.md:** text-area (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-md 12px, padding 24px, chiều cao tối thiểu 350px)
  - **Vị trí:** Vùng C (cột phải).
  - **Trạng thái:** Mặc định, focus. Trình duyệt bị vô hiệu hóa công cụ tự động sửa chính tả.
  - **Dữ liệu hiển thị / hành vi:** Nơi học viên gõ bài luận. Ở góc dưới bên phải có bộ đếm số từ: "Số từ: {X} words" (typography body-sm).

---

### TRANG KẾT QUẢ VIẾT CHẤM AI (WRITING RESULT PAGE)
- **Tên component:** Bảng điểm AI & Đánh giá chi tiết (AI Evaluation Panel)
  - **Loại component tham chiếu từ DESIGN.md:** cta-band-illustrated (nền surface-soft #faf5e8, rounded-xl 24px, padding 32px)
  - **Vị trí:** Vùng E, thay thế giao diện soạn thảo khi kết thúc.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:**
    - Tổng điểm hoặc ước lượng Band điểm IELTS (ví dụ: "IELTS Band: 6.5").
    - Điểm chi tiết theo 4 tiêu chí chuẩn quốc tế (Lexical Resource, Grammatical Range & Accuracy, Coherence & Cohesion, Task Achievement) dạng biểu đồ hoặc bảng.
    - Bản viết của học viên được trích xuất hiển thị lại, bôi đỏ các lỗi sai chính tả/ngữ pháp kèm popup bong bóng gợi ý sửa lỗi khi click vào.
    - Bài viết mẫu tối ưu của Admin và lời giải thích chi tiết.

---

### VÙNG D: HỘP THOẠI BÁO LỖI BÀI VIẾT TRỐNG (MODAL ALERT)
- **Tên component:** Hộp thoại Cảnh báo bài viết trống (Blank Essay Warning Modal - LN-08-M1)
  - **Loại component tham chiếu từ DESIGN.md:** overlay / backdrop + centered alert card (nền surface-card #f5f0e0, rounded-lg 16px, width 380px)
  - **Vị trí:** Vùng D, nổi đè lên màn hình.
  - **Trạng thái:** Xuất hiện khi học viên click nộp bài viết nhưng ô nhập liệu trống hoàn toàn.
  - **Dữ liệu hiển thị / hành vi:** Tiêu đề "Bài viết trống!" (màu error #ef4444). Dòng cảnh báo: "Bạn chưa nhập bất kỳ nội dung nào vào khung soạn thảo. Vui lòng hoàn thành bài viết trước khi nộp!". Nút bấm: "Đóng cảnh báo" (button-primary).

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Nhấp nút "Nộp bài"**
  - **Luồng chính:** Học viên nhập nội dung hợp lệ -> Click "Nộp bài" -> Nút chuyển sang trạng thái Loading -> Hệ thống gửi văn bản bài luận lên AI chấm điểm -> Thành công -> Hiển thị trang kết quả Vùng E và Toast thông báo thành công màu xanh lá.
  - **Luồng con / rẽ nhánh (Nộp bài viết trống - Rẽ nhánh E-1):** Click nộp bài nhưng không có chữ -> Hệ thống giữ nguyên trang, hiển thị Modal LN-08-M1 cảnh báo -> Học viên bấm đóng và quay lại soạn thảo.
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: `POST /api/writing/evaluate` (payload: `{ "essayText": "I agree with this statement because..." }`)
    - Nhận về: `{ "success": true, "bandScore": 6.5, "lexical": 6.0, "grammar": 7.0, "coherence": 6.5, "taskAch": 6.5, "corrections": [{ "text": "agree", "index": 8, "errorType": "spelling", "correction": "agree" }], "modelEssay": "..." }`

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Khung soạn thảo ban đầu hoàn toàn trống.
- **Trạng thái tải (loading state):** Khi gửi bài viết cho AI chấm điểm (thường tốn 3-5 giây đối với bài luận lớn), nút bấm chuyển sang Loading, màn hình phủ màng mờ mỏng hiển thị dòng chữ: "AI đang phân tích bài luận của bạn theo 4 tiêu chí chuẩn quốc tế...".
- **Trạng thái lỗi (error state):** Khi API AI bị ngắt kết nối -> Hiển thị thông báo: "Lỗi kết nối AI. Bài viết của bạn đã được ghi nhận vào hệ thống. Giáo viên sẽ chấm điểm thủ công sau!".
- **Trạng thái thành công (success state):** Trang kết quả hiển thị điểm EXP cộng thêm và Toast báo nộp bài thành công.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ Unit Detail Page (LN-02) sau khi học viên nhấp chọn bài luyện viết.
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Quay trở lại màn hình Unit Detail Page (LN-02) khi học viên bấm nút "Hoàn thành bài viết".
- **Các màn hình liên quan khác:** LN-02, Modal cảnh báo LN-08-M1.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0) đặc trưng.
- Split screen chia đôi 50/50 ở desktop giúp đối chiếu đề bài, gợi ý ZPD và khung soạn thảo trực quan, tránh gây mệt mỏi nhận thức (Coherence Principle).
- Khung soạn thảo văn bản được bo góc rounded-md (12px) trên nền canvas trắng ấm, không dùng bóng đổ.
- Theo Nguyên tắc Báo hiệu (Signaling Principle), các lỗi sai chính tả trong bài viết sau khi chấm được bôi đỏ đậm kèm gạch wavy dưới từ, lỗi dùng từ sai sắc thái bôi màu ochre, lỗi ngữ pháp bôi màu lavender để học viên phân biệt rõ rệt từng nhóm lỗi.
- Khung phản hồi ZPD sử dụng màu nền ấm brand-ochre nhạt để tạo cảm giác thân thiện nâng đỡ.
- Touch target nút bấm đạt chuẩn 44px.
