# MÀN HÌNH: SRS REVIEW PAGE (MÀN HÌNH LÀM BÀI ÔN TẬP LẶP LẠI NGẮT QUÃNG SRS)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** SRS Review Page (Màn hình làm bài ôn tập lặp lại ngắt quãng SRS)
- **Mã use case liên quan:** UC-08 (Tra cứu nhanh và ôn tập lặp lại ngắt quãng SRS)
- **Mã luồng người dùng liên quan:** Flow LN-FL-09 (Tra cứu nhanh & Ôn tập SRS)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Dashboard $\rightarrow$ Click tab "Tra cứu & Ôn tập" $\rightarrow$ Click "Ôn tập ngay" $\rightarrow$ SRS Review Page (LN-13-S1) $\rightarrow$ Bấm "Kiểm tra" $\rightarrow$ SRS Self-Evaluation View (LN-13-S2) $\rightarrow$ Hoàn thành từ cuối cùng $\rightarrow$ SRS Review Result View (LN-15) (URL: `/review/run`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này để ôn tập từ vựng và cấu trúc ngữ pháp đã học theo thuật toán lặp lại ngắt quãng (SRS). Người học điền từ vào câu ngữ cảnh khuyết dưới áp lực đồng hồ đếm ngược phản xạ 10 giây, tự đánh giá mức độ ghi nhớ (Nhớ rõ, Hơi phân vân, Quên mất) để tối ưu hóa thuật toán lặp lại, xem nhanh cứu trợ từ điển tại chỗ mà không làm mất thời gian làm bài (tạm dừng đếm ngược), và xem tổng kết hiệu năng của phiên ôn tập sau khi hoàn tất.

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục một cột căn giữa hoàn toàn (Centered Card Layout) sử dụng CSS Flexbox để neo giữ khối tương tác chính tại tâm màn hình, hạn chế tối đa các yếu tố gây nhiễu thị giác nhằm tăng cường sự tập trung cao độ.
- **Màu nền chung:** Nền trang sử dụng tông `{colors.canvas}` (`#F9F7FE`) dịu mát, được phủ lớp dải màu `{gradients.atmosphere-haze}` tạo cảm giác vũ trụ bồng bềnh.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Sticky Progress & Timer Bar (Thanh tiến độ & Đồng hồ 10 giây phản xạ):** Ghim sát mép trên màn hình.
  - **Zone 2: Central SRS Card Container (Thẻ học tập trung tâm):** Kích thước cố định `720px x 440px`, bo tròn `{rounded.xxl}` (32px), căn giữa màn hình.
  - **Zone 3: SRS Detail Lookup Modal (LN-13-M1 - Hộp thoại cứu trợ từ điển tại chỗ):** Hộp thoại kính mờ nổi đè lên trên Vùng 2 khi được kích hoạt, đồng thời tạm dừng đồng hồ đếm ngược.
  - **Zone 4: SRS Review Result View (LN-15 - Giao diện kết quả phiên ôn tập):** Hiển thị trực tiếp thay thế nội dung thẻ học tập trung tâm (Zone 2) khi học viên hoàn thành tất cả các từ trong lượt ôn tập.

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh điều hướng & Tiến độ đầu trang (Sticky Top Progress & Timer Bar)
- **Đặc tả Visual:**
  - Nền: Kính mờ `{colors.glass}` (`rgba(255, 255, 255, 0.7)`), có `backdrop-filter: blur(8px)`.
  - Chiều cao: `nav-height` (64px). Viền dưới mờ `1px solid rgba(155, 93, 224, 0.1)`.
- **Thành phần:**
  - **Thanh tiến độ (Progress Bar):** Thể hiện số lượng từ đã hoàn thành trên tổng số từ của phiên (ví dụ: *Từ 5 / 15*). Nền thanh là `{colors.light-accent}` (`#FDCFFA`), phần tiến độ chạy màu `{colors.primary}` (`#4E56C0`) kết hợp hiệu ứng sweep ánh sáng.
  - **Đồng hồ đếm ngược phản xạ 10s (10s Reaction Timer):**
    - Thiết kế: Nằm ngay dưới thanh tiến độ, độ cao cực mảnh `6px`.
    - Hành vi: Thanh thời gian co lại dần từ 100% về 0% trong 10 giây.
    - Màu sắc: Trạng thái bình thường chạy dải chuyển màu mượt `{gradients.morning-nebula}`. Khi thời gian còn dưới 3 giây, thanh chuyển sang màu cảnh báo nhấp nháy `{colors.error}` (`#EF4444`) để tăng kích thích phản xạ.
    - Chức năng: Khi đếm ngược chạm mốc `00:00`, tự động khóa trường nhập đáp án và tự động kích hoạt sự kiện "Kiểm tra" đáp án.

### 4.2 Thẻ học tập trung tâm (Central SRS Card Container - Zone 2)
- **Đặc tả Visual:**
  - Nền: `{colors.surface}` (`#FFFFFF`).
  - Bo góc: `{rounded.xxl}` (32px).
  - Hiệu ứng nâng: `{elevation.glow}` (soft glow nhẹ để thẻ lơ lửng trên canvas).
  - Viền: `1px solid rgba(155, 93, 224, 0.1)`.
  - Padding: `{spacing.xl}` (32px).
- **Thành phần bên trong:**
  - **Logo & Mascot nhỏ góc trên:** Sử dụng hình ảnh mascot [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`40px x 40px`) lấp ló góc trái trên kèm chữ "SRS Mode" dạng `{typography.caption}` để tăng tính thân thiện và nhắc nhở thương hiệu.
  - **Câu ngữ cảnh khuyết từ (Context Question Box):**
    - Font chữ: `{typography.title-lg}` (24px, Inter, weight 500), căn giữa, màu `{colors.text-primary}` (`#1A1A2E`).
    - Nội dung: Hiển thị câu bối cảnh chứa khoảng trống cần điền (ví dụ: *"We need to [ ______ ] on this project to finish it in time."*). Khoảng trống được tạo nổi bật bằng khung viền nét đứt màu `{colors.secondary}`.
    - Phía dưới hiển thị định nghĩa gợi ý nghĩa tiếng Việt dạng `{typography.body-sm}` màu `{colors.text-secondary}`.
  - **Ô nhập đáp án ôn tập (Answer Input):**
    - Loại component: `text-input` cao `48px`, bo góc `{rounded.lg}` (16px), căn giữa text.
    - Nền: `{colors.canvas}` (`#F9F7FE`). Viền mặc định: `1px solid rgba(155, 93, 224, 0.2)`. Focus: Viền tỏa sáng `{colors.primary}` (`#4E56C0`) với `{elevation.active-glow}`.
    - Chức năng: Cho phép học viên gõ đáp án. Tự động chuyển chữ thường và xóa khoảng trắng thừa ở hai đầu.
  - **Cụm nút điều khiển (Action Buttons Group):**
    - **Nút "Tra cứu nhanh":** Style `button-secondary`, viền `1px solid rgba(78, 86, 192, 0.2)`, nền `{colors.surface}`, chữ `{colors.primary}`, cao `44px`, bo góc `{rounded.lg}`.
    - **Nút "Kiểm tra":** Style `button-primary`, nền `{colors.primary}` (`#4E56C0`), chữ trắng, cao `44px`, bo góc `{rounded.lg}`, mặc định tỏa sáng `{elevation.active-glow}`. Hover tỏa sáng mạnh `{elevation.hover-glow}`.

### 4.3 Bảng tự đánh giá ghi nhớ (SRS Self-Evaluation View - LN-13-S2)
*Khi học viên click "Kiểm tra" hoặc hết 10 giây đếm ngược, cụm nút điều khiển và ô nhập đáp án sẽ biến mất để nhường chỗ cho Bảng tự đánh giá ghi nhớ hiển thị động với các thành phần:*
- **Đáp án chính thức & Phát âm:**
  - Hiển thị từ vựng mục tiêu (ví dụ: **collaborate**) dạng `{typography.display-sm}` (28px, Manrope, màu `{colors.primary}`) kèm theo ký tự phiên âm IPA (ví dụ: `/kəˈlæb.ə.reɪt/`).
  - Nút Loa phát âm: Style hình tròn `{rounded.full}` (`40px x 40px`), nền `{colors.light-accent}`, tự động phát âm thanh khi hiển thị.
- **Trạng thái Đáp án của học viên:**
  - Nếu học viên điền đúng: Hiển thị tag màu `{colors.success}` (`#22C55E`) "Chính xác!".
  - Nếu học viên điền sai hoặc hết giờ: Hiển thị câu trả lời của học viên bị gạch ngang màu `{colors.error}` (`#EF4444`) kèm tag "Chưa chính xác!".
- **Lưới 3 nút tự đánh giá (3-Up Evaluation Buttons Grid):**
  - Cấu trúc gồm 3 nút xếp ngang bằng nhau, chiều cao `48px` để tối ưu hóa touch target trên thiết bị di động:
    1. **Nút "Nhớ rõ" (Easy):** Style `button-primary` nền `{colors.primary}` (`#4E56C0`), chữ trắng. Sử dụng khi học viên gõ đúng ngay tức khắc và không cần suy nghĩ nhiều.
    2. **Nút "Hơi phân vân" (Good/Medium):** Style `button-secondary` nền `{colors.surface}`, viền `rgba(78, 86, 192, 0.3)`, chữ `{colors.primary}`. Sử dụng khi cần suy nghĩ một lát mới ra đáp án hoặc điền sai lỗi chính tả nhỏ.
    3. **Nút "Quên mất" (Hard/Reset):** Nền `{colors.error}` nhạt (`rgba(239, 68, 68, 0.1)`), chữ và viền màu `{colors.error}` (`#EF4444`). Sử dụng khi hoàn toàn không nhớ từ hoặc hết giờ mà chưa gõ được đáp án.

### 4.4 Hộp thoại xem nhanh chi tiết từ vựng (SRS Detail Lookup Modal - LN-13-M1)
- **Đặc tả Visual:**
  - Nền: Kính mờ phủ lớp che mờ `{colors.dark-floor}` ở mức `50%` opacity làm backdrop.
  - Khung nội dung: Bo góc `{rounded.xl}` (24px), nền `{colors.surface}`, viền mờ `1px solid rgba(155, 93, 224, 0.15)`, rộng `480px`, có `{elevation.hover-glow}` cực mạnh.
- **Nội dung:**
  - Từ khóa, IPA, định nghĩa chi tiết, 3 cụm collocations phổ biến và 1 câu ví dụ thực tế.
  - Nút "Đóng lại" ở dưới cùng: Style `button-primary` rộng `100%`, cao `44px`.
- **Hành vi đặc biệt:** Khi Modal mở ra $\rightarrow$ Trình đếm ngược 10 giây ở Zone 1 lập tức **tạm dừng (PAUSE)**. Khi đóng modal $\rightarrow$ Trình đếm ngược tiếp tục chạy từ số giây đã tạm dừng trước đó.

### 4.5 Khối tổng kết phiên ôn tập (SRS Review Result View - LN-15)
*Khi hoàn thành từ cuối cùng, Central Card chuyển mượt sang giao diện tổng kết với hiệu ứng Confetti nhẹ rơi tự động:*
- **Banner hoàn thành:**
  - Nền dải màu chuyển `{gradients.morning-nebula}` sang xịn mịn, bo góc `{rounded.xl}` (24px), padding `{spacing.lg}` (24px).
  - Tiêu đề: *"Hoàn thành phiên ôn tập hôm nay!"* dạng `{typography.title-lg}` (24px, Manrope, màu trắng).
  - Hình minh họa Mascot: Chú Cá Voi Vũ Trụ [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`120px x 120px`) đội vương miện sao bay lượn ở góc phải banner.
- **Khối chỉ số hiệu năng:**
  - Xếp dạng lưới 3 cột hiển thị các thông tin:
    - *Số từ đã ôn:* **15 từ & cấu trúc**.
    - *Đánh giá bộ nhớ:* Nhớ rõ 12 từ, Hơi phân vân 2 từ, Quên mất 1 từ.
    - *Phần thưởng tích lũy:* **+20 EXP** (hiển thị kèm icon cúp tỏa sáng `{colors.warning}`).
- **Biểu đồ chuyển hóa bộ nhớ:**
  - Biểu đồ thanh ngang (Horizontal progress bars stacked) mô tả tỷ lệ phần trăm từ vựng chuyển từ bộ nhớ ngắn hạn sang bộ nhớ trung & dài hạn sau phiên ôn tập.
- **Nút hành động:**
  - Nút "Quay lại trang ôn tập": Style `button-primary` nền `{colors.primary}`, cao `48px`, bo góc `{rounded.lg}`, rộng `320px`, tự động canh giữa bên dưới biểu đồ.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Gõ đáp án và bấm "Kiểm tra"**
  - **Luồng sự kiện chính:** Học viên nhập đáp án $\rightarrow$ Click "Kiểm tra" (hoặc đồng hồ đếm ngược hết 10 giây) $\rightarrow$ Hệ thống dừng đồng hồ $\rightarrow$ Phát file audio phát âm `.mp3` $\rightarrow$ Render Bảng tự đánh giá ghi nhớ LN-13-S2 $\rightarrow$ Học viên nhấp chọn 1 trong 3 nút (Nhớ rõ / Hơi phân vân / Quên mất) $\rightarrow$ Hệ thống cập nhật dữ liệu SRS $\rightarrow$ Chuyển sang từ kế tiếp $\rightarrow$ Reset lại trạng thái đếm ngược 10 giây từ đầu.
  - **API Gửi mức độ đánh giá:** `POST /api/srs/evaluate`
    - Payload: `{ "wordId": 45, "rating": "easy" | "medium" | "hard" }`
    - Response: `{ "success": true, "nextReviewDate": "2026-05-28T17:00:00Z" }`
- **Hành động: Tra cứu nhanh từ vựng**
  - Học viên click "Tra cứu nhanh" $\rightarrow$ Đồng hồ 10s tạm dừng $\rightarrow$ Hiển thị Modal LN-13-M1 $\rightarrow$ Học viên bấm "Đóng lại" $\rightarrow$ Modal ẩn $\rightarrow$ Đồng hồ chạy tiếp giây còn lại $\rightarrow$ Học viên làm bài tiếp.

---

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái tải dữ liệu (Loading State):** Khi nộp đánh giá và tải câu hỏi tiếp theo, nút bấm hiển thị vòng xoay spinner nhỏ mờ, khóa thao tác click trùng lặp để tránh spam.
- **Trạng thái lỗi kết nối (Error State):** Nếu mất mạng khi nộp đánh giá $\rightarrow$ Không hiện modal gây gián đoạn làm bài. Hệ thống tự động lưu kết quả vào `LocalStorage` với flag `synced: false`, hiện một badge nhỏ màu `{colors.warning}` ("Đang ngoại tuyến - Đang lưu tạm kết quả") ở góc phải thẻ, và sẽ tự động đồng bộ lại khi có kết nối mạng trở lại.

---

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [personal_review_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/personal_review_page.md) khi bấm "Ôn tập ngay".
- **Đi đến:** Quay lại [personal_review_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/personal_review_page.md) sau khi kết thúc phiên ôn tập và click "Quay lại trang ôn tập".

---

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Đảm bảo thời gian chuyển cảnh (transition) giữa các từ vựng cực kỳ mượt mà (sử dụng `transition: all 0.3s ease-in-out`), tránh gây giật lag ảnh hưởng tới tốc độ phản xạ của học viên.
- **NÊN:** Thiết lập thuộc tính `autofocus` cho ô nhập đáp án của mỗi câu mới để người học không phải click chuột vào ô nhập liệu.
- **KHÔNG ĐƯỢC:** Sử dụng bất cứ bóng đổ dạng xám đen nào. Toàn bộ hiệu ứng chiều sâu bắt buộc dùng các cấp độ phát quang `{elevation.glow}` và viền nhạt để đảm bảo tính mỹ thuật nhẹ nhàng của DiveVerse.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Danh sách từ ôn tập đến hạn (SRS Queue Items):** Liên kết với mảng `srsReviewQueue`. Mỗi từ chứa:
  - Từ khóa: `{word}`
  - Phiên âm IPA: `{ipa}`
  - Từ loại: `{partOfSpeech}`
  - Định nghĩa chính thức: `{definition}`
  - Các collocations đi kèm: `{collocations}`
  - Câu bối cảnh điền khuyết: `{contextSentence}`
  - Gợi ý dịch tiếng Việt: `{translationHint}`
- **Tra cứu từ điển tại chỗ (Inline Dictionary Lookup):** Liên kết với đối tượng `dictionary` theo khóa của từ vựng (ví dụ: `dictionary.collaborate`).
