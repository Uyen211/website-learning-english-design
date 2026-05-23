# MÀN HÌNH: UNIT DETAIL PAGE (MÀN HÌNH CHI TIẾT UNIT, DANH SÁCH BÀI HỌC)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Unit Detail Page (Màn hình chi tiết Unit, danh sách bài học)
- Mã use case liên quan: UC-05a, UC-05b, UC-06a, UC-06b, UC-06c, UC-06d, UC-07
- Mã luồng người dùng liên quan: Flow LN-FL-02, LN-FL-03, LN-FL-04, LN-FL-05, LN-FL-06, LN-FL-07, LN-FL-08 (Màn hình điều phối bài học của từng Unit)
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Dashboard -> Click Unit -> Unit Detail Page (URL: /units/{unit_id})

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Người học sử dụng màn hình này để xem danh sách 6 bài học kỹ năng (Từ vựng, Ngữ pháp, Nghe, Nói, Đọc, Viết) và trạm thi cuối Unit (Mini-exam), theo dõi trạng thái hoàn thành từng phần và click chọn bắt đầu học hoặc làm bài kiểm tra.

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục một cột có thanh điều hướng ghim cố định đầu trang (Sticky Navbar) và danh sách thẻ bài học chạy dọc (Vertical List Layout) trên nền canvas sáng ấm (#fffaf0).
- Các vùng chính trên màn hình:
  - Vùng A: Thanh điều hướng đầu trang (Learner Top Nav) ghim cố định ở đầu trang.
  - Vùng B: Banner tiêu đề Unit (Unit Header Hero Card) hiển thị tên Unit, chủ đề lớn, mô tả mục tiêu học tập và tiến trình % hoàn thành của Unit đó.
  - Vùng C: Vùng danh sách thẻ bài học (Lesson list section) hiển thị 6 bài học kỹ năng dưới dạng thẻ hình chữ nhật bo góc lớn.
  - Vùng D: Trạm thi cuối Unit (Unit Exam Anchor Card) nằm ở cuối danh sách bài học, hiển thị to và nổi bật hơn để báo hiệu cột mốc hoàn thành.
- Kích thước / Grid tham khảo:
  - Chiều rộng tối đa của container nội dung chính: 960px căn giữa.
  - Các thẻ bài học ở Vùng C xếp dọc 1 cột, khoảng cách spacing-md (16px) giữa các thẻ.
  - Khoảng cách padding dọc của banner: spacing-xl (32px).

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)
- **Tên component:** Thanh dẫn Breadcrumbs
  - **Loại component tham chiếu từ DESIGN.md:** body-sm (màu muted #6a6a6a)
  - **Vị trí:** Nằm ngay dưới Top Nav ở Vùng B.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị dòng chữ: "Lộ trình học / Unit 2: Đời sống công sở". Nhấp vào "Lộ trình học" để quay về Learner Dashboard (LN-01).

- **Tên component:** Banner thông tin Unit (Unit Header Hero Card)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-ochre (nền brand-ochre #e8b94a, chữ màu ink #0a0a0a, rounded-xl 24px, padding 32px)
  - **Vị trí:** Vùng B.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:**
    - Tiêu đề Unit: "Unit 2: Đời sống công sở" (Plain Black, size 28px, weight 500).
    - Dòng mô tả: "Chủ đề từ vựng công sở và ngữ pháp câu điều kiện loại 1. Hoàn thành toàn bộ bài học để mở khóa bài thi Mini-exam cuối Unit.".
    - Thanh tiến trình học tập của Unit: Progress Bar màu xanh lá success (#22c55e) hiển thị tỉ lệ phần trăm bài học đã học xong của Unit đó.

- **Tên component:** Thẻ bài học Từ vựng (Vocabulary Lesson Card)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream (nền surface-card #f5f0e0, border 1px hairline #e5e5e5, rounded-lg 16px, padding 20px)
  - **Vị trí:** Vùng C, thẻ thứ nhất trong danh sách.
  - **Trạng thái:**
    - Hoàn thành: Có badge tích xanh lá, điểm số EXP đạt được, hiển thị nút "Luyện tập lại" (`button-secondary`).
    - Đang học: Hiển thị thanh tiến trình phụ, nút "Học tiếp" (`button-primary`).
    - Chưa học: Hiển thị nút "Bắt đầu học" (`button-primary`).
  - **Dữ liệu hiển thị / hành vi:** Tên bài học "Bài học Từ vựng: Workplace Collocations". Nhấp nút hành động chuyển hướng đến Vocabulary Learning Page (LN-03).

- **Tên component:** Thẻ bài học Ngữ pháp (Grammar Lesson Card)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream
  - **Vị trí:** Vùng C, thẻ thứ hai.
  - **Trạng thái:** Tương tự thẻ từ vựng (chưa học / đang học / hoàn thành).
  - **Dữ liệu hiển thị / hành vi:** Tên bài học "Bài học Ngữ pháp: First Conditional (Câu điều kiện loại 1)". Nhấp nút hành động chuyển hướng đến Grammar Learning Page (LN-04).

- **Tên component:** Các thẻ Luyện kỹ năng (Listening / Speaking / Reading / Writing Cards)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-cream
  - **Vị trí:** Vùng C, các thẻ từ thứ ba đến thứ sáu.
  - **Trạng thái:** Tương tự các thẻ trước.
  - **Dữ liệu hiển thị / hành vi:**
    - Luyện nghe: "Luyện nghe truyện tương tác: The Office Gossip".
    - Luyện nói: "Hội thoại giả lập AI: Interviewing for a job".
    - Luyện đọc: "Đọc báo chí thực tế: Future of Remote Work".
    - Luyện viết: "Viết gợi ý ZPD: Writing a professional email".
    - Nhấp nút hành động tương ứng dẫn tới phòng luyện kỹ năng Listening (LN-05), Speaking (LN-06), Reading (LN-07), Writing (LN-08).

- **Tên component:** Thẻ Bài thi cuối Unit (Unit Exam Anchor Card)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-pink (nền brand-pink #ff4d8b, chữ màu trắng on-dark #ffffff, rounded-xl 24px, padding 24px)
  - **Vị trí:** Vùng D.
  - **Trạng thái:**
    - Khóa: mờ nhẹ (opacity 0.7), hiển thị icon ổ khóa vàng, nút "Bắt đầu thi" bị disabled (nền xám mờ). Xuất hiện khi chưa hoàn thành đủ 6 bài học kỹ năng phía trên.
    - Mở khóa: hiển thị rõ, nút "Bắt đầu thi" chuyển sang dạng `button-on-color` (nền trắng, chữ ink). Xuất hiện khi 6 bài học kỹ năng phía trên đều đạt trạng thái hoàn thành.
  - **Dữ liệu hiển thị / hành vi:** Tiêu đề "Mini-exam cuối Unit" (Plain Black 22px), dòng chữ "Thời gian làm bài: 30 phút - Điểm tối đa: 100 EXP. Đạt tối thiểu 50 EXP để vượt qua Unit.". Nhấp nút hành động chuyển sang Pre-test Setup Page (LN-09).

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động:** Nhấp vào nút hành động trên một thẻ Bài học chưa học / đang học / hoàn thành
  - **Luồng chính:** Học viên click nút -> Chuyển hướng trình duyệt đến màn hình tương ứng (ví dụ: click "Bắt đầu học" trên thẻ Từ vựng -> Chuyển đến LN-03).
- **Hành động:** Nhấp vào nút "Bắt đầu thi" trên thẻ Bài thi cuối Unit
  - **Luồng chính (khi đã mở khóa):** Học viên click nút -> Chuyển hướng trình duyệt sang màn hình Pre-test Setup Page (LN-09).
  - **Luồng rẽ nhánh (khi bị khóa):** Học viên không thể click nút bấm (nút bị disabled). Khi rê chuột qua thẻ bài thi bị khóa, xuất hiện tooltip cảnh báo màu tối: "Bạn phải hoàn thành cả 6 bài học kỹ năng phía trên để mở khóa bài thi này!".

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Không áp dụng vì 6 bài học và 1 bài thi cuối Unit luôn hiển thị cố định.
- **Trạng thái tải (loading state):** Khi đang gọi API lấy tiến trình học tập của các bài học, toàn bộ danh sách thẻ hiển thị khung xương skeleton và các nút bấm bị khóa click.
- **Trạng thái lỗi (error state):** Nếu API tiến trình bài học bị lỗi, hiển thị text đỏ "Lỗi tải bài học. Vui lòng tải lại trang!" kèm nút secondary "Tải lại trang".
- **Trạng thái thành công (success state):** Khi học viên vừa hoàn thành bài thi cuối Unit và đạt điểm đỗ -> Quay lại trang này hiển thị pháo hoa giấy rơi, thẻ Bài thi cuối Unit chuyển sang trạng thái tích xanh hoàn thành, đồng thời xuất hiện nút "Mở khóa Unit tiếp theo" dẫn về Dashboard (LN-01).

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ Learner Dashboard (LN-01) sau khi học viên nhấp chọn một trạm Unit đã mở khóa.
- **Sau khi hoàn thành hành động, đi đến màn hình nào?**
  - Chuyển sang Vocabulary Learning Page (LN-03) khi bấm học Từ vựng.
  - Chuyển sang Grammar Learning Page (LN-04) khi bấm học Ngữ pháp.
  - Chuyển sang Listening (LN-05), Speaking (LN-06), Reading (LN-07), Writing (LN-08) khi bấm luyện kỹ năng.
  - Chuyển sang Pre-test Setup Page (LN-09) khi bấm bắt đầu thi cuối Unit.
  - Chuyển sang Learner Dashboard (LN-01) khi bấm Breadcrumbs "Lộ trình học".
- **Các màn hình liên quan khác:** LN-01.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0).
- Thẻ bài học được thiết kế bằng phong cách `feature-card-cream` màu surface-card (#f5f0e0) nhằm tạo sự thống nhất và dịu mắt, tránh quá tải nhận thức khi có nhiều thẻ xếp cạnh nhau.
- Thẻ bài thi cuối Unit (Mini-exam) sử dụng màu hồng đậm `feature-card-pink` (#ff4d8b) để làm nổi bật cột mốc cuối cùng cần chinh phục theo Nguyên tắc Báo hiệu (Signaling Principle).
- Khoảng cách spacing-md (16px) giữa các thẻ bài học tạo cảm giác thông thoáng và bố cục gọn gàng, có nhịp điệu trực quan tốt.
- Touch target của các nút bấm hành động được thiết lập tối thiểu chiều cao 44px để thuận tiện click trên màn hình cảm ứng di động.
