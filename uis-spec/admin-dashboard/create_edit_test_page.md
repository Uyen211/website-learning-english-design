# MÀN HÌNH: CREATE / EDIT TEST PAGE (MÀN HÌNH SOẠN THẢO BÀI KIỂM TRA)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Create / Edit Test Page (Màn hình soạn thảo bài kiểm tra: Mini-test / Level test / Mock test)
- **Mã use case liên quan:** UC-04a, UC-04b
- **Mã luồng người dùng liên quan:** Flow AD-FL-04 (Quản lý Bài kiểm tra)
- **Vai trò người dùng:** Admin (Quản trị viên)
- **Vị trí trong sitemap:** Trang chủ quản trị $\rightarrow$ AD-04 $\rightarrow$ AD-04-Form: Create / Edit Test Page (URL: `/admin/tests/create` hoặc `/admin/tests/{test_id}/edit`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng màn hình này để nhập thông tin thiết lập chung của đề kiểm tra (Tên đề, mô tả, thời gian, thang điểm tối đa), chọn định dạng đề thi quy chuẩn (Mini-test cuối Unit, Level test cuối cấp độ, hoặc Mock Test thực tế), và tiến hành soạn thảo chi tiết danh sách câu hỏi, đáp án đúng, tải file âm thanh nghe, cấu hình bài viết mẫu cho AI chấm, và nhập bảng quy đổi điểm tương ứng.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục một cột cuộn dọc có thanh điều hướng ghim cố định đầu trang (Sticky Header Action Bar) và chia phân hệ nội dung dạng Tab lớn bên trong thân trang.
- **Màu nền chung:** Nền trang chính sử dụng tông màu `{colors.canvas}` (`#F9F7FE`) phối dải sương mờ `{gradients.atmosphere-haze}`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Sticky Top Bar (Vùng A):** Thanh hành động ghim cố định ở đầu viewport, chứa Breadcrumbs và cặp nút Lưu/Hủy đề thi.
  - **Zone 2: General Settings Form (Vùng B):** Biểu mẫu thiết lập các thông số chung (Tên đề, mô tả, thời gian, thang điểm).
  - **Zone 3: Test Type Selector (Vùng C):** Hộp chọn dạng đề thi để thay đổi giao diện thiết kế câu hỏi bên dưới.
  - **Zone 4: Dynamic Question Builder (Vùng D):** Vùng thiết kế câu hỏi động (hoặc Section Editor phân theo 4 kỹ năng chính nếu chọn dạng đề Mock Test).
- **Kích thước tham khảo:**
  - Chiều rộng tối đa của khu vực nhập liệu: `1100px` căn giữa.
  - Chia cột đôi 50/50 cho các trường nhập số ngắn (Thời gian và Điểm số tối đa).
  - Khoảng cách dọc giữa các khối câu hỏi: `{spacing.xl}` (32px).
  - Padding trong các khối câu hỏi: `{spacing.lg}` (24px).

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh hành động cố định đầu trang (Sticky Top Bar - Vùng A)
- **Đặc tả Visual:**
  - Nền bar: Kính mờ `{colors.glass}` (`rgba(255, 255, 255, 0.7)`), có `backdrop-filter: blur(8px)`.
  - Chiều cao: `64px`. Viền dưới mờ `1px solid rgba(155, 93, 224, 0.1)`.
- **Thành phần:**
  - **Breadcrumbs:** Dòng chữ dạng `{typography.caption}` (12px), màu `{colors.text-secondary}`. Hiển thị: *"Admin / Quản lý đề thi / Soạn thảo đề thi"*.
  - **Nút "Lưu bài kiểm tra":** Style `button-primary` nền `{colors.primary}` (`#4E56C0`), chữ trắng, cao `44px`, bo góc `{rounded.lg}` (16px). Mặc định tỏa sáng `{elevation.active-glow}`. Bấm vào kích hoạt kiểm tra hợp lệ toàn bộ đề thi và gửi API lưu trữ.
  - **Nút "Hủy":** Style `button-secondary` nền `{colors.surface}`, viền mờ, chữ `{colors.primary}`, cao `44px`, bo góc `{rounded.lg}`.

### 4.2 Khối thiết lập chung của đề (General Settings - Vùng B)
- **Tên các trường nhập liệu:**
  - *Tên bài kiểm tra:* `text-input` cao `44px`, bo góc `{rounded.lg}`, nền `{colors.surface}`. Nhãn in đậm có dấu sao đỏ (*). Placeholder: *"Ví dụ: Mock Test IELTS Academic Vol 1..."*.
  - *Mô tả đề thi:* `text-input` cao `44px`, nhãn *"Mô tả ngắn"*.
  - *Thời gian làm bài (phút):* `text-input` (number) cao `44px` (ví dụ: *60*).
  - *Điểm số tối đa:* `text-input` cao `44px` (ví dụ: *9.0* hoặc *100*).

### 4.3 Khối chọn dạng đề & Soạn thảo (Test Builder Areas - Vùng C & D)
- **Dropdown chọn Dạng bài kiểm tra (Vùng C):**
  - Loại component: Dropdown/Select cao `44px`, bo góc `{rounded.lg}`, nền `{colors.surface}`.
  - Lựa chọn: *Mini-test cuối Unit*, *Level test cuối cấp độ*, *Mock Test thực tế (Full Test)*.
- **Vùng thiết kế câu hỏi dạng Mini-test / Level test (Vùng D):**
  - Khối câu hỏi thiết kế trong thẻ Card: Nền `{colors.surface}`, bo góc `{rounded.xl}` (24px), viền mờ, padding `{spacing.lg}` (24px).
  - Cho phép chọn Unit liên kết (đối với Mini-test) hoặc Cấp độ liên kết (đối với Level test).
  - Nút "+ Thêm câu hỏi": Style `button-secondary` cao `40px`, bo góc `{rounded.lg}`. Bấm vào chèn thêm một khối câu hỏi mới ở cuối.
  - Mỗi khối câu hỏi gồm: Trường nhập đề bài, điểm số, dropdown chọn loại câu hỏi (trắc nghiệm, điền từ, kéo thả), cụm nhập đáp án và tích chọn đáp án đúng, và trường nhập *"Lời giải thích chi tiết bắt buộc"*.
- **Vùng thiết kế đề thi Mock Test thực tế (Vùng D):**
  - Gồm Dropdown chọn định dạng thi (*IELTS* hoặc *TOEIC*) và Cấp độ mục tiêu.
  - **Thanh tab điều hướng kỹ năng (Tab Switcher Area):**
    - Sử dụng component `category-tab` bo tròn cao `48px`, nền `{colors.glass}`.
    - Gồm 4 tab: *Listening*, *Reading*, *Writing*, *Speaking*.
    - Tab đang được click chọn (Active) sẽ đổi nền sang `{colors.surface}` và chữ màu `{colors.primary}` (weight 600) kèm `{elevation.glow}`.
  - **Nội dung Tab-view:**
    - *Tab Listening:* Chứa File Uploader tải file Audio đề thi (.mp3) (độ cao uploader `80px`, viền nét đứt màu `{colors.secondary}`) kèm theo vùng nhập câu hỏi trắc nghiệm chia theo Section 1, 2, 3, 4.
    - *Tab Reading:* Chứa trường nhập văn bản lớn "Đoạn văn đọc hiểu Passage" và vùng soạn câu hỏi đọc hiểu (Trắc nghiệm, Matching Headings, v.v.).
    - *Tab Writing:* Chứa trường nhập đề bài luận viết, trường nhập "Cấu trúc đích bắt buộc" và "Từ khóa gợi ý" để nạp dữ liệu cho AI chấm, và trường nhập bài mẫu tham khảo.
    - *Tab Speaking:* Chứa danh sách câu hỏi Nói phân theo Part 1, 2, 3. Mỗi câu hỏi có trường nhập chữ và file uploader audio câu hỏi của giám khảo AI (.mp3).
- **Bảng cấu hình quy đổi điểm (Score Conversion Table):**
  - Hiển thị bảng dạng danh sách cuộn dọc ở dưới cùng Vùng D.
  - Liệt kê 40 hàng nhập liệu tương ứng từ 1 đến 40 câu đúng, mỗi hàng cho phép nhập Band điểm hoặc điểm số TOEIC tương đương (ví dụ: *39 câu đúng -> 9.0 IELTS*).

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Thay đổi Dạng bài kiểm tra ở Dropdown Vùng C**
  - Admin click thay đổi dạng đề $\rightarrow$ Vùng D cập nhật động biểu mẫu soạn câu hỏi tương ứng với hiệu ứng chuyển trang mượt mà.
- **Hành động: Click nút "Lưu bài kiểm tra"**
  - Hệ thống kiểm tra hợp lệ dữ liệu toàn bộ đề thi:
    - Tên đề, thời gian, điểm tối đa không được trống.
    - Tất cả câu hỏi phải có đáp án đúng và lời giải thích chi tiết.
    - Với Mock test: Phải cấu hình đầy đủ cả 4 phần kỹ năng Listening, Reading, Writing, Speaking và có bảng quy đổi điểm.
    - Tên đề thi không trùng lặp trong cùng danh mục.
    - *Nhánh hợp lệ:* Nút Lưu hiển thị Loading $\rightarrow$ Gửi API lưu trữ đề thi $\rightarrow$ Thành công $\rightarrow$ Chuyển hướng quay lại danh sách đề thi `AD-04` $\rightarrow$ Hiện Toast màu xanh lá `{colors.success}`: *"Tạo bài kiểm tra thành công!"*.
    - *Nhánh lỗi cấu trúc (Rẽ nhánh E-1/E-2):* Giữ nguyên màn hình, bôi đỏ trường bị lỗi màu `{colors.error}` kèm dòng chữ lỗi đỏ: *"Đề thi không hợp lệ: các câu hỏi phải có đáp án đúng, trọng số điểm khác 0, và bài thi Mock Test phải có đầy đủ 4 phần thi kỹ năng"*.
  - **API Lưu bài kiểm tra:** `POST /api/tests/save-test`
    - Payload: `{ "testId": 5, "name": "IELTS Mock Test 1", "duration": 180, "maxScore": 9.0, "type": "mock_test", "sections": { "listening": {...}, "reading": {...}, "writing": {...}, "speaking": {...} } }`
    - Response: `{ "success": true }`

---

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái tải dữ liệu (Loading State):** Khi bấm nút Lưu, nút chuyển sang trạng thái Loading (hiển thị spinner mờ, khóa click), đồng thời hiển thị overlay che mờ mỏng trang web biểu thị đang đồng bộ dữ liệu.
- **Trạng thái lỗi API (Error State):** Nếu API lưu thất bại, hiển thị thông báo lỗi màu đỏ ngay dưới nút Lưu và bôi đỏ trường lỗi.

---

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [test_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/test_list_page.md) khi click nút "Tạo đề thi mới" hoặc nút "Sửa" đề thi cũ.
- **Đi đến:** Quay lại [test_list_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/admin-dashboard/test_list_page.md) sau khi click lưu thành công hoặc bấm nút hủy.

---

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Thiết kế các tab kỹ năng Mock Test phản hồi chuyển đổi tức thì không có độ trễ giật lag để Admin thuận tiện rà soát nội dung.
- **KHÔNG ĐƯỢC:** Sử dụng bất cứ bóng đổ dạng xám đen nào dưới các thẻ Card và Uploader. Chỉ sử dụng các cấp độ phát quang `{elevation.glow}` và viền mờ theo định hướng hệ thống Light Mode Universe để giữ nét tối giản, thoáng khí.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Thông tin cấu hình bài thi (Test Configuration Form fields):** Liên kết với cấu trúc bài thi mẫu trong mảng `tests` (ví dụ: `tests[1]` cho bài thi cuối Unit 2) để pre-fill các trường biểu mẫu soạn đề (tên bài thi, mô tả, thời gian làm bài, điểm tối đa).
