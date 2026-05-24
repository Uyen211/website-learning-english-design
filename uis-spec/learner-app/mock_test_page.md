# MÀN HÌNH: MOCK TEST ROOM (GIAO DIỆN LÀM BÀI THI THỬ IELTS / TOEIC)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Mock test Room (Giao diện làm bài thi thử IELTS/TOEIC)
- **Mã use case liên quan:** UC-07 (Thực hiện bài thi đánh giá năng lực)
- **Mã luồng người dùng liên quan:** LN-FL-04 (Phòng thi - Exam Room)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Dashboard $\rightarrow$ Unit Detail $\rightarrow$ Pre-test Setup Page $\rightarrow$ Mock test Room (URL: `/exams/mock/{mock_id}/run`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên thực hiện bài thi thử quốc tế toàn diện (IELTS hoặc TOEIC) chạy tuần tự qua 4 kỹ năng (Nghe, Đọc, Viết, Nói). Hệ thống thực thi giám sát nghiêm ngặt về thời gian đếm ngược của từng phần, vô hiệu hóa các công cụ gian lận và tự động thu âm giọng nói trong phần thi Nói.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục thay đổi linh hoạt theo từng phần thi (Dynamic Phase Layout) trên nền canvas, có thanh Sticky Exam Header ghim ở đầu trang.
  - **Listening Section View:** Một cột cuộn dọc, danh sách câu hỏi nằm chính giữa màn hình rộng `900px`.
  - **Reading Section View:** Chia đôi màn hình 50/50 (bài đọc bên trái, câu hỏi bên phải) dùng CSS Grid 12 cột.
  - **Writing Section View:** Chia đôi màn hình 40/60 (đề bài viết bên trái, khung nhập văn bản lớn bên phải).
  - **Speaking Section View:** Bố cục một cột căn giữa tối giản chứa avatar giám khảo AI, thanh soundwave sóng âm nhấp nháy, và bộ đếm ngược.
- **Màu nền chung:** Nền trang sử dụng `{colors.canvas}` (`#F9F7FE`).

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh công cụ thi thử (Sticky Exam Header - Vùng A)
- **Đặc tả Visual:**
  - Nền: Kính mờ `{colors.glass}` (`rgba(255, 255, 255, 0.7)`), có `backdrop-filter: blur(8px)`.
  - Chiều cao: `nav-height` (64px). Viền dưới mờ `1px solid rgba(155, 93, 224, 0.1)`.
- **Thành phần:**
  - **Tên bài thi & Kỹ năng:** Tên bài thi (ví dụ: *"IELTS Mock Test #1"*) và nhãn kỹ năng đang thi dạng badge (ví dụ: *"LISTENING SECTION"*).
  - **Đồng hồ đếm ngược (Countdown Clock):** Đếm ngược thời gian của riêng phần thi hiện tại. Cỡ chữ `{typography.title-lg}`.
  - **Nút "Hủy thi" (Exit Exam Link):** Liên kết chữ màu đỏ `{colors.error}` (`#EF4444`). Click để kích hoạt Modal cảnh báo hủy thi.

---

### 4.2 PHẦN THI 1: LISTENING SECTION
- **Trình phát file audio đề Listening (Ẩn/Disabled Controls):**
  - Audio phát tự động ngay khi vào phần thi. Toàn bộ các thanh seeker, nút tua nhạc, nút tạm dừng bị khóa cứng (disabled) để đảm bảo tính nghiêm ngặt.
  - Tổng thời lượng phát: Khoảng 30-40 phút.
- **Phiếu trả lời Listening (Listening Question Sheet - Vùng C):**
  - Các thẻ câu hỏi nền `{colors.surface}` (`#FFFFFF`), bo góc `{rounded.xl}` (24px), viền mờ. Tự động khóa toàn bộ trường nhập khi hết giờ hoặc khi tệp âm thanh kết thúc.

---

### 4.3 PHẦN THI 2: READING SECTION
- **Đoạn văn đọc hiểu bên trái (Reading Passages Tab - Vùng B):**
  - Nền `{colors.surface}`, bo góc `{rounded.xl}` (24px), padding `{spacing.lg}` (24px). Có thanh cuộn dọc độc lập.
  - Phía trên có các tab *"Passage 1"*, *"Passage 2"*, *"Passage 3"* để chuyển đổi văn bản đọc.
  - **Ràng buộc nghiêm ngặt:** Khóa hoàn toàn chức năng tra từ điển nhanh tại chỗ (không hiển thị Dictionary Tooltip khi bôi đen).
- **Phiếu trả lời Reading bên phải (Reading Question Sheet - Vùng C):**
  - Nền `{colors.surface}`, bo góc `{rounded.xl}` (24px), chứa các câu hỏi tương ứng. Tự động khóa nhập liệu khi hết giờ (60 phút).

---

### 4.4 PHẦN THI 3: WRITING SECTION
- **Đề bài viết bên trái (Writing Prompts - Vùng B):**
  - Nền `{colors.surface}`, bo góc `{rounded.xl}` (24px), hiển thị đề bài Task 1 và Task 2.
- **Khung viết bài luận bên phải (Essay Writing Editor - Vùng C):**
  - Khung nhập văn bản lớn (Textarea), nền `{colors.surface}`, bo góc `{rounded.xl}` (24px), chiều cao tối thiểu `400px`.
  - **Ràng buộc nghiêm ngặt:** Hệ thống vô hiệu hóa hoàn toàn công cụ tự động kiểm tra/sửa lỗi chính tả (spellcheck/autocorrect) mặc định của trình duyệt.
  - Bộ đếm từ ở góc dưới: *"Số từ: {X} words"* dạng `{typography.body-sm}` màu `{colors.text-secondary}`.

---

### 4.5 PHẦN THI 4: SPEAKING SECTION
- **Khung thử micro (Mic Test Card):**
  - Xuất hiện ở đầu phần thi. Yêu cầu học viên đọc to câu mẫu để kiểm tra độ nhạy mic và hiển thị vạch đo âm lượng. Đạt yêu cầu sẽ tự động bắt đầu bài nói.
- **Giám khảo AI (AI Examiner Card - Vùng B):**
  - Nền: `{colors.surface}`. Bo góc: `{rounded.xxl}` (32px). Padding: `{spacing.xl}` (32px).
  - **Mascot Giám khảo:** Sử dụng hình ảnh chú Cá Voi xanh chính [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) kích thước `120px` lơ lửng ở vị trí trung tâm, đóng vai trò giám khảo AI phát âm thanh câu hỏi bài nói.
- **Thanh thu âm & Sóng âm (Soundwave - Vùng C):**
  - Xuất hiện động ngay sau khi câu hỏi của giám khảo kết thúc.
  - Hiển thị thanh sóng âm soundwave màu đỏ `{colors.error}` dao động theo giọng nói của học viên biểu thị đang thu âm.
  - Đồng hồ đếm ngược thời gian nói cho từng câu hỏi (ví dụ: đếm ngược 2 phút đối với IELTS Part 2).

---

### 4.6 Các hộp thoại cảnh báo lớp phủ (Modals - Vùng D)
- **Hộp thoại Cảnh báo hủy thi (Exit Warning Modal - LN-11-M1):**
  - Tiêu đề màu đỏ `{colors.error}`. Cảnh báo kết quả thi sẽ bị hủy bỏ hoàn toàn và tính trượt bài thi. Nhấp "Xác nhận hủy" sẽ thoát phòng thi về Dashboard; nhấp "Tiếp tục" đóng modal.
- **Hộp thoại Lỗi Microphone khi thi (Speaking Mic Error Modal - LN-11-M2):**
  - Xuất hiện trong phần thi Speaking nếu micro bị mất quyền truy cập hoặc hỏng đột ngột.
  - Tiêu đề màu đỏ `{colors.error}`: *"Lỗi thiết bị Microphone"*. Mô tả: *"Không phát hiện thấy microphone hoạt động hoặc trình duyệt bị chặn quyền truy cập. Bài thi thử Mock Test bắt buộc phải hủy kết quả."*. Nút *"Xác nhận hủy bài thi"* (`button-primary` style).

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Chuyển phần thi tự động (Listening -> Reading -> Writing -> Speaking)**
  - Hết giờ hoặc kết thúc file nghe của từng phần thi $\rightarrow$ Hệ thống tự động khóa trường nhập, lưu kết quả tạm thời $\rightarrow$ Tự động chuyển hướng hiển thị sang giao diện phần thi tiếp theo.
  - Sau khi câu hỏi Speaking cuối cùng kết thúc $\rightarrow$ Tự động nộp toàn bộ bài Mock Test lên máy chủ chấm điểm $\rightarrow$ Chuyển hướng sang [test_result_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/test_result_page.md).
- **Hành động: Trả lời câu hỏi Nói trong phần Speaking**
  - Giám khảo AI phát xong câu hỏi $\rightarrow$ Micro tự động ghi âm $\rightarrow$ Soundwave nhấp nháy đỏ $\rightarrow$ Học viên nói $\rightarrow$ Click nút "Nộp câu trả lời" để nộp sớm (hoặc hết giờ nói tự nộp) $\rightarrow$ Lưu file ghi âm tạm thời, tự chuyển sang câu tiếp theo.
  - **Dữ liệu API:** `POST /api/mock-test/submit`
    - Payload gửi đi: Tệp ghi âm nói, văn bản bài viết, đáp án nghe đọc.
    - Response: `{ "success": true, "resultId": 509 }`

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT
- **Học viên giữ im lặng (Rẽ nhánh E-3):** Trong suốt thời gian đếm ngược, hệ thống phát hiện cường độ âm ghi được bằng 0 $\rightarrow$ Tự động dừng ghi âm, lưu file audio trống và ghi nhận 0 điểm cho câu hỏi Nói tương ứng $\rightarrow$ Tự chuyển câu tiếp.
- **Trạng thái tải (Loading state):** Hiển thị màn hình loading mờ khi chuyển giao giữa các phần thi.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [pre_test_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/pre_test_page.md).
- **Đi đến:** [test_result_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/test_result_page.md) (Sau khi nộp bài thi thành công), hoặc [learner_dashboard.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/learner_dashboard.md) (nếu hủy thi).

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Sử dụng ảnh gốc [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) kích thước `120px` làm avatar giám khảo AI trong phần thi Speaking để tăng tính tương tác sinh động.
- **KHÔNG ĐƯỢC:** Cho phép học viên điều khiển trình phát nghe trong phần thi Listening. Khóa tất cả các tính năng sửa lỗi chính tả ở trình duyệt trong phần thi Writing.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Thông tin đề thi thử IELTS/TOEIC (Mock Test Info):** Liên kết với đối tượng `tests[2]` (id: `test_2`), bao gồm các trường `{name}`, `{typeLabel}`, `{levelUnit}`, `{duration}`, `{questionsCount}`, `{maxScore}`.
