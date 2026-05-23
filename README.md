# DiveVerse Design & Specification System

Thư mục này chứa toàn bộ hệ thống tài liệu phân tích, thiết kế giao diện (UI/UX), cấu trúc luồng người dùng (User Flows) và hệ thống đặc tả các màn hình của ứng dụng học tiếng Anh DiveVerse.

---

## 📂 Cấu trúc thư mục

```text
project/design/
├── README.md                 # Tài liệu hướng dẫn này
├── DESIGN.md                 # Hệ thống thiết kế (Tokens, Typography, Iconography)
├── USE_CASES.md              # Đặc tả Use Case chi tiết (UC-01 -> UC-08)
├── IA-and-routing/           # Kiến trúc thông tin & Định tuyến
│   ├── sitemap.md            # Cây cấu trúc màn hình & Hộp thoại (Sitemap)
│   └── user-flows.md         # Luồng tương tác (Concise Version)
├── design-system/            # Tài nguyên Design System
│   ├── tokens.json           # Danh sách token CSS
│   └── icon-library.json     # Thư viện 67 Lucide SVG cho Figma/Code
└── uis-spec/                 # Đặc tả chi tiết giao diện màn hình (UI specs)
```

---

## 📖 Chi tiết các tài liệu cốt lõi

### 1. Hệ thống thiết kế (Clay.com Style Guidelines)
Tài liệu **[DESIGN.md](file:///d:/Study/research_DiveVerse/project/design/DESIGN.md)** thiết lập bộ quy chuẩn giao diện dựa trên phong cách **Clay.com**:
- **Nền sàn (Canvas):** Màu kem ấm sáng `#fffaf0` làm màu nền chủ đạo cho toàn bộ ứng dụng.
- **Màu chữ & CTA chính:** Đen tuyền/Navy đậm `#0a0a0a` mang lại cảm giác hiện đại và độ tương phản cao.
- **Thẻ tính năng màu sắc (Saturated Cards):** Sử dụng 5 gam màu saturated bắt mắt (Hot Pink `#ff4d8b`, Deep Teal `#1a3a3a`, Lavender `#b8a4ed`, Peach `#ffb084`, Ochre `#e8b94a`).
- **Hình ảnh thương hiệu:** Sử dụng các hình vẽ minh họa đất sét 3D (3D claymation illustrations) mềm mại.
- **Bo góc (Border Radius):** Bo góc lớn thân thiện (12px cho nút/input, 16px cho thẻ nội dung, 24px cho thẻ tính năng lớn).
- **Nguyên lý tương tác:** Không sử dụng đổ bóng đậm (chỉ dùng hairline border 1px `#e5e5e5`), khoảng cách section rộng rãi (96px), touch target tối thiểu 44x44px.

### 2. Đặc tả chức năng hệ thống
Tài liệu **[USE_CASES.md](file:///d:/Study/research_DiveVerse/project/design/USE_CASES.md)** chi tiết hóa luồng xử lý nghiệp vụ cho 8 Use Case chính (UC-01 đến UC-08):
- **UC-01 -> UC-04 (Admin):** Quản lý Cấp độ, Quản lý Unit, Cấu hình bài học & bài tập động, Quản lý đề thi.
- **UC-05 -> UC-08 (Learner):** Quy trình học từ vựng 6 giai đoạn, học ngữ pháp 7 giai đoạn, phòng luyện 4 kỹ năng ( shadow nói đuổi, viết gợi ý ZPD, đọc báo chí), thi cử nghiêm ngặt, và ôn tập lặp lại ngắt quãng SRS.

### 3. Kiến trúc thông tin & Định tuyến
Thư mục **[IA-and-routing/](IA-and-routing/)** định hình khung xương và đường đi của ứng dụng:
- **[sitemap.md](IA-and-routing/sitemap.md)**: Sơ đồ cây thư mục trang, đã được liên kết trực tiếp với UI Specs.
- **[user-flows.md](IA-and-routing/user-flows.md)**: Phiên bản rút gọn tối ưu context, mô tả luồng chuyển động màn hình.

### 4. Tài nguyên Design System
- **[DESIGN.md](DESIGN.md)**: Chứa YAML Frontmatter cho Google Stick và quy tắc Iconography.
- **[icon-library.json](design-system/icon-library.json)**: Bộ 67 icon SVG đã trích xuất, sẵn sàng để import vào Figma.

---

## 🤖 Guide for AI Agents (Instruction for UI Design & Coding)

Nếu bạn là một AI Agent được giao nhiệm vụ thiết kế UI hoặc lập trình frontend cho folder này, hãy tuân thủ quy trình đọc sau để tránh sai sót:

### 1. Luồng đọc tài liệu (Workflow)
1.  **BẮT ĐẦU từ [DESIGN.md](DESIGN.md):** Nắm vững phong cách "Clay.com Style" (màu Ochre/Peach, bo góc 24px, canvas krem). Mọi input/button/card phải tuân theo style này.
2.  **HIỂU NGHIỆP VỤ tại [USE_CASES.md](USE_CASES.md):** Đọc kỹ các luồng xử lý (Main Success Scenario) và các trường hợp lỗi (Extension) để biết UI cần hiển thị gì khi thành công hoặc thất bại.
3.  **XÁC ĐỊNH VỊ TRÍ qua [IA-and-routing/sitemap.md](IA-and-routing/sitemap.md):** Tra cứu mã màn hình (ví dụ: `LN-03`) để biết trang đó nằm ở đâu trong hệ thống.
4.  **BÁM SÁT TƯƠNG TÁC tại [IA-and-routing/user-flows.md](IA-and-routing/user-flows.md):** Đây là "bản đồ đường đi". Phải xem màn hình trước và sau của trang đang thiết kế là gì để đảm bảo nút "Quay lại" hoặc "Tiếp theo" dẫn đúng chỗ.
5.  **CHI TIẾT HÓA tại [uis-spec/](uis-spec/):** Mở file MD tương ứng với mã màn hình để xem layout chi tiết (Header, Content, Sidebar) và các trạng thái Component.

### 2. Nguyên tắc quan trọng
*   **User Flows là bắt buộc:** Không được tự ý tạo luồng đi mới nếu không có trong `user-flows.md`. File này cực kỳ quan trọng để lập trình định tuyến (Routing).
*   **Trạng thái UI:** Luôn kiểm tra `user-flows.md` để biết khi nào hiện Toast, khi nào hiện Modal, khi nào chuyển trang.
*   **Nhất quán Component:** Nếu thiết kế 1 trang mới, hãy kiểm tra các trang cùng nhóm trong `uis-spec` để đảm bảo dùng chung component (ví dụ: `ZPD Feedback Modal`).
*   **Sử dụng Icon tiết chế (Iconography):** Tra cứu file `design-system/icon-library.json` (67 Lucide icons). **KHÔNG LẠM DỤNG ICON**. Chỉ dùng icon cho điều hướng, trạng thái, hệ thống, hoặc gamification. Button có text rõ ràng thì không cần icon trang trí. (Xem chi tiết tại mục *Iconography* trong `DESIGN.md`).

Gồm 13 tệp đặc tả chi tiết giao diện quản lý:
- *Xác thực:* [admin_login_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/admin-dashboard/admin_login_page.md).
- *Lộ trình:* [level_list_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/admin-dashboard/level_list_page.md), [add_edit_level_modal.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/admin-dashboard/add_edit_level_modal.md), [delete_level_modal.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/admin-dashboard/delete_level_modal.md).
- *Unit:* [unit_list_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/admin-dashboard/unit_list_page.md), [add_edit_unit_modal.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/admin-dashboard/add_edit_unit_modal.md), [delete_unit_modal.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/admin-dashboard/delete_unit_modal.md).
- *Bài học:* [lesson_list_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/admin-dashboard/lesson_list_page.md), [lesson_configuration_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/admin-dashboard/lesson_configuration_page.md), [delete_lesson_modal.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/admin-dashboard/delete_lesson_modal.md).
- *Đề thi:* [test_list_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/admin-dashboard/test_list_page.md), [create_edit_test_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/admin-dashboard/create_edit_test_page.md), [delete_test_modal.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/admin-dashboard/delete_test_modal.md).

#### 📱 Phân hệ Người học ([learner-app](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/))
Gồm 18 tệp đặc tả chi tiết giao diện học tập:
- *Xác thực:* [guest_landing_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/guest_landing_page.md), [learner_login_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/learner_login_page.md), [learner_register_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/learner_register_page.md).
- *Lộ trình:* [learner_dashboard.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/learner_dashboard.md), [unit_detail_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/unit_detail_page.md).
- *Học quy nạp:* [vocabulary_learning_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/vocabulary_learning_page.md), [grammar_learning_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/grammar_learning_page.md).
- *Phòng luyện kỹ năng:* [listening_practice_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/listening_practice_page.md), [speaking_practice_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/speaking_practice_page.md), [reading_practice_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/reading_practice_page.md), [writing_practice_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/writing_practice_page.md).
- *Phòng thi cử:* [pre_test_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/pre_test_page.md), [unit_level_test_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/unit_level_test_page.md), [mock_test_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/mock_test_page.md), [test_result_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/test_result_page.md).
- *Tra cứu & Ôn tập:* [personal_review_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/personal_review_page.md), [srs_review_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/srs_review_page.md).
- *Cá nhân:* [profile_settings_page.md](file:///d:/Study/research_DiveVerse/project/design/uis-spec/learner-app/profile_settings_page.md).

---

## 🎯 Hướng dẫn sử dụng cho các vị trí

1. **UX Designer (Thiết kế sản phẩm):**
   - Đọc kỹ `DESIGN.md` để nắm bắt hệ thống font, màu sắc và linh hồn thiết kế Clay.com.
   - Đối chiếu với sơ đồ `IA-and-routing/sitemap.md` để biết tổng số trang và modal cần vẽ trên Figma.
   - Đọc các tệp tương ứng trong `uis-spec/` để nắm rõ bố cục, vị trí các nút, và các trạng thái đặc biệt cần thiết kế (empty state, loading state, error state).

2. **UI Prototyper (Thiết kế luồng tương tác):**
   - Đọc tệp `IA-and-routing/user-flows.md` làm nền tảng để thiết kế các liên kết tương tác (Figma Prototyping) chạy từ trang này qua trang khác đúng theo hành động của người dùng.

3. **Frontend Developer (Lập trình viên Giao diện):**
   - Import file `design-system/tokens.json` vào dự án để thiết lập các biến CSS Variables hoặc TailwindConfig (nếu được yêu cầu).
   - Xem cấu trúc chia vùng layout trong mục **## 3. BỐ CỤC (LAYOUT)** của từng tệp đặc tả màn hình để viết code HTML/CSS Grid.
   - Cài đặt các xử lý lỗi, validate form ở mục **## 5. CHI TIẾT TƯƠNG TÁC (INTERACTION DETAILS)** và **## 6. CÁC TRẠNG THÁI ĐẶC BIỆT (SPECIAL STATES)** để đảm bảo ứng dụng vận hành đúng nghiệp vụ.
