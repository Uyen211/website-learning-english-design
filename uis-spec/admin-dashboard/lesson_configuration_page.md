# MÀN HÌNH: LESSON CONFIGURATION PAGE (MÀN HÌNH CẤU HÌNH BÀI HỌC & BÀI TẬP)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Lesson Configuration Page (Màn hình cấu hình bài học & bài tập)
- **Mã use case liên quan:** UC-03a, UC-03b
- **Mã luồng người dùng liên quan:** Flow AD-FL-03 (Cấu hình Bài học và Luyện tập)
- **Vai trò người dùng:** Admin (Quản trị viên)
- **Vị trí trong sitemap:** Trang chủ quản trị $\rightarrow$ AD-01 $\rightarrow$ AD-02 $\rightarrow$ AD-03 $\rightarrow$ AD-03-Form: Lesson Configuration Page (URL: `/admin/lessons/{lesson_id}/configure`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng màn hình này để đặt tên bài học, tích chọn các hình thức bài tập áp dụng cho bài học đó (ví dụ: *Flashcards SRS*, *Đoán nghĩa ngữ cảnh*, *Viết câu cá nhân hóa*, v.v.) và nhập chi tiết dữ liệu giảng dạy, tải lên tệp âm thanh phát âm bản xứ/hình ảnh minh họa cùng với đáp án chính xác và lời giải thích chi tiết cho từng phần bài tập tương ứng.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục một cột cuộn dọc có thanh tiêu đề hành động ghim cố định phía trên (Sticky Action Bar).
- **Màu nền chung:** Nền trang chính sử dụng tông màu `{colors.canvas}` (`#F9F7FE`) phủ sương mờ `{gradients.atmosphere-haze}`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Sticky Action Bar (Vùng A):** Thanh tiêu đề hành động ghim cố định ở đầu màn hình khi cuộn, chứa Breadcrumbs và nhóm nút Lưu/Hủy.
  - **Zone 2: General Lesson Info (Vùng B):** Vùng nhập thông tin chung của bài học (Tên bài học, thể loại bài học).
  - **Zone 3: Exercise Form Selector (Vùng C):** Thẻ lớn chứa danh sách các hộp kiểm (checkboxes) lựa chọn hình thức bài tập áp dụng.
  - **Zone 4: Dynamic Content Builder Area (Vùng D):** Vùng soạn thảo chi tiết hiển thị động các khối form nhập liệu tương ứng với các checkbox được tích chọn ở Vùng C.
- **Kích thước tham khảo:**
  - Chiều rộng tối đa của khu vực nhập liệu: `1000px` căn giữa để Admin tập trung cao độ vào soạn thảo.
  - Khoảng cách dọc giữa các phân đoạn chính: `{spacing.xl}` (32px).
  - Padding trong các khối soạn thảo: `{spacing.lg}` (24px).

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh hành động cố định đầu trang (Sticky Action Bar - Vùng A)
- **Đặc tả Visual:**
  - Nền bar: Kính mờ `{colors.glass}` (`rgba(255, 255, 255, 0.7)`), có `backdrop-filter: blur(8px)`.
  - Chiều cao: `64px`. Viền dưới mờ: `1px solid rgba(155, 93, 224, 0.1)`.
- **Thành phần:**
  - **Breadcrumbs:** Dòng chữ dạng `{typography.caption}` (12px), màu `{colors.text-secondary}`. Hiển thị: *"Admin / Lộ trình học / Cấu hình bài học"*.
  - **Nút "Lưu bài học":** Style `button-primary` nền `{colors.primary}` (`#4E56C0`), chữ trắng, cao `44px`, bo góc `{rounded.lg}` (16px). Tỏa sáng `{elevation.active-glow}`. Bấm vào kích hoạt kiểm tra hợp lệ dữ liệu và gửi API lưu trữ.
  - **Nút "Hủy":** Style `button-secondary` nền `{colors.surface}`, viền mờ, chữ `{colors.primary}`, cao `44px`, bo góc `{rounded.lg}`.

### 4.2 Vùng thông tin chung bài học (General Info - Vùng B)
- **Tên component:** Trường nhập Tên bài học
  - **Đặc tả:**
    - Loại component: `text-input` cao `44px`, bo góc `{rounded.lg}` (16px), nền `{colors.surface}` (`#FFFFFF`).
    - Viền mặc định: `1px solid rgba(155, 93, 224, 0.2)`. Focus: Viền đổi sang `{colors.primary}` với `{elevation.active-glow}`.
    - Nhãn: *"Tên bài học *"* (in đậm, có dấu sao đỏ bắt buộc). Placeholder: *"Nhập tên bài học..."*.
- **Tên component:** Nhãn Thể loại bài học (Locked Category Tag)
  - **Đặc tả:** Badge viên thuốc `{rounded.pill}` nền nhạt `{colors.light-accent}` (`#FDCFFA`), chữ màu `{colors.primary}` (weight 600) ghi: *"Thể loại: Từ vựng"* hoặc *"Thể loại: Nghe"*. Đây là nhãn hiển thị cố định (read-only) do hệ thống phân loại.

### 4.3 Thẻ chọn hình thức bài tập (Exercise Form Selector - Vùng C)
- **Đặc tả Visual:**
  - Nền thẻ: `{colors.surface}`. Bo góc: `{rounded.xl}` (24px). Viền: `1px solid rgba(155, 93, 224, 0.1)`.
  - Padding: `{spacing.lg}` (24px). Hiệu ứng nâng: `{elevation.glow}`.
- **Nội dung:**
  - Tiêu đề phụ: *"Chọn hình thức bài tập áp dụng"* dạng `{typography.title-md}` (18px, weight 600).
  - Danh sách hộp kiểm (checkboxes) xếp dạng lưới nằm ngang, thay đổi động theo Thể loại bài học (dựa trên luồng quy định trong `USE_CASES.md`):
    - *Thể loại Từ vựng:* checkboxes: Flashcards SRS, Kéo thả/Ghép đôi, Đoán nghĩa ngữ cảnh, Dự đoán từ, Đọc to từ vựng, Viết câu cá nhân hóa.
    - *Thể loại Luyện viết:* checkboxes: Ghép câu (Basic), Viết gợi ý 3 vòng (ZPD), Viết luận chấm AI.

### 4.4 Vùng soạn thảo chi tiết động (Dynamic Content Builder Area - Vùng D)
- **Đặc tả Visual:**
  - Mỗi hình thức bài tập được tích chọn ở Vùng C sẽ tự động hiển thị một thẻ soạn thảo tương ứng ở Vùng D.
  - Thẻ soạn thảo: Nền `{colors.surface}`. Bo góc lớn: `{rounded.xl}` (24px). Viền mờ.
  - Padding: `{spacing.xl}` (32px). Hiệu ứng nâng: `{elevation.glow}`.
- **Các khối form nhập liệu phổ biến:**
  - **Khối soạn Flashcards SRS:**
    - Các trường `text-input` xếp dọc: Từ vựng, phiên âm IPA, định nghĩa tiếng Việt.
    - Khu vực tải file âm thanh phát âm bản xứ (.mp3) và ảnh minh họa (.png/.jpg).
    - Trường văn bản lớn nhập *"Lời giải thích chi tiết"* dạng text-area.
  - **Khối soạn Viết luận chấm AI (Essay Form):**
    - Trường nhập đề bài luận viết.
    - Trường nhập *"Cấu trúc đích bắt buộc"* và *"Từ khóa gợi ý"* (dạng tag-input hoặc ngăn cách nhau bằng dấu phẩy) để Cá Voi chấm điểm tự động.
    - Trường nhập bài viết mẫu tham khảo.
- **Khu vực tải tệp tin (File Uploader):**
  - Nền: `{colors.canvas}` (`#F9F7FE`). Viền: `1.5px dashed rgba(155, 93, 224, 0.3)`. Bo góc: `{rounded.lg}` (16px).
  - Chiều cao: `80px`. Căn giữa chữ.
  - Hiệu ứng: Khi kéo tệp qua (drag-over) $\rightarrow$ Viền đổi sang màu chủ đạo `{colors.primary}` nét liền và có `{elevation.active-glow}`.
  - Hành vi: Chọn tệp thành công $\rightarrow$ Hiển thị icon tệp kèm tên tệp màu xanh lá `{colors.success}` và nút nhỏ "Xóa tệp".
  - Icon minh họa: Sử dụng tệp ảnh Cá Voi Vũ Trụ nhỏ [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`28px x 28px`) bay lượn ở góc uploader để tăng tính sinh động.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Tích chọn hộp kiểm ở Vùng C**
  - Admin tích chọn checkbox $\rightarrow$ Khối form soạn thảo tương ứng xuất hiện động ở Vùng D với hiệu ứng fade-in mượt mà. Nếu bỏ tích $\rightarrow$ Khối form ẩn đi và tự động xóa dữ liệu tạm trong khối để tránh gửi dư thừa lên server.
- **Hành động: Click nút "Lưu bài học"**
  - Hệ thống kiểm tra tính hợp lệ của toàn bộ form ở Vùng D:
    - Tên bài học không được trống.
    - Tất cả các trường câu hỏi bắt buộc, đáp án đúng và giải thích chi tiết không được để trống.
    - File âm thanh chuẩn định dạng MP3/WAV dưới 5MB. File ảnh chuẩn JPG/PNG dưới 2MB.
    - *Nhánh hợp lệ:* Nút Lưu chuyển sang trạng thái Loading (hiển thị spinner mờ, khóa click) $\rightarrow$ Gửi API lưu trữ $\rightarrow$ Thành công $\rightarrow$ Chuyển hướng về danh sách bài học `AD-03` $\rightarrow$ Hiện Toast màu xanh lá `{colors.success}`: *"Cấu hình bài học thành công!"*.
    - *Nhánh dữ liệu lỗi:* Giữ nguyên màn hình, tự động cuộn đến trường lỗi đầu tiên $\rightarrow$ Bôi đỏ viền trường bị lỗi màu `{colors.error}` (`#EF4444`) kèm dòng chữ cảnh báo lỗi đỏ ngay bên dưới.
  - **API Lưu bài học:** `POST /api/lessons/save-config`
    - Payload: `{ "lessonId": 24, "name": "Greetings Practice", "appliedForms": ["flashcard"], "flashcardData": { "word": "Hello", "ipa": "/həˈloʊ/", "meaning": "Xin chào", "audioUrl": "files/hello.mp3", "explanation": "Dùng để chào hỏi..." } }`
    - Response: `{ "success": true }`

---

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái chưa chọn gì (Empty State):** Khi bài học chưa được cấu hình lần nào, Vùng D hiển thị trống hoàn toàn kèm dòng chữ hướng dẫn mờ: *"Vui lòng tích chọn ít nhất một hình thức bài tập ở phía trên để bắt đầu soạn thảo nội dung giảng dạy."*.
- **Trạng thái tải dữ liệu cũ (Loading State):** Hiển thị spinner ở giữa trang và hiệu ứng Skeleton mờ cho toàn bộ các khối nhập liệu khi đang tải dữ liệu cũ ở chế độ Sửa cấu hình.

---

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [lesson_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/lesson_list_page.md) khi click nút "Cấu hình" hoặc "Sửa cấu hình".
- **Đi đến:** Quay lại [lesson_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/lesson_list_page.md) sau khi click lưu thành công hoặc bấm nút hủy.

---

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Bố trí khoảng cách thưa thớt giữa các khối form nhập liệu ở Vùng D (khoảng cách dọc `{spacing.xl}` 32px) để giảm bớt áp lực nhận thức cho Admin khi nhập lượng văn bản và câu hỏi khổng lồ.
- **KHÔNG ĐƯỢC:** Sử dụng các bóng đổ thô ráp màu xám đen. Toàn bộ hiệu ứng chiều sâu bắt buộc dùng các cấp độ phát quang nhẹ `{elevation.glow}` để đảm bảo tính mỹ thuật nhẹ dịu của DiveVerse.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Thông tin bài học cấu hình (Configured Lesson Metadata):** Liên kết với bài học tương ứng trong `lessons.unit_1[0]` (đối với bài học Từ vựng) hoặc các bài học kỹ năng khác để tự động điền sẵn (pre-fill) nội dung hiện tại lên biểu mẫu cấu hình.
