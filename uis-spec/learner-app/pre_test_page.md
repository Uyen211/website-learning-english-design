# MÀN HÌNH: PRE-TEST SETUP PAGE (MÀN HÌNH THIẾT LẬP TRƯỚC KHI THI)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Pre-test Setup Page (Màn hình thiết lập trước khi thi)
- Mã use case liên quan: UC-07 (Làm bài thi đánh giá năng lực)
- Mã luồng người dùng liên quan: Flow LN-FL-08 (Thực hiện bài thi đánh giá năng lực)
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Dashboard -> Click Unit -> Unit Detail Page -> Click Bài thi -> Pre-test Setup Page (URL: /units/{unit_id}/exams/{exam_id}/setup)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Người học sử dụng màn hình này để đọc cấu trúc đề thi, số lượng câu hỏi, thời gian quy định, lựa chọn chế độ làm bài (Tập dượt hoặc Thi thật) trước khi chính thức nhấn nút bắt đầu làm bài thi.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Centered card layout (Bố cục một cột căn giữa hoàn toàn) sử dụng nền canvas sáng ấm (#fffaf0).
- Các vùng chính trên màn hình:
  - Vùng A: Breadcrumbs điều hướng và tiêu đề trang ở chính giữa phía trên.
  - Vùng B: Thẻ thông tin đề thi (Test Spec Card) hiển thị chi tiết số câu, thời gian và cấu trúc đề.
  - Vùng C: Bảng chọn Chế độ làm bài (Exam Mode Selector Grid) hiển thị hai tùy chọn song song.
  - Vùng D: Nút hành động "Bắt đầu làm bài" (Start Action Box) nằm ở dưới cùng.
- Kích thước / Grid tham khảo:
  - Chiều rộng tối đa của Central Card: 680px.
  - Căn giữa dọc và ngang bằng CSS Flexbox.
  - Khoảng cách padding trong thẻ: spacing-xl (32px).
  - Khoảng cách dọc giữa các phân đoạn: spacing-lg (24px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)
- **Tên component:** Thanh dẫn Breadcrumbs
  - **Loại component tham chiếu từ DESIGN.md:** body-sm (màu muted #6a6a6a)
  - **Vị trí:** Vùng A, góc trên bên trái.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị dòng text: "Lộ trình học / Unit 2 / Bài thi cuối khóa". Nhấp chọn "Lộ trình học" để quay lại LN-01.

- **Tên component:** Tiêu đề bài thi (Exam Title)
  - **Loại component tham chiếu từ DESIGN.md:** display-md (Plain Black display typeface, font Inter weight 500, size 36px, letter-spacing -1px)
  - **Vị trí:** Vùng A, nằm dưới Breadcrumbs.
  - **Trạng thái:** Mặc định, màu chữ ink (#0a0a0a).
  - **Dữ liệu hiển thị / hành vi:** Hiển thị tên bài thi (ví dụ: "Mini-exam cuối Unit 2: Everyday Work").

- **Tên component:** Thẻ thông tin đề thi (Test Spec Card)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền surface-card #f5f0e0, border 1px hairline #e5e5e5, rounded-xl 24px, padding 24px)
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị các thông tin chi tiết:
    - *Số lượng câu hỏi:* "40 câu hỏi".
    - *Thời gian làm bài:* "30 phút".
    - *Điểm tối đa:* "100 EXP".
    - *Cấu trúc đề:* "15 câu Từ vựng, 15 câu Ngữ pháp, 5 câu Đọc hiểu, 5 câu Nghe hiểu".
    - *Điểm đỗ yêu cầu:* "Tối thiểu 50 EXP để vượt qua Unit".

- **Tên component:** Chế độ làm bài "Tập dượt" (Practice Mode Option)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-lg 16px, padding 16px, cursor pointer)
  - **Vị trí:** Vùng C, nằm bên trái.
  - **Trạng thái:** Mặc định (chưa chọn), active (viền đen đậm 2px primary #0a0a0a, nền surface-card #f5f0e0).
  - **Dữ liệu hiển thị / hành vi:** Hiển thị tiêu đề "Tập dượt" (Inter 16px weight 600) và mô tả: "Không giới hạn thời gian, có thể xem ngay giải thích đáp án sau mỗi câu hỏi. Kết quả không lưu vào học bạ.".

- **Tên component:** Chế độ làm bài "Thi thật" (Real Exam Mode Option)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-lg 16px, padding 16px, cursor pointer)
  - **Vị trí:** Vùng C, nằm bên phải.
  - **Trạng thái:** Mặc định, active (viền đen đậm 2px primary #0a0a0a, nền surface-card #f5f0e0).
  - **Dữ liệu hiển thị / hành vi:** Hiển thị tiêu đề "Thi thật" (Inter 16px weight 600) và mô tả: "Có đếm ngược thời gian nghiêm ngặt, tự động nộp bài khi hết giờ. Kết quả được ghi nhận chính thức để mở khóa Unit mới.".

- **Tên component:** Nút "Bắt đầu làm bài"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, font Inter size 15px, weight 600, rounded-md 12px, height 44px, width 100%)
  - **Vị trí:** Vùng D.
  - **Trạng thái:** Mặc định, hover, disabled (nếu chưa chọn chế độ).
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Bắt đầu làm bài". Nhấp chọn sẽ kích hoạt tải đề thi và chuyển hướng sang giao diện phòng thi tương ứng.

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Chọn Chế độ làm bài**
  - **Luồng chính:** Học viên click vào một trong hai thẻ ở Vùng C -> Thẻ đó chuyển sang trạng thái Active (viền dày lên màu đen, nền ngả vàng nhạt), thẻ còn lại chuyển về mặc định -> Nút "Bắt đầu làm bài" ở Vùng D chuyển sang trạng thái kích hoạt (mặc định chọn sẵn "Thi thật").
- **Hành động: Nhấp nút "Bắt đầu làm bài"**
  - **Luồng chính:** Học viên click nút -> Hệ thống gửi API khởi tạo phiên thi -> Thành công -> Chuyển hướng sang màn hình phòng thi:
    - Nếu đề thi là Mini-exam hoặc Level test -> Chuyển sang màn hình `LN-10-S1`.
    - Nếu đề thi là Mock test thực tế -> Chuyển sang màn hình `LN-10-S2`.
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: `POST /api/exams/start` (payload: `{ "examId": 82, "mode": "real_exam" }`)
    - Nhận về: `{ "success": true, "sessionToken": "exam_sess_94827" }`

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Không áp dụng.
- **Trạng thái tải (loading state):** Khi đang gọi API khởi tạo phiên thi, nút Bắt đầu hiển thị spinner và vô hiệu hóa click.
- **Trạng thái lỗi (error state):** Khi mất kết nối API khởi tạo phiên thi -> Hiển thị Toast thông báo đỏ: "Không thể khởi tạo phòng thi lúc này. Vui lòng kiểm tra lại đường truyền!".

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ Unit Detail Page (LN-02) hoặc Dashboard (LN-01) sau khi học viên nhấp chọn Bài thi.
- **Sau khi hoàn thành hành động, đi đến màn hình nào?**
  - Chuyển sang Giao diện làm bài thi tích hợp / cuối cấp độ (LN-10-S1).
  - Chuyển sang Giao diện làm bài thi thử IELTS/TOEIC (LN-10-S2).
- **Các màn hình liên quan khác:** LN-02, LN-10-S1, LN-10-S2.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0) đặc trưng.
- Thẻ Test Spec Card sử dụng phong cách `feature-card-cream` màu surface-card (#f5f0e0), viền hairline 1px (#e5e5e5) bo tròn góc bo lớn rounded-xl (24px) tạo cảm giác mập mạp và chuyên nghiệp.
- Hai thẻ chọn chế độ ở Vùng C được thiết kế trực quan, khi di chuột qua sẽ đổi màu nhẹ, khi nhấp chọn sẽ viền dày lên giúp học viên nhận biết rõ ràng chế độ đang chọn (Nguyên tắc Báo hiệu - Signaling Principle).
- Touch target nút bấm đạt chuẩn 44px. Khoảng cách dọc thưa 24px giúp bố cục thoáng đãng và giảm áp lực tâm lý trước khi thi.



