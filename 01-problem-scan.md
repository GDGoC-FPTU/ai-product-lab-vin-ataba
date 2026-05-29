# 01-problem-scan — Phase 1 & Phase 2

# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

### 📝 List bài toán của tôi:
| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **Xanh SM** | Lặp lại | Cuối mỗi ca, tài xế phải chụp ảnh nội thất/ngoại thất xe; nhân viên vận hành kiểm tra thủ công ảnh để phát hiện xe bẩn, móp xước, thiếu vật dụng trước khi giao ca tiếp theo. |
| 2 | **VinFast** | Tốn thời gian | Kỹ thuật viên xưởng dịch vụ phải đọc lịch sử sửa chữa, phiếu bảo hành và mô tả lỗi từ nhiều lần vào xưởng để tổng hợp hồ sơ trước khi xin phê duyệt thay thế linh kiện. |
| 3 | **Vinhomes** | Stakeholder Pain | Ban quản lý phải theo dõi thủ công biên bản bảo trì thang máy, máy bơm, PCCC từ nhiều nhà thầu; cư dân phàn nàn khi hạng mục quá hạn nhưng chưa được cảnh báo sớm. |
| 4 | **VinWonders** | AI-upgrade | Nhân viên vận hành khu vui chơi phải quan sát hàng chờ tại các trò chơi/nhà hàng và cập nhật thủ công tình trạng đông khách, khiến điều phối nhân sự và khuyến nghị tuyến tham quan bị chậm. |
| 5 | **Vinmec** | Lặp lại | Nhân viên bảo hiểm y tế phải kiểm tra thủ công hồ sơ thanh toán trước khi gửi hãng bảo hiểm: thiếu chữ ký, thiếu chỉ định, sai mã dịch vụ hoặc thiếu giấy ra viện. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

Chọn top 3 từ danh sách SCAN: **#1 (Xanh SM kiểm tra ảnh tình trạng xe cuối ca), #2 (VinFast tổng hợp hồ sơ phê duyệt thay linh kiện), #5 (Vinmec kiểm tra hồ sơ bảo hiểm trước khi gửi).**

## Quick Problem Card #1 — Xanh SM kiểm tra ảnh tình trạng xe cuối ca

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Nhân viên vận hành Xanh SM kiểm tra ảnh xe cuối   │
│ ca để phát hiện bẩn, móp xước hoặc thiếu vật dụng.          │
│ Công ty thành viên: [x] Xanh SM                             │
│                                                             │
│ Ai đang đau? Nhân viên vận hành đội xe, tài xế ca sau và    │
│ khách hàng nhận xe không sạch/không đạt chuẩn dịch vụ.      │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Tài xế chụp 6-8 ảnh xe khi kết thúc ca                 │
│   → 2. Ảnh được tải lên hệ thống vận hành                   │
│   → 3. Nhân viên mở từng ảnh để kiểm tra nội/ngoại thất     │
│   → 4. Ghi nhận lỗi: bẩn, móp xước, thiếu dây sạc/vật dụng  │
│   → 5. Tạo ticket vệ sinh/sửa chữa hoặc cho phép giao ca    │
│                                                             │
│ Bước nào tốn nhất? Bước 3-4 (⏱ 5 phút/xe)                  │
│ AI có thể hỗ trợ ở bước nào? Bước 3-4: tự đánh dấu ảnh có   │
│ dấu hiệu bất thường và gợi ý nhãn lỗi để nhân viên duyệt.   │
│                                                             │
│ Đo thành công bằng gì?                                      │
│ Giảm thời gian kiểm tra từ 5 phút xuống dưới 1 phút/xe;     │
│ phát hiện tối thiểu 90% ảnh có dấu hiệu bẩn/hư hỏng rõ ràng │
│ trước khi giao ca.                                          │
│                                                             │
│ Quick Architecture: [x] LLM Feature + Vision Model + HITL   │
└─────────────────────────────────────────────────────────────┘
```

## Quick Problem Card #2 — VinFast tổng hợp hồ sơ phê duyệt thay linh kiện

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Kỹ thuật viên VinFast phải tổng hợp hồ sơ sửa     │
│ chữa/bảo hành trước khi xin duyệt thay thế linh kiện.       │
│ Công ty thành viên: [x] VinFast                             │
│                                                             │
│ Ai đang đau? Kỹ thuật viên xưởng dịch vụ, cố vấn dịch vụ,   │
│ bộ phận bảo hành và khách hàng đang chờ quyết định sửa xe.  │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Kỹ thuật viên nhận xe và ghi nhận mô tả lỗi của khách  │
│   → 2. Tra lịch sử sửa chữa, phiếu bảo hành, log chẩn đoán  │
│   → 3. Tổng hợp bằng chứng: ảnh, mã lỗi, lần sửa trước      │
│   → 4. Viết đề xuất thay linh kiện và lý do kỹ thuật        │
│   → 5. Gửi quản lý/bộ phận bảo hành phê duyệt               │
│                                                             │
│ Bước nào tốn nhất? Bước 2-4 (⏱ 25 phút/hồ sơ)              │
│ AI có thể hỗ trợ ở bước nào? Bước 2-4: tóm tắt lịch sử sửa  │
│ chữa, gom bằng chứng liên quan và draft đề xuất kỹ thuật.   │
│                                                             │
│ Đo thành công bằng gì?                                      │
│ Giảm thời gian chuẩn bị hồ sơ từ 30 phút xuống dưới 8 phút; │
│ 90% hồ sơ có đủ mã lỗi, ảnh, lịch sử sửa chữa và lý do đề   │
│ xuất trước khi gửi duyệt.                                   │
│                                                             │
│ Quick Architecture: [x] LLM Feature + Rule checklist + HITL │
└─────────────────────────────────────────────────────────────┘
```

## Quick Problem Card #3 — Vinmec kiểm tra hồ sơ bảo hiểm trước khi gửi

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Nhân viên Vinmec kiểm tra hồ sơ bảo hiểm thủ công │
│ trước khi gửi hãng bảo hiểm, dễ thiếu giấy tờ hoặc sai mã.  │
│ Công ty thành viên: [x] Vinmec                              │
│                                                             │
│ Ai đang đau? Nhân viên bảo hiểm y tế, bệnh nhân chờ duyệt   │
│ thanh toán và bộ phận tài chính phải xử lý hồ sơ trả về.    │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Nhân viên gom chỉ định, hóa đơn, kết quả xét nghiệm    │
│   → 2. Đọc điều khoản bảo hiểm/điều kiện chi trả            │
│   → 3. Kiểm tra thiếu chữ ký, thiếu giấy, sai mã dịch vụ    │
│   → 4. Liên hệ khoa/phòng để bổ sung giấy tờ                │
│   → 5. Gửi hồ sơ sang hãng bảo hiểm                         │
│                                                             │
│ Bước nào tốn nhất? Bước 2-3 (⏱ 15 phút/hồ sơ)               │
│ AI có thể hỗ trợ ở bước nào? Bước 1-3: đọc checklist bảo    │
│ hiểm, trích xuất giấy tờ hiện có và cảnh báo mục còn thiếu. │
│                                                             │
│ Đo thành công bằng gì?                                      │
│ Giảm thời gian kiểm tra hồ sơ từ 15 phút xuống dưới 4 phút; │
│ giảm tỉ lệ hồ sơ bị hãng bảo hiểm trả về do thiếu thông tin │
│ từ 12% xuống dưới 4%.                                       │
│                                                             │
│ Quick Architecture: [x] LLM Feature + Rule checklist + HITL │
└─────────────────────────────────────────────────────────────┘
```
