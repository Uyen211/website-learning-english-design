# MÀN HÌNH: LESSON CONFIGURATION PAGE (MÀN HÌNH CẤU HÌNH BÀI HỌC & BÀI TẬP)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Lesson Configuration Page (Màn hình cấu hình bài học & bài tập)
- Mã use case liên quan: UC-03a, UC-03b
- Mã luồng người dùng liên quan: Flow AD-FL-03 (Cấu hình Bài học và Luyện tập)
- Vai trò người dùng: Admin (Quản trị viên)
- Vị trí trong sitemap: Trang chủ quản trị -> AD-01 -> AD-02 -> AD-03 -> AD-03-Form: Lesson Configuration Page (URL: /admin/lessons/{lesson_id}/configure)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Quản trị viên sử dụng màn hình này để đặt tên bài học, tích chọn các hình thức bài tập áp dụng cho bài học đó và nhập chi tiết dữ liệu giảng dạy, tải lên tệp âm thanh/hình ảnh cùng đáp án và lời giải thích chi tiết cho từng phần bài tập tương ứng.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục một cột cuộn dọc có thanh điều hướng cố định phía trên (Top Sticky Navbar).
- Các vùng chính trên màn hình:
  - Vùng A: Thanh tiêu đề cố định phía trên (Sticky Action Bar) chứa Breadcrumbs, nút "Lưu bài học" và nút "Hủy".
  - Vùng B: Vùng thông tin chung của bài học (General Info Section) nằm trên cùng của thân trang, hiển thị tên và thể loại bài học.
  - Vùng C: Vùng chọn hình thức bài tập (Exercise Selector Section) hiển thị các hộp kiểm (checkboxes) tương ứng với thể loại bài học.
  - Vùng D: Vùng soạn thảo chi tiết (Dynamic Content Builder Section) hiển thị động các form biểu mẫu nhập liệu dựa theo các checkbox được tích chọn ở Vùng C.
- Kích thước / Grid tham khảo:
  - Vùng nội dung chính căn giữa, có chiều rộng tối đa 1000px để Admin tập trung cao độ vào việc nhập liệu.
  - Khoảng cách dọc giữa các phân đoạn chính: spacing-xl (32px).
  - Khoảng cách padding trong các khối nhập liệu: spacing-lg (24px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)
- **Tên component:** Thanh hành động cố định đầu trang (Sticky Action Bar)
  - **Loại component tham chiếu từ DESIGN.md:** top-nav (chiều cao 64px, nền canvas #fffaf0, border-bottom 1px hairline #e5e5e5)
  - **Vị trí:** Vùng A.
  - **Trạng thái:** Mặc định cố định ở đầu viewport khi cuộn trang.

- **Tên component:** Nút "Lưu bài học"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng A, góc trên bên phải.
  - **Trạng thái:** Mặc định, hover, loading (hiển thị spinner xoay vòng, khóa click).
  - **Dữ liệu hiển thị / hành vi:** Hiển thị text "Lưu bài học". Nhấn vào kích hoạt kiểm tra hợp lệ dữ liệu và gửi API.

- **Tên component:** Nút "Hủy"
  - **Loại component tham chiếu từ DESIGN.md:** button-secondary (nền canvas #fffaf0, border 1px hairline #e5e5e5, chữ ink #0a0a0a, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng A, bên trái nút Lưu.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Hủy". Nhấp vào để hủy các sửa đổi và quay lại màn hình AD-03.

- **Tên component:** Trường nhập Tên bài học
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-md 12px, height 44px, font Inter size 15px)
  - **Vị trí:** Vùng B, nằm phía bên trái.
  - **Trạng thái:** Mặc định, focus, error.
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Tên bài học *". Placeholder: "Nhập tên bài học...". Đây là trường bắt buộc.

- **Tên component:** Trường Thể loại bài học (locked)
  - **Loại component tham chiếu từ DESIGN.md:** badge-pill (nền surface-strong #ebe6d6, chữ ink #0a0a0a, font Inter weight 600, size 13px)
  - **Vị trí:** Vùng B, nằm bên phải trường Tên bài học.
  - **Trạng thái:** Read-only (đã được khóa tự động dựa trên cấu trúc bài học của hệ thống).
  - **Dữ liệu hiển thị / hành vi:** Hiển thị nhãn cố định như: "Thể loại: Từ vựng", "Thể loại: Luyện nghe", v.v.

- **Tên component:** Nhóm hộp kiểm hình thức bài tập (Exercise Form Checkboxes)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền surface-card #f5f0e0, rounded-lg 16px, padding 20px)
  - **Vị trí:** Vùng C.
  - **Trạng thái:** Mặc định. Các checkbox có thể tích chọn/bỏ chọn.
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Chọn hình thức bài tập áp dụng". Hiển thị danh sách checkbox thay đổi động theo Thể loại bài học:
    - *Với Từ vựng:* Flashcards SRS, Kéo thả/Ghép đôi, Đoán nghĩa ngữ cảnh, Dự đoán từ, Đọc to từ vựng, Viết câu cá nhân hóa.
    - *Với Ngữ pháp:* Focus Mode, Nhận diện khuôn mẫu, Cặp câu tương phản, Cấu trúc hạt nhân, Chính tả chunk, Viết lại câu, Viết câu cá nhân hóa.
    - *Với Luyện nghe:* Interactive Stories, Trắc nghiệm nghe hiểu, Shadowing.
    - *Với Luyện nói:* Phát âm từ/câu, Hội thoại nhập vai AI.
    - *Với Luyện đọc:* Đọc hiểu thông thường, Đọc báo chí thực tế.
    - *Với Luyện viết:* Ghép câu (Basic), Viết gợi ý 3 vòng (Cá Voi Thông Thái), Viết luận chấm AI.

- **Tên component:** Vùng soạn thảo chi tiết (Dynamic Form Blocks)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền surface-card #f5f0e0, border 1px hairline #e5e5e5, rounded-xl 24px, padding 24px)
  - **Vị trí:** Vùng D.
  - **Trạng thái:** Xuất hiện/Ẩn động theo lựa chọn ở Vùng C.
  - **Dữ liệu hiển thị / hành vi:** Chứa các biểu mẫu nhập liệu chi tiết. Với từng hình thức bài tập được chọn, sẽ hiển thị một khối form soạn thảo tương ứng.
    - *Khối Flashcard SRS:* Ô nhập từ vựng, phiên âm IPA, định nghĩa, khu vực tải ảnh lên (kéo thả tệp), khu vực tải tệp âm thanh phát âm (.mp3), ô nhập văn bản lớn "Lời giải thích chi tiết".
    - *Khối Kéo thả/Ghép đôi:* Danh sách các cặp Từ - Nghĩa/Ảnh (cho phép bấm nút "Thêm dòng" để tạo nhiều cặp).
    - *Khối Đoán nghĩa ngữ cảnh:* 3-4 ô nhập câu ví dụ ngữ cảnh, khu vực tải tệp âm thanh tương ứng, ô giải thích.
    - *Khối Đọc hiểu thông thường:* Ô nhập văn bản lớn "Đoạn văn đọc hiểu", danh sách câu hỏi trắc nghiệm (cho phép tạo câu hỏi, nhập các tùy chọn A, B, C, D, tích chọn đáp án đúng và nhập lời giải thích chi tiết).
    - *Khối Viết luận chấm AI:* Ô nhập đề bài luận, các ô chọn tiêu đề, trường nhập danh sách từ khóa bắt buộc/cấu trúc gợi ý để Cá Voi chấm điểm, bài viết mẫu.

- **Tên component:** Khu vực tải tệp lên (File Uploader)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, border 1px dashed #6a6a6a, rounded-md 12px, height 80px, căn giữa văn bản)
  - **Vị trí:** Nằm bên trong các khối form ở Vùng D yêu cầu tệp tin.
  - **Trạng thái:** Mặc định, drag-over (viền đổi màu primary #0a0a0a), success (hiển thị tên tệp đã chọn kèm dung lượng).
  - **Dữ liệu hiển thị / hành vi:** Hiển thị biểu tượng 3D claymation nhỏ của file nhạc/ảnh và dòng chữ "Kéo thả tệp âm thanh/hình ảnh vào đây hoặc nhấp để chọn".

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động:** Tích chọn/Bỏ chọn một Hộp kiểm hình thức bài tập ở Vùng C
  - **Luồng chính:** Admin click vào checkbox -> Hệ thống hiển thị mượt mà (fade-in) khối form soạn thảo của hình thức đó ở Vùng D. Nếu bỏ tích -> Ẩn khối form đó đi (dữ liệu trong khối đó sẽ bị xóa để tránh gửi thừa dữ liệu lên server).
- **Hành động:** Nhấp nút "Lưu bài học"
  - **Luồng chính:**
    1. Admin click nút "Lưu bài học".
    2. Hệ thống kiểm tra hợp lệ dữ liệu của tất cả các khối form đang hiển thị ở Vùng D:
       - Tên bài học không được trống.
       - Mỗi câu hỏi phải có đáp án đúng được tích chọn và có lời giải thích chi tiết.
       - Tệp âm thanh phải là MP3/WAV dưới 5MB. Tệp ảnh phải là JPG/PNG dưới 2MB.
    3. *Nhánh hợp lệ:* Nút Lưu chuyển sang trạng thái Loading -> Gửi API cập nhật bài học -> API trả về thành công -> Quay lại màn hình AD-03 -> Hiển thị Toast thông báo xanh lá: "Cấu hình bài học thành công!".
    4. *Nhánh lỗi thông tin (Rẽ nhánh E-1/E-2):* Hệ thống giữ nguyên trang, cuộn màn hình đến vị trí lỗi đầu tiên. Bôi đỏ viền ô nhập bị lỗi, hiển thị text báo lỗi đỏ bên dưới: "Vui lòng điền đầy đủ thông tin..." hoặc "Định dạng tệp không tương thích...".
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: `{ "lessonId": 24, "name": "Everyday Objects", "category": "vocabulary", "appliedForms": ["flashcard", "dictation"], "flashcardData": { "word": "Apple", "ipa": "/ˈæp.əl/", "meaning": "Quả táo", "audioUrl": "files/apple.mp3", "imageUrl": "files/apple.png", "explanation": "Apple là một danh từ..." }, "dictationData": { "audioUrl": "files/apple.mp3", "correctText": "apple", "explanation": "Học viên nghe và gõ lại..." } }`
    - Nhận về: `{ "success": true }`

- **Hành động:** Kéo thả tệp tin vào Khu vực tải tệp
  - **Luồng chính:** Admin kéo file thả vào ô tải tệp -> Hệ thống kiểm tra dung lượng và định dạng:
    - *Hợp lệ:* Hiển thị tên file màu xanh lá kèm nút "Xóa tệp".
    - *Lỗi:* Báo đỏ viền ô uploader và hiển thị dòng chữ lỗi đỏ: "Tệp âm thanh phải dưới 5MB và ở định dạng MP3/WAV!".

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Khi bài học chưa được cấu hình, Vùng D hiển thị trống hoàn toàn cho đến khi có ít nhất một checkbox ở Vùng C được tích chọn.
- **Trạng thái tải (loading state):** Khi đang tải dữ liệu cũ (đối với chế độ Sửa cấu hình), toàn bộ form hiển thị các vòng xoay spinner và skeleton cho đến khi dữ liệu hiển thị đầy đủ. Nút Lưu bị vô hiệu hóa.
- **Trạng thái lỗi (error state):** Nếu API lưu thất bại do mất mạng hoặc lỗi máy chủ, hiển thị thông báo lỗi màu đỏ ngay bên dưới nút Lưu để Admin biết.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ màn hình danh sách bài học AD-03 sau khi Admin click nút "Cấu hình" hoặc "Sửa cấu hình" của một bài học cụ thể.
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Chuyển hướng quay trở lại màn hình danh sách bài học AD-03.
- **Các màn hình liên quan khác:** Không có.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0).
- Các khối form soạn thảo ở Vùng D được đặt trong thẻ `feature-card-cream` màu surface-card (#f5f0e0), có bo tròn lớn rounded-xl (24px) giúp phân tách rõ ràng từng nhóm câu hỏi/hình thức bài tập.
- Sử dụng Nguyên tắc Báo hiệu (Signaling Principle) bằng cách in đậm các nhãn trường bắt buộc kèm dấu sao đỏ (*), viền đỏ và nhãn lỗi (#ef4444) nổi bật trên nền canvas để dễ nhận diện lỗi.
- Đảm bảo khoảng cách spacing-md (16px) giữa các trường nhập liệu và spacing-xl (32px) giữa các khối form để tránh gây cảm giác ngột ngạt và rối mắt cho Admin khi soạn thảo đề bài dài.
- Chiều cao các trường nhập là 44px, nút uploader có chiều cao 80px để thuận tiện click chọn.



