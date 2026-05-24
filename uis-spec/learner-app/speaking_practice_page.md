# MÀN HÌNH: SPEAKING PRACTICE PAGE (MÀN HÌNH LUYỆN NÓI)

## 1. THÔNG TIN CHUNG
- **Tên màn hình:** Speaking Practice Page (Màn hình luyện nói)
- **Mã use case liên quan:** UC-06b (Luyện nói)
- **Mã luồng người dùng liên quan:** Flow LN-FL-03 (Trạm luyện Kỹ năng - Nói)
- **Vai trò người dùng:** Learner (Người học)
- **Vị trí trong sitemap:** Trang chủ $\rightarrow$ Dashboard $\rightarrow$ Click Unit $\rightarrow$ Unit Detail $\rightarrow$ Click Luyện Nói (URL: `/units/{unit_id}/lessons/{lesson_id}/speaking`)

## 2. MỤC ĐÍCH CỦA MÀN HÌNH
Học viên phát triển kỹ năng nói tiếng Anh qua hai chế độ: Luyện phát âm từ đơn/câu ngắn bằng ASR và Hội thoại giả lập nhập vai (AI Role-play) cùng Cá Voi Thông Thái, đồng thời tích hợp các cơ chế kiểm tra và xử lý lỗi thiết bị thu âm (micro).

## 3. BỐ CỤC TỔNG THỂ (LAYOUT ARCHITECTURE)
- **Triết lý bố cục:** Bố cục thẻ căn giữa dạng thẻ biểu mẫu (Central Card Layout) trên nền canvas, có thể mở rộng bảng chat hội thoại dạng bong bóng (Chat Bubble Stream Layout) khi chuyển sang chế độ giả lập.
- **Màu nền chung:** Nền trang sử dụng `{colors.canvas}` (`#F9F7FE`) phối dải chuyển màu mờ `{gradients.atmosphere-haze}`.
- **Phân bổ các vùng chính (Layout Zones):**
  - **Zone 1: Progress Header (Thanh tiến độ bài học)**
    - Ghim cố định ở sát mép trên. Chiều cao: `64px`.
  - **Zone 2: Speaking Interaction Card (Thẻ tương tác luyện nói chính)**
    - Kích thước: Rộng `760px` trên desktop. Căn giữa dọc và ngang bằng Flexbox.
  - **Zone 3: Footer Controls (Nhóm nút hành động ở chân thẻ)**
    - Chứa nút micro lớn thu âm và các nút phụ.
  - **Zone 4: Error Modals (Hộp thoại báo lỗi thiết bị)**
    - Các cửa sổ overlay kính mờ nổi đè lên màn hình khi xảy ra lỗi micro.

---

## 4. THÀNH PHẦN GIAO DIỆN CHI TIẾT (UI COMPONENTS)

### 4.1 Thanh tiến trình nói (Progress Header)
- **Đặc tả Visual:**
  - Nền: Kính mờ `{colors.glass}` (`rgba(255, 255, 255, 0.7)`), có `backdrop-filter: blur(8px)`.
  - Chiều cao: `nav-height` (64px). Viền dưới mờ `1px solid rgba(155, 93, 224, 0.1)`.
- **Thành phần:**
  - **Thanh tiến trình ngang:** Nằm sát cạnh đỉnh Nav. Cao `6px`. Nền `{colors.light-accent}`. Phần hoàn thành chạy màu dải ngân hà `{gradients.galactic-glow}` thể hiện tiến độ (ví dụ: *"Lượt thoại 2 / 5"*).
  - **Nút thoát bài học (Exit Button):** Icon Lucide `x` màu `{colors.text-secondary}`. Click để thoát về Unit Detail Page.

### 4.2 Thẻ tương tác luyện nói chính (Speaking Interaction Card - Vùng B)
Nội dung thay đổi linh hoạt theo 2 chế độ luyện nói do Admin cấu hình:

#### CHẾ ĐỘ 1: ASR PRONUNCIATION (LÝ THUYẾT & PHÁT ÂM CÂU NGẮN)
- **Từ/Câu mẫu cần đọc (Target Phrase Box):** 
  - Hiển thị từ vựng hoặc câu ngắn mục tiêu cần luyện phát âm (ví dụ: *"I'd like to book a table for tonight."*). Cỡ chữ lớn `{typography.title-lg}` (Inter, 24px, weight 600) màu `{colors.text-primary}`.
  - Bên cạnh có icon loa phát âm mẫu màu `{colors.secondary}`.
- **Kết quả nhận diện giọng nói (ASR Color feedback text):**
  - Hiển thị đè lên câu mẫu sau khi ghi âm kết thúc.
  - Từ phát âm tốt (>=80%): màu xanh success `{colors.success}` (`#22C55E`).
  - Từ phát âm chưa đạt (<80%): màu đỏ error `{colors.error}` (`#EF4444`) kèm gạch wavy. Rê chuột vào hiện bảng gợi ý IPA đúng và lời khuyên của Admin.
- **Nút "Luyện nói lại" (Retry Button):** 
  - Nền trắng `{colors.surface}`, chữ và viền màu `{colors.primary}`, bo góc `{rounded.lg}` (16px), touch target `44px`. Click để xóa kết quả cũ và ghi âm lại.

#### CHẾ ĐỘ 2: AI ROLE-PLAY (HỘI THOẠI GIẢ LẬP NHẬP VAI VỚI AI)
- **Khung thông tin kịch bản (Scenario Banner):**
  - Nền: `{colors.light-accent}` (`#FDCFFA`) mờ. Bo góc: `{rounded.lg}` (16px). Padding: `{spacing.md}` (16px).
  - Hiển thị bối cảnh nhập vai (ví dụ: *"Nhập vai: Bạn là khách hàng, AI là nhân viên phục vụ nhà hàng. Hãy gọi món khai vị."*).
- **Dòng thoại của Cá Voi Xanh AI (AI Chat Bubble):**
  - Nền: `{colors.surface}`. Bo góc: `{rounded.xl}`. Viền mờ, padding `{spacing.md}`, căn lề trái.
  - Hiển thị câu nói của Cá Voi dưới dạng bong bóng chat kèm icon loa để nghe giọng đọc và hình ảnh Cá Voi nhỏ [whale-removebg.png](file:///d:/Study/research_DiveVerse/project/built-ui/design/design-system/whale-removebg.png) (`36px`).
- **Dòng thoại của học viên (Learner Chat Bubble):**
  - Nền: `{colors.primary}` (`#4E56C0`), chữ trắng. Bo góc: `{rounded.xl}`. Căn lề phải.
  - Xuất hiện sau khi học viên bấm giữ mic nói và AI chuyển giọng nói thành văn bản.
- **Nút Ghi âm đàm thoại (Push-to-Talk Microphone Button):**
  - Nút tròn lớn ở chân thẻ. Đường kính `64px`. Nền `{colors.primary}`, chữ trắng.
  - Học viên nhấn giữ nút này để nói và thả ra để nộp câu thoại cho AI phân tích. Khi thu âm, nút hiển thị sóng âm soundwave màu đỏ nhấp nháy.

### 4.3 Trang kết quả luyện nói (Speaking Result Page)
- **Bảng tổng hợp điểm phát âm (Speaking Stats Dashboard):**
  - Nền: `{colors.surface}`. Bo góc `{rounded.xl}`. Padding `{spacing.xl}` (32px).
  - Hiển thị điểm số trung bình phát âm (ví dụ: *"Điểm phát âm: 85% - Tốt"*), tổng lượt hội thoại và lời khen ngợi của Cá Voi kèm các lời khuyên thực hành từ Admin.

### 4.4 Các hộp thoại báo lỗi micro (Error Modals - Vùng D)
- **Hộp thoại Không nhận dạng được giọng nói (No Audio Received Modal - LN-06-M1):**
  - Nền overlay kính mờ `{colors.glass}`, ở giữa là card báo lỗi nền `{colors.surface}` bo tròn `{rounded.xl}` (24px).
  - Xuất hiện khi cường độ âm thanh ghi nhận bằng 0 (học viên giữ im lặng). Tiêu đề màu đỏ `{colors.error}`: *"Không nghe thấy âm thanh!"*. Hướng dẫn học viên kiểm tra jack cắm micro và nói to hơn. Nút "Đóng cảnh báo" (`button-primary` style).
- **Hộp thoại Lỗi quyền Microphone (Microphone Permission Blocked Modal - LN-06-M2):**
  - Xuất hiện khi trình duyệt báo micro bị chặn quyền truy cập. Tiêu đề màu đỏ `{colors.error}`: *"Lỗi truy cập Microphone"*. Hướng dẫn học viên cấp quyền trong cài đặt trình duyệt và tải lại trang. Nút "Thoát bài học" (`button-secondary` style) dẫn về trang Unit Detail Page.

---

## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)
- **Hành động: Nhấn giữ nút Microphone để nói trong Hội thoại AI**
  - Học viên click giữ chuột trái vào nút Mic $\rightarrow$ Soundwave nhấp nháy $\rightarrow$ Học viên nói $\rightarrow$ Nhả chuột ra $\rightarrow$ Nút Mic chuyển loading spinner $\rightarrow$ Khung chat hiển thị bong bóng thoại học viên căn lề phải $\rightarrow$ Cá Voi Xanh AI phản hồi lại bằng bong bóng thoại căn lề trái và phát file thoại audio $\rightarrow$ Mở nút Mic cho lượt tiếp theo.
  - **Dữ liệu API:** `POST /api/speaking/dialogue` gửi file ghi âm `.wav`
    - Response: `{ "success": true, "userText": "I want to order soup.", "aiResponseText": "Sure, which soup would you like?", "aiAudioUrl": "files/response1.mp3" }`

## 6. CÁC TRẠNG THÁI ĐẶC BIỆT
- **Trạng thái tải (Loading state):** Khi đang gửi file ghi âm lên AI và chờ chuyển đổi văn bản $\rightarrow$ Nút Micro chuyển sang xoay spinner, khóa click, khung chat hiển thị dấu ba chấm nhấp nháy.
- **Trạng thái lỗi micro:** Xuất hiện các Modal báo lỗi LN-06-M1 hoặc LN-06-M2 đè lên giao diện.

## 7. THAM CHIẾU LUỒNG (FLOW REFERENCES)
- **Đến từ:** [unit_detail_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/unit_detail_page.md).
- **Đi đến:** [unit_detail_page.md](file:///d:/Study/research_DiveVerse/project/built-ui/design/uis-spec/learner-app/unit_detail_page.md) (khi click "Hoàn thành bài học").

## 8. LƯU Ý THIẾT KẾ CHO LẬP TRÌNH VIÊN (DO'S AND DON'TS)
- **NÊN:** Thiết kế nút Micro có touch target rất lớn (`64px x 64px`) để dễ tương tác trên di động. Khoảng cách dọc giữa các dòng thoại trong khung chat là `{spacing.md}` (16px) giúp cuộc hội thoại hiển thị mạch lạc.
- **KHÔNG ĐƯỢC:** Để hiển thị bóng đổ đen bên dưới các bong bóng chat. Màu sắc báo lỗi bắt buộc dùng đỏ semantic `{colors.error}` để cảnh báo tức thời.

## ÁNH XẠ DỮ LIỆU MOCK (MOCK DATA BINDING)
- **Thông tin bài học (Lesson Header):** Liên kết với `lessons.unit_1[3]` (các trường `{name}`).
- **Các dạng luyện tập Nói (Speaking Activities):**
  - Phát âm ASR từ/câu ngắn: `{lessons.unit_1[3].exercises.asrPractice}` (câu mẫu phát âm, IPA, audio mẫu).
  - Hội thoại AI Roleplay: `{lessons.unit_1[3].exercises.roleplay}` (bối cảnh hội thoại, lời thoại của Whale AI và các câu gợi ý cho người học).
