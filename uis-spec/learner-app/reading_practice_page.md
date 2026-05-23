# MÀN HÌNH: READING PRACTICE PAGE (MÀN HÌNH LUYỆN ĐỌC)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Reading Practice Page (Màn hình luyện đọc)
- Mã use case liên quan: UC-06c (Luyện đọc)
- Mã luồng người dùng liên quan: Flow LN-FL-06 (Luyện tập kỹ năng Đọc)
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Dashboard -> Click Unit -> Unit Detail Page -> Click bài học Luyện Đọc -> Reading Practice Page (URL: /units/{unit_id}/lessons/{lesson_id}/reading)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này để nâng cao kỹ năng đọc hiểu qua hai hình thức: Đọc hiểu văn bản thông thường và Đọc báo chí thực tế, tích hợp công cụ tra nghĩa từ điển nhanh tại chỗ và giải đáp thắc mắc bằng Người bạn Cá Voi.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục chia đôi màn hình (Split Screen 50/50 Layout) rất phổ biến trong các đề thi đọc hiểu chuẩn quốc tế.
- Các vùng chính trên màn hình:
  - Vùng A: Thanh dẫn Breadcrumbs và tiến độ ở đầu trang.
  - Vùng B: Vùng nội dung đọc hiểu bên trái (Left Passage Panel) chứa văn bản đọc, hỗ trợ bôi đen tra cứu.
  - Vùng C: Vùng câu hỏi tương tác bên phải (Right Question Panel) chứa các câu hỏi trắc nghiệm/điền từ.
  - Vùng D: Hộp thoại xem từ điển nhanh (Popup Dictionary Tooltip) hiển thị nổi tại vị trí bôi đen văn bản.
  - Vùng E: Bảng chat Người bạn Cá Voi hỏi đáp (Cá Voi Thông Thái Side Chat Panel) trượt mở từ bên phải khi ở trang kết quả.
- Kích thước / Grid tham khảo:
  - Chia tỷ lệ màn hình 50% bên trái ( Passage Panel) và 50% bên phải (Question Panel) bằng CSS Grid 12 cột.
  - Khi xem kết quả, Vùng E (AI Panel) mở rộng chiếm 360px bên phải màn hình.
  - Khoảng cách padding trong mỗi vùng: spacing-lg (24px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)

### THÀNH PHẦN CHUNG (PROGRESS HEADER)
- **Tên component:** Thanh tiến trình đọc (Reading Progress Bar)
  - **Loại component tham chiếu từ DESIGN.md:** progress-bar (nền surface-strong #ebe6d6, thanh tiến độ xanh success #22c55e, height 8px)
  - **Vị trí:** Vùng A.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị tỉ lệ câu hỏi đã hoàn thành (ví dụ: "Câu hỏi 3 / 8").

---

### PHÂN HỆ VĂN BẢN VÀ CÂU HỎI (VÙNG B & C)

#### 1. READING COMPREHENSION MODE (LUỒNG ĐỌC HIỂU THÔNG THƯỜNG)
- **Tên component:** Vùng văn bản đọc (Passage Reader Box)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-lg 16px, padding 24px, scrollable vertical)
  - **Vị trí:** Vùng B (cột trái).
  - **Trạng thái:** Mặc định. Cho phép bôi đen hoặc double-click vào từ mới để tra cứu.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị bài đọc tiếng Anh (độ dài theo cấp độ: 500 từ đối với Basic, 1500 từ đối với Intermediate). Font chữ Inter size 16px, line-height 1.55 giúp đọc thoải mái.

- **Tên component:** Cửa sổ tra từ điển nhanh (Popup Dictionary Tooltip)
  - **Loại component tham chiếu từ DESIGN.md:** overlay / tooltip (nền surface-card #f5f0e0, border 1px hairline #e5e5e5, rounded-md 12px, padding 16px, drop shadow mờ nhẹ)
  - **Vị trí:** Vùng D, xuất hiện nổi ngay trên vị trí từ được bôi đen ở Vùng B.
  - **Trạng thái:** Ẩn mặc định, hiển thị khi người học bôi đen một từ.
  - **Dữ liệu hiển thị / hành vi:** 
    - Hiển thị từ vựng, phiên âm IPA (ví dụ: "Fascinating /ˈfæs.ən.eɪ.tɪŋ/").
    - Định nghĩa ngắn: "Hấp dẫn, lôi cuốn".
    - Nút "Lưu từ vào SRS" (`button-primary` dạng nhỏ).

- **Tên component:** Khối câu hỏi đọc hiểu (Question Board)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền surface-card #f5f0e0, border 1px hairline #e5e5e5, rounded-lg 16px, padding 24px, scrollable)
  - **Vị trí:** Vùng C (cột phải).
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Danh sách các câu hỏi điền từ vào chỗ trống hoặc trắc nghiệm A, B, C, D. Học viên điền/chọn đáp án trực tiếp.

#### 2. NEWS-BASED LEARNING MODE (LUỒNG ĐỌC BÁO CHÍ THỰC TẾ)
- **Tên component:** Văn bản báo chí đã lọc từ nhiễu (Filtered News Article)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Mặc định. Các từ vựng quá phức tạp ngoài cấp độ học (nhiễu) được hệ thống tự động làm mờ nhẹ hoặc thay thế bằng từ đồng nghĩa tương ứng.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị bài báo thực tế kèm hình ảnh 3D claymation minh họa ở đầu bài báo.

- **Tên component:** Câu hỏi phân tích sâu (Deep Analytical Questions)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream
  - **Vị trí:** Vùng C.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị câu hỏi phân tích thái độ/quan điểm tác giả, hoặc câu hỏi ghép tiêu đề đoạn văn (Matching Headings).

---

### TRANG KẾT QUẢ & HỎI AI (READING RESULT PAGE)
- **Tên component:** Bảng tổng hợp kết quả đọc hiểu
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card
  - **Vị trí:** Vùng C (thay thế Question Board khi kết thúc).
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Chấm điểm tự động, hiển thị số câu đúng/sai, bôi màu xanh lá cho câu trả lời đúng của học viên, bôi đỏ câu sai kèm đáp án đúng chính thức và giải thích chi tiết của Admin.

- **Tên component:** Khung chat Người bạn Cá Voi (Cá Voi Thông Thái Side Chat Panel)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-ochre (nền brand-ochre #e8b94a nhạt, border-left 1px hairline #e5e5e5, padding 20px)
  - **Vị trí:** Vùng E (bên phải).
  - **Trạng thái:** Hiển thị ở trang kết quả.
  - **Dữ liệu hiển thị / hành vi:** Khung chat giúp học viên gõ câu hỏi để AI giải thích các cấu trúc ngữ pháp/từ vựng khó xuất hiện trong bài đọc.

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Bôi đen một từ mới trong bài đọc để tra cứu**
  - **Luồng chính:** Học viên bôi đen từ "fascinating" ở Vùng B -> Popup Dictionary Tooltip Vùng D tự động hiển thị nổi -> Học viên xem nghĩa -> Click nút "Lưu từ" -> Từ được đưa vào SRS -> Popup đóng lại khi click ra ngoài.
- **Hành động: Click nộp bài đọc ở Vùng D**
  - **Luồng chính:** Học viên hoàn thành tất cả câu hỏi -> Click "Nộp bài" -> Hệ thống chấm điểm -> Chuyển Vùng C sang hiển thị trang kết quả chi tiết -> Toast thông báo thành công xanh lá -> Cá Voi Thông Thái Chat Panel mở rộng ở Vùng E.
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: `{ "userId": 105, "lessonId": 26, "answers": { "q1": "A", "q2": "collaborate" } }`
    - Nhận về: `{ "score": 90, "correctCount": 9, "totalCount": 10, "details": { "q1": { "isCorrect": true, "correctAnswer": "A", "explanation": "..." } } }`

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Không áp dụng.
- **Trạng thái tải (loading state):** Khi đang tải bài đọc từ máy chủ, Vùng B và Vùng C hiển thị các khối xám nhấp nháy skeleton.
- **Trạng thái lỗi (error state):** Khi tải bài đọc bị lỗi mạng -> Hiển thị text cảnh báo đỏ "Lỗi tải bài đọc. Vui lòng nhấn nút thử lại!".
- **Trạng thái thành công (success state):** Trang kết quả hiển thị điểm EXP cộng thêm và Toast báo nộp bài thành công.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ Unit Detail Page (LN-02) sau khi học viên click bài luyện đọc.
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Quay trở lại màn hình Unit Detail Page (LN-02) khi học viên bấm nút "Hoàn thành bài đọc".
- **Các màn hình liên quan khác:** LN-02, Popup từ điển LN-13-M1.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0) đặc trưng.
- Split screen chia đôi 50/50 tạo cảm giác thoải mái khi vừa đối chiếu văn bản vừa làm câu hỏi mà không cần cuộn trang lên xuống nhiều lần (tránh quá tải nhận thức).
- Popup từ điển nhanh được thiết kế bo tròn nhẹ rounded-md (12px) trên nền surface-card (#f5f0e0), không dùng bóng đổ đen thô ráp mà chỉ có viền hairline tinh tế (#e5e5e5).
- Các từ được tra cứu thành công và lưu vào SRS được highlight màu brand-mint (#a4d4c5) nhạt trong văn bản để biểu thị trạng thái đã lưu theo Nguyên tắc Báo hiệu (Signaling Principle).
- Touch target của các đáp án trắc nghiệm và nút lưu tối thiểu 44px.



