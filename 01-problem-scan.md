# 01 — Problem Scan & Quick Assessments (Vin Smart Future)

**Học viên:** Nguyễn Cường — 2A202603425 (Team Lead)  
**Nhánh Git:** `NguyenCuong`  
**Đơn vị:** Vin Smart Future — Khối Đổi mới & Ứng dụng AI Vingroup  
**Chủ đề lựa chọn:** Vinpearl — Tổng hợp & phân tích review khách sạn đa kênh  

---

## 🔍 Phase 1 — SCAN: Bảng quét cơ hội vận hành Vingroup

Sử dụng **4 Lenses** (Lặp lại, Tốn thời gian, AI có thể tốt hơn, Pain từ người khác) để rà soát toàn diện các hoạt động vận hành tại các công ty thành viên Vingroup:

| # | Subsidiary | Tên bài toán / Bottleneck | Lens | Mô tả ngắn bài toán |
|---|---|---|---|---|
| 1 | **Vinpearl** | Tổng hợp & Phân tích review khách sạn đa kênh | **Pain từ người khác** | Khách hàng phàn nàn tiêu cực trên Booking.com, Agoda, Google Maps, TripAdvisor; nhân viên CSKH/Guest Relations rà soát thủ công chậm trễ, dẫn đến phản hồi muộn khi khách đã check-out và tổn hại uy tín thương hiệu. |
| 2 | **VinFast** | Trợ lý định tuyến & Hướng dẫn trạm sạc xe điện | **AI có thể tốt hơn** | Tài xế các dòng xe VF5, VF8, VF9 tìm trạm sạc thủ công; hệ thống hiện tại chưa tự động phân tích loại cổng sạc (CCS2), công suất trụ sạc khả dụng và thói quen pin để gợi ý lộ trình sạc tối ưu. |
| 3 | **Xanh SM** | Phân loại & Tóm tắt lý do hủy cuốc xe thực địa | **Tốn thời gian** | Đội ngũ điều phối viên phải nghe lại hàng trăm đoạn ghi âm cuộc gọi hủy chuyến và đọc ghi chú vắn tắt của tài xế mỗi ngày để tìm pattern lỗi hệ thống hoặc xung đột điểm đón. |
| 4 | **Vinhomes** | Phân loại & Điều phối phản ánh cư dân trên App | **Lặp lại** | Hàng ngày có hàng nghìn phản ánh (mất nước, vệ sinh, phí quản lý, thẻ cư dân) gửi về ban quản lý tòa nhà; nhân viên phải đọc và phân loại thủ công vào các phòng ban liên quan. |
| 5 | **Vinmec** | Soạn thảo tóm tắt bệnh án xuất viện (Discharge Summary) | **Tốn thời gian** | Bác sĩ mất 20–30 phút cho mỗi bệnh nhân để tổng hợp lịch sử lâm sàng, kết quả xét nghiệm thành văn bản tóm tắt xuất viện dễ hiểu cho bệnh nhân và người nhà. |

---

## 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Chọn **top 3 bài toán** tiềm năng nhất từ danh sách trên để lập thẻ đánh giá nhanh:

---

### 🎴 QUICK PROBLEM CARD #1 (Lựa chọn chính của nhóm)

```text
┌─────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                   │
│                                                                         │
│ Bài toán (1 câu): Nhân viên CSKH Vinpearl mất quá nhiều thời gian rà    │
│ soát thủ công review từ Booking/Agoda/Google Maps, làm chậm trễ phát    │
│ hiện phàn nàn khẩn cấp và rò rỉ điểm đánh giá cơ sở nghỉ dưỡng.         │
│ Công ty thành viên: [x] Vinpearl / VinWonders                           │
│                                                                         │
│ Ai đang đau (Actor)?                                                    │
│ - Nhân viên Guest Relations / CSKH (quá tải đọc hàng trăm review/ngày)   │
│ - Quản lý vận hành khách sạn (General Manager - thiếu thông tin kịp thời)│
│ - Khách lưu trú (bức xúc không được xử lý ngay tại chỗ)                 │
│                                                                         │
│ Workflow thủ công hiện tại (5 bước):                                    │
│   1. Mở lần lượt các trang quản trị (Booking, Agoda, Google Maps, Trip) │
│   → 2. Đọc từng review, ghi nhận ngôn ngữ (Anh/Việt/Hàn/Trung)          │
│   → 3. Tự phân loại chủ đề (Buồng phòng, F&B, Lễ tân, Tiện ích)        │
│   → 4. Copy các phản ánh nghiêm trọng vào file Excel / nhóm chat Zalo   │
│   → 5. Soạn email báo cáo tổng hợp gửi Trưởng bộ phận và General Manager│
│                                                                         │
│ Bước nào tốn thời gian/lỗi nhất?                                         │
│ Bước 2 & 3: Đọc và phân loại review đa nguồn, đa ngôn ngữ (~15-20 min/lượt)│
│                                                                         │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                   │
│ Bước 2, 3 & 5: Dùng LLM tự động trích xuất ý chính, gắn nhãn cảm xúc    │
│ (Sentiment), phân loại mức độ khẩn cấp (P1-P3) và draft bản tóm tắt ca. │
│                                                                         │
│ Đo thành công bằng gì (Metric có số)?                                    │
│ 1. Giảm thời gian phát hiện phàn nàn khẩn cấp từ 24–48h xuống < 15 phút.│
│ 2. Giảm 75% thời gian tổng hợp báo cáo review hàng ngày (60p -> 15p).   │
│ 3. Đạt độ chính xác gắn nhãn chủ đề và mức độ khẩn cấp >= 92%.          │
│                                                                         │
│ Quick Architecture: [x] LLM Feature (Kết hợp Rule trích xuất + HITL)   │
└─────────────────────────────────────────────────────────────────────────┘
```

---

### 🎴 QUICK PROBLEM CARD #2

```text
┌─────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                                   │
│                                                                         │
│ Bài toán (1 câu): Khách hàng lái xe điện VinFast gặp khó khăn khi chọn   │
│ trạm sạc phù hợp còn trống trụ và tối ưu với lộ trình di chuyển xa.     │
│ Công ty thành viên: [x] VinFast                                         │
│                                                                         │
│ Ai đang đau (Actor)?                                                    │
│ Khách hàng sử dụng ô tô điện VinFast (lo ngại cạn pin - range anxiety)  │
│                                                                         │
│ Workflow thủ công hiện tại (4 bước):                                    │
│   1. Khách hàng mở ứng dụng VinFast kiểm tra bản đồ trạm sạc             │
│   → 2. Tự tính toán dung lượng pin còn lại với quãng đường cần đi       │
│   → 3. So khớp loại cổng sạc (sạc thường AC hay sạc siêu nhanh DC)      │
│   → 4. Chọn trạm và điều hướng qua Google Maps bên ngoài                │
│                                                                         │
│ Bước nào tốn thời gian/lỗi nhất?                                         │
│ Bước 2 & 3: Khách hàng phải tự ước tính tiêu hao pin và kiểm tra loại trụ│
│                                                                         │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                   │
│ Tự động dự đoán mức tiêu thụ pin dựa trên địa hình, tải trọng, thời tiết│
│ và gợi ý lịch sạc tối ưu trực tiếp trên màn hình trung tâm xe.          │
│                                                                         │
│ Đo thành công bằng gì (Metric có số)?                                    │
│ Tăng tỉ lệ đến trạm sạc đúng lúc pin > 10% đạt 99%; giảm 20% thời gian   │
│ chờ đợi tại trạm sạc nhờ phân bổ tải thông minh.                        │
│                                                                         │
│ Quick Architecture: [x] Rule / Optimization Engine + LLM Co-pilot       │
└─────────────────────────────────────────────────────────────────────────┘
```

---

### 🎴 QUICK PROBLEM CARD #3

```text
┌─────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                   │
│                                                                         │
│ Bài toán (1 câu): Điều phối viên Xanh SM mất nhiều thời gian rà soát     │
│ nguyên nhân hủy chuyến của tài xế và khách hàng để xử lý khiếu nại.     │
│ Công ty thành viên: [x] Xanh SM (GSM)                                   │
│                                                                         │
│ Ai đang đau (Actor)?                                                    │
│ Điều phối viên trung tâm điều vận và Quản lý chất lượng dịch vụ Xanh SM │
│                                                                         │
│ Workflow thủ công hiện tại (4 bước):                                    │
│   1. Hệ thống ghi nhận cuốc xe bị hủy                                   │
│   → 2. Điều phối viên mở file ghi âm cuộc gọi hoặc đọc lý do vắn tắt    │
│   → 3. Đánh giá tính xác thực của lý do (lỗi khách, lỗi tài xế, lỗi app)│
│   → 4. Nhập mã phân loại khiếu nại và chuyển bộ phận hoàn tiền/phạt     │
│                                                                         │
│ Bước nào tốn thời gian/lỗi nhất?                                         │
│ Bước 2 & 3: Nghe ghi âm và phân tích ngữ cảnh hủy cuốc (5-7 min/ca)     │
│                                                                         │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                   │
│ Tự động Speech-to-Text cuộc gọi ghi âm và dùng LLM tóm tắt lý do cốt lõi │
│                                                                         │
│ Đo thành công bằng gì (Metric có số)?                                    │
│ Giảm thời gian xử lý khiếu nại hủy cuốc từ 10 phút xuống dưới 2 phút;    │
│ độ chính xác phân loại nguyên nhân đạt >= 90%.                          │
│                                                                         │
│ Quick Architecture: [x] LLM Feature (Speech-to-Text + LLM Classifier)   │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 🗳️ Quyết định lựa chọn của Nhóm & Lý do

Toàn thể nhóm đã họp bàn và **thống nhất 100% lựa chọn Quick Problem Card #1 (Vinpearl — Tổng hợp & phân tích review khách sạn)** để thực hiện Deep-Dive.

### Lý do lựa chọn Card #1:
1. **Giá trị kinh doanh trực diện (Business Impact cao):** Ngành khách sạn/nghỉ dưỡng phụ thuộc sống còn vào điểm số đánh giá trực tuyến (OTA Score trên Booking, Agoda, Google Maps). Việc phát hiện sớm phàn nàn giúp xử lý kịp thời ngay khi khách còn đang lưu trú, ngăn chặn khủng hoảng truyền thông và giữ vững hình ảnh cao cấp của Vinpearl.
2. **Độ phù hợp của AI (AI Fit hoàn hảo):** Đánh giá của khách hàng là dữ liệu văn bản phi cấu trúc, đa ngôn ngữ (Việt, Anh, Hàn, Trung, Nga), chứa nhiều sắc thái cảm xúc, châm biếm, khen chê đan xen. Các bộ lọc từ khóa thông thường (Rule-based) hoàn toàn thất bại trong ngữ cảnh này, trong khi LLM giải quyết cực kỳ xuất sắc.
3. **Tính khả thi và rủi ro có kiểm soát:** Đây là bài toán nội bộ hỗ trợ quyết định (Internal Co-pilot), có con người kiểm duyệt (Human-in-the-loop) trước khi đưa ra hành động khắc phục, không can thiệp trực tiếp vào an toàn vận hành vật lý như xe điện hay y tế.

### Lý do loại bỏ các Card khác:
* **Card #2 (VinFast Sạc xe):** Đòi hỏi tích hợp sâu vào hệ thống phần cứng xe, telemetry thời gian thực và mạng lưới IoT của trạm sạc VinFast. Độ phức tạp hạ tầng vượt quá phạm vi triển khai nhanh trong giai đoạn scoping này.
* **Card #3 (Xanh SM Hủy chuyến):** Đây là tác vụ phân tích dữ liệu hồi cứu (post-mortem analysis), mang tính báo cáo chất lượng định kỳ chứ không tạo ra tác động cứu vãn tức thì cho trải nghiệm khách hàng như bài toán của Vinpearl.

