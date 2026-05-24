# DiveVerse: Cosmic Design System & Product Specifications

Tài liệu này là "trung tâm điều khiển" thiết kế và đặc tả sản phẩm cho DiveVerse. Dự án kết hợp phương pháp học tập hiện đại với ngôn ngữ thiết kế **Clay.com** và trải nghiệm **Cá Voi Xanh Vũ Trụ**.

---

## 📂 Cấu trúc dự án thiết kế

```text
project/built-ui/design/
├── README.md                    # Hướng dẫn tổng quan & Mục lục
├── STICK_PROMPTS_MASTER_LIST.md # Hệ thống Prompt tạo UI cho Google Stick/Stitch
├── website-detail/              # Tài liệu chi tiết về bản sắc & nghiệp vụ
│   ├── BRAND_IDENTITY.md        # Bản sắc thương hiệu (Mascot, Tone & Voice)
│   ├── USE_CASES.md             # Đặc tả nghiệp vụ (Logic & Xử lý phía Server)
│   └── level_built.md           # Cấu trúc cấp độ học tập
├── IA-and-routing/              # Kiến trúc Thông tin & Định tuyến
│   ├── sitemap.md               # Danh mục 32 màn hình & Modal lớp phủ
│   └── user-flows.md            # Luồng tương tác (Hành trình học viên & Admin)
├── .stitch/
│   └── DESIGN.md                # Design Tokens (Màu, Typography, Spacing) - STITCH READY
├── design-system/               # Tài nguyên hệ thống thiết kế
│   └── icon-library.json        # Thư viện 67 Icon SVG đồng nhất
└── uis-spec/                    # Hệ thống 32 file đặc tả giao diện (UI Specs)
    ├── admin-dashboard/         # Phân hệ quản trị nội dung (13 trang)
    └── learner-app/             # Phân hệ trải nghiệm người học (19 trang)
```

---

## 🐋 1. Định hướng Thương hiệu (The Cosmic Whale)
Hành trình học tập được nhân hóa qua hình tượng **Chú Cá Voi Xanh Vũ Trụ** bơi lội giữa dải ngân hà kiến thức.
- **Linh vật:** Chú Cá Voi Xanh tròn trịa, thân thiện, đại diện cho sự điềm tĩnh và học sâu.
- **Phong cách:** Claymation 3D (Đất sét), tối giản, màu sắc tươi sáng trên nền kem ấm.
- **Tông giọng:** Khuyến khích, truyền cảm hứng, loại bỏ jargon kỹ thuật (ZPD -> Gợi ý từ Cá Voi).

---

## 🛠 2. Quy trình "Thiết kế bằng AI" (Stitch Flow)
Hệ thống được thiết kế để **Google Stick (Stitch)** có thể render mã giao diện lập tức:
1. **Bước 1:** Nạp link GitHub và chạy prompt khởi tạo tại Giai đoạn 0 trong [STICK_PROMPTS_MASTER_LIST.md](STICK_PROMPTS_MASTER_LIST.md).
2. **Bước 2:** AI tự động đọc Tokens tại [.stitch/DESIGN.md](.stitch/DESIGN.md) và Icons tại [icon-library.json](design-system/icon-library.json).
3. **Bước 3:** Sử dụng các lệnh render chỉ điểm trực tiếp vào từng file trong thư mục `uis-spec/`.

---

## 📝 3. Hệ thống Đặc tả chi tiết (UI Specifications)

### 🎓 Phân hệ Người học (Learner App - 19 trang)
Dẫn dắt người học qua lộ trình khám phá ngôn ngữ tự nhiên:
- **Khởi hành:** [guest_landing_page.md](uis-spec/learner-app/guest_landing_page.md), [learner_login_page.md](uis-spec/learner-app/learner_login_page.md), [learner_register_page.md](uis-spec/learner-app/learner_register_page.md).
- **Trạm điều khiển:** [learner_dashboard.md](uis-spec/learner-app/learner_dashboard.md), [unit_detail_page.md](uis-spec/learner-app/unit_detail_page.md).
- **Phòng luyện kỹ năng:** 
    - [vocabulary_learning_page.md](uis-spec/learner-app/vocabulary_learning_page.md) (Luồng 6 bước).
    - [grammar_learning_page.md](uis-spec/learner-app/grammar_learning_page.md) (Hành trình 7 chặng).
    - Luyện [Nghe](uis-spec/learner-app/listening_practice_page.md), [Nói](uis-spec/learner-app/speaking_practice_page.md), [Đọc](uis-spec/learner-app/reading_practice_page.md), [Viết](uis-spec/learner-app/writing_practice_page.md) tích hợp hỗ trợ AI.
- **Đánh giá & Ôn tập:** [pre_test_page.md](uis-spec/learner-app/pre_test_page.md), [unit_level_test_page.md](uis-spec/learner-app/unit_level_test_page.md), [mock_test_page.md](uis-spec/learner-app/mock_test_page.md), [test_result_page.md](uis-spec/learner-app/test_result_page.md), [srs_review_page.md](uis-spec/learner-app/srs_review_page.md), [personal_review_page.md](uis-spec/learner-app/personal_review_page.md).
- **Cài đặt & Tiện ích:** [dictionary_page.md](uis-spec/learner-app/dictionary_page.md), [profile_settings_page.md](uis-spec/learner-app/profile_settings_page.md).

### 🛠 Phân hệ Quản trị (Admin Dashboard - 13 trang)
Công cụ quản lý nội dung khoa học cho quản trị viên:
- **Danh sách:** [level_list_page.md](uis-spec/admin-dashboard/level_list_page.md), [unit_list_page.md](uis-spec/admin-dashboard/unit_list_page.md), [lesson_list_page.md](uis-spec/admin-dashboard/lesson_list_page.md), [test_list_page.md](uis-spec/admin-dashboard/test_list_page.md).
- **Cấu hình & Soạn thảo:** [lesson_configuration_page.md](uis-spec/admin-dashboard/lesson_configuration_page.md), [create_edit_test_page.md](uis-spec/admin-dashboard/create_edit_test_page.md).
- **Modals (Lớp phủ):** Toàn bộ các hộp thoại Add/Edit/Delete cho Level, Unit, Lesson và Test.

---

## 🎨 4. Design System (Clay.com Style)
- **Cốt lõi:** Canvas kem ấm `#fffaf0`, Chữ mực Navy `#0a0a0a`.
- **Tương tác:** Bo góc cực đại `24px`, không gian thở rộng rãi, sử dụng Component thẻ (Card) làm đơn vị cơ bản.
