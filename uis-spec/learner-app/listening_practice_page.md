# MÀN HÌNH: LISTENING PRACTICE PAGE (MÀN HÌNH LUYỆN NGHE)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Listening Practice Page (Màn hình luyện nghe)
- Mã use case liên quan: UC-06a (Luyện nghe)
- Mã luồng người dùng liên quan: Flow LN-FL-04 (Luyện tập kỹ năng Nghe)
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Dashboard -> Click Unit -> Unit Detail Page -> Click bài học Luyện Nghe -> Listening Practice Page (URL: /units/{unit_id}/lessons/{lesson_id}/listening)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này để rèn luyện kỹ năng nghe hiểu tiếng Anh qua 3 hình thức luyện tập phong phú: nghe truyện tương tác, trắc nghiệm nghe hiểu đa dạng giọng nói (accents), và luyện nói đuổi (Shadowing), sau đó xem kết quả chi tiết và tương tác giải đáp trực tiếp với trợ lý AI.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục cột kép linh hoạt (Split View Layout). 
  - Khi luyện tập: Vùng chính ở giữa hiển thị trình phát và câu hỏi.
  - Khi xem kết quả: Bên trái hiển thị transcript và câu trả lời; bên phải là khung chat trợ lý AI (Side Chat Panel) có thể thu gọn.
- Các vùng chính trên màn hình:
  - Vùng A: Thanh tiến độ và ghim đầu trang (Header Progress Bar).
  - Vùng B: Vùng tương tác luyện nghe chính (Central Listening Player & Questions Area) có nội dung thay đổi theo 3 chế độ (Interactive Stories, Quiz, Shadowing).
  - Vùng C: Bảng trợ lý AI hỏi đáp (Side AI Chat Panel) ở bên phải màn hình khi hiển thị trang kết quả.
  - Vùng D: Thanh điều hướng hành động ở chân trang (Footer Toolbar).
- Kích thước / Grid tham khảo:
  - Vùng B (Vùng tương tác chính) chiếm chiều rộng 800px khi học.
  - Khi hiện ZPD AI Chat Panel ở trang kết quả: Chia tỷ lệ 7:5 (Vùng chính 720px, AI Panel 380px) trên lưới 12 cột.
  - Khoảng cách padding trong thẻ: spacing-xl (32px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)

### THÀNH PHẦN CHUNG (PROGRESS HEADER)
- **Tên component:** Thanh tiến trình nghe (Listening Progress Bar)
  - **Loại component tham chiếu từ DESIGN.md:** progress-bar (nền surface-strong #ebe6d6, thanh tiến độ xanh success #22c55e, height 8px)
  - **Vị trí:** Vùng A, sát cạnh đỉnh.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị vị trí phần bài nghe đang thực hiện (ví dụ: "Đoạn 2 / 5" hoặc "Câu hỏi 4 / 10").

---

### CẤU HÌNH CÁC CHẾ ĐỘ LUYỆN TẬP (VÙNG B)

#### 1. INTERACTIVE STORIES MODE (GIAO DIỆN NGHE TRUYỆN TƯƠNG TÁC)
- **Tên component:** Trình phát phân đoạn truyện (Audio Player Segment)
  - **Loại component tham chiếu từ DESIGN.md:** rounded-full (nền primary #0a0a0a, màu chữ on-primary #ffffff, touch target 48x48px)
  - **Vị trí:** Vùng B, trung tâm.
  - **Trạng thái:** Mặc định. Tự động dừng ở cuối phân đoạn.
  - **Dữ liệu hiển thị / hành vi:** Phát âm thanh đoạn truyện ngắn (ví dụ: 20-30 giây). Người học bắt buộc phải nghe hết đoạn mới hiển thị câu hỏi mở khóa.

- **Tên component:** Câu hỏi mở khóa đoạn (Unlocking Question Card)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền surface-card #f5f0e0, border 1px hairline #e5e5e5, rounded-lg 16px, padding 20px)
  - **Vị trí:** Vùng B, xuất hiện dưới player sau khi audio dừng.
  - **Trạng thái:** Xuất hiện động.
  - **Dữ liệu hiển thị / hành vi:** Câu hỏi trắc nghiệm hoặc kéo thả từ để kiểm tra thông tin vừa nghe. Học viên phải chọn đáp án đúng để mở khóa nghe tiếp đoạn truyện sau.

#### 2. AUDIO COMPREHENSION QUIZ MODE (GIAO DIỆN TRẮC NGHIỆM NGHE HIỂU)
- **Tên component:** Bảng điều khiển Audio (Audio Controls Dashboard)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền surface-card #f5f0e0, rounded-lg 16px, padding 24px)
  - **Vị trí:** Vùng B, phía trên.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** 
    - Nút Play/Pause.
    - Thanh tua âm thanh (seeker bar).
    - Dropdown chọn Tốc độ phát (0.75x, 1.0x, 1.25x, 1.5x).
    - Dropdown chọn Accent phát âm (UK Accent / US Accent / Australian Accent).

- **Tên component:** Lưới câu hỏi nghe hiểu (Quiz Sheet)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (padding 20px, khoảng cách giữa các câu spacing-md 16px)
  - **Vị trí:** Vùng B, dưới player.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Danh sách các câu hỏi điền khuyết cụm từ hoặc trắc nghiệm A, B, C, D dựa theo nội dung bài nghe dài (1-2 phút đối với Basic, 3-5 phút đối với Intermediate).

#### 3. SHADOWING MODE (GIAO DIỆN LUYỆN NÓI ĐUỔI)
- **Tên component:** Danh sách câu thoại (Transcript Timed Lines)
  - **Loại component tham chiếu từ DESIGN.md:** vertical list (các câu thoại xếp dọc, mỗi câu cách nhau 12px)
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Mặc định. Câu thoại đang phát sáng nhẹ màu brand-peach (#ffb084) nhạt.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị transcript tiếng Anh chia theo câu thoại có timestamp (ví dụ: "00:12 - 00:15: I am working on the database."). Đầu dòng có nút icon loa nhỏ để nghe riêng câu đó, cuối dòng có icon Micro.

- **Tên component:** Nút Ghi âm nói đuổi (Microphone Shadowing Button)
  - **Loại component tham chiếu từ DESIGN.md:** rounded-full (đường kính 48px, nền primary #0a0a0a, chữ trắng)
  - **Vị trí:** Vùng B, nằm ở cuối mỗi câu thoại.
  - **Trạng thái:** Mặc định, đang ghi âm (soundwave sóng âm đỏ nhấp nháy), đang tải AI chấm điểm.
  - **Dữ liệu hiển thị / hành vi:** Bấm giữ hoặc nhấp vào để thu âm giọng nói của người học nói đuổi theo câu thoại đó.

- **Tên component:** Kết quả phát âm từ đơn (Word-by-word Coloring)
  - **Loại component tham chiếu từ DESIGN.md:** text-span (màu sắc thay đổi theo điểm phát âm)
  - **Vị trí:** Hiển thị đè lên văn bản câu thoại sau khi AI chấm xong.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:**
    - Từ phát âm đúng: màu success (#22c55e) xanh lá.
    - Từ phát âm sai: màu error (#ef4444) đỏ gạch, rê chuột vào hiển thị gợi ý phát âm IPA đúng và lời giải thích.

---

### GIAI ĐOẠN 4: TRANG KẾT QUẢ & HỎI AI (LISTENING RESULT PAGE)
- **Tên component:** Bảng kết quả đúng sai (Listening Result Table)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền canvas #fffaf0, rounded-lg 16px, padding 20px)
  - **Vị trí:** Vùng B, hiển thị ở trang kết quả.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị tổng số câu trả lời đúng (ví dụ: "Điểm số: 8 / 10 câu đúng (+10 EXP)"). Hiển thị lại toàn bộ câu hỏi kèm tích xanh cho câu đúng, dấu nhân đỏ cho câu sai cùng đáp án và lời giải thích chi tiết của Admin.

- **Tên component:** Nút "Lưu từ vựng" nhanh (Quick Save to SRS)
  - **Loại component tham chiếu từ DESIGN.md:** badge-pill (nền #f5f0e0, border 1px hairline #e5e5e5, rounded-pill)
  - **Vị trí:** Vùng B, nằm cạnh các từ mới được bôi đậm trong transcript.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Icon dấu cộng và chữ "Lưu từ". Học viên nhấp chọn sẽ tự động đưa từ vựng đó vào danh sách ôn tập SRS cá nhân.

- **Tên component:** Khung chat Trợ lý AI (ZPD AI Side Chat Panel)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-ochre (nền brand-ochre #e8b94a nhạt, border-left 1px hairline #e5e5e5, padding 20px, height 100% dọc)
  - **Vị trí:** Vùng C, hiển thị ở bên phải.
  - **Trạng thái:** Mặc định ở trang kết quả.
  - **Dữ liệu hiển thị / hành vi:**
    - Khung chứa lịch sử chat hiển thị các giải đáp ngữ pháp.
    - Ô nhập câu hỏi (text-input) ở dưới cùng: "Hỏi trợ lý AI giải thích câu này...".
    - Nút gửi chat.

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Trả lời trắc nghiệm mở khóa (Interactive Stories)**
  - **Luồng chính:** Học viên nghe hết đoạn audio -> Audio dừng, câu hỏi xuất hiện -> Chọn đáp án đúng -> Bấm "Tiếp tục" -> Hệ thống hiện thông báo chính xác -> Mở khóa đoạn tiếp theo và tự động phát audio đoạn kế tiếp.
  - **Luồng con / rẽ nhánh (Chọn sai):** Chọn sai -> Báo đỏ viền câu hỏi, hiện nút "Nghe lại đoạn này" -> Học viên bấm để phát lại âm thanh phân đoạn đó và chọn lại.
- **Hành động: Thực hiện ghi âm Shadowing**
  - **Luồng chính:** Học viên nhấp icon Micro bên cạnh câu thoại -> Sóng âm soundwave nhấp nháy -> Học viên nói -> Bấm dừng ghi âm -> Hệ thống hiển thị trạng thái loading chấm điểm -> Sau 2 giây, hiển thị màu xanh/đỏ đè lên transcript.
- **Hành động: Nhập câu hỏi và gửi Chat AI**
  - **Luồng chính:** Học viên nhập câu hỏi vào ô chat (ví dụ: "Tại sao ở phút 01:23 lại dùng thì Quá khứ hoàn thành?") -> Click nút gửi -> AI nhận dữ liệu ngữ cảnh bài nghe -> Phản hồi giải thích chi tiết trong vòng 2 giây.
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: `{ "userId": 105, "lessonId": 24, "userQuestion": "Giải thích cấu trúc 'had gone' trong câu..." }`
    - Nhận về: `{ "success": true, "aiResponse": "Trong câu này, 'had gone' được dùng vì..." }`

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Không áp dụng.
- **Trạng thái tải (loading state):** Khi đang tải dữ liệu âm thanh hoặc gửi file ghi âm Shadowing lên máy chủ -> Nút micro hoặc player hiển thị spinner xoay mờ, tạm khóa click.
- **Trạng thái lỗi (error state):** Khi API AI bị ngắt kết nối trong khung chat -> Chatbox hiển thị thông báo: "Trợ lý AI tạm thời mất kết nối. Bạn có thể xem lời giải thích chi tiết của Admin phía dưới!".
- **Trạng thái thành công (success state):** Trang kết quả hiển thị tổng kết EXP đạt được, Toast xanh báo "Nộp bài nghe thành công!".

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ Unit Detail Page (LN-02) sau khi học viên nhấp chọn bài luyện nghe.
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Chuyển hướng quay trở lại Unit Detail Page (LN-02) khi học viên bấm nút "Hoàn thành bài học" ở dưới trang kết quả.
- **Các màn hình liên quan khác:** LN-02.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0).
- Các khối nội dung sử dụng màu surface-card (#f5f0e0), viền hairline 1px (#e5e5e5) bo tròn rounded-lg (16px) hoặc rounded-xl (24px).
- Nút loa và uploader có các góc bo tròn mềm mại rounded-md (12px) tạo cảm giác sờ nắn được như phong cách Clay.com.
- Theo Nguyên tắc Báo hiệu (Signaling Principle), các từ phát âm sai trong phần Shadowing được tô đỏ gạch chân wavy, từ đúng tô xanh lá rõ ràng để người học nhận biết lỗi ngay tức khắc.
- Khung chat AI ZPD ở bên phải dùng màu vàng ấm của brand-ochre để phân tách trực quan với vùng xem transcript kết quả.
- Touch target nút bấm đạt chuẩn 44px.
