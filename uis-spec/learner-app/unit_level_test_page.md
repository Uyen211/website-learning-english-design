# MÀN HÌNH: MINI-EXAM / LEVEL TEST ROOM (GIAO DIỆN LÀM BÀI THI TÍCH HỢP / CUỐI CẤP ĐỘ)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Mini-exam / Level test Room (Giao diện làm bài thi tích hợp / cuối cấp độ)
- Mã use case liên quan: UC-07 (Làm bài thi đánh giá năng lực)
- Mã luồng người dùng liên quan: Flow LN-FL-08 (Thực hiện bài thi đánh giá năng lực)
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Dashboard -> Unit Detail -> Pre-test Setup Page -> Mini-exam / Level test Room (URL: /exams/{exam_id}/run)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này để thực hiện bài thi trắc nghiệm ngắn (Mini-test cuối Unit) hoặc bài thi tổng hợp cuối cấp độ (Level test), di chuyển qua các câu hỏi và nộp bài để đánh giá năng lực.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục cột kép chia tỷ lệ không đối xứng 8:4 (Split Column Layout) gồm Vùng câu hỏi cuộn dọc bên trái và Bảng điều hướng câu hỏi cố định bên phải.
- Các vùng chính trên màn hình:
  - Vùng A: Sticky Header Action Bar (Thanh công cụ cố định đầu trang) chứa tên bài thi, đồng hồ đếm ngược và nút "Nộp bài".
  - Vùng B: Vùng hiển thị câu hỏi bên trái (Left Question Sheet Panel) hiển thị danh sách các câu hỏi theo thứ tự dọc.
  - Vùng C: Bảng lưới câu hỏi bên phải (Right Question Navigation Panel) cố định, hiển thị sơ đồ các câu số 1 đến N.
  - Vùng D: Hộp thoại cảnh báo hủy thi giữa chừng (Exit Warning Modal - LN-11-M1) hiển thị đè lên màn hình khi học viên bấm nút hủy thi.
- Kích thước / Grid tham khảo:
  - Vùng B (Câu hỏi) chiếm tỷ lệ 8 cột và Vùng C (Lưới câu hỏi) chiếm 4 cột trên lưới 12-column.
  - Chiều rộng tối đa của container: 1200px.
  - Khoảng cách padding trong mỗi vùng: spacing-lg (24px).
  - Khoảng cách dọc giữa các câu hỏi: spacing-xl (32px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)

### THÀNH PHẦN CHUNG (STICKY HEADER)
- **Tên component:** Thanh công cụ thi (Sticky Exam Header)
  - **Loại component tham chiếu từ DESIGN.md:** top-nav (nền canvas #fffaf0, height 64px, border-bottom 1px hairline #e5e5e5)
  - **Vị trí:** Vùng A, ghim cố định đầu trang.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** 
    - Bên trái: Tên đề thi (ví dụ: "Mini-exam cuối Unit 2: Everyday Work").
    - Ở giữa: Đồng hồ đếm ngược (Countdown Clock) hiển thị thời gian phút:giây (ví dụ: "29:59") màu đỏ sẫm (#ef4444) nhấp nháy chậm nếu dưới 5 phút.
    - Bên phải: Nút "Nộp bài" (`button-primary` màu đen).

---

### PHÂN HỆ LÀM BÀI VÀ ĐIỀU HƯỚNG (VÙNG B & C)
- **Tên component:** Danh sách câu hỏi (Question Sheets)
  - **Loại component tham chiếu từ DESIGN.md:** vertical list of feature-card-cream (mỗi câu đặt trong một thẻ nền surface-card #f5f0e0, bo góc rounded-lg 16px, padding 20px)
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** 
    - Hiển thị số thứ tự câu hỏi (ví dụ: "Câu 1:").
    - Nội dung đề câu hỏi bằng tiếng Anh (ví dụ: điền từ, trắc nghiệm, hoặc đọc hiểu ngắn).
    - Các tùy chọn trả lời (A, B, C, D) dạng radio button hoặc ô gõ nhập liệu.

- **Tên component:** Bảng lưới câu hỏi (Question Navigation Panel)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-lg 16px, padding 20px)
  - **Vị trí:** Vùng C.
  - **Trạng thái:** Mặc định cố định bên phải (sticky sidebar).
  - **Dữ liệu hiển thị / hành vi:** 
    - Hiển thị nhãn: "Lưới câu hỏi".
    - Sơ đồ các ô số (từ 1 đến 40). Mỗi ô số là một badge bo tròn. Học viên có thể click vào ô số để cuộn nhanh đến câu hỏi đó ở Vùng B.
    - Trạng thái ô số:
      - Ô chưa làm: nền trắng canvas, viền hairline #e5e5e5, chữ muted.
      - Ô đã làm: nền đen primary #0a0a0a, chữ trắng on-primary #ffffff.
      - Ô đang làm (focus): viền dày 2px màu cam peach (#ffb084).

- **Tên component:** Liên kết "Hủy thi" (Exit Exam Link)
  - **Loại component tham chiếu từ DESIGN.md:** button-text-link (màu error #ef4444, font Inter 14px, weight 600)
  - **Vị trí:** Vùng C, nằm dưới bảng lưới câu hỏi.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Hủy bài thi giữa chừng". Nhấp chuột để kích hoạt Modal cảnh báo hủy thi LN-11-M1.

---

### VÙNG D: HỘP THOẠI CẢNH BÁO HỦY THI GIỮA CHỪNG (EXIT WARNING MODAL)
- **Tên component:** Hộp thoại Cảnh báo hủy thi (Exit Warning Modal - LN-11-M1)
  - **Loại component tham chiếu từ DESIGN.md:** overlay / backdrop + centered alert card (nền surface-card #f5f0e0, rounded-lg 16px, width 420px)
  - **Vị trí:** Vùng D, nổi đè lên màn hình.
  - **Trạng thái:** Xuất hiện khi bấm nút "Hủy bài thi giữa chừng" hoặc cố tình tắt/load lại tab trình duyệt.
  - **Dữ liệu hiển thị / hành vi:**
    - Tiêu đề: "Bạn muốn hủy thi?" (màu error #ef4444).
    - Dòng mô tả: "Hủy thi giữa chừng sẽ không được ghi nhận kết quả và bạn sẽ bị tính là trượt bài thi này. Bạn có chắc chắn muốn hủy?".
    - Nút "Có, tôi muốn hủy" (`button-text-link` màu error #ef4444, bên trái). Nhấp chọn sẽ xóa dữ liệu phiên thi và đưa về dashboard LN-01.
    - Nút "Tiếp tục làm bài" (`button-primary` màu đen, bên phải). Nhấp chọn đóng modal quay lại thi.

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Click chọn đáp án trắc nghiệm hoặc nhập liệu**
  - **Luồng chính:** Học viên click chọn hoặc gõ câu trả lời vào một câu hỏi ở Vùng B -> Hệ thống tự động ghi nhận câu trả lời tạm thời vào LocalStorage/Server -> Ô số tương ứng trong Lưới câu hỏi ở Vùng C đổi trạng thái sang nền đen primary (đã làm).
- **Hành động: Nhấp nút "Nộp bài" ở Vùng A**
  - **Luồng chính:**
    1. Học viên click "Nộp bài".
    2. Hệ thống kiểm tra:
       - Nếu còn câu hỏi chưa làm -> Hiển thị hộp thoại cảnh báo: "Bạn còn [X] câu hỏi chưa hoàn thành. Bạn có chắc chắn muốn nộp bài thi ngay?".
       - Nếu đã làm đủ -> Gửi API POST nộp bài thi chính thức.
    3. Nút nộp bài hiển thị Loading.
    4. Máy chủ chấm điểm tự động.
    5. Chuyển hướng sang màn hình Test Result Page (LN-11).
  - **Luồng con / rẽ nhánh (Hết giờ làm bài):** Đồng hồ đếm ngược chạy về 00:00 -> Hệ thống tự động khóa tất cả trường nhập và vô hiệu hóa click làm bài -> Tự động kích hoạt nộp bài thi cưỡng bức lên máy chủ -> Chuyển hướng sang LN-11.
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: `POST /api/exams/submit` (payload: `{ "sessionToken": "exam_sess_94827", "answers": { "1": "A", "2": "C" } }`)
    - Nhận về: `{ "success": true, "resultId": 508 }`

- **Hành động: Tải lại trang hoặc đóng tab trình duyệt**
  - **Luồng chính:** Hệ thống chặn sự kiện window.beforeunload -> Hiển thị thông báo cảnh báo của trình duyệt -> Nếu học viên vẫn đồng ý load lại/đóng -> Hủy bỏ phiên thi (tương tự chọn hủy thi).

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Không áp dụng.
- **Trạng thái tải (loading state):** Khi bắt đầu vào trang, toàn bộ danh sách câu hỏi hiển thị dạng skeleton mờ nhấp nháy, các ô số trong lưới cũng trống mờ cho đến khi đề thi tải xong.
- **Trạng thái lỗi (error state):** Khi API đề thi bị lỗi -> Vùng B hiển thị dòng cảnh báo: "Lỗi tải đề thi. Vui lòng quay lại hoặc bấm tải lại trang!".

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ Pre-test Setup Page (LN-09) sau khi học viên chọn chế độ thi và bấm nút "Bắt đầu làm bài".
- **Sau khi hoàn thành hành động, đi đến màn hình nào?**
  - Chuyển sang Test Result Page (LN-11) sau khi nộp bài thi thành công (hoặc khi hết giờ).
  - Chuyển sang Learner Dashboard (LN-01) sau khi xác nhận hủy bài thi giữa chừng.
- **Các màn hình liên quan khác:** LN-09, LN-11, Modal LN-11-M1.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0).
- Bố cục bất đối xứng 8:4 giúp tập trung thị giác vào danh sách câu hỏi ở bên trái, đồng thời bảng lưới câu hỏi cố định bên phải đóng vai trò bản đồ định vị giúp học viên quản lý tốc độ làm bài tốt hơn mà không bị quá tải nhận thức.
- Các ô số trong Lưới câu hỏi sử dụng hình tròn bo góc tuyệt đối, trạng thái đã làm đổi sang màu đen tuyền (#0a0a0a) tương phản cực cao trên nền canvas để học viên dễ nhận biết các câu bỏ sót (Nguyên tắc Báo hiệu - Signaling Principle).
- Đồng hồ đếm ngược màu đỏ nổi bật tạo sự cảnh báo trực quan.
- Touch target của các đáp án và ô số tối thiểu 44px.



