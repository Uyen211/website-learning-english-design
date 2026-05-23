# MÀN HÌNH: MOCK TEST ROOM (GIAO DIỆN LÀM BÀI THI THỬ IELTS / TOEIC)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Mock test Room (Giao diện làm bài thi thử IELTS/TOEIC)
- Mã use case liên quan: UC-07 (Làm bài thi đánh giá năng lực)
- Mã luồng người dùng liên quan: Flow LN-FL-08 (Thực hiện bài thi đánh giá năng lực)
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Dashboard -> Unit Detail -> Pre-test Setup Page -> Mock test Room (URL: /exams/mock/{mock_id}/run)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này để trải qua phiên thi thử quốc tế toàn diện (IELTS hoặc TOEIC) chạy tuần tự qua 4 kỹ năng (Nghe, Đọc, Viết, Nói) dưới sự giám sát nghiêm ngặt của hệ thống tính giờ và thu âm tự động.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục thay đổi linh hoạt theo từng phần thi (Dynamic Phase Layout) trên nền canvas sáng ấm (#fffaf0) có thanh Sticky Action Header ghim đầu trang.
  - *Listening Section View:* Một cột cuộn dọc, bảng câu hỏi chiếm vị trí trung tâm.
  - *Reading Section View:* Chia đôi màn hình 50/50 (bài đọc bên trái, câu hỏi bên phải).
  - *Writing Section View:* Chia đôi màn hình 40/60 (đề bài viết bên trái, khung nhập văn bản lớn bên phải).
  - *Speaking Section View:* Bố cục một cột căn giữa tối giản chứa avatar giám khảo AI, soundwave sóng âm nhấp nháy và thanh đếm ngược.
- Các vùng chính trên màn hình:
  - Vùng A: Sticky Exam Header (Thanh đầu trang cố định) chứa tên kỹ năng đang thi, đồng hồ đếm ngược của phần đó và nút "Hủy thi".
  - Vùng B: Vùng nội dung thi chính (Central Test Workbench) hiển thị văn bản, audio hoặc avatar tùy thuộc phần thi.
  - Vùng C: Vùng nhập câu trả lời (Answer sheet/Editor).
  - Vùng D: Các hộp thoại lớp phủ (Modals) hiển thị cảnh báo khi xảy ra sự cố thiết bị hoặc yêu cầu thoát.
- Kích thước / Grid tham khảo:
  - Chiều rộng tối đa của workbench: 1200px.
  - Căn giữa dọc và ngang bằng CSS Flexbox cho các phần thi nghe, viết, nói.
  - Phần thi Reading chia đôi 50/50 bằng CSS Grid 12 cột.

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)

### THÀNH PHẦN CHUNG (STICKY HEADER)
- **Tên component:** Thanh công cụ thi thử (Mock Test Header)
  - **Loại component tham chiếu từ DESIGN.md:** top-nav (nền canvas #fffaf0, height 64px, border-bottom 1px hairline #e5e5e5)
  - **Vị trí:** Vùng A.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** 
    - Bên trái: Tên bài thi (ví dụ: "IELTS Mock Test #1") và tên phần thi (Badge: "LISTENING SECTION", "READING SECTION", v.v.).
    - Ở giữa: Đồng hồ đếm ngược của phần thi hiện tại (Countdown Clock). Ví dụ: Listening đếm ngược 40 phút.
    - Bên phải: Nút "Hủy thi" (`button-text-link` màu error #ef4444). Nhấp vào kích hoạt Modal LN-11-M1.

---

### PHẦN THI 1: LISTENING SECTION VIEW
- **Tên component:** Trình phát file audio đề Listening
  - **Loại component tham chiếu từ DESIGN.md:** audio-player (bị ẩn hoặc vô hiệu hóa điều khiển)
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Tự động phát ngay khi vào phòng. Toàn bộ nút tạm dừng, tua nhạc, tua lùi bị khóa cứng hoàn toàn (disabled).
  - **Dữ liệu hiển thị / hành vi:** Phát file audio bài thi Listening tổng độ dài khoảng 30-40 phút.

- **Tên component:** Phiếu trả lời Listening (Listening Question Sheet)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền surface-card #f5f0e0, bo góc rounded-lg 16px, padding 20px)
  - **Vị trí:** Vùng C.
  - **Trạng thái:** Mặc định. Tự động khóa trường nhập khi hết giờ hoặc audio phát xong.

---

### PHẦN THI 2: READING SECTION VIEW
- **Tên component:** Đoạn văn đọc hiểu (Reading Passages Tab)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền canvas #fffaf0, rounded-lg 16px, padding 24px, scrollable vertical)
  - **Vị trí:** Vùng B (bên trái).
  - **Trạng thái:** Mặc định. Cho phép click các Tab "Passage 1", "Passage 2", "Passage 3" ở đầu để chuyển đổi văn bản đọc.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị bài đọc IELTS dài. Trình duyệt bị khóa tính năng tra từ điển nhanh (khác với Reading Practice Room).

- **Tên component:** Phiếu trả lời Reading (Reading Question Sheet)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền surface-card #f5f0e0, padding 24px)
  - **Vị trí:** Vùng C (bên phải).
  - **Trạng thái:** Mặc định. Tự động khóa khi hết giờ.

---

### PHẦN THI 3: WRITING SECTION VIEW
- **Tên component:** Đề bài viết (Writing Prompts)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền surface-card #f5f0e0, padding 24px)
  - **Vị trí:** Vùng B (bên trái).
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị đề thi Task 1 và Task 2 (đối với IELTS) hoặc đề thư tín (đối với TOEIC).

- **Tên component:** Khung viết bài luận (Essay Writing Editor)
  - **Loại component tham chiếu từ DESIGN.md:** text-area (nền canvas #fffaf0, rounded-md 12px, border 1px hairline #e5e5e5, height 400px, padding 24px)
  - **Vị trí:** Vùng C (bên phải).
  - **Trạng thái:** Mặc định, focus. Bị tắt tự động sửa chính tả của trình duyệt. Dưới góc hiển thị bộ đếm số từ (Word Counter).

---

### PHẦN THI 4: SPEAKING SECTION VIEW
- **Tên component:** Khung thử micro (Mic Test Card)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền surface-card #f5f0e0, rounded-xl 24px, padding 24px, width 500px, căn giữa)
  - **Vị trí:** Vùng B, hiển thị đầu phần thi Speaking.
  - **Trạng thái:** Xuất hiện động.
  - **Dữ liệu hiển thị / hành vi:** Yêu cầu học viên nói thử một câu: "Đọc to câu này để kiểm tra Micro: 'I am ready to start the Speaking test.'". Hiển thị vạch đo âm lượng. Đạt yêu cầu sẽ tự động bắt đầu phần thi nói.

- **Tên component:** Giám khảo AI (AI Examiner Card)
  - **Loại component tham chiếu từ DESIGN.md:** hero-illustration-card (nền surface-soft #faf5e8, rounded-xl 24px)
  - **Vị trí:** Vùng B, trung tâm.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị hình ảnh mascot 3D của giám khảo AI DiveVerse. Tự động phát âm thanh câu hỏi của giám khảo AI.

- **Tên component:** Thanh thu âm & Sóng âm (Soundwave Recording Status)
  - **Loại component tham chiếu từ DESIGN.md:** progress-bar / soundwave (nền primary #0a0a0a, soundwave sóng âm màu đỏ #ef4444 nhấp nháy chuyển động)
  - **Vị trí:** Vùng C, nằm dưới hình ảnh giám khảo.
  - **Trạng thái:** Xuất hiện động ngay sau khi file câu hỏi audio của giám khảo phát hết.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị thanh soundwave dao động theo giọng nói của học viên biểu thị đang thu âm, bên cạnh có đồng hồ đếm ngược thời gian nói cho câu hỏi đó (ví dụ: đếm ngược 2 phút cho IELTS Part 2).

---

### VÙNG D: CÁC HỘP THOẠI LỚP PHỦ CẢNH BÁO (MODALS)
- **Tên component:** Hộp thoại Cảnh báo hủy thi (Exit Warning Modal - LN-11-M1)
  - **Loại component tham chiếu từ DESIGN.md:** overlay / backdrop + centered alert card (width 420px)
  - **Vị trí:** Vùng D.
  - **Trạng thái:** Xuất hiện khi học viên bấm "Hủy thi" hoặc cố tình tắt trình duyệt.
  - **Dữ liệu hiển thị / hành vi:** Tiêu đề "Hủy thi giữa chừng?". Cảnh báo kết quả thi sẽ bị hủy bỏ hoàn toàn và tính trượt bài thi. Nhấp "Xác nhận hủy" sẽ thoát phòng thi về LN-01; nhấp "Tiếp tục" đóng modal.

- **Tên component:** Hộp thoại Lỗi Microphone khi thi (Speaking Mic Error Modal - LN-11-M2)
  - **Loại component tham chiếu từ DESIGN.md:** overlay / backdrop + centered alert card (width 420px)
  - **Vị trí:** Vùng D.
  - **Trạng thái:** Xuất hiện trong phần thi Speaking nếu micro bị mất quyền truy cập hoặc hỏng đột ngột.
  - **Dữ liệu hiển thị / hành vi:** Tiêu đề "Lỗi thiết bị Microphone" (màu error #ef4444). Dòng mô tả: "Không phát hiện thấy microphone hoạt động hoặc trình duyệt bị chặn quyền truy cập micro. Không thể tiếp tục phần thi Speaking. Hệ thống bắt buộc phải hủy kết quả làm bài của cả bài thi Mock Test này.". Nút bấm: "Xác nhận hủy bài thi" (`button-primary` màu đen).

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Chuyển phần thi tự động (Listening -> Reading -> Writing -> Speaking)**
  - **Luồng chính:**
    1. Phần thi Listening kết thúc (hết giờ hoặc hết file nghe) -> Hệ thống tự động lưu kết quả tạm thời -> Khóa ô nhập -> Tự động chuyển hướng hiển thị sang giao diện Reading Section View.
    2. Phần thi Reading kết thúc (hết giờ 60 phút) -> Tự động khóa -> Lưu kết quả -> Tự động chuyển hướng sang Writing Section View.
    3. Phần thi Writing kết thúc (hết giờ 60 phút) -> Tự động khóa -> Lưu kết quả -> Tự động chuyển hướng sang Speaking Section View.
    4. Phần thi Speaking bắt đầu bằng bước thử mic. Sau khi hoàn thành câu hỏi nói Speaking cuối cùng -> Hệ thống tự động nộp toàn bộ dữ liệu làm bài và gửi lên API chấm điểm -> Chuyển hướng sang Test Result Page (LN-11).
- **Hành động: Trả lời câu hỏi Nói trong phần Speaking**
  - **Luồng chính:** Giám khảo AI phát audio câu hỏi -> Audio kết thúc -> Micro tự động bật ghi âm -> Soundwave sóng âm nhấp nháy -> Học viên nói -> Click nút "Nộp câu trả lời" để nộp sớm (hoặc hết giờ nói tự nộp) -> Ghi âm tự động dừng, lưu tệp audio tạm thời -> Tự động chuyển sang câu hỏi nói tiếp theo.
  - **Luồng con / rẽ nhánh (Học viên giữ im lặng - Rẽ nhánh E-3):** Trong suốt thời gian đếm ngược ghi âm, hệ thống phát hiện cường độ âm bằng 0 -> Tự động dừng ghi âm, lưu file audio trống, ghi nhận 0 điểm cho câu hỏi đó -> Tự động chuyển sang câu hỏi nói tiếp theo.
  - **Luồng con / rẽ nhánh (Lỗi mic khi nói - Rẽ nhánh E-2):** Đang nói micro bị ngắt kết nối đột ngột -> Hệ thống hiển thị Modal LN-11-M2 -> Học viên bấm xác nhận -> Hủy kết quả toàn bộ bài Mock Test -> Quay lại danh sách bài thi.
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: `POST /api/mock-test/submit` (payload gồm toàn bộ tệp ghi âm nói, văn bản bài luận viết, đáp án nghe đọc).
    - Nhận về: `{ "success": true, "resultId": 509 }`

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Không áp dụng.
- **Trạng thái tải (loading state):** Khi chuyển giao giữa các phần thi hoặc đang nộp đề thi cuối bài, màn hình hiển thị trạng thái loading spinner và dòng chữ thông báo tương ứng.
- **Trạng thái lỗi (error state):** Lỗi micro đột ngột hiển thị Modal lỗi LN-11-M2.
- **Trạng thái thành công (success state):** Nộp bài thành công tự động dẫn sang Test Result Page (LN-11).

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ Pre-test Setup Page (LN-09) sau khi học viên chọn chế độ "Thi thật" của Mock Test và bấm nút "Bắt đầu làm bài".
- **Sau khi hoàn thành hành động, đi đến màn hình nào?**
  - Chuyển sang Test Result Page (LN-11) sau khi hoàn thành câu nói Speaking cuối cùng.
  - Chuyển sang Learner Dashboard (LN-01) khi học viên xác nhận hủy bài thi giữa chừng.
- **Các màn hình liên quan khác:** LN-09, LN-11, các Modal cảnh báo LN-11-M1 và LN-11-M2.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0) đặc trưng.
- Thiết kế giao diện thay đổi linh hoạt theo từng phần thi để phù hợp với định dạng thi thực tế (ví dụ: Reading chia đôi màn hình 50/50 giúp đối chiếu văn bản, Speaking hiển thị avatar giám khảo AI lớn ở trung tâm để tăng tính mô phỏng tương tác thực tế).
- Theo Nguyên tắc Báo hiệu (Signaling Principle), sóng âm soundwave màu đỏ rực (#ef4444) nhấp nháy biểu thị micro đang thu âm để nhắc nhở học viên tập trung nói, đồng hồ đếm ngược to rõ ở Sticky Header giúp theo dõi thời gian dễ dàng.
- Khóa toàn bộ các nút tua nhạc trong phần thi Listening để đảm bảo tính công bằng nghiêm ngặt của kỳ thi thử.
- Touch target của nút nộp và các đáp án trắc nghiệm tối thiểu 44px.
