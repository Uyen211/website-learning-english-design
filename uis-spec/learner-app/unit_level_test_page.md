# MÀN HÌNH: MINI-EXAM / LEVEL TEST ROOM (GIAO DIỆN LÀM BÀI THI TÍCH HỢP / CUỐI CẤP ĐỘ)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Mini-exam / Level test Room (Giao diện làm bài thi tích hợp / cuối cấp độ)
- **Mã use case liên quan:** UC-07 (Thực hiện bài thi đánh giá năng lực)
- **Mã luồng người dùng liên quan:** LN-FL-04 (Phòng thi - Exam Room)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Dashboard $\rightarrow$ Unit Detail $\rightarrow$ Pre-test Setup Page $\rightarrow$ Mini-exam / Level test Room (URL: `/exams/{exam_id}/run`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên thực hiện bài thi trắc nghiệm ngắn (Mini-test cuối Unit) hoặc bài thi tổng hợp cuối cấp độ (Level test). Học viên lần lượt trả lời các câu hỏi, theo dõi thời gian đếm ngược và tiến độ làm bài thông qua sơ đồ lưới câu hỏi, sau đó nộp bài thi để đánh giá năng lực.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục cột kép chia tỷ lệ không đối xứng 8:4 (Split Column Layout) nhằm tối ưu hóa việc phân chia thông tin: Vùng hiển thị câu hỏi cuộn dọc bên trái và Bảng điều hướng câu hỏi ghim cố định (sticky sidebar) bên phải.
- **Màu nền chung:** Nền trang sử dụng `{colors.canvas}` (`#F9F7FE`) phối dải chuyển màu mờ `{gradients.atmosphere-haze}`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Sticky Exam Header (Thanh công cụ cố định đầu trang)**
    - Ghim cố định ở mép trên. Chiều cao: `nav-height` (64px). Chứa tên đề thi, đồng hồ đếm ngược và nút nộp bài.
  - **Zone 2: Left Question Sheet Panel (Cột danh sách câu hỏi bên trái)**
    - Chiếm 8 cột trên lưới 12 cột. Cuộn dọc độc lập.
  - **Zone 3: Right Question Navigation Panel (Cột lưới câu hỏi bên phải)**
    - Chiếm 4 cột trên lưới 12 cột. Ghim cố định khi cuộn trang.
  - **Zone 4: Exit Warning Modal (Hộp thoại cảnh báo hủy thi)**
    - Hộp thoại lớp phủ xuất hiện đè lên giao diện khi học viên chọn hủy thi.

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh công cụ thi (Sticky Exam Header - Vùng A)
- **Đặc tả Visual:**
  - Nền: Kính mờ `{colors.glass}` (`rgba(255, 255, 255, 0.7)`), có `backdrop-filter: blur(8px)`.
  - Chiều cao: `nav-height` (64px). Viền dưới mờ `1px solid rgba(155, 93, 224, 0.1)`.
- **Thành phần:**
  - **Tên bài thi:** Dạng chữ `{typography.title-md}` màu `{colors.text-primary}` (ví dụ: *"Mini-exam cuối Unit 2: Everyday Work"*).
  - **Đồng hồ đếm ngược (Countdown Clock):** 
    - Hiển thị chính giữa. Định dạng phút:giây (ví dụ: *"29:59"*). Cỡ chữ `{typography.title-lg}`.
    - Màu sắc: Mặc định màu `{colors.text-primary}`. Khi thời gian còn dưới 5 phút: Chuyển sang màu đỏ cảnh báo `{colors.error}` (`#EF4444`) và nhấp nháy chậm.
  - **Nút "Nộp bài" (Submit Button):** Nền `{colors.primary}` (`#4E56C0`), chữ trắng. Bo góc `{rounded.lg}` (16px). Chiều cao tối thiểu `44px`.

### 4.2 Danh sách câu hỏi bên trái (Left Question Sheet Panel - Vùng B)
- **Đặc tả thẻ câu hỏi:**
  - Nền: `{colors.surface}` (`#FFFFFF`). Bo góc `{rounded.xl}` (24px). Viền: `1px solid rgba(155, 93, 224, 0.1)`.
  - Hiệu ứng: Soft glow `{elevation.glow}`. Padding: `{spacing.lg}` (24px).
  - Khoảng cách dọc giữa các câu hỏi: `{spacing.xl}` (32px).
- **Thành phần bên trong:**
  - **Số thứ tự câu:** *"Câu 1:"* dạng `{typography.title-md}` màu `{colors.primary}`.
  - **Nội dung đề câu hỏi:** Đoạn văn hoặc câu hỏi tiếng Anh dạng `{typography.body-md}`.
  - **Vùng chọn đáp án:** Gồm các ô Radio Buttons (A, B, C, D) hoặc ô nhập liệu văn bản (đối với câu điền từ). Ô nhập liệu cao `44px`, bo góc `{rounded.lg}`.

### 4.3 Bảng lưới câu hỏi bên phải (Right Question Navigation Panel - Vùng C)
- **Đặc tả Visual:**
  - Nền: `{colors.surface}` (`#FFFFFF`). Bo góc `{rounded.xl}` (24px). Padding `{spacing.lg}` (24px).
- **Thành phần:**
  - **Tiêu đề bảng:** *"Lưới câu hỏi"* dạng `{typography.caption}` in hoa.
  - **Sơ đồ các ô số (1 đến N):** 
    - Hiển thị lưới các nút tròn `{rounded.full}` đại diện cho câu hỏi. Học viên click vào ô số để cuộn nhanh đến câu hỏi tương ứng ở cột trái.
    - **Các trạng thái của ô số (Signaling Principle):**
      - *Ô chưa làm:* Nền `{colors.canvas}`, viền mờ, chữ màu `{colors.text-secondary}`.
      - *Ô đã làm:* Nền màu chủ đạo `{colors.primary}` (`#4E56C0`), chữ màu trắng `{colors.surface}`.
      - *Ô đang làm (focus):* Viền dày 2px màu tím nhạt `{colors.accent}` (`#D78FEE`) kèm soft glow.
  - **Nút "Hủy bài thi" (Exit Exam Link):**
    - Căn lề dưới bảng lưới. Dạng liên kết chữ màu đỏ `{colors.error}` (`#EF4444`), kiểu chữ `{typography.body-sm}` (weight 600). Click để kích hoạt Modal cảnh báo hủy thi.

### 4.4 Hộp thoại cảnh báo hủy thi giữa chừng (Exit Warning Modal - Vùng D)
- **Đặc tả Visual:**
  - Backdrop phủ lớp kính mờ `{colors.glass}` 50% opacity.
  - Thẻ cảnh báo ở giữa: Nền `{colors.surface}`, bo góc `{rounded.xl}` (24px), width `420px`.
- **Nội dung:**
  - Tiêu đề màu đỏ `{colors.error}`: *"Bạn muốn hủy thi?"*.
  - Mô tả: *"Hủy thi giữa chừng sẽ không được ghi nhận kết quả và bạn sẽ bị tính là trượt bài thi này. Bạn có chắc chắn muốn hủy?"*.
  - Nút bấm:
    - *"Có, tôi muốn hủy":* Liên kết chữ màu đỏ `{colors.error}` ở bên trái. Click xóa phiên thi, đưa về Dashboard.
    - *"Tiếp tục làm bài":* Nút bấm `button-primary` style (nền `{colors.primary}`, chữ trắng) ở bên phải. Click đóng modal.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Chọn đáp án hoặc điền câu trả lời**
  - Học viên tương tác làm bài $\rightarrow$ Hệ thống tự động ghi nhận câu trả lời tạm thời $\rightarrow$ Ô số tương ứng trong Lưới câu hỏi ở cột phải đổi màu sang nền `{colors.primary}` biểu thị đã làm.
- **Hành động: Nhấp nút "Nộp bài"**
  - Hệ thống kiểm tra: Nếu còn câu hỏi trống, hiện cảnh báo: *"Bạn còn [X] câu hỏi chưa làm. Bạn có chắc chắn muốn nộp bài?"*.
  - Gửi API nộp bài: `POST /api/exams/submit`
    - Payload: `{ "sessionToken": "exam_sess_94827", "answers": { "1": "A", "2": "C" } }`
    - Response: `{ "success": true, "resultId": 508 }`
  - Thành công: Chuyển sang [test_result_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/test_result_page.md).
- **Hết giờ làm bài:** Đồng hồ đếm ngược về `00:00` $\rightarrow$ Khóa toàn bộ các ô nhập $\rightarrow$ Tự động kích hoạt nộp bài thi cưỡng bức lên máy chủ $\rightarrow$ Chuyển hướng sang trang kết quả.

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT
- **Trạng thái tải (Loading state):** Hiển thị các khối skeleton mờ nhấp nháy khi đề thi đang được tải xuống từ máy chủ.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [pre_test_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/pre_test_page.md).
- **Đi đến:** [test_result_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/test_result_page.md) (Sau khi nộp bài), hoặc [learner_dashboard.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/learner_dashboard.md) (nếu hủy thi).

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Thiết kế lưới câu hỏi cố định bên phải đóng vai trò bản đồ định vị giúp học viên quản lý tốc độ làm bài tốt hơn.
- **KHÔNG ĐƯỢC:** Sử dụng bóng đổ xám/đen bên dưới các thẻ câu hỏi. Trạng thái của các ô số tròn bắt buộc dùng màu `{colors.primary}` để báo hiệu tương phản rõ nét nhất.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Thông tin bài thi cuối Unit (Mini-test Info):** Liên kết với đối tượng `tests[1]` (id: `test_1`), bao gồm các trường `{name}`, `{typeLabel}`, `{levelUnit}`, `{duration}`, `{questionsCount}`, `{maxScore}`.
