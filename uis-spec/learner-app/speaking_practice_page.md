# MÀN HÌNH: SPEAKING PRACTICE PAGE (MÀN HÌNH LUYỆN NÓI)

## 1. THÔNG TIN CHUNG
- Tên màn hình: Speaking Practice Page (Màn hình luyện nói)
- Mã use case liên quan: UC-06b (Luyện nói)
- Mã luồng người dùng liên quan: Flow LN-FL-05 (Luyện tập kỹ năng Nói)
- Vai trò người dùng: Learner (Người học / Học viên)
- Vị trí trong sitemap: Trang chủ -> Dashboard -> Click Unit -> Unit Detail Page -> Click bài học Luyện Nói -> Speaking Practice Page (URL: /units/{unit_id}/lessons/{lesson_id}/speaking)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên sử dụng màn hình này để phát triển kỹ năng giao tiếp tiếng Anh qua hai hình thức: Luyện phát âm từ đơn/câu ngắn bằng ASR và Hội thoại giả lập nhập vai cùng Cá Voi Thông Thái, đồng thời kiểm tra phát hiện và xử lý lỗi thiết bị thu âm (micro).

## 3. BỐ CỤC (LAYOUT)
- Loại bố cục: Bố cục một cột căn giữa dạng thẻ biểu mẫu (Central Card Layout) trên nền canvas sáng ấm (#fffaf0), có thể mở rộng bảng chat hội thoại dạng bong bóng (Chat Bubble Stream Layout) khi chuyển sang chế độ giả lập.
- Các vùng chính trên màn hình:
  - Vùng A: Thanh tiến độ bài học (Progress Header) cố định ở đầu màn hình.
  - Vùng B: Thẻ tương tác luyện nói chính (Speaking Interaction Card) thay đổi theo 2 chế độ (ASR Pronunciation, Hội thoại cùng Cá Voi).
  - Vùng C: Nhóm nút hành động ở chân thẻ (Footer Controls) chứa nút micro lớn để thu âm.
  - Vùng D: Các hộp thoại lớp phủ báo lỗi (Error Modals) chồng lên màn hình khi xảy ra sự cố thiết bị.
- Kích thước / Grid tham khảo:
  - Thẻ tương tác chính có chiều rộng 760px, bo tròn góc rounded-xl (24px).
  - Khung chat hội thoại giả lập chiếm chiều cao 400px có thanh cuộn dọc.
  - Khoảng cách padding trong thẻ: spacing-xl (32px).
  - Căn giữa dọc và ngang bằng CSS Flexbox.

## 4. THÀNH PHẦN GIAO DIỆN (UI COMPONENTS)

### THÀNH PHẦN CHUNG (PROGRESS HEADER)
- **Tên component:** Thanh tiến trình nói (Speaking Progress Bar)
  - **Loại component tham chiếu từ DESIGN.md:** progress-bar (nền surface-strong #ebe6d6, thanh tiến độ xanh success #22c55e, height 8px)
  - **Vị trí:** Vùng A.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị số lượng câu/lượt thoại đã hoàn thành (ví dụ: "Lượt thoại 2 / 5").

---

### CẤU HÌNH CÁC CHẾ ĐỘ LUYỆN TẬP (VÙNG B & C)

#### 1. ASR PRONUNCIATION MODE (GIAO DIỆN PHÁT ÂM TỪ ĐƠN / CÂU NGẮN)
- **Tên component:** Từ/Câu mẫu cần đọc (Target Phrase Box)
  - **Loại component tham chiếu từ DESIGN.md:** title-lg (font Inter size 26px, weight 600, màu ink #0a0a0a, căn giữa)
  - **Vị trí:** Vùng B, trung tâm Central Card.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị từ vựng hoặc câu ngắn mục tiêu cần luyện phát âm (ví dụ: "I'd like to book a table for tonight."). Bên cạnh có icon loa phát âm mẫu.

- **Tên component:** Kết quả nhận diện giọng nói (ASR Color feedback text)
  - **Loại component tham chiếu từ DESIGN.md:** text-span (màu sắc thay đổi theo điểm phát âm)
  - **Vị trí:** Vùng B, hiển thị đè lên câu mẫu sau khi ghi âm kết thúc.
  - **Trạng thái:** Xuất hiện sau khi AI chấm điểm.
  - **Dữ liệu hiển thị / hành vi:**
    - Từ phát âm tốt (>=80%): màu xanh success (#22c55e).
    - Từ phát âm chưa đạt (<80%): màu đỏ error (#ef4444) kèm gạch wavy. Rê chuột vào hiện bảng gợi ý IPA đúng của Admin.

- **Tên component:** Nút "Luyện nói lại" (Retry Button)
  - **Loại component tham chiếu từ DESIGN.md:** button-secondary (nền canvas #fffaf0, border 1px hairline #e5e5e5, rounded-md 12px, height 44px)
  - **Vị trí:** Vùng C, nằm cạnh nút micro khi có kết quả.
  - **Trạng thái:** Mặc định, hover.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị chữ "Luyện nói lại". Nhấp chọn để xóa kết quả cũ và ghi âm lại.

#### 2. Hội thoại cùng Cá Voi MODE (GIAO DIỆN HỘI THOẠI GIẢ LẬP cùng Cá Voi Thông Thái)
- **Tên component:** Khung thông tin kịch bản (Scenario Banner)
  - **Loại component tham chiếu từ DESIGN.md:** feature-card-ochre (nền brand-ochre #e8b94a nhạt, rounded-lg 16px, padding 16px)
  - **Vị trí:** Vùng B, đầu thẻ tương tác.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị bối cảnh nhập vai (ví dụ: "Nhập vai: Bạn là khách hàng, AI là nhân viên phục vụ nhà hàng. Hãy gọi món khai vị.").

- **Tên component:** Dòng thoại của Cá Voi (AI Chat Bubble)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền surface-card #f5f0e0, rounded-lg 16px, padding 12px x 16px, căn lề trái)
  - **Vị trí:** Vùng B, trong khung chat cuộn dọc.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị câu nói của Cá Voi Thông Thái dưới dạng bong bóng chat kèm icon loa để nghe giọng của Cá Voi (ví dụ: "Welcome! Are you ready to order?").

- **Tên component:** Dòng thoại của học viên (Learner Chat Bubble)
  - **Loại component tham chiếu từ DESIGN.md:** product-mockup-card (nền brand-teal #1a3a3a, chữ màu on-primary #ffffff, rounded-lg 16px, padding 12px x 16px, căn lề phải)
  - **Vị trí:** Vùng B, trong khung chat cuộn dọc.
  - **Trạng thái:** Xuất hiện sau khi học viên bấm giữ mic nói và AI chuyển giọng nói thành văn bản.

- **Tên component:** Nút Ghi âm đàm thoại (Push-to-Talk Microphone Button)
  - **Loại component tham chiếu từ DESIGN.md:** rounded-full (nền primary #0a0a0a, kích thước 64px x 64px, căn giữa)
  - **Vị trí:** Vùng C.
  - **Trạng thái:** Mặc định, hover, đang thu âm (soundwave sóng âm nhấp nháy, đổi viền đỏ).
  - **Dữ liệu hiển thị / hành vi:** Học viên nhấn giữ nút này để nói và thả ra để nộp câu thoại cho AI phân tích.

---

### TRANG KẾT QUẢ LUYỆN NÓI (SPEAKING RESULT PAGE)
- **Tên component:** Bảng tổng hợp điểm phát âm (Speaking Stats Dashboard)
  - **Loại component tham chiếu từ DESIGN.md:** cta-band-illustrated (nền surface-soft #faf5e8, rounded-xl 24px, padding 32px)
  - **Vị trí:** Vùng B, trang kết quả.
  - **Trạng thái:** Mặc định.
  - **Dữ liệu hiển thị / hành vi:** Hiển thị điểm số trung bình phát âm (ví dụ: "Điểm phát âm: 85% - Tốt"), tổng lượt hội thoại và lời khen ngợi của Cá Voi kèm các lời khuyên thực hành từ Admin.

---

### VÙNG D: HỘP THOẠI LỚP PHỦ BÁO LỖI MICRO (ERROR MODALS)
- **Tên component:** Hộp thoại Không nhận dạng được giọng nói (No Audio Received Modal - LN-06-M1)
  - **Loại component tham chiếu từ DESIGN.md:** overlay / backdrop + centered alert card (nền surface-card #f5f0e0, bo tròn rounded-lg 16px, width 380px)
  - **Vị trí:** Vùng D, nổi đè lên màn hình.
  - **Trạng thái:** Xuất hiện khi cường độ âm thanh ghi nhận bằng 0.
  - **Dữ liệu hiển thị / hành vi:** Tiêu đề "Không nghe thấy âm thanh!" (màu error #ef4444). Dòng mô tả: "Thiết bị không nhận được âm thanh của bạn. Vui lòng kiểm tra jack cắm micro và thử nói to hơn!". Nút bấm: "Đóng cảnh báo" (button-primary).

- **Tên component:** Hộp thoại Lỗi quyền Microphone (Microphone Permission Blocked Modal - LN-06-M2)
  - **Loại component tham chiếu từ DESIGN.md:** overlay / backdrop + centered alert card (nền surface-card #f5f0e0, rounded-lg 16px, width 400px)
  - **Vị trí:** Vùng D, nổi đè lên màn hình.
  - **Trạng thái:** Xuất hiện khi trình duyệt báo micro bị từ chối quyền truy cập.
  - **Dữ liệu hiển thị / hành vi:** Tiêu đề "Lỗi truy cập Microphone" (màu error #ef4444). Dòng hướng dẫn: "Trình duyệt đang chặn quyền truy cập Micro của DiveVerse. Hãy click vào biểu tượng ổ khóa/camera trên thanh địa chỉ URL để cấp quyền, sau đó tải lại trang!". Nút bấm: "Thoát bài học" (button-secondary) dẫn về LN-02.

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Nhấn giữ nút Microphone để nói trong Hội thoại AI**
  - **Luồng chính:** Học viên click giữ chuột trái vào nút Mic -> Soundwave nhấp nháy chuyển động -> Học viên nói -> Nhả chuột ra -> Hệ thống gửi file âm thanh lên máy chủ -> Nút Mic hiển thị spinner loading -> Văn bản hiển thị dạng text-bubble căn lề phải -> AI phản hồi lại bằng text-bubble căn lề trái và phát file thoại audio -> Mở nút Mic cho lượt tiếp theo.
  - **Luồng con / rẽ nhánh:**
    - *Lỗi không nghe thấy âm thanh (Rẽ nhánh E-1):* Nhả chuột, hệ thống phát hiện cường độ âm = 0 -> Hiển thị Modal LN-06-M1 -> Học viên nhấn "Đóng" và thử lại.
    - *Lỗi micro bị chặn (Rẽ nhánh E-2):* Bấm Mic, hệ thống báo lỗi không truy cập được -> Hiển thị Modal LN-06-M2 -> Học viên đọc hướng dẫn cấp quyền và chọn thoát bài học.
  - **Dữ liệu gửi lên / nhận về:**
    - Gửi đi: `POST /api/speaking/dialogue` (payload: file ghi âm .wav)
    - Nhận về: `{ "success": true, "userText": "I want to order soup.", "aiResponseText": "Sure, which soup would you like?", "aiAudioUrl": "files/response1.mp3" }`

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)
- **Trạng thái rỗng (empty state):** Không áp dụng.
- **Trạng thái tải (loading state):** Khi hệ thống đang gửi file ghi âm lên AI và chờ chuyển đổi văn bản -> Nút Micro chuyển sang xoay spinner, khóa click, khung chat hiển thị dấu ba chấm nhấp nháy (typing indicator).
- **Trạng thái lỗi (error state):** Khi API nói bị mất mạng, hiển thị lỗi đỏ ở viền dưới thẻ kèm nút thử lại.
- **Trạng thái thành công (success state):** Trang tổng kết hiển thị điểm số, pháo hoa giấy rơi, Toast xanh lá báo hoàn thành.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ màn hình nào trước đó?** Từ Unit Detail Page (LN-02) sau khi học viên nhấp chọn bài luyện nói.
- **Sau khi hoàn thành hành động, đi đến màn hình nào?** Quay trở lại màn hình Unit Detail Page (LN-02) khi học viên bấm nút "Hoàn thành bài học" trên trang kết quả.
- **Các màn hình liên quan khác:** LN-02, các Modal báo lỗi LN-06-M1 và LN-06-M2.

## 8. LƯU Ý THIẾT KẾ (DESIGN NOTES)
- Nền sàn của trang sử dụng màu canvas sáng ấm (#fffaf0) đặc trưng.
- Thẻ Speaking Interaction Card có phong cách `feature-card-cream` màu surface-card (#f5f0e0), viền hairline 1px (#e5e5e5) bo tròn góc bo lớn rounded-xl (24px) để tạo tính đồng điệu.
- Theo Nguyên tắc Báo hiệu (Signaling Principle), các từ bị phát âm sai được bôi đỏ đậm gạch wavy, từ đúng tô xanh lá rõ ràng. Các thông báo cảnh báo lỗi micro được hiển thị bằng màu đỏ của error (#ef4444) để báo động cho học viên xử lý.
- Micro có touch target rất lớn (64x64px) để dễ nhấn giữ trên thiết bị di động. Khoảng cách dọc giữa các dòng thoại trong khung chat là spacing-md (16px) giúp cuộc hội thoại hiển thị mạch lạc.



