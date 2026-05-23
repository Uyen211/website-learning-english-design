# MÀN HÌNH: CREATE / EDIT TEST PAGE (MÀN HÌNH SOẠN THẢO BÀI KI KIỂM TRA)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Create / Edit Test Page (Màn hình soạn thảo bài kiểm tra: Mini-test / Level test / Mock test)
- Mã use case liên quan: UC-04a, UC-04b
- Mã luồng người dùng liên quan: Flow AD-FL-04 (Quản lý Bài kiểm tra)
- Vai trò người dùng: Admin (Quản trị viên)
- Vị trí trong sitemap: Trang chủ quản trị -> AD-04 -> AD-04-Form: Create / Edit Test Page (URL: /admin/tests/create hoặc /admin/tests/{test_id}/edit)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng màn hình này để nhập thông tin thiết lập chung của đề thi (Tên đề, mô tả, thời gian, thang điểm), lựa chọn định dạng đề (Mini-test, Level test, Mock test) và tiến hành soạn thảo câu hỏi, đáp án, tải lên file âm thanh phát và nhập bảng quy đổi điểm tương ứng cho bài kiểm tra.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục một cột có thanh hành động cố định đầu trang (Sticky Header Action Bar) và phân phân hệ dạng tab bên trong thân trang.
- Các vùng chính trên màn hình:
  - Vùng A: Thanh hành động cố định (Sticky Top Bar) chứa Breadcrumbs điều hướng, nút "Lưu bài kiểm tra" và nút "Hủy".
  - Vùng B: Biểu mẫu Thiết lập chung (General Settings Form) ở trên cùng của thân trang.
  - Vùng C: Khu vực chuyển đổi loại đề kiểm tra (Test Type Customizer Layout). Khi chọn một loại, giao diện Vùng D sẽ thay đổi tương ứng.
  - Vùng D: Vùng thiết kế câu hỏi động (Dynamic Question Builder / Section Editor).
- Kích thước / Grid tham khảo:
  - Chiều rộng tối đa của khu vực nhập liệu: 1100px căn giữa màn hình.
  - Layout chia đôi 2 cột cho các trường nhập số ngắn (Thời gian và Điểm tối đa) để tối ưu không gian.
  - Khoảng cách padding trong các khối nhập câu hỏi: spacing-lg (24px).
  - Khoảng cách dọc giữa các khối: spacing-xl (32px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)
- **Tên component:** Thanh hành động cố định (Sticky Top Bar)
  - **Loại component tham chiếu từ DESIGN.md:** top-nav (nền canvas #fffaf0, height 64px, border-bottom 1px hairline #e5e5e5)
  - **Vị trí:** Vùng A.
  - **Trạng thái:** Mặc định.

- **Tên component:** Nút "Lưu bài kiểm tra"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng A, góc trên bên phải.
  - **Trạng thái:** Mặc định, hover, loading.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Lưu bài kiểm tra". Click để kiểm tra tính hợp lệ và lưu đề thi.

- **Tên component:** Nút "Hủy"
  - **Loại component tham chiếu từ DESIGN.md:** button-secondary (nền canvas #fffaf0, border 1px hairline #e5e5e5, chữ ink #0a0a0a, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng A, bên trái nút Lưu.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Hủy". Nhấn để quay lại AD-04.

- **Tên component:** Trường nhập Tên bài kiểm tra
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Mặc định, focus, error.
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Tên bài kiểm tra *". Placeholder: "Ví dụ: Mock Test IELTS Academic Vol 1...". Bắt buộc nhập.

- **Tên component:** Trường nhập Mô tả đề thi
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Mặc định, focus.
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Mô tả ngắn". Placeholder: "Ví dụ: Đề thi thử đánh giá năng lực đầu ra...".

- **Tên component:** Trường nhập Thời gian làm bài
  - **Loại component tham chiếu từ DESIGN.md:** text-input / number input (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng B (cột trái của hàng đôi).
  - **Trạng thái:** Mặc định, focus, error.
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Thời gian làm bài (phút) *". Nhập số phút làm bài (ví dụ: 60). Bắt buộc nhập.

- **Tên component:** Trường nhập Điểm tối đa
  - **Loại component tham chiếu từ DESIGN.md:** text-input / number input (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng B (cột phải của hàng đôi).
  - **Trạng thái:** Mặc định, focus.
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Điểm số tối đa *". Nhập điểm tối đa của đề thi (ví dụ: 100 hoặc 9.0). Bắt buộc nhập.

- **Tên component:** Dropdown chọn Dạng bài kiểm tra
  - **Loại component tham chiếu từ DESIGN.md:** dropdown / select (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng C.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Chọn dạng bài kiểm tra *". Danh sách lựa chọn gồm: "Mini-test cuối Unit", "Level test cuối cấp độ", "Mock Test thực tế (Full Test)".

- **Tên component:** Khu vực thiết kế câu hỏi dạng Mini-test / Level test
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền surface-card #f5f0e0, border 1px hairline #e5e5e5, rounded-xl 24px, padding 24px)
  - **Vị trí:** Vùng D (hiển thị khi chọn Mini-test hoặc Level test).
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** 
    - Dropdown chọn Unit (nếu là Mini-test) hoặc Cấp độ (nếu là Level test) để liên kết.
    - Cho phép bấm nút "+ Thêm câu hỏi" để chèn thêm một khối câu hỏi mới.
    - Mỗi khối câu hỏi chứa: Đề bài (text-input), Điểm số câu (number), Loại câu hỏi (trắc nghiệm, điền từ, kéo thả), các ô nhập đáp án lựa chọn và tích chọn đáp án đúng, và ô nhập văn bản "Lời giải thích chi tiết *".

- **Tên component:** Khu vực thiết kế Mock Test thực tế (IELTS / TOEIC)
  - **Loại component tham chiếu từ DESIGN.md:** tab-bar / category-tab (nền canvas #fffaf0, rounded-lg)
  - **Vị trí:** Vùng D (hiển thị khi chọn Mock Test thực tế).
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** 
    - Dropdown chọn định dạng thi: "IELTS" hoặc "TOEIC".
    - Dropdown chọn Cấp độ mục tiêu.
    - Thanh điều hướng ngang gồm 4 Tab kỹ năng: "Listening", "Reading", "Writing", "Speaking".
    - Bảng cấu hình "Bảng quy đổi điểm" (Quy đổi điểm thô ra Band điểm IELTS hoặc điểm số TOEIC).

- **Tên component:** Tab-view Listening (trong Mock Test)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền surface-card #f5f0e0, padding 24px)
  - **Vị trí:** Vùng D, hiển thị khi click tab "Listening".
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** 
    - Khu vực tải file đề thi Listening (.mp3) bằng File Uploader (chỉ nhận file dưới 5MB).
    - Vùng soạn câu hỏi trắc nghiệm/điền từ/nhãn bản đồ chia theo các Section 1, 2, 3, 4. Mỗi câu hỏi bắt buộc nhập đáp án đúng và giải thích chi tiết.

- **Tên component:** Tab-view Reading (trong Mock Test)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card
  - **Vị trí:** Vùng D, hiển thị khi click tab "Reading".
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** 
    - Trường nhập văn bản lớn "Đoạn văn đọc hiểu Passage" (text-area, tối thiểu 300 dòng chữ).
    - Vùng soạn câu hỏi đọc hiểu tương ứng với đoạn văn (Trắc nghiệm, Matching Headings, True/False/Not Given). Bắt buộc chọn đáp án đúng và nhập giải thích.

- **Tên component:** Tab-view Writing (trong Mock Test)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card
  - **Vị trí:** Vùng D, hiển thị khi click tab "Writing".
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** 
    - Trường soạn đề bài viết luận (ví dụ: Task 1 và Task 2 đối với IELTS).
    - Ô nhập "Cấu trúc đích bắt buộc" và "Từ khóa gợi ý" ngăn cách nhau bằng dấu phẩy để hệ thống nạp dữ liệu cho AI chấm điểm tự động.
    - Trường nhập văn bản lớn "Bài mẫu gợi ý".

- **Tên component:** Tab-view Speaking (trong Mock Test)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card
  - **Vị trí:** Vùng D, hiển thị khi click tab "Speaking".
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** 
    - Danh sách các câu hỏi Nói phân theo Part 1, 2, 3.
    - Với mỗi câu hỏi: Trường nhập câu hỏi chữ, và uploader tệp âm thanh của giám khảo AI phát âm câu hỏi (.mp3).

- **Tên component:** Bảng quy đổi điểm (Score Conversion Table)
  - **Loại component tham chiếu từ DESIGN.md:** table / input-row
  - **Vị trí:** Vùng D, nằm dưới 4 tab kỹ năng.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị 40 hàng nhập liệu quy đổi số câu đúng sang Band điểm tương ứng (ví dụ: 39-40 câu đúng -> IELTS Band 9.0).

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động:** Thay đổi Dạng bài kiểm tra ở Dropdown Vùng C
  - **Luồng chính:** Admin thay đổi dạng -> Vùng D hiển thị mượt mà biểu mẫu soạn câu hỏi tương thích:
    - Chọn "Mini-test" -> Hiển thị form liên kết Unit + soạn câu hỏi ngắn.
    - Chọn "Mock test" -> Hiển thị form chọn định dạng IELTS/TOEIC + 4 tab kỹ năng + Bảng quy đổi điểm.
- **Hành động:** Nhấp nút "Lưu bài kiểm tra"
  - **Luồng chính:**
    1. Hệ thống thực hiện kiểm tra tính hợp lệ của đề thi:
       - Tên đề, thời gian, điểm tối đa không được trống.
       - Tất cả các câu hỏi phải có đáp án đúng được thiết lập.
       - Mỗi câu hỏi bắt buộc nhập "Lời giải thích chi tiết".
       - Đối với Mock test, phải cấu hình đầy đủ cả 4 phần kỹ năng Listening, Reading, Writing, Speaking và có bảng quy đổi điểm.
       - Tên bài kiểm tra không được trùng lặp trong cùng danh mục.
    2. *Nhánh hợp lệ:* Nút Lưu hiển thị Loading -> Gửi yêu cầu API lưu trữ -> API trả về thành công -> Quay lại AD-04 -> Hiển thị Toast thông báo xanh lá thành công.
    3. *Nhánh lỗi cấu trúc (Rẽ nhánh E-1/E-2):* Giữ nguyên trang, báo đỏ trường lỗi, hiển thị text đỏ "Đề thi không hợp lệ: các câu hỏi phải có đáp án đúng, trọng số điểm khác 0, và bài thi Mock Test phải có đầy đủ 4 phần thi kỹ năng".
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: `{ "testId": 5, "name": "IELTS Full Test 1", "duration": 180, "maxScore": 9.0, "type": "mock_test", "format": "IELTS", "sections": { "listening": { "audioUrl": "...", "questions": [...] }, "reading": {...}, "writing": {...}, "speaking": {...} }, "scoreMap": { "40": 9.0, "39": 9.0, "38": 8.5, ... } }`
    - Nhận về: `{ "success": true }`

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Khi tạo mới, các form trống kèm placeholder. Khi sửa, dữ liệu đề cũ tự động điền sẵn vào các trường nhập và tab tương ứng.
- **Trạng thái tải (loading state):** Khi nhấn Lưu, nút Lưu khóa click và hiển thị spinner. Toàn bộ trang bị phủ một màng mờ mỏng biểu thị đang đồng bộ dữ liệu.
- **Trạng thái lỗi (error state):** Khi API trả về lỗi trùng tên hoặc lỗi CSDL, hiển thị thông báo lỗi màu đỏ ngay dưới nút Lưu và bôi đỏ trường tương ứng (ví dụ: trường Tên bài kiểm tra).

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ màn hình danh sách bài kiểm tra AD-04 sau khi Admin click nút "Tạo đề thi mới" hoặc nút "Sửa" đề thi cũ.
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Chuyển hướng quay trở lại màn hình AD-04.
- **Các màn hình liên quan khác:** Không có.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0).
- Các tab kỹ năng sử dụng component `category-tab` bo tròn, tab active hiển thị màu surface-card (#f5f0e0), chữ in đậm ink để làm nổi bật phân đoạn đang soạn thảo.
- Việc soạn thảo Mock Test rất đồ sộ, do đó khoảng cách giữa các khối câu hỏi được giãn rộng spacing-xl (32px) để giảm tải nhận thức (Coherence Principle), giúp Admin không bị rối mắt.
- Các trường bắt buộc được đánh dấu dấu sao đỏ (*), viền đỏ cảnh báo khi trống theo Nguyên tắc Báo hiệu (Signaling Principle) để hướng mắt Admin vào phần cần sửa đổi nhanh nhất.
- Chiều cao các nút bấm và ô nhập liệu là 44px đảm bảo touch target chuẩn mực.



