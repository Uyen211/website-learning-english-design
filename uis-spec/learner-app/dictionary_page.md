# MÀN HÌNH: DICTIONARY / SEARCH RESULT PAGE (MÀN HÌNH CHI TIẾT TRA CỨU TỪ ĐIỂN)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Dictionary / Search Result Page (Màn hình chi tiết tra cứu từ điển)
- Mã màn hình: LN-14
- Mã use case liên quan: UC-08 (Tra cứu nhanh và ôn tập lặp lại ngắt quãng SRS)
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Dashboard -> Click tab "Tra cứu & Ôn tập" -> Nhập từ khóa tại Search Bar -> Click chọn từ gợi ý -> Dictionary Page (URL: /dictionary/{word_slug})

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này để xem giải nghĩa chi tiết của một từ vựng hoặc cấu trúc ngữ pháp sau khi tìm kiến, bao gồm phiên âm, âm thanh, định nghĩa ngữ cảnh, ví dụ thực tế và các collocations đi kèm. Học viên cũng có thể chủ động lưu từ này vào sổ tay ôn tập SRS cá nhân.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục một cột căn giữa (Single Column Centered) trên nền canvas sáng ấm (#fffaf0).
- Các vùng chính trên màn hình:
  - Vùng A: Thanh điều hướng phía trên (Header Navigation) chứa nút Back.
  - Vùng B: Thông tin chính về từ vựng (Word Header - IPA, Audio).
  - Vùng C: Nội dung định nghĩa và ví dụ chi tiết (Meaning & Examples).
  - Vùng D: Các thông tin bổ trợ (Collocations, Common Mistakes).
  - Vùng E: Nút hành động chính (Action Bar - Save to SRS).
- Kích thước / Grid tham khảo:
  - Chiều rộng tối đa khối nội dung: 800px.
  - Khoảng cách padding: spacing-xl (32px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)

### THÀNH PHẦN ĐIỀU HƯỚNG (HEADER)
- **Tên component:** Nút "Quay lại" (Back Button)
  - **Loại component tham chiếu từ DESIGN.md:** button-text-link (màu muted #6a6a6a, font Inter 14px, weight 600)
  - **Vị trí:** Vùng A.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "← Quay lại". Click sẽ quay trở lại trang trước đó (thường là Personal Review Dashboard).

### THÀNH PHẦN NỘI DUNG CHÍNH (CONTENT AREA)
- **Tên component:** Chi tiết từ vựng (Word Header)
  - **Loại component tham chiếu từ DESIGN.md:** title-lg (Plain Black 32px, weight 600)
  - **Vị trí:** Vùng B.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị từ vựng mục tiêu, phiên âm IPA (ví dụ: "collaborate /kəˈlæb.ə.reɪt/"), kèm nút icon loa (audio-trigger) kế bên.

- **Tên component:** Bảng định nghĩa (Definition Card)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền surface-card #f5f0e0, border 1px hairline #e5e5e5, rounded-lg 16px, padding 24px)
  - **Vị trí:** Vùng C.
  - **Dữ liệu hiển thị / hành vi:**
    - Loại từ: "Động từ (Verb)".
    - Định nghĩa: "Hợp tác, cộng tác làm việc cùng người khác để tạo ra thứ gì đó.".
    - Ví dụ: Danh sách các câu ví dụ (Typography: body-md, màu Navy đậm #0a0a0a).

- **Tên component:** Thông tin bổ trợ (In-depth Usage)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền canvas #fffaf0, rounded-lg 16px, padding 24px)
  - **Vị trí:** Vùng D.
  - **Dữ liệu hiển thị / hành vi:**
    - Collocations: Hiển thị các cụm từ đi kèm (ví dụ: "collaborate on", "collaborate with").
    - Common Mistakes: Cảnh báo lỗi sai phổ biến.

### THÀNH PHẦN HÀNH ĐỘNG (FOOTER ACTION)
- **Tên component:** Nút "Thêm vào sổ tay SRS" (Save to SRS Button)
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, height 48px, rounded-md 12px, width 100%)
  - **Vị trí:** Vùng E.
  - **Trạng thái:** 
    - Mặc định: Nền đen chữ trắng.
    - Đã lưu: Nền surface-strong #ebe6d6, chữ muted, hiển thị text "Đã có trong sổ tay SRS".

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Click nút phát âm thanh**
  - Hệ thống phát file .mp3 phát âm bản xứ tương ứng với từ vựng.
- **Hành động: Click nút "Thêm vào sổ tay SRS"**
  - **Luồng chính:** Hệ thống gửi yêu cầu API lưu vào CSDL cá nhân. Hiển thị Toast thông báo thành công: "Đã thêm 'collaborate' vào lộ trình ôn tập!". Nút chuyển sang trạng thái disabled/already-saved.
- **Hành động: Click nút Quay lại**
  - Quay về URL: `/review`.

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Empty State:** Trường hợp slug word không tồn tại trong từ điển hệ thống -> Hiển thị trang 404 custom với minh họa 3D Claymation kèm nút "Quay lại tìm kiếm".
- **Loading State:** Hiển thị skeleton loading cho khối Definition Section khi đang cào dữ liệu từ điển.
