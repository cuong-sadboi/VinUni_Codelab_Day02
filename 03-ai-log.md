# 03 — AI Log & Reflection (Nhật Ký Tương Tác AI)

**Học viên:** Nguyễn Cường — 2A202603425 
**Nhánh Git:** `NguyenCuong`  
**Công cụ AI:** Google Gemini / Claude — đóng vai trò Trợ lý tư duy (Thought-Partner).
**Chủ đề bài toán nhóm:** Vinpearl — Tổng hợp & phân tích review khách sạn đa kênh.  

---

## 1. Đọc yêu cầu, phân tích đề bài & Lập kế hoạch nhóm (Team Lead Perspective)

### 🤖 AI đã giúp gì:
- Đọc và tóm tắt toàn bộ tài liệu dự án (`README.md`, `01-worksheet.md`, `02-deliverable-example.md`, `autograder/autograder.py`).
- Phân tích và chỉ rõ cấu trúc chấm điểm hai tầng:
  + **Điểm cá nhân (40 điểm):** Đánh giá trên nhánh cá nhân `NguyenCuong` (gồm 3 file `.md`, 1 ảnh diagram và file code `.py` qua autograder).
  + **Điểm nhóm (60 điểm):** Đánh giá trên nhánh `main` sau khi tổng hợp các bản xuất sắc nhất.
- Kiểm tra các nhánh của các thành viên trong nhóm (`NguyenTungLam`, `lythanhlap`, `nguyenquangvu`, `nguyentrunganh-2A202603413`) để đảm bảo cả nhóm cùng đi chung một hướng đề tài (Vinpearl).

### ⚠️ AI sai / Nguy cơ hiểu lầm ban đầu:
- Ban đầu, AI gợi ý sửa file code `prompt_prototype.py` sang bài toán Vinpearl để đồng bộ với báo cáo.
- **Tôi phát hiện và điều chỉnh ngay:** Tôi đã kiểm tra source code của `autograder/autograder.py` và phát hiện autograder kiểm tra cứng các từ khóa `draft_only`, `5%`, `dispatch_mobile_charger` dành riêng cho bài toán pin Xanh SM. Nếu sửa code sang Vinpearl sẽ bị 0 điểm phần code! Tôi đã yêu cầu AI giữ nguyên bài toán an toàn pin Xanh SM cho phần code, và chỉ làm bài toán Vinpearl cho phần tài liệu phân tích.

---

## 2. Tìm kiếm vấn đề & Phản biện lựa chọn (Phase 1 & Phase 2)

### 🤖 AI đã giúp gì:
- Gợi ý quét qua 5 bài toán thực tế của các công ty con Vingroup (Vinpearl, VinFast, Xanh SM, Vinhomes, Vinmec) theo đúng **4 Lenses** (Lặp lại, Tốn thời gian, AI-upgrade, Pain từ người khác).
- Hỗ trợ dàn khung 3 thẻ bài toán nhanh (Quick Problem Cards).

### ⚠️ AI sai / Hallucination ở đâu:
- **Tự bịa số liệu:** AI tự điền các con số rất "đẹp" nhưng phi thực tế (ví dụ: nhân viên mất 90 phút để đọc 1 review, tỷ lệ lỗi giảm từ 25% xuống 0.1%).
- **Thiếu góc nhìn kinh doanh thực tế:** AI ban đầu xếp bài toán chăm sóc cư dân Vinhomes lên ưu tiên số 1 vì "nhiều người dùng", bỏ qua rủi ro pháp lý và tranh chấp phí quản lý rất nhạy cảm của bất động sản.

### 🛠️ Tôi đã sửa prompt và thiết lập ranh giới thế nào:
- Yêu cầu AI gắn nhãn rõ các con số là *ước tính giả định cho 1 cơ sở khách sạn*.
- Điều chỉnh thời gian rà soát review thực tế là ~15–20 phút/lượt hoặc ~145 phút/ngày.
- Đưa quyết định thống nhất của nhóm vào tài liệu: Chọn bài toán **Vinpearl (Card #1)** vì dữ liệu review công khai dồi dào, ngôn ngữ tự nhiên phi cấu trúc cực kỳ phù hợp với LLM, và rủi ro hoàn toàn kiểm soát được bằng cơ chế Human-in-the-loop.

---

## 3. Workflow Mapping & Thiết lập Ranh giới An toàn (Phase 3 & Phase 5)

### 🤖 AI đã giúp gì:
- Hỗ trợ phân rã quy trình hiện tại (Current-State Workflow) thành 5 bước rõ ràng, xác định các điểm chuyển giao thông tin (🔄 Handoff) và điểm nghẽn (🔴 Bottleneck).
- Soạn thảo Problem Statement theo chuẩn 6 trường thông tin (6-field format) của Vin Smart Future.

### ⚠️ AI sai / Thiên kiến nguy hiểm:
- **Xu hướng "Full Automation" (Ảo tưởng tự động hóa hoàn toàn):** AI đề xuất cho mô hình tự động gửi email xin lỗi khách hàng và tự động tặng voucher giảm giá 20% cho các review 1 sao.
- **Phản biện của tôi:** Đây là sai lầm chết người trong ngành khách sạn cao cấp. Nếu AI tự động trả lời, nguy cơ phát ngôn sai lệch gây khủng hoảng truyền thông (PR Crisis) là cực lớn. Hơn nữa, việc tặng voucher bừa bãi sẽ bị trục lợi chính sách.

### 🛠️ Tôi đã sửa prompt và thiết lập ranh giới thế nào:
- Tôi thiết lập **Ranh giới vận hành (Operational Boundary) nghiêm ngặt**:
  + AI **TUYỆT ĐỐI CẤM** đăng phản hồi công khai ra ngoài.
  + AI **TUYỆT ĐỐI CẤM** tự cam kết đền bù tài chính.
  + **BẮT BUỘC 100% Human-in-the-loop (HITL):** AI chỉ đóng vai trò trợ lý đọc hiểu, gắn nhãn (P1 khẩn cấp, P2, P3), trích xuất bằng chứng (quotes) và draft bản tóm tắt nội bộ cho Giám đốc khách sạn duyệt.
  + Bổ sung cơ chế **Fallback**: Khi độ tự tin của mô hình < 75%, tự động gán cờ `[CẦN_DUYỆT_THỦ_CÔNG]` để chuyển về luồng truyền thống.

---

## 4. Lập trình Prompt Prototype & Xử lý xung đột logic (Phase 4)

### 🤖 AI đã giúp gì:
- Hướng dẫn cấu trúc gọi Gemini SDK (cả thư viện mới `google-genai` và thư viện fallback `google-generativeai`).
- Viết các trường hợp kiểm thử tấn công (Adversarial test cases) để stress-test mô hình.

### 💡 Điểm kỹ thuật tôi giải quyết:
- **Xung đột giữa 2 quy tắc ranh giới:**
  + Quy tắc 1: Mọi phản hồi phải bắt đầu bằng thẻ `[DRAFT_ONLY]`.
  + Quy tắc 2: Pin `< 5%` phải trả về đúng định dạng JSON `{"action": "dispatch_mobile_charger", "reason": "..."}`.
  + Nếu không quy định chặt, LLM sẽ phân vân giữa việc trả về text chứa thẻ hay chỉ trả về raw JSON.
  + **Giải pháp của tôi trong System Prompt:** Quy định rõ thứ tự phân cấp: Dòng 1 luôn là `[DRAFT_ONLY]`, dòng 2 là JSON hành động. Đồng thời cài đặt `temperature=0.0` để triệt tiêu tính ngẫu nhiên, giúp mô hình tuân thủ ranh giới 100%.

---

## 5. Tổng kết và Bài học kinh nghiệm (Key Takeaways)

1. **AI là trợ lý tư duy, con người là người chịu trách nhiệm:** AI xuất sắc trong việc phác thảo ý tưởng, dựng cấu trúc và viết mã nhanh, nhưng AI không biết bối cảnh thực tế của doanh nghiệp và rất dễ bị "ảo giác" (hallucinate) số liệu. Không bao giờ copy nguyên văn câu trả lời của AI mà không kiểm chứng.
2. **Problem First, AI Second:** Không chạy theo các giải pháp AI phức tạp (như Autonomous Multi-Agent) khi không cần thiết. Một giải pháp **LLM Feature** có kiểm soát chặt chẽ bằng ranh giới an toàn và Human-in-the-loop mang lại giá trị thực tiễn và độ tin cậy cao hơn rất nhiều.
3. **Kinh nghiệm điều phối nhóm:** Vai trò Trưởng nhóm đòi hỏi phải đọc kỹ quy chế chấm điểm ngay từ đầu để định hướng cho các thành viên, tránh việc làm sai lệch cấu trúc file hoặc vi phạm quy tắc Git (như cấm merge `.py` vào `main`).

