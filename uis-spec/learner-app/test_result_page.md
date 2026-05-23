# MÀN HÌNH: TEST RESULT PAGE (MÀN HÌNH KẾT QUẢ BÀI THI)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Test Result Page (Màn hình kết quả bài thi)
- Mã use case liên quan: UC-07 (Làm bài thi đánh giá năng lực)
- Mã luồng người dùng liên quan: Flow LN-FL-08 (Thực hiện bài thi đánh giá năng lực)
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Dashboard -> Unit Detail -> Pre-test Setup -> Phòng thi (LN-10) -> Test Result Page (URL: /exams/results/{result_id})

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Người học sử dụng màn hình này để xem kết quả bài thi chi tiết bao gồm tổng điểm số, ước lượng Band điểm IELTS / điểm TOEIC tương ứng, biểu đồ kỹ năng, đáp án đúng/sai kèm lời giải thích của Admin và đề xuất kiến thức cần ôn tập lại.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục một cột dọc kết hợp chia lưới linh hoạt (Flex Grid Layout) trên nền canvas sáng ấm (#fffaf0) có Top Sticky Navigation.
- Các vùng chính trên màn hình:
  - Vùng A: Banner điểm số tổng hợp (Score Overview Banner) hiển thị to ở đầu trang.
  - Vùng B: Biểu đồ năng lực 4 kỹ năng (Skills Breakdown Chart) dạng hình cột hoặc mạng nhện bên trái và Thẻ đề xuất ôn tập (Review Recommendation Card) bên phải.
  - Vùng C: Danh sách câu trả lời chi tiết (Question Review List) hiển thị đáp án đúng/sai, đáp án chính thức và giải thích chi tiết của Admin.
  - Vùng D: Nút hành động "Quay lại Dashboard" (Footer Action Button).
- Kích thước / Grid tham khảo:
  - Chiều rộng tối đa của nội dung: 1000px căn giữa.
  - Vùng B sử dụng lưới chia đôi 6:6 bằng CSS Grid 12 cột.
  - Khoảng cách padding trong các thẻ: spacing-lg (24px).
  - Khoảng cách dọc giữa các phần: spacing-xl (32px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)

### THÀNH PHẦN TỔNG HỢP KẾT QUẢ (VÙNG A & B)
- **Tên component:** Banner tổng hợp điểm số (Score Banner)
  - **Loại component tham chiếu từ DESIGN.md:** cta-band-illustrated (nền surface-soft #faf5e8, rounded-xl 24px, padding 32px, căn giữa)
  - **Vị trí:** Vùng A.
  - **Trạng thái:** Mặc định. Có confetti rơi tự động nếu đỗ bài thi.
  - **Dữ liệu hiển thị / hành vi:** 
    - Hiển thị ước lượng Band điểm IELTS hoặc điểm TOEIC (ví dụ: "IELTS Band ước lượng: 6.5").
    - Điểm số thô đạt được: "85 / 100 EXP (+100 EXP thưởng)".
    - Trạng thái đỗ/trượt: Badge màu success "ĐẠT YÊU CẦU" hoặc màu error "CHƯA ĐẠT YÊU CẦU".

- **Tên component:** Biểu đồ năng lực kỹ năng (Skills Chart Card)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền canvas #fffaf0, rounded-lg 16px, padding 20px)
  - **Vị trí:** Vùng B (bên trái).
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị biểu đồ hình cột hoặc tròn mô tả điểm số của 4 kỹ năng (Nghe, Nói, Đọc, Viết) giúp người học nhận biết điểm mạnh, điểm yếu.

- **Tên component:** Thẻ đề xuất ôn tập (Recommendation Card)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-ochre (nền brand-ochre #e8b94a nhạt, rounded-lg 16px, padding 20px)
  - **Vị trí:** Vùng B (bên phải).
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:**
    - Tiêu đề: "Đề xuất ôn tập từ giáo viên".
    - Danh sách các bài học/kiến thức bị sai nhiều cần xem lại (ví dụ: "Cần cải thiện: Thì Quá khứ hoàn thành (Ngữ pháp), Giới từ đi kèm động từ (Từ vựng)"). Nhấp vào tên bài học sẽ dẫn thẳng tới bài học đó.

---

### PHẦN XEM LẠI ĐỀ THI VÀ ĐÁP ÁN (VÙNG C)
- **Tên component:** Bộ lọc câu hỏi (Review Filters)
  - **Loại component tham chiếu từ DESIGN.md:** category-tab (nền canvas #fffaf0, rounded-pill)
  - **Vị trí:** Vùng C, trên đầu danh sách câu hỏi.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Các tab lọc: "Tất cả câu", "Câu đúng", "Câu sai". Click để lọc danh sách câu hỏi bên dưới.

- **Tên component:** Thẻ xem lại câu hỏi (Question Review Card)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền surface-card #f5f0e0, border 1px hairline #e5e5e5, rounded-lg 16px, padding 20px)
  - **Vị trí:** Vùng C.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị số thứ tự câu, đề bài câu hỏi, đáp án học viên chọn (được bôi đỏ kèm dấu nhân nếu sai; bôi xanh lá kèm tích nếu đúng), đáp án chính xác của đề thi.

- **Tên component:** Khối lời giải thích của Admin (Admin's Explanation Box)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền canvas #fffaf0, rounded-md 12px, border-left 3px solid primary #0a0a0a, padding 16px)
  - **Vị trí:** Vùng C, nằm dưới mỗi câu hỏi.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị tiêu đề "Lời giải thích từ giáo viên:" và đoạn văn phân tích chi tiết tại sao đáp án đó đúng, trích dẫn quy luật ngữ pháp hoặc cấu trúc từ vựng liên quan.

- **Tên component:** Đánh giá AI cho phần tự luận (AI Writing & Speaking Review Panel)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (padding 20px)
  - **Vị trí:** Vùng C, xuất hiện dưới các câu hỏi tự luận viết/nói.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị các tiêu chí chấm điểm chi tiết của AI và bản viết sửa lỗi chính tả/ngữ pháp bôi đỏ gạch wavy.

---

### THÀNH PHẦN ĐIỀU HƯỚNG CHÂN TRANG (VÙNG D)
- **Tên component:** Nút "Quay lại Dashboard"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, font Inter size 14px, weight 600, rounded-md 12px, height 44px, width 320px, căn giữa)
  - **Vị trí:** Vùng D.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Nhấp chuột để thoát trang kết quả và quay về Learner Dashboard (LN-01).

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Click chuyển đổi tab bộ lọc câu hỏi**
  - **Luồng chính:** Học viên click tab "Câu sai" -> Danh sách Vùng C ẩn các câu làm đúng, chỉ hiển thị các câu làm sai để học viên tập trung ôn tập -> Click tab "Tất cả" hiển thị đầy đủ.
- **Hành động: Click vào bài học được đề xuất ôn tập ở Vùng B**
  - **Luồng chính:** Học viên click vào liên kết -> Chuyển hướng trực tiếp sang trang học của bài học đó (ví dụ: Grammar Learning Page LN-04) để củng cố lại.
- **Hành động: Nhấp nút "Quay lại Dashboard"**
  - **Luồng chính:** Hệ thống kiểm tra kết quả thi, nếu đạt điểm đỗ -> Tự động cập nhật mở khóa bài học/Unit tiếp theo trên cơ sở dữ liệu -> Chuyển hướng quay lại màn hình Dashboard (LN-01).

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Không áp dụng.
- **Trạng thái tải (loading state):** Khi đang tải dữ liệu kết quả từ server, toàn bộ trang hiển thị skeleton nhấp nháy, biểu đồ hiển thị các khung xám mờ.
- **Trạng thái lỗi (error state):** Khi API kết quả bị lỗi -> Hiển thị cảnh báo đỏ đầu trang: "Lỗi tải kết quả bài thi. Vui lòng tải lại trang!".
- **Trạng thái thành công (success state):** Confetti pháo hoa giấy rơi sinh động khi người học đỗ bài thi, Toast xanh báo "Chúc mừng bạn đã vượt qua bài thi!".

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ phòng thi Mini-exam/Level test (LN-10-S1) hoặc Mock test (LN-10-S2) sau khi học viên nộp bài (hoặc hết giờ làm bài).
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Chuyển hướng quay trở lại Learner Dashboard (LN-01).
- **Các màn hình liên quan khác:** LN-10-S1, LN-10-S2, LN-01.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0) đặc trưng.
- Thẻ Banner kết quả ở đầu sử dụng phong cách `cta-band-illustrated` màu surface-soft (#faf5e8) có bo góc lớn rounded-xl (24px) tạo cảm giác vui tươi, khích lệ.
- Biểu đồ năng lực được bo tròn góc nhẹ rounded-lg (16px) trên nền canvas trắng ấm với viền hairline mỏng 1px (#e5e5e5).
- Theo Nguyên tắc Báo hiệu (Signaling Principle), các câu trả lời sai của học viên được bôi màu đỏ của error (#ef4444) kèm dấu nhân rõ ràng để nhận biết tức thì lỗi sai, câu trả lời đúng được bôi màu xanh success (#22c55e).
- Các thẻ đề xuất ôn tập dùng màu brand-ochre nhạt để kích thích hành động tiếp theo của học viên.
- Touch target nút bấm đạt chuẩn 44px.
