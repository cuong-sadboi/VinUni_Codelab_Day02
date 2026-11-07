# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)
**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước gây tắc nghẽn, tốn thời gian, hoặc sai sót nhiều nhất.
* 🔄 **Handoff:** Điểm chuyển giao thông tin giữa người và hệ thống, hoặc giữa các bộ phận.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = ____ phút/lượt**.

[1] Mở các nền tảng        [2] Đọc từng review        [3] Đánh giá mức độ
Booking / Agoda /    🔄    trên từng kênh        🔄   nghiêm trọng & phân loại
Google Map                 (~8 phút)                  chủ đề (~4 phút)
(~3 phút)                  🔴 BOTTLENECK               🔴 BOTTLENECK
                                                            │
                                                            🔄
                                                            ▼
                                       [4] Copy review quan trọng, soạn
                                       báo cáo, gửi Manager 
                                       (~3 phút)
Tổng cộng = ~18 phút/lượt rà review.


## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Nhân viên Guest Relations / CSKH của khách sạn Vinpearl (người rà review hằng ngày). Người nhận kết quả: Quản lý khách sạn (General Manager) |
| **2. Current Workflow** | MNhân viên mở lần lượt Booking.com, Agoda, Google Map, đọc từng review, tự đánh giá mức độ nghiêm trọng, rồi copy và gửi báo cáo cho Manager. |
| **3. Bottleneck** | Bước 2 và 3: đọc thủ công review đa nguồn, đa ngôn ngữ và tự phân loại mức khẩn cấp. Một phàn nàn nghiêm trọng (ví dụ “phòng bẩn”, “nhân viên thái độ tệ”, “mất đồ”) dễ bị chìm giữa hàng chục review bình thường. |
| **4. Business Impact** | 18 phút/lượt rà review, lặp lại nhiều lần mỗi ngày hoặc mỗi tuần. Tổn thất chính không nằm ở thời gian mà ở độ trễ và sót: phàn nàn nghiêm trọng bị chìm giữa review bình thường, phát hiện chậm hàng giờ đến hàng ngày, review tiêu cực lan rộng trước khi khách được xử lý. Ảnh hưởng điểm đánh giá trên OTA, tỉ lệ đặt phòng và uy tín Vinpearl. |
| **5. Success Metric** | Thời gian rà review: 18 phút → dưới 3 phút/lượt (chỉ còn bước duyệt).
• Phàn nàn khẩn cấp gửi alert cho Manager trong < 1 giờ kể từ khi review xuất hiện.
• Recall phát hiện phàn nàn nghiêm trọng ≥ 95%, precision ≥ 80%.
• Độ chính xác phân loại chủ đề ≥ 85%. |
| **6. Operational Boundary** | AI được làm: thu thập review từ nguồn được phép, dịch, phân loại chủ đề, chấm mức khẩn cấp, tóm tắt, soạn bản nháp alert.
AI TUYỆT ĐỐI không: tự đăng phản hồi công khai cho khách; tự hứa bồi thường hay hoàn tiền; xóa/ẩn review; đưa ra kết luận kỷ luật nhân viên.
Cần duyệt (HITL): mọi alert mức “Khẩn cấp” và mọi bản nháp phản hồi khách phải có người xác nhận trước khi gửi/đăng. |

## 3.3. Future-State Flow & AI Fit (25 min)
* **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [ ] Rule / State-Machine [x] LLM Feature [ ] Agentic Loop.
* **Vẽ Future-State Flow:** Đánh dấu rõ:
  * 🔵 **AI Step:** Tác vụ LLM xử lý.
  * 🟢 **Human Step (HITL):** Bước con người phê duyệt/review (Human-in-the-loop).
  * ↩️ **Fallback:** Kế hoạch dự phòng khi LLM trả về kết quả lỗi hoặc không tự tin.

 [Review mới từ Booking/Agoda/Google Map]
                 │
                 ▼
 🔵 AI 1: Gom review về một nơi, dịch sang tiếng Việt
                 │
                 ▼
 🔵 AI 2: Phân loại chủ đề + chấm mức khẩn cấp
          (Thấp / Trung bình / Khẩn cấp) + độ tin cậy
                 │
        ┌────────┴─────────────┐
        │                      │
  Độ tin cậy cao          Độ tin cậy thấp / lỗi LLM
        │                      │
        │                      ▼
        │               ↩️ FALLBACK: đẩy vào hàng chờ
        │               "cần người xem", gắn cờ mặc định
        │               "Trung bình"; nếu LLM lỗi thì
        │               quay về rule từ khóa (vd: "bẩn",
        │               "mất", "tệ") + thông báo nhân viên
        ▼                      │
 🟢 HITL 1: Nhân viên Guest Relations xem nhanh danh sách,
            xác nhận/sửa nhãn (~3-5 phút)
                 │
                 ▼
 🔵 AI 3: Tóm tắt thành báo cáo ngắn + soạn alert cho
          các case Khẩn cấp
                 │
                 ▼
 🟢 HITL 2: Manager nhận alert, quyết định xử lý
            (liên hệ khách, xử lý nội bộ)
                 │
                 ▼
 Lưu nhãn đã duyệt → dùng làm dữ liệu đánh giá/cải thiện AI
---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [x] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?
Có. Review công khai trên Booking.com, Agoda, Google Map có thể dùng làm tập test. Cần nhờ nhân viên Guest Relations gán nhãn tay khoảng 100-200 review (chủ đề + mức khẩn cấp) để làm ground truth đo baseline.
2. [x] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?
Có. AI chỉ phân loại, tóm tắt và soạn nháp alert, không tự đăng phản hồi hay hành động ra bên ngoài. Mọi alert mức “Khẩn cấp” đều qua người duyệt (HITL). Khi độ tin cậy thấp hoặc LLM lỗi, hệ thống chuyển sang hàng chờ cho người xem và dùng rule từ khóa dự phòng (Fallback).
3. [x] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?
Khả năng chấp nhận cao vì thay đổi nhỏ: nhân viên vẫn nhận kết quả qua mail/Zalo như hiện tại, chỉ thay phần đọc và phân loại thủ công bằng bước duyệt nhanh (~2 phút). (Cần xác nhận cam kết với Manager và Guest Relations trước khi bắt đầu prototype.)

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[x] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> *Viết lý giải chi tiết tại đây*
Quyết định: GO với scope hẹp. Prototype chỉ áp dụng cho 1 khách sạn Vinpearl và 1-2 kênh review, gồm phân loại chủ đề, chấm mức khẩn cấp và soạn alert cho Manager. Chưa bao gồm tự động phản hồi khách.

Bằng chứng kỹ thuật: Review là văn bản tự do, đa ngôn ngữ, nhiều sắc thái (mỉa mai, ẩn ý) nên rule/từ khóa không đủ, đây đúng là thế mạnh của LLM. Quy trình là chuỗi cố định (thu thập → phân loại → báo cáo) nên chỉ cần LLM Feature, không cần Agentic Loop. Rủi ro nằm trong tầm kiểm soát nhờ HITL và Fallback. Chất lượng đo được khách quan bằng cách so sánh với nhãn của nhân viên: recall phát hiện phàn nàn nghiêm trọng ≥ 95%, precision ≥ 80%, độ chính xác phân loại chủ đề ≥ 85%.

Chi phí/lợi ích: Thời gian rà review giảm từ ~18 phút xuống dưới 3 phút/lượt, tiết kiệm ~15 phút mỗi lượt. Với một khách sạn đơn lẻ, con số này khiêm tốn, nên giá trị chính nằm ở: (1) rút ngắn thời gian phát hiện phàn nàn nghiêm trọng xuống dưới 1 giờ, (2) không bỏ sót case khẩn cấp, bảo vệ điểm đánh giá trên OTA và tỉ lệ đặt phòng, (3) khả năng nhân rộng: cùng một giải pháp áp dụng cho nhiều khách sạn/resort Vinpearl thì thời gian tiết kiệm nhân lên theo số cơ sở. Chi phí gọi LLM thấp vì khối lượng review nhỏ đến vừa.

Điều kiện đi kèm: (1) Xác nhận cách lấy dữ liệu hợp lệ (API, đối tác hoặc export), tránh vi phạm điều khoản của Booking/Agoda. (2) Có tập nhãn mẫu 100-200 review để đo baseline trước khi mở rộng. (3) Manager cam kết sử dụng alert trong quy trình. Nếu chưa lấy được dữ liệu hợp lệ, chuyển quyết định sang NOT YET.

---