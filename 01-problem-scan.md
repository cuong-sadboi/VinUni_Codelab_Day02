# 01 — Problem Scan & Quick Problem Cards

**Chủ đề:** Vinpearl — Tổng hợp & Phân tích review khách sạn.  
**Bối cảnh bài lab:** Em đóng vai AI Product Engineer tại Vin Smart Future để tìm và xác định phạm vi một bài toán vận hành.

> **Cơ sở phân tích:** Bài làm dựa trên tình huống của worksheet và inspiration kit. Quy trình, công cụ và thời gian là giả định phục vụ bài lab, chưa được Vinpearl xác nhận. Các mục tiêu dưới đây là đề xuất để thử nghiệm, chưa phải kết quả đã đạt.

## Phase 1 — SCAN: Quét cơ hội bằng bốn lenses

| #   | Công ty thành viên | Lens               | Actor và bài toán cụ thể                                                                                                                 |
| --- | ------------------ | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Vinpearl           | Pain từ người khác | Nhân viên CSKH phải đọc review từ nhiều nguồn để phát hiện phản ánh cần ưu tiên; quản lý có thể nhận thông tin muộn hoặc thiếu ngữ cảnh. |
| 2   | Vinpearl           | Tốn thời gian      | Nhân viên quản lý chất lượng phải gắn chủ đề, đếm và viết báo cáo phàn nàn hàng tuần bằng bảng tính.                                     |
| 3   | Vinpearl           | AI có thể tốt hơn  | Nhân viên CSKH phải soạn phản hồi phù hợp từng review tiếng Việt/tiếng Anh; mẫu trả lời chung khó phản ánh đúng vấn đề khách nêu.        |
| 4   | Vinhomes           | Lặp lại            | Nhân viên ban quản lý phải đọc và chuyển phản ánh cư dân đến đúng tòa nhà, bộ phận kỹ thuật hoặc vệ sinh.                                |
| 5   | Xanh SM            | Pain từ người khác | Nhân viên vận hành phải tổng hợp lý do hủy chuyến từ ghi chú tự do để phát hiện các vấn đề khách và tài xế thường gặp.                   |

Em chọn ba bài toán Vinpearl (#1–#3) để lập Quick Problem Cards. Chúng có cùng nguồn dữ liệu dự kiến nhưng khác đầu ra: **ca cần xử lý**, **báo cáo xu hướng** và **bản nháp phản hồi**.

## Phase 2 — QUICK-ASSESS: Ba Quick Problem Cards

### Card 1 — Phân loại, tóm tắt và chuyển review cần xử lý

- **Bài toán một câu:** Nhân viên cần phát hiện review có phản ánh đáng chú ý, tóm tắt đúng nội dung và chuyển đến đúng người phụ trách.
- **Công ty thành viên:** Vinpearl.
- **Actor:** nhân viên CSKH/quản lý chất lượng trực tiếp đọc review; quản lý khách sạn tiếp nhận ca; khách hàng chịu ảnh hưởng nếu phản ánh bị bỏ sót.
- **Workflow hiện tại — cùng cách đánh số với báo cáo và sơ đồ:** B1 ghi nhận review → B2 đọc và phân loại → B3 tóm tắt, ghi ca → B4 gửi và chờ người phụ trách nhận → B5 xác minh sơ bộ, cập nhật hướng xử lý.
- **Thời gian giả định:** B1 2 phút; B2 4 phút; B3 3 phút; B4 1 phút gửi + 9 phút chờ; B5 15 phút xác minh sơ bộ. Từ bắt đầu B1 đến nhận ca là **19 phút**; đến hết B5 là **34 phút** cho một ca đi hết luồng.
- **Bottleneck:** B2–B3 chiếm **7 phút công/review**, cần hiểu nội dung và ghi lại bằng chứng; B4 có thêm 9 phút chờ ở điểm chuyển giao.
- **AI hỗ trợ tại B2–B3:** đề xuất chủ đề, mức ưu tiên, tóm tắt có trích dẫn và người nhận. Nhân viên duyệt trước khi gửi; báo cáo trong ngày chỉ tổng hợp các ca đã duyệt.
- **Metric đề xuất:** thời gian đọc, ghi ca và duyệt trung vị **≤2 phút/review**; recall review ưu tiên cao **≥95%**; precision cảnh báo ưu tiên cao **≥80%**; **100%** ca được con người duyệt trước khi chuyển. Định nghĩa và cách đo nằm trong báo cáo phân tích sâu.
- **Quick Architecture:** **LLM Feature**, kết hợp rule kiểm tra đầu vào, đếm số liệu và định tuyến sau khi người phụ trách duyệt.

### Card 2 — Tổng hợp chủ đề phản ánh hàng tuần

- **Bài toán một câu:** Nhân viên cần tổng hợp các chủ đề phàn nàn theo kỳ để quản lý biết vấn đề nào xuất hiện nhiều.
- **Công ty thành viên:** Vinpearl.
- **Actor:** nhân viên quản lý chất lượng và quản lý khách sạn.
- **Workflow hiện tại:** (1) xuất review → (2) kiểm tra trùng → (3) gắn chủ đề → (4) đếm theo kỳ → (5) viết và rà soát báo cáo.
- **Bottleneck:** bước 3–5; giả định **90 phút/báo cáo tuần** cho một cơ sở, phải đo lại với số review thực tế.
- **AI hỗ trợ:** gợi ý chủ đề và viết tóm tắt từ tập review được duyệt. Công cụ bảng tính thực hiện phép đếm; mỗi nhận định phải dẫn tới review nguồn.
- **Metric đề xuất:** ≥90% review có chủ đề chính khớp nhãn người đánh giá; giảm ≥30% thời gian lập báo cáo so với baseline đo được; 100% số đếm khớp dữ liệu nguồn đã loại trùng.
- **Quick Architecture:** **Rule + LLM Feature**; không cần agent tự hành động.

### Card 3 — Soạn nháp phản hồi công khai

- **Bài toán một câu:** Nhân viên cần bản nháp phản hồi đúng nội dung, ngôn ngữ và chính sách đã được duyệt.
- **Công ty thành viên:** Vinpearl.
- **Actor:** nhân viên CSKH soạn trả lời; quản lý phê duyệt nội dung nhạy cảm.
- **Workflow hiện tại:** (1) đọc review → (2) tra thông tin vụ việc và chính sách → (3) viết phản hồi → (4) duyệt → (5) đăng.
- **Bottleneck:** bước 2–3, giả định **6 phút/review**; cần đo riêng thời gian tra cứu và soạn thảo.
- **AI hỗ trợ:** soạn bản nháp ở bước 3 từ review, thông tin xác minh và chính sách được cung cấp. Thiếu thông tin thì đề nghị nhân viên bổ sung.
- **Metric đề xuất:** ≥90% bản nháp đạt checklist nội dung ngay lượt đầu; 100% phản hồi được người có thẩm quyền duyệt trước khi đăng; không có cam kết bồi thường thiếu căn cứ trong nội dung được duyệt. Tỷ lệ đạt lần đầu không thay thế kiểm tra ranh giới.
- **Quick Architecture:** **LLM Feature + Human-in-the-loop**; người phụ trách tự đăng phản hồi.

## Lựa chọn phân tích sâu

Em chọn **Card 1** làm phạm vi đầu tiên của chủ đề “Tổng hợp & Phân tích review khách sạn”. Đầu ra là danh sách review đã phân loại, tóm tắt từng ca và bản tổng hợp nội bộ cho quản lý. Đây là chuỗi công việc có thể đối chiếu từng kết quả với review gốc và đo cả chất lượng lẫn thời gian.

**Card 2** được để lại cho giai đoạn sau vì phân tích xu hướng tuần cần dữ liệu đủ dài và nhãn ổn định. Bản tổng hợp danh sách ca trong ngày của Card 1 chưa suy diễn xu hướng hay nguyên nhân gốc rễ. **Card 3** được để lại vì nội dung đăng công khai cần thông tin vụ việc đã xác minh và quy tắc phê duyệt chặt chẽ hơn.

Phạm vi thử nghiệm đề xuất là **một cơ sở, review tiếng Việt/tiếng Anh và dữ liệu xuất được phép sử dụng**. Em chưa giả định có quyền truy cập trực tiếp Booking.com, Agoda hoặc Google Maps. Quyết định về độ sẵn sàng được trình bày tại `02-deep-dive-report.md`.
