# HƯỚNG DẪN ĐIỀU PHỐI GOOGLE STICK TẠO UI TỪ GITHUB REPOSITORY
> **Tài liệu master prompts dùng để hướng dẫn công cụ Google Stick (hoặc các AI thiết kế UI Figma/React) nạp ngữ cảnh thương hiệu và render chuẩn xác 32 giao diện màn hình/modal của DiveVerse.**

---

## 🚀 GIAI ĐOẠN 0: NẠP NGỮ CẢNH TỔNG THỂ & THIẾT LẬP VAI TRÒ
*   **Mục đích:** Bắt buộc Google Stick phải đọc hiểu bản sắc thương hiệu, thiết kế màu sắc Vũ Trụ Ánh Sáng, thư viện icon và cấu trúc dữ liệu mock để đảm bảo tính đồng bộ trước khi tạo UI.
*   **Hành động:** Copy toàn bộ prompt dưới đây vào tin nhắn đầu tiên khi khởi tạo phiên làm việc với Google Stick:

> "Bạn là một Chuyên gia thiết kế UI/UX và Kỹ sư Frontend lão luyện. Nhiệm vụ của bạn là xây dựng hệ thống giao diện (Figma prototype / mã React UI) cho dự án DiveVerse (Chủ đề Vũ Trụ Ánh Sáng - Light Mode Universe).
> 
> Tôi cung cấp kho lưu trữ mã nguồn tại link: https://github.com/Uyen211/website-learning-english-design.git
> 
> **Nhiệm vụ bắt buộc đầu tiên:** Trước khi thực hiện thiết kế bất kỳ màn hình nào, bạn BẮT BUỘC phải đọc (crawl/read) và nạp vào bộ nhớ ngữ cảnh của 6 tệp tin nền tảng sau trong nhánh `main` thư mục `project/built-ui/design/`:
> 1. `website-detail/MASTER_UI_UX_GUIDELINES.md` (Quy chuẩn thiết kế visual, dải màu, hiệu ứng glow thay cho shadow, và quy tắc linh vật Cá Voi Xanh).
> 2. `.stitch/DESIGN.md` (Hệ thống Design Tokens chính thức về màu sắc, typography, border-radius, gradients).
> 3. `design-system/icon-library.json` (Thư viện icon SVG hợp lệ duy nhất được dùng).
> 4. `website-detail/mock_data.json` (Nguồn dữ liệu mock chuẩn để điền nội dung chữ, bảng biểu, tránh dùng lorem ipsum).
> 5. `website-detail/level_built.md` (Quy chuẩn lộ trình 3 cấp độ học và ánh xạ điểm IELTS/TOEIC).
> 6. `website-detail/USE_CASES.md` (Đặc tả các luồng nghiệp vụ và tương tác).
> 
> **Quy tắc thiết kế bất biến:**
> - Tuyệt đối không dùng bóng đổ xám/đen vật lý (`rgba(0,0,0,...)`). Phải sử dụng dải phát quang mờ ảo neon (Glow) như định nghĩa trong guidelines.
> - Đảm bảo Touch Target tối thiểu đạt 44px trở lên cho các nút và input.
> - Bo tròn góc lớn (`16px` đến `32px`), các layout kính mờ (glassmorphism) phải dùng `backdrop-filter: blur(8px)`.
> - Chỉ sử dụng các icon khớp với định nghĩa trong `icon-library.json`.
> - Dùng ảnh Cá Voi Xanh Vũ Trụ tại đường dẫn `project/built-ui/design/design-system/whale-removebg.png` cho phần mascot hiển thị.
> 
> Nếu bạn đã đọc hiểu đầy đủ 6 tệp tin trên và sẵn sàng thiết kế theo quy chuẩn, hãy phản hồi chính xác câu sau: **'Đã nạp toàn bộ ngữ cảnh Vũ Trụ Ánh Sáng và sẵn sàng thiết kế giao diện DiveVerse!'**"

---

## 🎨 GIAI ĐOẠN 1: THIẾT LẬP HỆ THỐNG DESIGN TOKENS TRONG FIGMA/REACT
*   **Mục đích:** Hướng dẫn AI khai báo các kiểu dáng (Styles) và thư viện dùng chung.
*   **Prompt gửi cho Google Stick:**

> "Dựa trên hai tệp tin `project/built-ui/design/.stitch/DESIGN.md` và `project/built-ui/design/design-system/icon-library.json`, hãy khai báo toàn bộ Design Tokens (màu sắc, gradient, shadow, kiểu chữ) và thiết lập một component `<Icon />` động để hiển thị các paths SVG từ thư viện icon. Hãy phản hồi xác nhận khi hoàn tất."

---

## 🎓 GIAI ĐOẠN 2: THIẾT KẾ PHÂN HỆ HỌC VIÊN (LEARNER APP - 19 TRANG)
*   **Mục đích:** Yêu cầu Google Stick render chi tiết từng giao diện học viên theo đúng tệp đặc tả và dữ liệu trong mock data.
*   **Các prompt gửi tuần tự (đợi AI phản hồi xong mỗi trang mới gửi tiếp):**

> "Hãy render mã giao diện trang chủ giới thiệu dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/guest_landing_page.md` và dữ liệu tương ứng từ `landingPage` trong `mock_data.json`."

> "Render giao diện đăng nhập dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/learner_login_page.md` và hiển thị các trạng thái lỗi từ `auth.loginErrors`."

> "Render giao diện đăng ký dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/learner_register_page.md` và hiển thị lỗi từ `auth.registerErrors`."

> "Render bảng điều khiển học viên dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/learner_dashboard.md` kết hợp dữ liệu EXP, Streak từ `profile` và sơ đồ trạm uốn lượn từ `levels[0].units`."

> "Render trang chi tiết trạm Unit dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/unit_detail_page.md` và dữ liệu danh sách bài học từ `lessons.unit_1`."

> "Render bài học Từ vựng với luồng tương tác 6 bước dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/vocabulary_learning_page.md` và các bước dữ liệu từ `lessons.unit_1[0].exercises`."

> "Render bài học Ngữ pháp quy nạp 7 chặng dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/grammar_learning_page.md` và các chặng từ `lessons.unit_1[1].exercises`."

> "Render bài luyện nghe (interactive stories, shadowing) dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/listening_practice_page.md` và dữ liệu tại `lessons.unit_1[2].exercises`."

> "Render bài luyện nói (ASR, roleplay với AI) dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/speaking_practice_page.md` và dữ liệu tại `lessons.unit_1[3].exercises`."

> "Render bài luyện đọc có popup từ điển tại chỗ dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/reading_practice_page.md` và dữ liệu bài đọc tại `lessons.unit_1[4].exercises`."

> "Render bài luyện viết hỗ trợ AI ZPD dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/writing_practice_page.md` và tiêu chí tại `lessons.unit_1[5].exercises`."

> "Render bài thi đánh giá năng lực đầu vào dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/pre_test_page.md` và đề thi mẫu tại `tests[0]`."

> "Render bài thi cuối Unit dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/unit_level_test_page.md` và đề thi `tests[1]`."

> "Render bài thi thử IELTS/TOEIC dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/mock_test_page.md` và đề thi `tests[2]`."

> "Render trang báo cáo kết quả thi dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/test_result_page.md` và thông tin chi tiết tại `testResult`."

> "Render phòng ôn tập lặp lại ngắt quãng dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/srs_review_page.md` và danh sách từ đến hạn tại `srsReviewQueue`."

> "Render trang ôn tập cá nhân dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/personal_review_page.md` kết hợp `profile.errorMemoryList` và `profile.studyHistory`."

> "Render trang tra cứu từ điển dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/dictionary_page.md` và dữ liệu từ điển `dictionary`."

> "Render trang thiết lập hồ sơ cá nhân và học bạ dựa trên đặc tả tại: `project/built-ui/design/uis-spec/learner-app/profile_settings_page.md` và dữ liệu cá nhân tại `profile`."

---

## 🛠️ GIAI ĐOẠN 3: THIẾT KẾ PHÂN HỆ QUẢN TRỊ (ADMIN DASHBOARD & MODALS - 13 TRANG)
*   **Mục đích:** Yêu cầu Google Stick render các giao diện quản trị viên và modal nổi tương thích.
*   **Các prompt gửi tuần tự:**

> "Render giao diện đăng nhập Admin dựa trên đặc tả tại: `project/built-ui/design/uis-spec/admin-dashboard/admin_login_page.md`."

> "Render trang danh sách cấp độ dựa trên đặc tả tại: `project/built-ui/design/uis-spec/admin-dashboard/level_list_page.md` và mảng `adminDashboardData.levelsList`."

> "Render hộp thoại nổi Modal Thêm/Sửa Cấp độ dựa trên đặc tả tại: `project/built-ui/design/uis-spec/admin-dashboard/add_edit_level_modal.md`."

> "Render hộp thoại cảnh báo Xóa Cấp độ dựa trên đặc tả tại: `project/built-ui/design/uis-spec/admin-dashboard/delete_level_modal.md`."

> "Render trang danh sách Unit dựa trên đặc tả tại: `project/built-ui/design/uis-spec/admin-dashboard/unit_list_page.md` và mảng `adminDashboardData.unitsList`."

> "Render hộp thoại nổi Modal Thêm/Sửa Unit dựa trên đặc tả tại: `project/built-ui/design/uis-spec/admin-dashboard/add_edit_unit_modal.md`."

> "Render hộp thoại cảnh báo Xóa Unit dựa trên đặc tả tại: `project/built-ui/design/uis-spec/admin-dashboard/delete_unit_modal.md`."

> "Render trang danh sách bài học dựa trên đặc tả tại: `project/built-ui/design/uis-spec/admin-dashboard/lesson_list_page.md` và mảng `adminDashboardData.lessonsList`."

> "Render trang cấu hình bài học & upload bài tập dựa trên đặc tả tại: `project/built-ui/design/uis-spec/admin-dashboard/lesson_configuration_page.md`."

> "Render hộp thoại cảnh báo Xóa Cấu hình Bài học dựa trên đặc tả tại: `project/built-ui/design/uis-spec/admin-dashboard/delete_lesson_modal.md`."

> "Render trang danh sách đề kiểm tra dựa trên đặc tả tại: `project/built-ui/design/uis-spec/admin-dashboard/test_list_page.md` và mảng `adminDashboardData.testsList`."

> "Render trang soạn thảo đề thi dựa trên đặc tả tại: `project/built-ui/design/uis-spec/admin-dashboard/create_edit_test_page.md`."

> "Render hộp thoại cảnh báo Xóa đề thi dựa trên đặc tả tại: `project/built-ui/design/uis-spec/admin-dashboard/delete_test_modal.md`."