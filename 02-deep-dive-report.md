# 02 — Deep-Dive Report: Vinpearl — Tổng Hợp & Phân Tích Review Khách Sạn

**Học viên:** Nguyễn Tiến Cường — 2A202603425 (Team Lead)  
**Nhánh Git:** `NguyenTienCuong-2A202603425`  
**Đề tài nhóm:** Vinpearl — Tổng hợp & phân tích review khách sạn đa kênh (Thống nhất toàn nhóm)  

---

## 🏛️ Bối cảnh & Mục tiêu dự án

Trong ngành dịch vụ nghỉ dưỡng cao cấp như **Vinpearl**, trải nghiệm của khách hàng và uy tín thương hiệu được phản ánh trực tiếp qua điểm số đánh giá trên các nền tảng OTA hàng đầu: **Booking.com, Agoda, Google Maps, và TripAdvisor**. Một đánh giá 1 sao chưa được giải quyết kịp thời không chỉ làm giảm điểm trung bình cơ sở mà còn có thể lan truyền trên mạng xã hội, gây tổn thất doanh thu trực tiếp.

Mục tiêu của dự án là xây dựng giải pháp **AI Co-pilot (LLM Feature)** hỗ trợ đội ngũ Chăm sóc khách hàng (Guest Relations / CSKH) và Ban Quản lý Khách sạn (General Manager) tự động quét, phân loại, đánh giá mức độ nghiêm trọng và soạn thảo phương án khắc phục cho các phàn nàn khẩn cấp ngay trong ngày.

---

## 🏗️ Phase 3 — DEEP-DIVE

### 3.1. Current-State Workflow Mapping (G1 — 20 Điểm)

Sơ đồ quy trình vận hành hiện tại (Current-State Workflow) được minh họa chi tiết tại file [04-workflow-diagram.png](04-workflow-diagram.png):

![Current-State Workflow](04-workflow-diagram.png)

#### Phân rã 5 bước trong quy trình thủ công hiện tại:

| Bước | Người thực hiện / Công cụ | Input → Output | Thời gian thao tác | Đánh giá & Rủi ro |
|---|---|---|---|---|
| **B1. Tiếp nhận review đa kênh** | Nhân viên Guest Relations / CSKH; mở lần lượt 4 portal quản trị (Booking, Agoda, Google Maps, TripAdvisor) | Review mới trên các nền tảng → Danh sách review thô trong ngày | ~25 phút/ngày | **🔄 Handoff 1:** Dữ liệu từ các nền tảng bên ngoài chuyển giao vào bộ phận CSKH nội bộ. Dễ bị sót nếu không kiểm tra liên tục. |
| **B2. Đọc & Dịch thuật đa ngôn ngữ** | Nhân viên CSKH; đọc thủ công từng review, dùng Google Dịch cho tiếng Hàn, Trung, Nga | Review thô đa ngôn ngữ → Nội dung đã hiểu nghĩa tiếng Việt | ~50 phút/ngày | **🔴 BOTTLENECK 1:** Review dài, khen chê đan xen, ngôn ngữ bản địa phức tạp khiến nhân viên mất rất nhiều thời gian đọc hiểu. |
| **B3. Phân loại chủ đề & Đánh giá mức độ nghiêm trọng** | Nhân viên CSKH; tự đánh giá theo cảm tính cá nhân và nhập vào file Excel theo dõi | Nội dung review → Nhãn chủ đề (Buồng phòng, F&B, Lễ tân, Tiện ích) & Mức ưu tiên (P1, P2, P3) | ~40 phút/ngày | **🔴 BOTTLENECK 2:** Đánh giá chủ quan; các phàn nàn nghiêm trọng (P1: phòng bẩn, mất đồ, thái độ nhân viên) dễ bị chìm giữa hàng trăm review khen ngợi thông thường. |
| **B4. Soạn báo cáo ca & Điều phối nội bộ** | Nhân viên CSKH; copy trích dẫn review, soạn email hoặc tin nhắn Zalo gửi Trưởng bộ phận phụ trách | Dữ liệu Excel → Phiếu báo cáo sự cố gửi Housekeeping/F&B/Front Office | ~30 phút/ngày | **🔄 Handoff 2:** CSKH chuyển giao thông tin cho các Trưởng bộ phận thực địa. Mất thời gian chờ phản hồi xác nhận. |
| **B5. Ban Quản lý xác minh & Xử lý khắc phục** | Trưởng bộ phận liên quan & General Manager (GM) | Báo cáo sự cố → Hành động liên hệ khách, đổi phòng, tặng voucher hoặc bảo trì | Trễ 24h – 48h | **🔄 Handoff 3:** Trao đổi giữa Trưởng bộ phận và khách lưu trú. Do phát hiện trễ, 80% trường hợp khách đã check-out về nước mới liên hệ được. |

* ⏱ **Tổng thời gian xử lý thủ công của CSKH:** Khoảng **145 phút/ngày/cơ sở** (chưa tính thời gian tổng hợp báo cáo tuần cho General Manager mất thêm ~2 giờ/tuần).
* 🔴 **Điểm nghẽn lớn nhất:** Bước B2 và B3 tốn tới 90 phút/ngày, khiến phàn nàn tiêu cực bị phát hiện trễ từ 1 đến 2 ngày, làm mất "thời điểm vàng" để xử lý sự cố trực tiếp khi khách còn lưu trú.

---

### 3.2. Problem Statement (6-Field) — Chuẩn Vin Smart Future (G2 — 20 Điểm)

| Trường thông tin (Field) | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | - **Người vận hành trực tiếp:** Nhân viên Quan hệ Khách hàng (Guest Relations Officer) / CSKH Vinpearl.<br>- **Người nhận báo cáo hành động:** Trưởng các bộ phận (Housekeeping, F&B, Lễ tân) và Giám đốc điều hành khách sạn (General Manager). |
| **2. Current Workflow** | Nhân viên CSKH mỗi sáng phải truy cập thủ công vào 4 nền tảng OTA, đọc từng đánh giá bằng nhiều thứ tiếng, tự phân loại vào file Excel, copy gửi qua Zalo/Email cho các bộ phận và định kỳ làm báo cáo tuần. Toàn bộ quy trình thủ công, rời rạc và tốn ~145 phút mỗi ngày. |
| **3. Bottleneck** | Bước đọc, dịch thuật và phân loại mức độ khẩn cấp (B2 & B3). Do lượng đánh giá lớn và văn phong phức tạp, các đánh giá tiêu cực nghiêm trọng (1-2 sao) thường bị phát hiện trễ sau 24–48 giờ, khi khách hàng đã rời khỏi khu nghỉ dưỡng. |
| **4. Business Impact** | - Khách hàng bức xúc không được giải quyết tại chỗ, để lại đánh giá tiêu cực vĩnh viễn trên OTA.<br>- Chỉ cần điểm trung bình trên Booking.com giảm 0.2 điểm (ví dụ từ 9.0 xuống 8.8), tỉ lệ chuyển đổi đặt phòng giảm ước tính 8–12%, gây thiệt hại doanh thu hàng trăm triệu đồng mỗi tháng cho mỗi cơ sở.<br>- Lãng phí ~75 giờ công làm việc/tháng của đội ngũ CSKH vào việc sao chép dữ liệu thủ công. |
| **5. Success Metric** | 1. **Thời gian phát hiện ca khẩn cấp (P1/P2):** Giảm từ 24–48 giờ xuống **dưới 15 phút** kể từ khi review xuất hiện trên hệ thống.<br>2. **Hiệu suất tổng hợp:** Giảm thời gian xử lý và lập báo cáo của nhân viên CSKH từ 145 phút xuống **dưới 35 phút/ngày** (giảm ~75%).<br>3. **Độ chính xác AI (Quality):** Đạt tỉ lệ phân loại đúng chủ đề và mức độ khẩn cấp **>= 90%** so với chuyên viên kiểm định. |
| **6. Operational Boundary (Ranh giới vận hành)** | - **AI ĐƯỢC PHÉP:** Thu thập văn bản review, dịch thuật chuẩn hóa sang tiếng Việt, trích xuất câu trích dẫn bằng chứng (quote), gắn nhãn chủ đề, chấm điểm cảm xúc (Sentiment: Positive/Neutral/Negative), phân loại mức độ khẩn cấp (P1, P2, P3), và draft bản tóm tắt ca nội bộ kèm gợi ý hướng xử lý.<br>- **AI TUYỆT ĐỐI CẤM:**<br>  + **CẤM** tự động đăng phản hồi công khai lên nền tảng Booking/Agoda/Google Maps.<br>  + **CẤM** tự động cam kết hoàn tiền, đền bù chi phí, hoặc tặng đêm nghỉ miễn phí cho khách hàng.<br>  + **BẮT BUỘC 100% HUMAN-IN-THE-LOOP:** Mọi bản tóm tắt ca và phương án xử lý bắt buộc phải có CSKH hoặc Quản lý phê duyệt trước khi chuyển giao hành động. |

---

### 3.3. Future-State Flow & AI Fit (G3 — 10 Điểm)

#### 🔹 Đánh giá Ma trận AI Fit (AI-Fit Matrix)
* **Rule-based thuần:** *Không khả thi* vì ngôn ngữ đánh giá của khách hàng phi cấu trúc, giàu cảm xúc, chứa tiếng lóng, mỉa mai (ví dụ: *"Khách sạn 5 sao mà nước nóng như mùa đông Bắc Cực"*). Bộ lọc từ khóa (Regex/Rule) sẽ bỏ sót ngữ cảnh nghiêm trọng.
* **Autonomous Agent:** *Quá rủi ro* vì nếu để Agent tự động gửi phản hồi ra các kênh truyền thông công khai hoặc tự quyết định chính sách đền bù sẽ tiềm ẩn nguy cơ khủng hoảng quan hệ công chúng (PR Crisis) và thất thoát tài chính.
* **Lựa chọn tối ưu:** **LLM Feature kết hợp Human-in-the-loop (HITL)**. LLM đóng vai trò trợ lý đọc hiểu, trích xuất dữ liệu và dự thảo (co-pilot draft), con người giữ quyền kiểm duyệt và ra quyết định cuối cùng.

#### 🔹 Sơ đồ Quy trình tương lai (Future-State Flow):

```text
┌───────────────────────┐
│ Bước 1: Ingest Data   │
│ 🔵 Rule / API tự động │
│ quét review đa kênh   │
└──────────┬────────────┘
           │
           ▼
┌────────────────────────────────────────────────────────┐
│ Bước 2: AI Processing (LLM Feature)                    │
│ 🔵 Chuẩn hóa dịch thuật sang Tiếng Việt                │
│ 🔵 Trích xuất trích dẫn bằng chứng (Evidence quotes)  │
│ 🔵 Phân loại chủ đề (Housekeeping / F&B / Front Desk)  │
│ 🔵 Phân loại mức khẩn cấp: P1 (Khẩn cấp), P2, P3      │
│ 🔵 Draft bản tóm tắt ca sự cố & đề xuất hướng giải quyết│
└──────────┬─────────────────────────────────────────────┘
           │
           ▼
┌────────────────────────────────────────────────────────┐
│ Bước 3: Human-in-the-Loop Review (HITL)               │
│ 🟢 Nhân viên CSKH / Manager xem Dashboard:            │
│    - Kiểm tra trích dẫn và nhãn phân loại              │
│    - Bấm [DUYỆT] hoặc [CHỈNH SỬA] bản nháp            │
└──────────┬─────────────────────────────────────────────┘
           │
           ├───► [Nếu AI trả về lỗi / Độ tự tin thấp < 75%]
           │     │
           │     ▼
           │  ↩️ Fallback Mechanism:
           │  Hệ thống tự động đánh dấu [CẦN_DUYỆT_THỦ_CÔNG],
           │  chuyển nguyên văn bản gốc về hàng đợi xử lý truyền thống.
           ▼
┌────────────────────────────────────────────────────────┐
│ Bước 4: Điều phối tức thì (Instant Ticket Dispatch)    │
│ 🟢 Hệ thống tự động bắn cảnh báo qua App/Zalo nội bộ   │
│    đến đúng Trưởng bộ phận để xử lý ngay cho khách!    │
└────────────────────────────────────────────────────────┘
```

---

## 🏁 Phase 5 — EVALUATE & DECISION (G4 — 10 Điểm)

### 📋 AI Readiness Checklist

| Tiêu chí sẵn sàng | Đánh giá | Bằng chứng thực tế |
|---|:---:|---|
| **1. Dữ liệu mẫu/logs sạch để kiểm thử?** | **ĐẠT (YES)** | Dữ liệu review trên Booking.com, Agoda, Google Maps của Vinpearl là dữ liệu công khai, có sẵn hàng chục nghìn mẫu với đầy đủ điểm số sao (1-5 sao) và phản hồi thực tế để làm tập benchmark. |
| **2. Rủi ro khi AI sai nằm trong tầm kiểm soát?** | **ĐẠT (YES)** | Thiết kế hệ thống áp dụng cơ chế Human-in-the-loop 100%. AI chỉ hoạt động trong môi trường nội bộ, có tiền tố nháp bắt buộc. Sai sót của AI chỉ là nhãn gợi ý, nhân viên luôn là người chốt cuối cùng. Cơ chế Fallback sẵn sàng xử lý ca khó. |
| **3. Stakeholders sẵn sàng thay đổi quy trình?** | **ĐẠT (YES)** | Khối Quản lý Khách sạn Vinpearl cực kỳ ủng hộ vì giải pháp giúp giảm tải tức thì áp lực đọc review hàng ngày cho nhân viên và giúp GM nắm bắt tình hình sự cố theo thời gian thực thay vì chờ báo cáo tuần. |

---

### 🏛️ Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:

**[ x ] GO (Bắt đầu xây dựng Prototype — Pilot với scope hẹp)**

### 💡 Justification (Lý giải quyết định):

1. **Hiệu quả kinh tế rõ ràng (ROI cao):**
   * *Chi phí:* Tận dụng Gemini 2.5 Flash với chi phí token cực thấp (~0.0001 USD/review). Với quy mô ~3.000 review/tháng cho toàn chuỗi Vinpearl, chi phí API LLM ước tính chưa đến 50 USD/tháng (~1.2 triệu VNĐ).
   * *Lợi ích:* Tiết kiệm hơn 70 giờ công làm việc/tháng của nhân viên CSKH tại mỗi khách sạn; quan trọng hơn là bảo vệ điểm số OTA, giữ chân khách hàng cao cấp và giảm thiểu rủi ro khủng hoảng truyền thông.
2. **Tính khả thi kỹ thuật vượt trội:**
   * Bài toán NLP trích xuất thực thể, phân loại chủ đề và tóm tắt văn bản ngắn là thế mạnh cốt lõi của các mô hình LLM hiện đại. Không cần fine-tune tốn kém, chỉ cần Prompt Engineering chất lượng cao kết hợp Few-shot examples là đạt độ chính xác > 90%.
3. **Kế hoạch triển khai giai đoạn Pilot:**
   * Triển khai thử nghiệm trong **4 tuần** tại duy nhất **1 cơ sở thí điểm: Vinpearl Resort & Spa Nha Trang**.
   * Chỉ xử lý review dạng văn bản bằng tiếng Việt và tiếng Anh.
   * Đánh giá hiệu quả thực tế và độ chính xác phân loại trước khi xem xét mở rộng sang các cơ sở Vinpearl khác trên toàn quốc.