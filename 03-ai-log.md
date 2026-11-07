1. AI giúp gì?
Chuyển 5 bài toán thành 5 Quick Problem Card hoàn chỉnh và gợi ý chọn top 3.
Dựng khung Phase 3: workflow hiện tại (🔴 Bottleneck, 🔄 Handoff), Problem Statement 6 trường, future-state flow (🔵 AI, 🟢 HITL, ↩️ Fallback).
Soạn Phase 5: checklist, quyết định GO và Justification; nhắc rủi ro về điều khoản thu thập dữ liệu của Booking/Agoda.
2. AI sai / hallucination ở đâu?
Số liệu tự bịa: AI tự điền các con số (60-90 phút, lỗi 3% → 0.5%, 12% → 3%...) không có nguồn thực tế.
Ước lượng lệch: AI ghi review tốn ~60 phút/lượt, thực tế chỉ khoảng 15-20 phút.
Sai Actor bài #5: AI chọn đội vận hành, trong khi người chịu đau thật sự là tài xế Xanh SM.
Checklist quá lạc quan: AI tick "sẵn sàng" cho các mục chưa có bằng chứng (stakeholder đồng ý, quyền truy cập dữ liệu).
3. Tôi đã sửa prompt / đặt ranh giới thế nào?
Yêu cầu AI ghi rõ đâu là ước tính, và thay bằng số thực tế của mình.
Cung cấp dữ kiện thật (15-20 phút) và yêu cầu cập nhật đồng bộ mọi phần liên quan (Card, Workflow, Metric, Justification).
Chốt đơn vị: chỉ tính thời gian cho 1 lượt, không theo tuần/tháng.
Bổ sung góc nhìn đề bài (lens "Pain từ người khác") để AI sửa đúng Actor.
Đặt ranh giới: AI chỉ soạn và đề xuất; các mục chưa có bằng chứng do tôi xác nhận. Quyết định GO kèm điều kiện, nếu chưa có dữ liệu hợp lệ thì chuyển NOT YET.
4. Bài học

AI mạnh về dựng cấu trúc và viết nhanh nhưng không biết thực tế đơn vị, nên dễ lấp chỗ trống bằng thông tin nghe hợp lý. Lần sau tôi sẽ đưa dữ kiện thật ngay từ prompt đầu và luôn kiểm chứng số liệu, Actor trước khi dùng.