# USER FLOWS – DIVEVERSE (CONCISE VERSION)

Tài liệu tóm lược các luồng tương tác chính (User Flows) dựa trên [USE_CASES.md](../USE_CASES.md) và [sitemap.md](sitemap.md).

---

## 1. NHÓM ADMIN (AD-FL)

### **AD-FL-01: Quản lý Cấp độ (UC-01)**
`Admin Login` → `Level List` → `Modal Add/Edit/Delete` → `Toast Success` → `Reload List`.
*   *Lưu ý:* Xóa cấp độ sẽ bị chặn nếu có học viên đang hoạt động (E-1).

### **AD-FL-02: Quản lý Unit (UC-02)**
`Level List` → click Level → `Unit List` → `Modal Add/Edit/Delete` OR `Drag & Drop Reorder` → `Save Order` → `Reload List`.

### **AD-FL-03: Cấu hình Bài học (UC-03)**
`Unit List` → click Unit → `Lesson List` → `Lesson Config Page` → Chọn hình thức (Dynamic Form) → Nhập dữ liệu/File/Giải thích → `Save` → Quay về `Lesson List`.

### **AD-FL-04: Quản lý Bài kiểm tra (Test Management - UC-04)**
`Nav: Tests` → `Test List` → `Create/Edit Test Page` → Chọn loại (Mini/Level/Mock) → Form soạn thảo kỹ năng (Audio/Text/ZPD Keywords) → `Save` → `Reload Test List`.

---

## 2. NHÓM LEARNER (LN-FL)

### **LN-FL-01: Xác thực (Authentication)**
`Landing Page` → `Login/Register Page` → `Validation` → `Learner Dashboard`.

### **LN-FL-02: Khám phá Ngôn ngữ (Từ vựng/Ngữ pháp - UC-05)**
`Dashboard` → `Unit Detail` → click Bài học → `Learning Page`:
1.  **Discovery:** Khám phá Ngữ cảnh/Tình huống (Cùng Cá Voi).
2.  **Explicit:** Giải mã Nghĩa/Quy tắc/IPA.
3.  **Active Practice:** Chinh phục trạm Flashcard/Kéo thả.
4.  **Dictation:** Ghi nhớ âm thanh (Nghe & gõ lại).
5.  **Production:** Tự viết câu + `Gợi ý Cá Voi Thông Thái` (Sửa lỗi 2 vòng).
6.  **Completion:** Chúc mừng + Cộng EXP + Lưu SRS.

### **LN-FL-03: Trạm luyện Kỹ năng (Practice Room - UC-06)**
`Unit Detail` → click Kỹ năng → `Practice Page`:
*   **Listening:** Stories (Interactive) / Quiz / Shadowing (Cá Voi so khớp).
*   **Speaking:** Phát âm câu / Nhập vai Cá Voi (Hội thoại AI).
*   **Reading:** Comprehension / News-based (Tra từ tại chỗ).
*   **Writing:** Basic / Cá Voi dẫn dắt / Chấm luận AI.
→ `Result Page` → Ask AI / Save to SRS → `Finish`.

### **LN-FL-04: Phòng thi (Exam Room - UC-07)**
`Unit Detail/Dashboard` → click Test → `Pre-test Page` → Chọn mode (Tập dượt/Thi thật) → `Start`:
*   **Mini/Level Test:** Làm tuần tự các Tab kỹ năng.
*   **Mock Test (Strict):** `Listening` (Auto-next) → `Reading` → `Writing` → `Speaking` (AI Examiner).
→ `Test Result Page` (Band score/Điểm chi tiết/Giải thích) → `Exit`.

### **LN-FL-05: Tra cứu & Ôn tập SRS (UC-08)**
*   **Tra cứu:** `Review Dashboard` → Search Bar → Click gợi ý → `Dictionary Page` (Slug-based) → `Save to SRS`.
*   **Ôn tập:** `Review Dashboard` → `SRS Review Page`:
    1. Hiện câu khuyết + 10s đếm ngược.
    2. Nhập đáp án (hoặc Quick Lookup Modal).
    3. Xem kết quả + `Self-Evaluation` (3 mức độ nhớ).
    4. Cập nhật thuật toán SRS → `Review Result`.
