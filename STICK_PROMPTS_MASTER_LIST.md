# HƯỚNG DẪN ĐIỀU PHỐI GOOGLE STICK TẠO UI TỪ GITHUB REPOSITORY

Tài liệu này dùng để điều phối Google Stick (hoặc các AI Render UI bám sát Figma) sinh ra đầy đủ 32 màn hình (bao gồm cả các component Modal) dựa trên repository GitHub đã cung cấp. 

Vì toàn bộ cấu trúc dữ liệu, layout và component đều đã được mô tả MỨC ĐỘ PIXEL TRONG TỪNG FILE `.md`, prompt ở đây tuyệt đối KHÔNG MÔ TẢ LẠI GIAO DIỆN. Prompt chỉ làm nhiệm vụ CẤP QUYỀN, THIẾT LẬP VAI TRÒ và CHỈ ĐIỂM FILE.

---

## BƯỚC 1: KHỞI TẠO VAI TRÒ VÀ NẠP NGỮ CẢNH TỪ GITHUB
**Mục đích:** Gắn link GitHub và ép AI (Google Stick) đọc các file cấu trúc mốc để lấy rules design, components và nhận diện thương hiệu.

**Hãy đưa prompt này vào tin nhắn đầu tiên với Google Stick:**

> "Bạn là một Chuyên gia UI/UX và Kỹ sư Frontend lão luyện. Tôi cung cấp cho bạn kho lưu trữ (repository) chứa toàn bộ đặc tả giao diện của dự án tại link: https://github.com/Uyen211/website-learning-english-design.git 
> 
> Trước khi chúng ta bắt tay vào tạo bất kỳ giao diện (Figma-like prototype / UI components) nào, bạn BẮT BUỘC phải cào (crawl/read) và nạp vào bộ nhớ các file nền tảng sau nằm trong nhánh `main` thư mục `project/design/`:
> 1. `BRAND_IDENTITY.md` (Định hướng linh vật Cá Voi Xanh Vũ Trụ và tone & voice).
> 2. `STICK_GUIDE.md` (Hướng dẫn quy tắc làm việc khắt khe cho AI).
> 3. `.stitch/DESIGN.md` (Hệ thống Design Tokens, mã màu Clay.com, typography, border-radius...).
> 4. `design-system/icon-library.json` (Danh sách các icon hợp lệ).
> 
> Luật chơi: Tuyệt đối tuân thủ từng ly từng tí các mô tả bố cục (layout), văn bản (text), thành phần UI từ các file spec. Bạn không tự ý sáng tạo hay thêm thắt ngoài spec.
> LƯU Ý: Tuyệt đối chỉ phản hồi bằng thiết kế React, không giải thích dài dòng.
> 
> Nếu bạn đã phân tích xong link GitHub và sẵn sàng khởi tạo bộ nhận diện chuẩn, hãy trả lời ngắn gọn: ''Đã sẵn sàng tạo giao diện thiết kế hệ thống Cá Voi Xanh!''"

---

## BƯỚC 2: RENDER HỆ THỐNG MÀN HÌNH LEARNER APP (19 TRANG)
**Mục đích:** Chỉ định từng file cụ thể trong hệ thống để Google Stick "ráp" giao diện thành trực quan. Dùng chung một form Prompt đơn giản vì thông tin đã có đủ trong file.

**Copy lần lượt các lệnh này để tạo giao diện Learner:**

> "Dựa vào repository, hãy render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/guest_landing_page.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/learner_login_page.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/learner_register_page.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/learner_dashboard.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/profile_settings_page.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/unit_detail_page.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/vocabulary_learning_page.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/grammar_learning_page.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/listening_practice_page.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/speaking_practice_page.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/reading_practice_page.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/writing_practice_page.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/dictionary_page.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/personal_review_page.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/srs_review_page.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/pre_test_page.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/unit_level_test_page.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/mock_test_page.md`"

> "Render mã giao diện hoàn chỉnh theo đặc tả tại: `project/design/uis-spec/learner-app/test_result_page.md`"

---

## BƯỚC 3: RENDER HỆ THỐNG ADMIN DASHBOARD VÀ MODALS (13 TRANG)
**Tương tự, tiếp tục yêu cầu Google Stick load các file thuộc phân hệ quản trị viên.**

> "Chuyển sang phân hệ Quản trị. Đọc kỹ file trên repo và render mã giao diện theo đặc tả: `project/design/uis-spec/admin-dashboard/admin_login_page.md`"

> "Render mã giao diện theo đặc tả tại: `project/design/uis-spec/admin-dashboard/level_list_page.md`"

> "Render mã giao diện Modal theo đặc tả tại: `project/design/uis-spec/admin-dashboard/add_edit_level_modal.md`"

> "Render mã giao diện Modal theo đặc tả tại: `project/design/uis-spec/admin-dashboard/delete_level_modal.md`"

> "Render mã giao diện theo đặc tả tại: `project/design/uis-spec/admin-dashboard/unit_list_page.md`"

> "Render mã giao diện Modal theo đặc tả tại: `project/design/uis-spec/admin-dashboard/add_edit_unit_modal.md`"

> "Render mã giao diện Modal theo đặc tả tại: `project/design/uis-spec/admin-dashboard/delete_unit_modal.md`"

> "Render mã giao diện theo đặc tả tại: `project/design/uis-spec/admin-dashboard/lesson_list_page.md`"

> "Render mã giao diện theo đặc tả tại: `project/design/uis-spec/admin-dashboard/lesson_configuration_page.md`"

> "Render mã giao diện Modal theo đặc tả tại: `project/design/uis-spec/admin-dashboard/delete_lesson_modal.md`"

> "Render mã giao diện theo đặc tả tại: `project/design/uis-spec/admin-dashboard/test_list_page.md`"

> "Render mã giao diện theo đặc tả tại: `project/design/uis-spec/admin-dashboard/create_edit_test_page.md`"

> "Render mã giao diện Modal theo đặc tả tại: `project/design/uis-spec/admin-dashboard/delete_test_modal.md`"