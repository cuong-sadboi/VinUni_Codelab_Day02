🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 |**Vinpearl** | Tổng hợp & Phân tích review khách sạn | Pain từ người khác | Quét qua các review trên Booking.com, Agoda, Google Map của Vinpearl để lọc ra các phàn nàn khẩn cấp (ví dụ: *"phòng bẩn"*, *"nhân viên thái độ tệ"*) gửi về Manager. |
| 2 |**Vinpearl**| Tự động hóa xếp ca & điều phối nhân sự| Tốn thời gian|Tự động lập bảng phân ca làm việc cho nhân viên buồng phòng, nhà hàng dựa trên công suất phòng dự báo thay vì xếp lịch thủ công trên Excel hàng tuần|
| 3 |**Vinpearl** | Trích xuất & Nhập liệu hóa đơn nhà cung cấp F&B| Lặp lại | Dùng OCR + LLM tự động đọc, đối chiếu và nhập dữ liệu từ hàng trăm hóa đơn, phiếu giao hàng nguyên vật liệu vào hệ thống ERP mỗi ngày.
| 4 |**VinFast** | Trợ lý hướng dẫn trạm sạc thông minh | AI có thể tốt hơn | Tự động đề xuất lịch trình sạc tối ưu và trạm sạc trống phù hợp với loại cổng sạc (CCS2/GBT) của từng dòng xe điện (VF5, VF8, VF9). |
| 5 |**Xanh SM** | Phân tích lý do hủy chuyến của khách hàng | Pain từ người khác | Tự động nghe ghi âm cuộc gọi hủy chuyến và ghi chú của tài xế để phân loại 10 lý do phổ biến nhất gây rò rỉ cuốc. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu):  Tổng hợp & Phân tích review khách sạn    │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [x] Khác Vinpearl          │
│                                                             │
│ Ai đang đau (Actor)? Quản lý khách sạn                      |
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Mở Booking/Agoda/Google Map ──> 2. Đọc từng review 
      ──> 3. Tự đánh giá mức độ nghiêm trọng ──> 
      4. Gửi báo cáo cho Manager                              │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? 2 (⏱ 15-20 phút/lượt)      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3 (phân loại   │
│ chủ đề, chấm mức khẩn cấp) và bước 4 (tóm tắt, gửi báo cáo) │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? Giảm thời gian rà 
  review từ 15-20 min → under 5 min/lượt;thời gian phát hiện 
  phàn nàn nghiêm trọng < 1 giờ                               │
│   VD: "Giảm thời gian soạn phản hồi từ 10 min ──> under 2 min"│
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                     │
│                                                             │
│ Bài toán (1 câu): Trợ lý hướng dẫn trạm sạc thông minh  │
│ Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Chủ xe VinFast                         │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│    1. Mở app tìm trạm → 2. Tự kiểm tra loại cổng sạc phù hợp  │
│  → 3. Đến nơi mới biết trạm bận/hỏng → 4. Chờ hoặc đi trạm  │
│  khác                                                       │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? 3-4 (⏱ 30 phút - 1 tiếng/lượt)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 1-3 gợi ý trạm  │
│ theo dòng xe, mức pin, lộ trình, dự đoán trạm trống, hỏng    │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? Giảm thời gian tìm trạm sạc
trung bình xuống dưới 15 phút, giảm tỉ lệ gặp trạm hỏng, nhầm trạm 
xuống 10%                                                     │
│   VD: "Giảm thời gian soạn phản hồi từ 10 min ──> under 2 min"│
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [ ] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                     │
│                                                             │
│ Bài toán (1 câu): Tự động hóa xếp ca & điều phối nhân sự  │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [x] Khác (Ghi rõ)Vinpearl  │
│                                                             │
│ Ai đang đau (Actor)? Trưởng bộ phận Housekeeping            │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│  1. Lấy dữ liệu công suất phòng (occupancy) từ PMS          │
│  → 2. Ước tính thủ công số lượng nhân sự cần thiết theo kinh  │
│  nghiệm → 3. Xếp ca thủ công trên Excel                     │
│  → 4. Điều chỉnh gấp khi có thay đổi lịch check-in/check-out │
│  → 5. Phát sinh chi phí làm thêm giờ (overtime) do lệch tải
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? 3-5 (⏱ 2-3giờ/tuần)      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3 
  (Sử dụng AI Machine Learning dự báo tải trọng thực │
│ tế kết hợp thuật toán Tối ưu hóa Operations Research/OR-    │
│ Tools để tự động giải bài toán xếp ca thỏa mãn ràng buộc)
│                                                             │
│ Đo thành công bằng gì (Metric có số)? 
- Giảm 12% - 15% tổng chi phí nhân công tính trên mỗi phòng  │
│   có khách (Labor Cost per Occupied Room - CPOR).           │
│ - Kiểm soát tỷ lệ giờ làm thêm (Overtime) xuống dưới 3%.     │
│ - Giảm 100% thời gian xếp ca thủ công hàng tuần xuống       │
│   dưới 15 phút chạy hệ thống.
│   VD: "Giảm thời gian soạn phản hồi từ 10 min ──> under 2 min"│
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [ ] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*