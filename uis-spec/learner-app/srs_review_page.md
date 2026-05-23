# MÀN HÌNH: SRS REVIEW PAGE (MÀN HÌNH LÀM BÀI ÔN TẬP LẶP LẠI NGẮT QUÃNG)

## 1. THÔNG TIN CHUNG
- Tên màn hình: SRS Review Page (Màn hình làm bài ôn tập lặp lại ngắt quãng SRS)
- Mã use case liên quan: UC-08 (Tra cứu nhanh và ôn tập lặp lại ngắt quãng SRS)
- Mã luồng người dùng liên quan: Flow LN-FL-09 (Tra cứu nhanh & Ôn tập SRS)
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Dashboard -> Tra cứu & Ôn tập -> Click "Ôn tập ngay" -> SRS Review Page (LN-13-S1) -> Bấm Kiểm tra -> SRS Self-Evaluation View (LN-13-S2) -> Đóng tất cả -> SRS Review Result Page (LN-15) (URL: /review/run)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này để ôn tập các từ vựng và cấu trúc ngữ pháp đã học theo thuật toán lặp lại ngắt quãng (SRS), điền từ vào câu ngữ pháp khuyết dưới áp lực đồng hồ đếm ngược 10 giây, tự đánh giá mức độ ghi nhớ của bản thân, xem nhanh cứu trợ từ điển tại chỗ và xem tổng kết phiên ôn tập.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Centered card layout (Bố cục một cột căn giữa hoàn toàn) sử dụng nền canvas sáng ấm (#fffaf0) có thanh tiến độ ngang và đồng hồ đếm ngược phản xạ ở đỉnh màn hình.
- Các vùng chính trên màn hình:
  - Vùng A: Sticky Progress & Timer Bar (Thanh tiến độ và đồng hồ đếm ngược 10 giây phản xạ) ở đỉnh trang.
  - Vùng B: Thẻ học tập trung tâm (Central SRS Card Container) hiển thị câu hỏi điền từ và các nút tương tác.
  - Vùng C: Hộp thoại xem nhanh chi tiết từ vựng (SRS Detail Lookup Modal - LN-13-M1) nổi đè lên màn hình khi cần trợ giúp.
  - Vùng D: Giao diện kết quả phiên ôn (SRS Review Result Page - LN-15) hiển thị thay thế Vùng B khi học viên hoàn thành tất cả các từ trong phiên.
- Kích thước / Grid tham khảo:
  - Central Card có kích thước cố định: 700px x 420px, bo tròn góc rounded-xl (24px).
  - Lookup Modal rộng 460px căn giữa.
  - padding trong thẻ: spacing-xl (32px).
  - CSS Flexbox căn giữa dọc và ngang.

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)

### THÀNH PHẦN CHUNG (PROGRESS & REFLECTION TIMER)
- **Tên component:** Đồng hồ phản xạ 10 giây (10s Reaction Timer)
  - **Loại component tham chiếu từ DESIGN.md:** progress-bar / timer (nền surface-strong #ebe6d6, thanh thời gian màu brand-pink #ff4d8b co lại dần, height 8px)
  - **Vị trí:** Vùng A, sát cạnh đỉnh.
  - **Trạng thái:** Chạy co lại dần từ 10 giây về 0 giây. Nhấp nháy đỏ khi còn dưới 3 giây.
  - **Dữ liệu hiển thị / hành vi:** Đếm ngược thời gian phản xạ gõ đáp án. Khi về 00:00, tự động khóa trường nhập và kích hoạt kiểm tra đáp án.

---

### PHÂN HỆ LÀM BÀI ÔN TẬP (SRS REVIEW PAGE - LN-13-S1 & LN-13-S2)
- **Tên component:** Câu ngữ cảnh khuyết từ (Context Question Box)
  - **Loại component tham chiếu từ DESIGN.md:** body-strong (font Inter size 18px, weight 500, màu ink #0a0a0a, căn giữa)
  - **Vị trí:** Vùng B, thân Central Card.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị câu bối cảnh mới khuyết từ mục tiêu (ví dụ: "We need to ___________ on this project to finish it in time.").

- **Tên component:** Ô nhập đáp án ôn tập (Answer Input)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, rounded-md 12px, border 1px hairline #e5e5e5, height 44px, font Inter size 16px, căn giữa)
  - **Vị trí:** Vùng B, nằm dưới câu ngữ cảnh.
  - **Trạng thái:** Mặc định, focus, error. Tự động khóa nhập khi hết giờ.

- **Tên component:** Nút "Kiểm tra" / "Xác nhận"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, height 44px, rounded-md 12px)
  - **Vị trí:** Vùng B, dưới ô nhập liệu.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Kiểm tra". Bấm vào để chấm câu trả lời và chuyển sang giao diện tự đánh giá LN-13-S2.

- **Tên component:** Nút "Tra cứu chi tiết" (Quick Lookup Button)
  - **Loại component tham chiếu từ DESIGN.md:** button-secondary (nền canvas #fffaf0, border 1px hairline #e5e5e5, chữ ink #0a0a0a, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng B, nằm cạnh nút Kiểm tra về bên trái.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Tra cứu nhanh". Bấm vào để kích hoạt mở Modal cứu trợ LN-13-M1.

- **Tên component:** Bảng tự đánh giá ghi nhớ (SRS Self-Evaluation View - LN-13-S2)
  - **Loại component tham chiếu từ DESIGN.md:** grid 3-up (3 nút nằm ngang song song)
  - **Vị trí:** Vùng B, hiển thị thay thế nút Kiểm tra/Tra cứu sau khi nộp đáp án.
  - **Trạng thái:** Xuất hiện động.
  - **Dữ liệu hiển thị / hành vi:**
    - Hiển thị đáp án đúng chính thức (ví dụ: "**collaborate**") và phát file audio phát âm của từ.
    - 3 nút tự đánh giá mức độ nhớ:
      - *1. Nhớ rõ:* `button-primary` nền đen, chữ trắng.
      - *2. Hơi phân vân:* `button-secondary` viền hairline, nền canvas.
      - *3. Quên mất:* `button-text-link` màu error #ef4444.
    - Học viên click một nút tự đánh giá để nộp dữ liệu và chuyển sang câu tiếp theo.

---

### VÙNG C: HỘP THOẠI XEM NHANH TỪ VỰNG (SRS DETAIL LOOKUP MODAL - LN-13-M1)
- **Tên component:** Hộp thoại xem từ vựng nhanh (Popup Detail Card)
  - **Loại component tham chiếu từ DESIGN.md:** overlay / backdrop + centered card (nền surface-card #f5f0e0, bo tròn rounded-lg 16px, padding 20px, width 460px)
  - **Vị trí:** Vùng C, nổi đè lên Central Card.
  - **Trạng thái:** Xuất hiện khi bấm "Tra cứu nhanh". Đồng hồ đếm ngược 10s tạm dừng chạy khi mở popup.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị định nghĩa từ, phiên âm IPA, collocations và 1 ví dụ của từ đang ôn tập. Bấm nút "Quay lại" hoặc click ra ngoài để đóng popup, tiếp tục thời gian làm bài.

---

### VÙNG D: TRANG KẾT QUẢ PHIÊN ÔN TẬP (SRS REVIEW RESULT PAGE - LN-15)
*Vùng D xuất hiện bao phủ Central Card khi hoàn thành tất cả các thẻ trong ngày:*

- **Tên component:** Khối tổng kết phiên ôn tập (SRS Completion Banner)
  - **Loại component tham chiếu từ DESIGN.md:** cta-band-illustrated (nền surface-soft #faf5e8, rounded-xl 24px, padding 32px, căn giữa)
  - **Vị trí:** Vùng D.
  - **Trạng thái:** Mặc định. confetti rơi tự động.
  - **Dữ liệu hiển thị / hành vi:** 
    - Tiêu đề: "Hoàn thành phiên ôn tập hôm nay!" (display-md 36px, màu ink #0a0a0a).
    - Thống kê: "Đã ôn tập: 15 từ. Đánh giá: Nhớ rõ 12 từ, Quên mất 3 từ. Điểm EXP thưởng: +20 EXP".
    - Biểu đồ thống kê số từ chuyển hóa vào bộ nhớ dài hạn.

- **Tên component:** Nút "Thoát phòng ôn tập"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, height 44px, rounded-md 12px, width 280px)
  - **Vị trí:** Vùng D.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị text "Quay lại trang ôn tập". Click sẽ chuyển hướng về Personal Review Dashboard (LN-12).

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Gõ đáp án và click "Kiểm tra"**
  - **Luồng chính:** Học viên gõ "collaborate" -> Bấm "Kiểm tra" (hoặc hết 10 giây phản xạ) -> Hệ thống tự động ghi nhận đúng/sai, phát âm thanh từ vựng -> Hiển thị Bảng tự đánh giá ghi nhớ LN-13-S2 chứa 3 nút bấm -> Học viên click nút "Nhớ rõ" -> Hệ thống gửi mức độ nhớ về máy chủ để cập nhật thuật toán SRS -> Tự động chuyển sang câu tiếp theo và khởi tạo lại đồng hồ đếm ngược 10 giây.
  - **Luồng con / rẽ nhánh (Hỏi cứu trợ từ điển):** Click "Tra cứu nhanh" -> Đồng hồ đếm ngược 10s tạm dừng chạy -> Hiện Popup LN-13-M1 -> Học viên xem -> Bấm "Quay lại" -> Popup đóng, đồng hồ chạy tiếp số giây còn lại -> Học viên gõ đáp án.
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: `POST /api/srs/evaluate` (payload: `{ "wordId": 45, "rating": "easy" }` - easy tương đương Nhớ rõ, medium là Hơi phân vân, hard là Quên mất).
    - Nhận về: `{ "success": true, "nextReviewDate": "2026-05-28T17:00:00Z" }`

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Không áp dụng.
- **Trạng thái tải (loading state):** Khi chuyển tiếp giữa các câu hoặc khi nộp kết quả cuối cùng, nút bấm hiển thị spinner loading mờ.
- **Trạng thái lỗi (error state):** Khi API nộp đánh giá bị mất mạng -> Hiển thị cảnh báo đỏ viền dưới thẻ và lưu tạm kết quả vào LocalStorage để đồng bộ lại sau khi có mạng.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ Personal Review Dashboard (LN-12) sau khi học viên nhấp chọn nút "Ôn tập ngay".
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Chuyển hướng quay trở lại Personal Review Dashboard (LN-12) sau khi hoàn thành từ cuối cùng và bấm nút thoát ở trang kết quả.
- **Các màn hình liên quan khác:** LN-12, các Modal cứu trợ LN-13-M1, trang kết quả LN-15.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0) đặc trưng.
- Thẻ Central Card sử dụng phong cách `feature-card-cream` màu surface-card (#f5f0e0), viền hairline 1px (#e5e5e5) bo tròn góc bo lớn rounded-xl (24px) tạo cảm giác dễ chịu khi thực hành.
- Thanh đếm ngược 10s phản xạ sử dụng màu hồng đậm `brand-pink` (#ff4d8b) chạy co dần để tạo cảm giác áp lực thời gian phản xạ nhanh (Nguyên tắc Báo hiệu - Signaling Principle).
- Ba nút tự đánh giá ở Vùng B được sắp xếp phân cấp thị giác rõ ràng: nút "Nhớ rõ" màu đen tuyền primary nổi bật nhất để học viên dễ bấm khi làm tốt, nút "Quên mất" hiển thị dạng liên kết chữ đỏ để cảnh báo hành động đánh giá trí nhớ yếu.
- Touch target nút bấm đạt chuẩn 44px.



