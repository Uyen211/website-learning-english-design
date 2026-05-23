# MÀN HÌNH: VOCABULARY LEARNING PAGE (MÀN HÌNH HỌC TỪ VỰNG NỀN TẢNG)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Vocabulary Learning Page (Màn hình học từ vựng nền tảng - UC-05a)
- Mã use case liên quan: UC-05a (Học từ vựng nền tảng)
- Mã luồng người dùng liên quan: Flow LN-FL-02 (Học từ vựng nền tảng)
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Dashboard -> Click Unit -> Unit Detail Page -> Click bài học Từ vựng -> Vocabulary Learning Page (URL: /units/{unit_id}/lessons/{lesson_id}/vocabulary)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này để trải qua quy trình học từ vựng quy nạp đa giác quan gồm 6 giai đoạn nối tiếp nhau (từ làm quen qua ngữ cảnh, xem định nghĩa, thực hành nhận diện, gõ chính tả, sản sinh tự viết câu có trợ lý AI ZPD phản hồi lỗi sai, đến khi hoàn thành bài học để đưa từ vựng vào lịch ôn tập SRS).

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Centered card layout (Bố cục một cột căn giữa hoàn toàn theo cả chiều ngang và dọc) sử dụng nền canvas sáng ấm (#fffaf0), kết hợp thanh tiến độ ngang ở đầu màn hình và bảng điều khiển phụ (Side/Bottom Panel) cho phản hồi AI ZPD.
- Các vùng chính trên màn hình:
  - Vùng A: Thanh tiêu đề và tiến độ bài học (Progress Header) cố định ở đầu màn hình.
  - Vùng B: Thẻ học tập trung tâm (Central Learning Card Container) là nơi hiển thị nội dung của từng giai đoạn học.
  - Vùng C: Bảng phản hồi AI ZPD (ZPD AI Feedback Panel) xuất hiện ở bên phải (trên desktop) hoặc trượt từ dưới lên (trên mobile) trong giai đoạn sản sinh câu.
  - Vùng D: Thanh điều hướng chân trang (Footer Action Bar) chứa các nút điều hướng chuyển tiếp.
- Kích thước / Grid tham khảo:
  - Thẻ học tập trung tâm có kích thước cố định: 720px x 480px, góc bo rounded-xl (24px).
  - Vùng C (ZPD Panel) có chiều rộng 360px khi mở rộng bên phải thẻ trung tâm.
  - Khoảng cách padding trong thẻ học tập: spacing-xl (32px).
  - Màn hình sử dụng lưới grid linh hoạt: 1 cột cho Mobile, 2 cột (7:5) cho Desktop khi ZPD Panel mở ra.

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)

### THÀNH PHẦN CHUNG (PROGRESS HEADER & CONTROLS)
- **Tên component:** Thanh tiến độ bài học (Lesson Progress Bar)
  - **Loại component tham chiếu từ DESIGN.md:** progress-bar (nền surface-strong #ebe6d6, thanh tiến độ xanh success #22c55e, height 8px, rounded-pill)
  - **Vị trí:** Vùng A, chạy ngang đầu màn hình dưới header.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị phần trăm số từ vựng đã hoàn thành trong bài học hiện tại (ví dụ: "Từ 3 / 10 - Hoàn thành 30%").

- **Tên component:** Nút đóng bài học (Exit Button)
  - **Loại component tham chiếu từ DESIGN.md:** rounded-full (icon button kích thước 36px x 36px, màu muted #6a6a6a)
  - **Vị trí:** Vùng A, góc trên bên phải.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị icon dấu "X" màu ink. Nhấn vào sẽ thoát bài học, hiển thị popup xác nhận lưu tiến độ trước khi quay lại màn hình AD-02/LN-02.

---

### GIAI ĐOẠN 1: LÀM QUEN QUA NGỮ CẢNH (CONTEXTUAL GUESSING STAGE)
- **Tên component:** Khu vực phát âm thanh (Audio Player Component)
  - **Loại component tham chiếu từ DESIGN.md:** rounded-full (nền primary #0a0a0a, màu chữ on-primary #ffffff, touch target 48x48px)
  - **Vị trí:** Vùng B, nằm trên cùng của Central Card.
  - **Trạng thái:** Mặc định, đang phát (sóng âm soundwave chuyển động), dừng phát.
  - **Dữ liệu hiển thị / hành vi:** Nhấp chuột vào để phát file phát âm của từ vựng mục tiêu từ người bản xứ chuẩn.

- **Tên component:** Danh sách câu ngữ cảnh (Contextual Sentences)
  - **Loại component tham chiếu từ DESIGN.md:** body-strong / body-md (chữ màu body #3a3a3a, từ mục tiêu in đậm màu ink #0a0a0a)
  - **Vị trí:** Vùng B, phần thân Central Card.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị 3 câu ví dụ thực tế chứa từ mục tiêu (ví dụ: "We need to **collaborate** on this project to finish it in time.").

- **Tên component:** Nút "Xem nghĩa"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng D.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Xem nghĩa từ vựng". Nhấn vào sẽ chuyển Central Card sang Giai đoạn 2.

---

### GIAI ĐOẠN 2: XEM NGHĨA CHI TIẾT (VOCABULARY DETAIL STAGE)
- **Tên component:** Tên từ vựng & Phiên âm IPA
  - **Loại component tham chiếu từ DESIGN.md:** title-lg (font Inter size 28px, weight 600, màu ink #0a0a0a)
  - **Vị trí:** Vùng B, trên cùng Central Card.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị từ vựng mục tiêu và phiên âm (ví dụ: "Collaborate /kəˈlæb.ə.reɪt/"). Cạnh đó có icon loa nhỏ màu primary để nghe lại.

- **Tên component:** Bảng định nghĩa & Collocations
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền canvas #fffaf0, rounded-lg 16px, border 1px hairline #e5e5e5, padding 16px)
  - **Vị trí:** Vùng B, thân Central Card.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** 
    - Hiển thị Định nghĩa: "Hợp tác, cộng tác làm việc cùng nhau".
    - Sắc thái từ (Register/Nuance): "Động từ trang trọng (Formal verb), thường dùng trong môi trường học thuật/công sở".
    - Collocations phổ biến: "collaborate with somebody, collaborate on something".

- **Tên component:** Nút "Tiếp tục" (chuyển sang thực hành)
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, height 44px, rounded-md 12px)
  - **Vị trí:** Vùng D.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị "Tiếp tục học". Nhấn vào chuyển sang Giai đoạn 3.

---

### GIAI ĐOẠN 3: THỰC HÀNH NHẬN DIỆN (ACTIVE PRACTICE STAGE)
*Màn hình hiển thị hình thức bài tập tương ứng do Admin cấu hình cho từ này:*

- **Tên component:** Bộ ghép thẻ hình ảnh - từ vựng (Drag & Drop / Matching Interface)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (các thẻ nhỏ kích thước 120px x 80px, bo góc rounded-md 12px)
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Mặc định, đang kéo, đặt đúng (thẻ đổi màu success #22c55e nhạt), đặt sai (thẻ đổi màu error #ef4444 nhạt).
  - **Dữ liệu hiển thị / hành vi:** Học viên kéo thẻ chữ "Collaborate" thả vào đúng thẻ hình ảnh 3D mô tả hành động hợp tác nhóm.

- **Tên component:** Ô nhập dự đoán collocation (AI Next-word Prediction / Smart Concordance)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, border 1px hairline #e5e5e5, height 44px, rounded-md 12px)
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Mặc định, focus, error.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị câu văn bị ẩn cụm từ: "The two departments decided to ______ on the campaign." Học viên gõ từ "collaborate" vào ô trống. Nhấn nút "Kiểm tra" ở Vùng D.

---

### GIAI ĐOẠN 4: NGHE GÕ LẠI CHÍNH TẢ (DICTATION STAGE)
- **Tên component:** Icon phát âm thanh Dictation
  - **Loại component tham chiếu từ DESIGN.md:** rounded-full (nền primary #0a0a0a, kích thước 64px x 64px, căn giữa)
  - **Vị trí:** Vùng B, trung tâm Central Card.
  - **Trạng thái:** Mặc định. Tự động phát âm thanh khi bắt đầu giai đoạn.
  - **Dữ liệu hiển thị / hành vi:** Click vào để nghe lại âm thanh từ vựng cần gõ chính tả.

- **Tên component:** Ô nhập chính tả (Dictation Input Field)
  - **Loại component tham chiếu từ DESIGN.md:** text-input (nền canvas #fffaf0, text ink #0a0a0a, rounded-md 12px, border 1px hairline #e5e5e5, height 44px, font Inter size 18px, weight 500, căn giữa văn bản)
  - **Vị trí:** Vùng B, nằm dưới icon phát âm thanh.
  - **Trạng thái:** Mặc định, focus, error (viền đỏ màu error #ef4444).
  - **Dữ liệu hiển thị / hành vi:** Placeholder: "Nghe và gõ lại từ vựng...". Trình duyệt bị tắt tính năng tự sửa lỗi chính tả.

- **Tên component:** Khối văn bản đáp án cưỡng bức (Forced Sample Box)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền surface-strong #ebe6d6, chữ ink #0a0a0a, border 1px hairline #e5e5e5, rounded-md 12px, padding 16px)
  - **Vị trí:** Vùng B, hiển thị sát dưới ô nhập liệu khi học viên gõ sai quá 3 lần.
  - **Trạng thái:** Ẩn mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị dòng chữ: "Bạn đã gõ sai quá 3 lần. Đáp án đúng là: **collaborate**. Hãy gõ lại chính xác từ khóa này để tiếp tục bài học!". Ô nhập liệu bị khóa click ngoài, bắt buộc học viên phải gõ đúng chuỗi "collaborate" mới được chuyển tiếp.

---

### GIAI ĐOẠN 5: TỰ VIẾT CÂU CÁ HÂN HÓA & TRỢ LÝ ZPD AI (PERSONALIZED PRODUCTION STAGE)
- **Tên component:** Khung đặt câu cá nhân hóa
  - **Loại component tham chiếu từ DESIGN.md:** text-area (nền canvas #fffaf0, text ink #0a0a0a, border 1px hairline #e5e5e5, rounded-md 12px, padding 16px, chiều cao 100px)
  - **Vị trí:** Vùng B, nằm ở thân Central Card.
  - **Trạng thái:** Mặc định, focus, error.
  - **Dữ liệu hiển thị / hành vi:** Nhãn "Hãy tự đặt một câu tiếng Anh sử dụng từ '**collaborate**' để nói về công việc hoặc đời sống của bạn *". Placeholder: "Ví dụ: I usually collaborate with my colleagues to..."

- **Tên component:** Nút "Nộp câu"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, height 44px, rounded-md 12px)
  - **Vị trí:** Vùng D.
  - **Trạng thái:** Mặc định, hover, loading.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Nộp bài viết". Click để gửi câu cho AI chấm chữa lỗi.

---

### VÙNG C: BẢNG PHẢN HỒI AI ZPD (ZPD AI FEEDBACK PANEL)
- **Tên component:** Bảng điều khiển ZPD AI (ZPD AI Panel Container)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-ochre (nền brand-ochre #e8b94a nhạt hoặc surface-card #f5f0e0, border-left 1px hairline #e5e5e5, padding 20px)
  - **Vị trí:** Vùng C, hiển thị dọc bên phải Central Card khi chuyển sang Giai đoạn 5.
  - **Trạng thái:** Ẩn mặc định ở 4 giai đoạn đầu, tự động mở rộng ra ở giai đoạn 5 khi có phản hồi lỗi từ AI.
  - **Dữ liệu hiển thị / hành vi:** Chứa tiêu đề "Phân tích ZPD AI" (Plain Black 18px), đoạn văn bản chấm lỗi sai ngữ pháp, và các câu gợi ý mẫu.

- **Tên component:** Nhãn bôi đỏ lỗi ngữ pháp (Error Highlights)
  - **Loại component tham chiếu từ DESIGN.md:** text-span (màu error #ef4444, in đậm, có gạch chân wavy dưới chữ)
  - **Vị trí:** Vùng C, trong đoạn văn câu của học viên viết được trích xuất hiển thị lại.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** AI bôi đỏ từ viết sai (ví dụ: gõ "collaborate to him" -> bôi đỏ "to" và gợi ý đổi thành "with").

- **Tên component:** Khung gợi ý ZPD 3 vòng (Scaffolded Hints)
  - **Loại component tham chiếu từ DESIGN.md:** body-sm (font Inter size 13px, màu body #3a3a3a)
  - **Vị trí:** Vùng C, thân ZPD Panel.
  - **Trạng thái:** Hiển thị tăng dần mức độ trợ giúp khi học viên nộp câu sai lần 1 và lần 2.
  - **Dữ liệu hiển thị / hành vi:**
    - *Nộp sai lần 1:* Hiển thị Gợi ý lỗi từ loại/cấu trúc (ví dụ: "Hãy kiểm tra lại giới từ đi kèm với 'collaborate'.").
    - *Nộp sai lần 2:* Hiển thị Gợi ý cấu trúc chi tiết (ví dụ: "Cấu trúc đúng là: collaborate + with + somebody. Hãy sửa lại câu của bạn.").
    - *Nộp sai lần 3:* Khóa khung nhập tự do, hiển thị câu mẫu khuyết từ của Admin để điền từ (ví dụ: "I usually collaborate _____ my team to design new features. Hãy điền từ thích hợp vào chỗ trống!").

---

### GIAI ĐOẠN 6: HOÀN THÀNH BÀI HỌC (LESSON COMPLETION PAGE)
- **Tên component:** Khối chúc mừng hoàn thành (Congratulatory Box)
  - **Loại component tham chiếu từ DESIGN.md:** cta-band-illustrated (nền surface-soft #faf5e8, rounded-xl 24px, padding 40px)
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Mặc định. Tự động rơi confetti hiệu ứng giấy bay khi chuyển sang.
  - **Dữ liệu hiển thị / hành vi:** 
    - Tiêu đề: "Tuyệt vời! Bạn đã hoàn thành từ vựng này!" (display-sm 32px, màu ink #0a0a0a).
    - Icon 3D Mascot chú bạch tuộc nhỏ đang cầm bảng tích xanh đứng vỗ tay.
    - Điểm EXP cộng thêm: "EXP tích lũy: +10 EXP" (badge-pill màu success).
    - Trạng thái SRS: "Từ vựng 'collaborate' đã được lên lịch ôn tập sau 24 giờ tới (SRS)".

- **Tên component:** Nút "Hoàn thành bài học"
  - **Loại component tham chiếu từ DESIGN.md:** button-primary (nền primary #0a0a0a, chữ màu on-primary #ffffff, height 44px, rounded-md 12px)
  - **Vị trí:** Vùng D.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị text "Hoàn thành & Quay lại". Nhấp chuột để thoát màn hình và quay về Unit Detail Page (LN-02).

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Giai đoạn 4 - Nhập từ vựng và click "Kiểm tra"**
  - **Luồng chính:** Học viên nghe audio -> Nhập đúng từ "collaborate" vào ô nhập liệu -> Click nút "Kiểm tra" -> Hệ thống hiện viền xanh success (#22c55e) quanh input, phát âm thanh báo đúng -> Central Card tự động chuyển sang Giai đoạn 5 sau 1 giây.
  - **Luồng con / rẽ nhánh (Gõ sai chính tả):**
    - Học viên gõ sai (ví dụ: "colaborate") -> Hệ thống báo đỏ viền ô nhập, phát audio âm báo sai, phát lại file phát âm bản xứ -> Học viên gõ lại.
    - Nếu gõ sai lần 3 -> Hệ thống tự động khóa ô nhập tự do, hiển thị Hộp đáp án cưỡng bức chứa từ mẫu "collaborate". Học viên bắt buộc phải gõ chính xác theo chuỗi này mới được kích hoạt nút "Tiếp tục" để chuyển sang Giai đoạn 5.
- **Hành động: Giai đoạn 5 - Tự viết câu và click "Nộp câu"**
  - **Luồng chính:** Học viên đặt câu chính xác -> Click "Nộp câu" -> AI phân tích không thấy lỗi -> Nút chuyển sang trạng thái thành công -> Tự động chuyển sang Giai đoạn 6 (Hoàn thành bài học).
  - **Luồng con / rẽ nhánh (Sai ngữ pháp/Cấu trúc - Phản hồi ZPD AI):**
    - Học viên viết câu có lỗi (ví dụ: "I collaborate to him.") -> Click "Nộp câu" -> Nút nộp tắt loading. ZPD AI Panel ở Vùng C trượt mở ra.
    - *Lần sửa 1:* AI bôi đỏ vị trí lỗi "to" trên câu học viên và đưa ra gợi ý gợi mở ở ZPD Panel: "Bạn đang sử dụng sai giới từ đi kèm với động từ collaborate. Hãy sửa lại!". Học viên sửa câu (ví dụ: gõ "I collaborate about him") -> Bấm nộp lại.
    - *Lần sửa 2:* AI phát hiện vẫn lỗi -> Bôi đỏ lỗi và đưa ra gợi ý cấu trúc trực tiếp ở ZPD Panel: "Hãy nhớ cấu trúc: collaborate WITH somebody (hợp tác với ai). Hãy sửa lại câu của bạn!". Học viên sửa lại câu chính xác và bấm nộp -> Chuyển sang Giai đoạn 6.
    - *Lần sửa 3 (nếu nộp lại lần 2 vẫn sai):* Hệ thống tự động khóa ô đặt câu tự do. Hiển thị câu mẫu của Admin bị khuyết giới từ: "I collaborate _____ my colleagues. (Hãy điền giới từ thích hợp)". Học viên gõ từ "with" vào ô khuyết -> Nhấn xác nhận -> Chuyển sang Giai đoạn 6.
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: `{ "userId": 105, "vocabularyId": 45, "userSentence": "I collaborate to him." }`
    - Nhận về: `{ "isValid": false, "errorCount": 1, "errors": [{ "text": "to", "index": 14, "suggestion": "with", "type": "preposition" }], "hint": "Bạn đang sử dụng sai giới từ..." }`

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Không áp dụng.
- **Trạng thái tải (loading state):** Khi nhấn "Nộp câu" ở Giai đoạn 5, AI đang chạy phân tích cú pháp câu (thời gian khoảng 1-2 giây) -> Nút nộp chuyển sang trạng thái Loading (hiển thị spinner, khóa click), ZPD Panel hiển thị các thanh xương skeleton lướt nhẹ.
- **Trạng thái lỗi (error state):** Khi API AI bị mất kết nối mạng -> Hiển thị text cảnh báo đỏ ở chân ZPD Panel: "Lỗi kết nối AI. Hệ thống tự động chuyển sang chế độ câu mẫu khuyết từ..." để học viên điền từ và hoàn tất bài học, không bị kẹt lại.
- **Trạng thái thành công (success state):** Giai đoạn 6 chúc mừng hoàn thành bài học, rơi confetti đầy màu sắc sinh động, cộng điểm EXP tích lũy.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ Unit Detail Page (LN-02) sau khi học viên nhấp chọn bài học Từ vựng và bấm nút "Bắt đầu học".
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Chuyển hướng quay trở lại Unit Detail Page (LN-02) khi bấm nút "Hoàn thành bài học" ở Giai đoạn 6.
- **Các màn hình liên quan khác:** LN-02.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0) để giữ trạng thái dịu mắt cho học viên trong suốt quá trình tập trung học.
- Hộp chứa biểu mẫu học tập Central Card sử dụng phong cách `feature-card-cream` màu surface-card (#f5f0e0), các nút bấm bo góc rounded-md (12px) màu đen ink hoặc canvas hairline mỏng 1px (#e5e5e5).
- Trong giai đoạn 5, ZPD AI Panel sử dụng màu vàng ấm nhạt của `feature-card-ochre` để tạo sự chú ý vừa phải cho học viên mà không gây cảm giác hoảng sợ khi làm sai câu.
- Theo Nguyên tắc Báo hiệu (Signaling Principle), các ký tự viết sai chính tả hoặc sai giới từ được bôi màu đỏ sáng (#ef4444) kết hợp gạch wavy để thu hút tiêu điểm thị giác tức thì giúp học viên tự điều chỉnh nhận thức lỗi sai.
- Đảm bảo khoảng cách spacing-lg (24px) giữa câu ví dụ và các trường nhập để tránh chật chội. Touch target của các nút bấm và ô nhập là 44px.
