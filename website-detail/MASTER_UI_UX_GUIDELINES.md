# BỘ QUY CHUẨN THIẾT KẾ UI/UX TỔNG THỂ (MASTER UI/UX GUIDELINES)
**Nền tảng học tiếng Anh DiveVerse - Chủ đề "Vũ Trụ Ánh Sáng" (Light Mode Universe)**

> **Lưu ý quan trọng:** Đây là tài liệu duy nhất và toàn diện nhất (Single Source of Truth) định hướng toàn bộ việc thiết kế UI/UX trên hệ thống. Tài liệu này thay thế hoàn toàn các văn bản đơn lẻ trước đây. 

---

## MỤC LỤC
1. [PHẦN 0: BẢN SẮC THƯƠNG HIỆU (BRAND IDENTITY)](#phần-0-bản-sắc-thương-hiệu-brand-identity)
2. [PHẦN 1: ĐỊNH HƯỚNG THỊ GIÁC (VISUAL DIRECTION)](#phần-1-định-hướng-thị-giác-visual-direction)
3. [PHẦN 2: CẤU TRÚC LAYOUT VÀ IA (UX ARCHITECTURE)](#phần-2-cấu-trúc-layout-và-ia-ux-architecture)
4. [PHẦN 3: TÍCH HỢP UI COMPONENT (MAPPING LAYOUT & VISUAL)](#phần-3-tích-hợp-ui-component-mapping-layout--visual)

---

## PHẦN 0: BẢN SẮC THƯƠNG HIỆU (BRAND IDENTITY)

Tài liệu này định nghĩa linh hồn, hình ảnh và phong cách cốt lõi của thương hiệu DiveVerse, giúp các AI Agent và Designer thấu hiểu và truyền tải đúng thông điệp qua từng pixel giao diện.

### 0.1 Ý Nghĩa Tựa Đề & Khẩu Hiệu
- **DiveVerse = Dive (Lặn/Đắm mình) + Universe (Vũ trụ)**: Việc học tiếng Anh ở đây không phải là nhồi nhét từ vựng, mà là một hành trình "đắm mình" vào một không gian kiến thức vô hạn, nơi người học tự do khám phá chân trời ngôn ngữ.
- **Slogan:** *"Dive Deep, Reach the Stars."* (Lặn sâu, Chạm tới những vì sao) / *"Đắm mình vào vũ trụ tiếng Anh theo cách của bạn."*

### 0.2 Cá Tính Thương Hiệu (Brand Personality)
1. **Explorative (Khám phá):** Khuyến khích người học thử nghiệm và khám phá cái mới (Inductive Learning).
2. **Whimsical (Ngẫu hứng/Kỳ ảo):** Vũ trụ và tinh tú tạo cảm giác tò mò, thú vị, giảm bớt sự nhàm chán của việc học.
3. **Encouraging (Khích lệ):** Ứng dụng AI Feedback (ZPD) đóng vai trò như một người bạn đồng hành ân cần, giúp vượt qua nỗi sợ sai.
4. **Sophisticated but Simple (Tinh tế nhưng Đơn giản):** Tổng thể phong cách tuân thủ "Clay.com Aesthetic" x "Space-Indie". Trông cực kỳ sạch sẽ, hiện đại nhưng thao tác và nhận thức phải thật thân thiện, ngây ngô.

### 0.3 Biểu Tượng & Linh Vật (The Mascot)
- **Nhân vật:** Chú Cá Voi Xanh Vũ Trụ (Cosmic Blue Whale). Đại diện cho sự điềm tĩnh và "Deep Learning".
- **Concept cho AI tạo hình:** Luôn vẽ ở dạng hình khối tròn trịa (Chubby/Round), phong cách 3D Clay tối giản, tránh dùng chi tiết phức tạp (da, vây nhiều lớp) để giữ sự đồng nhất thiết kế hoàn hảo. Cụ thể các quy tắc xuất hiện UI xem tại Phần [1.5 Quy Tắc Ứng Dụng Mascot](#15-quy-tắc-ứng-dụng-mascot-cá-voi-xanh-vũ-trụ).

---

## PHẦN 1: ĐỊNH HƯỚNG THỊ GIÁC (VISUAL DIRECTION)

Phong cách thị giác của website là một **chuyến du hành nhẹ nhàng qua Dải Ngân hà của ngôn ngữ**. Tập trung vào ánh sáng, không gian thoáng đãng, lơ lửng, tạo sự thoải mái không gò bó.

### 1.1 Bảng Màu Nhận Diện & Trạng Thái
| Mã hex    | Vai trò / Yếu tố                     | Sắc thái & Ứng dụng                                                        |
| :-------- | :----------------------------------- | :------------------------------------------------------------------------- |
| `#4E56C0` | **Primary (Chính)**                  | Xanh đêm vĩnh cửu. Dùng cho Nút CTA quan trọng, Text nhấn, viền active.    |
| `#9B5DE0` | **Secondary (Phụ/Chuyển tiếp)**      | Trí tuệ & Bay bổng. Dùng cho icon, các cụm nổi bật (highlight).            |
| `#D78FEE` | **Accent (Nhấn mạnh/Hover)**         | Nhẹ nhàng. Dùng cho trạng thái hover, vùng chọn nội dung.                  |
| `#FDCFFA` | **Light Accent (Nền phụ/Khí quyển)** | Ấm áp. Dùng cho nền thanh tiến trình, nền mờ của các card con.             |
| `#F9F7FE` | **Canvas (Nền web tổng thể)**        | Trắng pha sắc tím/hồng cực nhẹ, tạo cảm giác khí quyển bồng bềnh.          |
| `#FFFFFF` | **Surface (Nền Card/Panel)**         | Thẻ nội dung, thanh điều hướng. Trắng tinh để tạo sự tách biệt với Canvas. |
| `#1A1A2E` | **Text Primary (Chữ chính)**         | Gần đen nhưng không chói tay. Đọc lâu không mỏi mắt.                       |
| `#5A5A7A` | **Text Secondary (Chữ phụ)**         | Màu xám tím cho đoạn text phụ, mô tả, breadcrumbs.                         |
| `#1C1B2E` | **Dark Floor (Nền vùng tối)**        | Chỉ xuất hiện ở footer hoặc vùng nghỉ siêu nhỏ (có overlay sao mờ).        |

### 1.2 Hệ Thống Gradient "Khí Quyển"
Tuyệt đối không dùng màu bệt nhàm chán cho các vùng rộng, sử dụng 3 công thức gradient:
- **Morning Nebula (Tinh vân ban mai):** `linear-gradient(135deg, #FDCFFA 0%, #D78FEE 50%, #9B5DE0 100%)`. Dùng cho: Vòng progress ring, Banner báo danh/chào mừng.
- **Galactic Glow (Dải ngân hà):** `linear-gradient(120deg, #4E56C0, #9B5DE0, #D78FEE)`. Dùng cho: Nút CTA siêu cỡ, viền card VIP.
- **Atmosphere Haze (Khí quyển sương mờ):** `radial-gradient(circle at 20% 30%, #FDCFFA, #F9F7FE)`. Dùng cho: Background phía sau khu vực Hero hoặc Dashboard tĩnh.

### 1.3 Ánh Sáng & Bóng (Glow thay cho Shadow)
Website KHÔNG dùng bóng đen (drop-shadow) nặng nề tạo cảm giác vật lý. Hệ thống dùng **ánh sáng phát quang (glow)** từ các thiên thể:
- **Glow nhẹ (Soft):** `box-shadow: 0 0 12px rgba(155, 93, 224, 0.15);` (Cho thẻ bài học tĩnh, avatar).
- **Glow trung bình (Normal):** `box-shadow: 0 0 20px rgba(78, 86, 192, 0.25);` (Cho nút chính, thanh tiến trình đang active).
- **Glow mạnh (Hover/Active):** `box-shadow: 0 0 32px rgba(215, 143, 238, 0.4);` (Cảm giác "chạm tay vào tinh vân").

### 1.4 Hình Khối & Bố Cục Không Gian Cụ Thể
- **Bo góc cực đại (Border-Radius):** Các phần tử từ nút bấm đến thẻ bài học phải bóp góc từ `16px` đến `32px` (hoặc bo tròn hoàn toàn `999px` dạng viên thuốc). KHÔNG DÙNG góc vuông sắc nhọn.
- **Glassmorphism ấm (Khoảng trong suốt):** Panel thông báo, Sidebar dùng `box-shadow` nhẹ kết hợp `backdrop-filter: blur(8px)`, nền trắng `rgba(255, 255, 255, 0.7)`. Xuyên thấu lớp nền sao mờ bên dưới.
- **Họa tiết (Patterns):** Background điểm xuyết các *chấm sao 1-3px* ngẫu nhiên, các vệt *quỹ đạo elip* mỏng nét 0.5px. Tuyệt đối không dùng lưới 3D phức tạp, chỉ dùng vector minimal.

### 1.5 Quy Tắc Ứng Dụng Mascot (Cá Voi Xanh Vũ Trụ)
- **Hình ảnh:** Tĩnh động (Idle animation siêu chậm). Xanh đêm, bụng phát quang `#FDCFFA`, đuôi và vây cong nhẹ.
- **Quy tắc xuất hiện:**
  - *Trang chủ (Hero):* Góc phải dưới, 120-160px.
  - *Dashboard (Menu):* Icon nhỏ nhắc nhở (48px).
  - *Popup Hoàn Thành / Khen ngợi:* Phóng to tối đa (200px - 240px) kèm hiệu ứng sao rơi. KHÔNG màn hình nào Mascot được chiếm quá 20% diện tích.
  - KHÔNG thay đổi khuôn mặt lố lăng hay giật cục.

---

## PHẦN 2: CẤU TRÚC LAYOUT VÀ IA (UX ARCHITECTURE)

**Triết lý cốt lõi (Learner-Centric Progression Architecture):** Lấy người học làm trung tâm. Giao diện tồn tại để trả lời trực tiếp 3 câu hỏi ngay tắp lự: *"Tôi đang ở đâu?", "Bước tiếp theo là gì?", và "Tiến độ của tôi đang như thế nào?"*. Mọi quyết định layout phải ưu tiên sự an toàn tâm lý thông qua các pattern có thể đoán trước.

### 2.0 Tháp Nhu Cầu UX Của Người Học (UX Maslow)
Hệ thống được xây dựng theo 5 cấp độ nhu cầu từ cơ bản đến nâng cao:
1. **Khả năng tiếp cận chức năng (Cơ bản):** Điều hướng dễ đoán, màn hình dễ đọc, thao tác tự tin.
2. **Sự gắn kết & Động lực:** Hiển thị chuỗi ngày học (Streak), Theo dõi mục tiêu ngày, Dự báo phần thưởng.
3. **Định hướng & An toàn:** Chỉ báo vị trí hiện tại, Tính minh bạch của Lộ trình, Rõ ràng trạng thái Khóa/Mở Khóa, Dễ dàng Undo/Retry.
4. **Năng lực & Trạng thái Dòng chảy (Flow):** Cấu trúc bài học rõ ràng, Mức độ thử thách phù hợp, Đặt phản hồi ngay lập tức.
5. **Thành thạo & Thành tựu (Cao nhất):** Trực quan hóa tiến độ dài hạn, Tín hiệu củng cố kỹ năng, Các trình kích hoạt Ôn tập (Review triggers).

### 2.1 Mười (10) Nguyên Tắc Kiến Trúc Bất Biến (Non-Negotiable)
1. **Neo tiến trình (Persistent Progress Anchor):** Dấu hoàn thành và tiến độ ngày phải LUÔN nằm ở Top bar hoặc góc dễ thấy, không bị giấu vào Hamburger menu.
2. **Quy tắc 1 CTA Độc Tôn (Single Primary Action):** Mỗi màn hình học và dashboard chỉ chốt hạ bằng 1 Nút Hành Động Lớn ("Tiếp tục bài", "Kiểm tra"). Nó phải lấy mọi focus Glow mạnh nhất màn hình.
3. **Quy tắc 3 Nhấp Chuột (Three-Click Max):** Học viên tới được bài học mới tối đa trong 3 cú click từ trang chủ (Dashboard > Unit > Lesson).
4. **Minh bạch Khóa (Locked Transparency):** Node/Bài học chưa tới LUÔN hiển thị RÕ điều kiện mở khóa (vd: "Đạt mốc Unit 2" hoặc ổ khóa bóng mờ).
5. **Breadcrumb & Hiện diện luồng:** Thanh điều hướng trên cùng báo hiệu rõ Level 2 > Unit 4 > Lesson 2.
6. **Không quá 2 Cột/Panel:** Trang làm bài chỉ bao gồm tối đa 2 vùng: Vùng đề bài (Nội dung) và vùng phản hồi bài làm. 3 Panel gây quá tải não bộ.
7. **Quy tắc Tỉ lệ Tiến độ (20% Rule):** Thông số Goal/Streak phải chiếm tối đa 20% khung hình cố định trên dashboard, giữ lửa động lực liên tục.
8. **Định luật đón đầu (Anticipation):** Nút Chuyển kế tiếp phải luôn để ở góc Dưới Cùng - Bên Phải.
9. **Zero Modal Interruption:** Đang làm bài KHÔNG ĐƯỢC sinh popup chúc mừng hay quảng cáo. Phản hồi nội tuyến (inline), Modal thi triển ở điểm dừng (hoàn thành Unit).
10. **Phân bổ trọng lượng Thị giác:** Flow chính (Lộ trình học) > Khu vực Bài tập trễ hạn > Công cụ (Tra từ) > Profile Settings.

### 2.2 Sơ đồ Kiến trúc Thông Tin (Information Architecture)
Hệ thống cây phân nhánh rõ ràng định hình luồng tương tác (Hierarchy Specification):

```text
ROOT
│
├── DASHBOARD (Trạm không gian)
│   ├── Tiếp tục (Continue Learning)
│   ├── Tổng quan Lộ trình (Path Overview)
│   ├── Mục tiêu ngày & Chuỗi ngày (Daily Goals & Streak)
│   └── Hàng đợi Ôn tập (Review Queue)
│
├── LỘ TRÌNH HỌC (Learning Path - Hành trình chính)
│   ├── LEVEL (Basic/Intermediate/Advanced)
│   │   ├── Unit (Chủ đề chuyên biệt)
│   │   │   ├── Bài học Từ vựng nền tảng (Vocabulary)
│   │   │   ├── Bài học Ngữ pháp quy nạp (Grammar)
│   │   │   ├── Bài luyện Nghe (Listening: Interactive/Quiz/Shadowing)
│   │   │   ├── Bài luyện Nói (Speaking: ASR/Role-play)
│   │   │   ├── Bài luyện Đọc (Reading: Comprehension/News)
│   │   │   ├── Bài luyện Viết (Writing: Basic/ZPD/AI-assessed)
│   │   │   └── Mini-test Cuối Unit
│   │   └── Unit 2 (Đợi mở khóa)...
│   └── Level Test (Bài thi cuối cấp độ)
│
├── PHÒNG THI (Exam Room)
│   ├── Mini-test / Level test
│   └── Mock test thực tế (IELTS / TOEIC Full Test)
│
├── REVIEW HUB (Trạm Ôn tập SRS)
│   ├── Đến hạn hôm nay (Tra cứu nhanh, Ôn lỗi sai)
│   └── Từ vựng yếu (Dưới 70% độ thuần thục)
│
├── KNOWLEDGE TOOLS (Công cụ tham khảo)
│   ├── Từ điển (Dictionary)
│   └── Ngữ pháp (Grammar Reference)
│
└── PROFILE & ANALYTICS (Hồ sơ & Phân tích)
    ├── Bản đồ nhiệt học tập (Mastery Heatmap)
    └── Cài đặt (Settings)
```

**Định nghĩa Phân tầng (Layer Role Definitions):**
- **Dashboard:** Định hướng & Khởi chạy (Mặc định sau đăng nhập / 0 click).
- **Learning Path:** Hành trình chính (Top nav / 1 click).
- **Level / Unit:** Nhóm cột mốc / Trạm học tuần (Path hoặc Breadcrumb / 2-3 clicks max).
- **Lesson:** Phiên học một lần ngồi (15-20 phút), màn hình tương tác chính.
- **Exercise:** Tương tác học nguyên tử (Bên trong hộp thoại Lesson / Tuần tự).
- **Review Hub:** Vùng củng cố / Gia cố trí nhớ (1 click / Thông báo liên tục).
- **Tools:** Tham khảo tức thời (Pop-up ngang hoặc Modal).

### 2.3 Phân Tích Khu Vực Bố Cục Dashboard (Dashboard Zones)
Bố cục cuộn dọc, theo thứ tự từ trên xuống dưới (độ ưu tiên giảm dần). Việc tổ chức cấu trúc này lấy cảm hứng từ Dashboard Schema chuẩn:

```text
┌─────────────────────────────────────────────────────────────┐
│  ZONE 1: TOP BAR (Persistent / Cố định)                      │
│  [Logo]  [Hành trình]  [Ôn tập]  [Công cụ]  [EXP]  [Avatar]  │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  ZONE 2: HERO ZONE (Khu vực Vàng - Quan trọng nhất)           │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  TIẾP TỤC HỌC (Hero CTA)                            │   │
│  │  "Unit 4, Bài 2: Hội thoại nhà hàng"                 │   │
│  │  [Thanh tiến độ: 3/8 bài tập đã xong]               │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                               │
│  ZONE 3: PROGRESS SNAPSHOT (Thống kê nhanh)                   │
│  ┌──────────────┐ ┌──────────────┐ ┌──────────────┐       │
│  │ Cấp độ Level │ │ Mục tiêu ngày│ │ Chuỗi ngày 🔥 │       │
│  │ B1 (45%)     │ │ 15/20 XP     │ │ 12 ngày      │       │
│  └──────────────┘ └──────────────┘ └──────────────┘       │
│                                                               │
│  ZONE 4: PATH PREVIEW (Xem trước Lộ trình)                    │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ LỘ TRÌNH CỦA BẠN (Dạng các hành tinh)    [Xem tất cả]│   │
│  │ [===HOÀN THÀNH===][===HOÀN THÀNH===][ĐANG HỌC][KHÓA]  │   │
│  │      Unit 1             Unit 2       Unit 3  Unit 4 │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                               │
│  ZONE 5: REVIEW QUEUE (Hàng đợi Ôn tập)                       │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ ĐẾN HẠN ÔN TẬP (5 Mục)                        [Bắt đầu]│   │
│  │ • "restaurant" - Quá hạn 3 ngày                     │   │
│  │ • "bill" - Đến hạn hôm nay                          │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

- **Zone 1: Top Bar (Cố định).** Dùng hiệu ứng Glassmorphism. Căn ngang trên cùng. Trả lời ngay bạn đang ở mục nào.
- **Zone 2: HERO ZONE (Khu vực Vàng).** Vị trí ngay dưới Top bar. Ôm 1 Card cực lớn chứa "TIẾP TỤC HỌC". Nút CTA dùng dải Glow `#4E56C0`. Kéo 100% sự tập trung vào việc học tiếp.
- **Zone 3: Progress Snapshot.** Đặt ngang ngay dưới Hero. Dạng 3 ô thẻ nhỏ nền trong suốt blur. Tạo động lực (Năng lượng tích cực cấp 2 của UX Maslow).
- **Zone 4: Vùng Lộ Trình (Path Preview - Nằm dọc giữa màn).** Biểu diễn dạng dọc nối tiếp. Các điểm "Node" là các tinh cầu/hành tinh có line nối mờ ảo.
- **Zone 5: Vùng Cấp bách (Review Queue - Bên phải hoặc ngang dưới).** Bảng thông báo SRS: Các từ vựng/ngữ pháp đang ở điểm chuẩn bị quên, yêu cầu vào Review khẩn cấp. Mức ưu tiên 4.

---

## PHẦN 3: TÍCH HỢP UI COMPONENT (MAPPING LAYOUT & VISUAL)

Dưới đây là công thức áp dụng định hướng thị giác (Visual) thẳng vào các thành phần tương tác (UX):

| Component hệ thống | Hướng dẫn Tổ chức Layout & Hành vi (UX) | Đặc tả Visual (UI & CSS) |
| :--- | :--- | :--- |
| **Top Navigation (Nav)** | Đính cố định đầu trang. Chứa logo trái, link giữa, thông tin Auth/Avatar góc phải. | Nền `rgba(255, 255, 255, 0.8)`, `backdrop-blur(12px)`. Có 1 light sweep (dải sáng quét qua) mỗi 15 giây. Text link màu `#5A5A7A`, active có vạch `#4E56C0` phía dưới. |
| **Nút Hành Đồng Chính (Primary CTA)** | Hình Oval hoặc Bo góc cực đại. Nằm ở trung tâm Panel hoặc Góc dưới-phải màn hình. Hành vi Click 1 lần chuyển màn. | Mã nền `#4E56C0`, chữ Trắng `#FFFFFF`. Ở trạng thái Default kèm Normal Glow (20px blur). Hover đổi glow tím siêu sáng `box-shadow: 0 0 32px rgba(...)`. |
| **Lộ Trình Học (Learning Path)** | Tổ chức như dòng chảy dọc dạng zitzac. Các ô bài học khóa thì chặn click, bật tooltip báo điều kiện mở. | Các đơn vị bài học thiết kế dạng chòm sao. Đường nối đứt đoạn mờ, nếu đã đi qua thì đường sẽ tỏa sáng (Glow). Hạt đã học sẽ sáng đậm, hạt bị khóa chỉ viền nét đứt. |
| **Card (Thẻ bài giảng tĩnh)** | Không giới hạn chiều cao nhưng tối đa 1 dòng mô tả, tối giản padding bên trong `padding: 24px`. | Nền Trắng tuyệt đối (`#FFF`) xen nền web tím mờ, bo góc 24px, viền mờ `border: 1px solid rgba(155, 93, 224, 0.1)`. Đổ Glow Soft (12px). |
| **Thanh Tiến Độ (Progress Bar)** | Nằm viền sát trên mép của mọi màn hình làm bài (Lesson Layout). Cố định độ cao nhỏ (6px-8px). | Thay vì khối đặc, dùng hiệu ứng Dải Ngân Hà rực rỡ (`Galactic Glow` Gradient). Animation load như làn sóng ánh sáng tràn dâng từ trái qua phải. |
| **Modal / Popup Chúc mừng** | Chỉ nhảy ra cuối bài, bật ra ở điểm trúng tâm màn hình (Center). Có nút tắt (X) ở góc phải trên. | Trái với thiết kế đè tối background (Background overlay thường), sử dụng nền Overlay Tím `#1C1B2E` với `opacity 50%`, bên trong pop-up bật nền Kính Mờ (Glass). Cá voi nhún nhảy chậm rải rác sao băng bay quanh modal. |
| **Vùng Footer / Cài Đặt** | Cuối cùng của màn cuộn dài. Mức độ ưu tiên rất thấp. Liệt kê link text thông thường. | Khu vực duy nhất nhuộm dark mode: Background `#1C1B2E` đậm. Cài cắm các chấm sao mờ xịt. Mắt được thư giãn nghỉ ngơi tuyệt đối khi lướt tới điểm cuối. |

**Chỉ dẫn thi công kỹ thuật:** Lập trình viên Front-End khi dựng UI bắt buộc phải viết System Design Token bám theo các mã màu quy định, thay thế `box-shadow` xám đen thành màu có alpha tử đinh hương/xanh đêm cực nhẹ. Mọi thành phần tương tác phải đảm bảo "Mượt dẻo (ease-in-out > 0.3s)", không gắt nét để giữ trọn vẹn hồn của DiveVerse.

---

## PHẦN 4: NGUỒN DỮ LIỆU MOCK CHO THIẾT KẾ UI (MOCK DATA SOURCE)

Để đảm bảo tính đồng nhất về nội dung hiển thị (copywriting), dữ liệu điểm số, thông số học bạ và các từ vựng mẫu trên toàn bộ các trang giao diện của cả phân hệ Learner App và Admin Dashboard, lập trình viên và designer bắt buộc phải sử dụng tệp dữ liệu Mock tập trung làm nguồn tham chiếu duy nhất:

*   **Tệp Mock Data chính thức:** [mock_data.json](file:///d:/Study/research_DiveVerse/project/built-ui/design/website-detail/mock_data.json)

**Các nhóm dữ liệu mẫu được quy định sẵn:**
1.  **Levels & Units:** Phân bổ lộ trình 3 cấp độ (Basic, Intermediate, Advanced) cùng cấu trúc 25/35/40 Units (mẫu Unit 1, 2, 3, 4 chi tiết).
2.  **Lessons & Exercises:** Các hoạt động giảng dạy cho 6 bài học kỹ năng bắt buộc (Từ vựng, Ngữ pháp, Nghe, Nói, Đọc, Viết) bao gồm cả các câu ví dụ ngữ cảnh của từ `collaborate` và quy luật ngữ pháp hiện tại đơn.
3.  **SRS Review Queue:** Hàng đợi ôn tập lặp lại ngắt quãng gồm 15 từ mẫu (chữ khuyết và gợi ý dịch).
4.  **Dictionary Detail:** Định nghĩa chi tiết từ điển cho từ `collaborate` (IPA, collocations, lỗi sai phổ biến).
5.  **Profile & Stats:** Học viên Nguyễn Văn A, email `nguyenvana@gmail.com`, Streak 12 ngày, tích lũy 1,250 EXP, lịch sử bài thi đã làm và Sổ tay lỗi sai tương ứng.
6.  **Tests & Mock Exams:** Cấu hình đề Mini-test cuối Unit và IELTS Mock Test (thời gian làm bài, thang điểm quy đổi).