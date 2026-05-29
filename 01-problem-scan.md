
### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 |VinFast| Repetitive |Nhân viên CSKH phải trả lời lặp đi lặp lại các câu hỏi về thời gian sạc, bảo hành pin, lỗi màn hình và lịch bảo dưỡng xe điện. Mỗi ngày có hàng nghìn ticket tương tự nhau gây quá tải tổng đài. |
| 2 |Xanh SM |Stakeholder Pain |Tài xế phàn nàn hệ thống gợi ý điểm đón khách chưa chính xác tại khu đông người như trung tâm thương mại hoặc bệnh viện, dẫn đến mất thời gian tìm khách và tăng tỷ lệ hủy chuyến. |
| 3 |Vinhomes |Time-consuming |Ban quản lý khu đô thị mất nhiều thời gian đọc và phân loại phản ánh cư dân như hỏng thang máy, mất nước, tiếng ồn, đỗ xe sai quy định trước khi chuyển đúng bộ phận xử lý. |
| 4 |Vinmec |AI-upgrade |Quy trình đặt lịch khám hiện tại còn thủ công, bệnh nhân phải mô tả triệu chứng với nhân viên tổng đài nhiều lần. AI có thể hỗ trợ phân loại triệu chứng và gợi ý chuyên khoa phù hợp nhanh hơn |
| 5 |Xanh SM |Repetitive |Bộ phận hỗ trợ tài xế phải kiểm tra thủ công các khiếu nại về phí chuyến đi, quãng đường và thanh toán ví điện tử, mất nhiều thời gian đối chiếu dữ liệu. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): AI hỗ trợ tự động phân loại phản ánh      │
│ cư dân và chuyển đúng bộ phận xử lý.                        │
│                                                             │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác                   │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Nhân viên chăm sóc cư dân và ban quản lý tòa nhà.           │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Cư dân gửi phản ánh qua app/Zalo                       │
│      ──> 2. Nhân viên đọc nội dung                          │
│      ──> 3. Phân loại vấn đề                                │ 
│      ──> 4. Chuyển cho bộ phận phù hợp                      │
│      ──> 5. Theo dõi trạng thái xử lý                       │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Đọc và phân loại phản ánh (⏱ 5-7 phút/lượt)                │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ AI tự động phân loại ticket theo nhóm: điện, nước,          │
│ an ninh, vệ sinh, thang máy, bãi đỗ xe...                   │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - Giảm thời gian phân loại từ 7 phút → dưới 1 phút          │
│ - Tăng độ chính xác route ticket lên trên 90%               │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM [ ] Agent  │
└─────────────────────────────────────────────────────────────┘
```
```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): AI hỗ trợ phân loại triệu chứng và        │
│ gợi ý chuyên khoa phù hợp khi đặt lịch khám.                │
│                                                             │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [x] Vinmec   [ ] Khác                   │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Nhân viên tổng đài và bệnh nhân đặt lịch khám.              │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Bệnh nhân gọi điện đặt lịch                            │
│      ──> 2. Mô tả triệu chứng                               │
│      ──> 3. Nhân viên hỏi lại nhiều lần                     │
│      ──> 4. Xác định chuyên khoa                            │
│      ──> 5. Đặt lịch khám                                   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Thu thập và phân loại triệu chứng (⏱ 10-15 phút/lượt)      │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ AI chatbot hỏi triệu chứng tự động và gợi ý chuyên khoa     │
│ phù hợp trước khi chuyển cho nhân viên xác nhận.            │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - Giảm thời gian đặt lịch từ 15 phút → dưới 3 phút          │
│ - Giảm 50% workload cho tổng đài viên                       │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM [ ] Agent  │
└─────────────────────────────────────────────────────────────┘
```
```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): AI chatbot hỗ trợ trả lời tự động các     │
│ câu hỏi lặp lại của khách hàng VinFast.                     │
│                                                             │
│ Công ty thành viên: [x] VinFast [ ] Xanh SM [ ] Vinhomes    │
│                     [ ] Vinmec   [ ] Khác                   │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Nhân viên chăm sóc khách hàng và chủ xe VinFast.            │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Khách hàng gửi câu hỏi                                 │
│      ──> 2. Nhân viên đọc ticket                            │
│      ──> 3. Tra cứu thông tin bảo hành/sạc xe               │
│      ──> 4. Soạn phản hồi                                   │
│      ──> 5. Gửi trả lời cho khách hàng                      │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Tra cứu và soạn phản hồi (⏱ 8-10 phút/lượt)                │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ AI chatbot tự động trả lời các FAQ phổ biến và hỗ trợ       │
│ xử lý ticket cơ bản trước khi chuyển cho nhân viên.         │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - Giảm thời gian phản hồi từ 10 phút → dưới 1 phút          │
│ - Giảm 60% số ticket FAQ cần xử lý thủ công                 │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM [ ] Agent  │
└─────────────────────────────────────────────────────────────┘
```