# MÀN HÌNH: DICTIONARY / SEARCH RESULT PAGE (MÀN HÌNH CHI TIẾT TRA CỨU TỪ ĐIỂN)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Dictionary / Search Result Page (Màn hình chi tiết tra cứu từ điển)
- **Mã màn hình:** LN-14
- **Mã use case liên quan:** UC-08 (Tra cứu nhanh và ôn tập lặp lại ngắt quãng SRS)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Dashboard $\rightarrow$ Click tab "Tra cứu & Ôn tập" $\rightarrow$ Nhập từ khóa tại thanh tìm kiếm $\rightarrow$ Click chọn từ gợi ý $\rightarrow$ Dictionary Page (URL: `/dictionary/{word_slug}`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này để xem giải nghĩa toàn diện và chi tiết của một từ vựng hoặc cấu trúc ngữ pháp cụ thể. Trang cung cấp thông tin chuẩn xác bao gồm phiên âm IPA, phát âm giọng bản xứ trực quan, phân loại từ, định nghĩa tiếng Việt/tiếng Anh, ví dụ ngữ cảnh thực tế, các cấu trúc collocation đi kèm, lỗi sai phổ biến (Common Mistakes), và nút lưu nhanh từ vựng vào lộ trình ôn tập lặp lại ngắt quãng (SRS).

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục một cột căn giữa hoàn toàn (Single Column Centered Layout) tập trung cao độ vào nội dung thông tin tra cứu.
- **Màu nền chung:** Nền trang sử dụng tông màu `{colors.canvas}` (`#F9F7FE`) dịu nhẹ, kết hợp dải mờ `{gradients.atmosphere-haze}` tạo cảm giác mở rộng và thoáng đãng.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Navigation Header (Vùng A):** Chứa nút "Quay lại" điều hướng mượt mà về trang trước.
  - **Zone 2: Word Main Info (Vùng B):** Khối thông tin đầu từ gồm từ vựng, phiên âm IPA và nút phát âm thanh.
  - **Zone 3: Meaning & Examples Card (Vùng C):** Thẻ lớn chứa phân loại từ, định nghĩa chi tiết và các câu ví dụ minh họa ngữ cảnh.
  - **Zone 4: In-depth Usage Card (Vùng D):** Thẻ chứa thông tin bổ trợ nâng cao như collocations thường gặp và các lỗi sai kinh điển khi sử dụng.
  - **Zone 5: Floating/Bottom Action Bar (Vùng E):** Chứa nút lưu vào lộ trình ôn tập SRS cá nhân.
- **Kích thước tham khảo:**
  - Chiều rộng tối đa của khối nội dung: `800px` căn giữa.
  - Padding tổng thể: `{spacing.xl}` (32px) để các phần tử có khoảng không thở thoải mái.
  - Khoảng cách giữa các thẻ: `{spacing.lg}` (24px).

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh điều hướng & Nút "Quay lại" (Navigation Header - Vùng A)
- **Tên component:** Nút "Quay lại" (Back Button)
  - **Đặc tả Visual:**
    - Style: `button-text-link`, chữ màu `{colors.text-secondary}` (`#5A5A7A`), font Inter 14px, weight 600.
    - Icon: Mũi tên trái (Lucide `arrow-left`) kích thước `16px`.
  - **Hành vi:** Khi bấm, quay trở về trang Bảng điều khiển tra cứu & ôn tập cá nhân `/review` (LN-12) hoặc trang trước đó trong lịch sử duyệt. Chiều cao chạm tối thiểu `44px` để tối ưu thao tác click.

### 4.2 Khối thông tin chính của từ (Word Header - Vùng B)
- **Tên component:** Word Header Detail
  - **Đặc tả Visual:**
    - Từ vựng mục tiêu: Dạng chữ `{typography.display-lg}` (Manrope, 48px, weight 700, letter-spacing -1.5px), màu `{colors.text-primary}` (`#1A1A2E`).
    - Phiên âm IPA: Dạng chữ `{typography.title-md}` (18px, Inter, weight 500), màu `{colors.secondary}` (`#9B5DE0`) để tạo điểm nhấn nhẹ. Ví dụ: `/kəˈlæb.ə.reɪt/`.
  - **Tên component:** Nút phát âm (Audio Pronunciation Trigger)
    - Đặc tả: Nút tròn đường kính `44px`, nền nhạt `{colors.light-accent}` (`#FDCFFA`), icon loa phát thanh (Lucide `volume-2`) màu `{colors.primary}` (`#4E56C0`).
    - Hiệu ứng: Hover tỏa sáng nhẹ `{elevation.glow}`.
    - Hành vi: Khi click, hệ thống tự động phát file `.mp3` giọng phát âm bản xứ chuẩn.

### 4.3 Thẻ định nghĩa và ví dụ (Definition Card - Vùng C)
- **Đặc tả Visual:**
  - Nền: `{colors.surface}` (`#FFFFFF`). Bo góc lớn: `{rounded.xl}` (24px).
  - Viền mờ: `1px solid rgba(155, 93, 224, 0.1)`. Padding: `{spacing.xl}` (32px).
  - Hiệu ứng nâng: `{elevation.glow}`.
- **Nội dung:**
  - **Loại từ (Part of Speech Tag):** Badge dạng viên thuốc `{rounded.pill}`, nền nhạt `{colors.light-accent}`, chữ màu `{colors.primary}` ghi *"Động từ (Verb)"*.
  - **Định nghĩa chính thức:** Chữ dạng `{typography.title-md}` (18px, weight 600, màu `{colors.text-primary}`). Ví dụ: *"Hợp tác, cộng tác làm việc cùng người khác để tạo ra hoặc đạt được thứ gì đó."*
  - **Các ví dụ ngữ cảnh (Contextual Examples):**
    - Danh sách các ví dụ thực tế được xếp dọc.
    - Mỗi ví dụ gồm: Câu tiếng Anh (dạng `{typography.body-md}` màu `{colors.text-primary}` đậm) và bản dịch tiếng Việt đi kèm (dạng `{typography.body-sm}` màu `{colors.text-secondary}`).
    - Ví dụ:
      - *"The two companies agreed to collaborate on the project."*
      - (Hai công ty đồng ý hợp tác cùng nhau trong dự án này.)

### 4.4 Thẻ thông tin bổ trợ (In-depth Usage Card - Vùng D)
- **Đặc tả Visual:**
  - Nền: `{colors.surface}`. Bo góc: `{rounded.xl}` (24px). Viền: `1px solid rgba(155, 93, 224, 0.1)`. Padding: `{spacing.lg}` (24px).
- **Nội dung:**
  - **Mục Cụm từ đi kèm (Collocations):**
    - Tiêu đề phụ dạng `{typography.title-md}` kèm icon tia chớp nhỏ (Lucide `sparkles`).
    - Liệt kê các cụm từ (ví dụ: *collaborate with somebody*, *collaborate on something*).
  - **Mục Lỗi thường gặp (Common Mistakes):**
    - Nền khối lỗi sai được tô màu cảnh báo nhạt `{colors.warning}` ở mức 10% opacity, viền mờ màu `{colors.warning}`.
    - Nội dung: Cảnh báo học viên tránh dùng sai giới từ (ví dụ: *"Tránh viết 'collaborate to', hãy dùng 'collaborate on/with' để diễn đạt sự hợp tác"*).

### 4.5 Nút hành động "Lưu vào sổ tay SRS" (Save to SRS Action - Vùng E)
- **Đặc tả Visual & Trạng thái chuyển đổi (State Transitions):**
  - Chiều rộng: 100% của container. Chiều cao: `48px` đạt chuẩn touch target. Bo góc: `{rounded.lg}` (16px).
  - **Trạng thái 1: Chưa lưu (Mặc định)**
    - Nút style `button-primary` nền `{colors.primary}` (`#4E56C0`), chữ trắng.
    - Nội dung: Icon dấu cộng (Lucide `plus`) + *"Thêm vào sổ tay ôn tập SRS"*.
    - Hiệu ứng: `{elevation.active-glow}`. Hover tỏa sáng `{elevation.hover-glow}`.
    - Hành vi: Học viên click $\rightarrow$ Gọi API lưu từ $\rightarrow$ Hiện Toast thông báo thành công $\rightarrow$ Chuyển sang Trạng thái 2.
  - **Trạng thái 2: Đã lưu thành công**
    - Nút chuyển sang nền nhạt `{colors.canvas}` (`#F9F7FE`), viền mờ màu `{colors.success}` (`#22C55E`), chữ màu `{colors.text-secondary}`.
    - Nội dung: Icon Bookmark (Lucide `bookmark`) màu `{colors.success}` + *"Đã có trong sổ tay SRS (Ôn tập định kỳ)"*.
    - Hiệu ứng: Không có glow. Bị disabled thao tác click để tránh gửi trùng lặp.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Lưu từ vào SRS**
  - Học viên click nút "Thêm vào sổ tay ôn tập SRS" $\rightarrow$ Nút hiển thị spinner loading mờ $\rightarrow$ Gọi API lưu trữ $\rightarrow$ Nhận kết quả thành công $\rightarrow$ Hiển thị Toast thông báo màu xanh lá `{colors.success}` ở góc phải màn hình: *"Đã thêm 'collaborate' vào lộ trình ôn tập SRS thành công!"* $\rightarrow$ Nút chuyển sang trạng thái đã lưu.
  - **API Lưu từ:** `POST /api/srs/save`
    - Payload: `{ "wordId": 45 }`
    - Response: `{ "success": true }`

---

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái không tìm thấy từ (Empty State / 404 Page):**
  - Khi slug từ vựng truy cập không tồn tại trong hệ thống từ điển $\rightarrow$ Hiển thị trang trống thiết kế cao cấp.
  - Hình ảnh: Chú Cá Voi Vũ Trụ [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`160px x 160px`) vẽ dạng ngơ ngác, đang soi kính lúp tìm kiếm các vì sao mờ ảo.
  - Thông báo: *"Rất tiếc! DiveVerse chưa tìm thấy từ vựng hoặc cấu trúc này trong từ điển vũ trụ."*
  - Nút quay lại: Style `button-primary` đưa học viên trở về Dashboard ôn tập để tìm từ khác.
- **Trạng thái tải dữ liệu (Loading State):** Hiển thị các khối skeleton mờ bo tròn che phủ phần Definition Card khi đang tải thông tin từ cơ sở dữ liệu.

---

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [personal_review_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/personal_review_page.md) sau khi học viên chọn từ gợi ý ở dropdown tìm kiếm.
- **Đi đến:** Quay lại [personal_review_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/personal_review_page.md) khi click nút quay lại.

---

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Thiết kế hiệu ứng chuyển trạng thái nút "Lưu vào SRS" thật nhẹ nhàng (sử dụng CSS transition `duration: 0.4s` cho cả màu nền và viền).
- **KHÔNG ĐƯỢC:** Sử dụng các bóng đổ thô cứng dưới các thẻ thông tin bổ trợ. Mọi cấp độ nổi đều phải dùng hiệu ứng phát quang dịu mắt `{colors.secondary}` để duy trì sự nhất quán của phong cách Light Mode Universe.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Chi tiết định nghĩa từ vựng (Dictionary Entry View):** Liên kết với các khóa từ vựng trong đối tượng `dictionary` (ví dụ: `dictionary.collaborate`, `dictionary.alternative`). Mỗi mục từ gồm:
  - Từ & Phiên âm: `{word}`, `{ipa}`
  - Từ loại & Định nghĩa tiếng Việt: `{partOfSpeech}`, `{definition}`
  - Ví dụ song ngữ Anh-Việt: `{examples}` (mảng các cặp `{en}`, `{vi}`)
  - Các Collocations: `{collocations}`
  - Lỗi sai thường gặp cần tránh: `{commonMistakes}`
