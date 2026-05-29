# Phase 1: SCAN — Bảng Quét Cơ Hội Ứng Dụng AI (Cá nhân: Nguyễn Trung Kiên)

| STT | Công ty thành viên | Tên bài toán / Nghiệp vụ gặp điểm nghẽn | Loại thấu kính áp dụng | Đề xuất giải pháp sơ bộ |
|:---|:---|:---|:---|:---|
| 1 | VinFast | Phân tích log lịch sử vận hành, hỏng hóc để đưa ra gợi ý bảo trì chủ động. | **Tốn thời gian & Lặp lại** | Sử dụng RAG + LLM Feature kết hợp Predictive Analytics để dự đoán hạn bảo trì. |
| 2 | VinFast | Phân tích dữ liệu cảm biến và luồng giao thông thời gian thực để cảnh báo nguy hiểm. | **AI-upgrade & An toàn** | Sử dụng Deep Learning (Computer Vision + Time-series) trên xe để phát hiện rủi ro khẩn cấp. |
| 3 | Vinmec | Chẩn đoán hình ảnh (X-ray, MRI) tự động và hỗ trợ điều phối, xếp lịch khám thông minh. | **Tốn thời gian** | Sử dụng Computer Vision để phân loại ca bệnh, dùng Rule Engine để tự động sắp xếp lịch. |
| 4 | V-Green | Tối ưu hóa quy trình quản lý hạ tầng và điều phối lắp đặt mạng lưới trạm sạc xe điện. | **Operational Boundary** | Sử dụng Algorithmic Optimization (Quy hoạch tuyến tính) kết hợp Agentic AI để xếp lịch nhân sự. |
| 5 | Vinpearl | Dự đoán hành vi, gợi ý lộ trình tour cá nhân hóa và tối ưu thời gian chờ phục vụ của khách. | **Stakeholder Pain** | Sử dụng Recommender System kết hợp LLM để tự động tương tác và lập lịch cá nhân hóa. |

---

# Phase 2: QUICK-ASSESS — 3 Quick Problem Cards

## ┌─────────────────────────────────────────────────────────────┐
## │ QUICK PROBLEM CARD #01                                      │
## │                                                             │
## │ Bài toán: Hệ thống ADAS cảnh báo an toàn giao thông thời gian thực │
## │ Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
## │                     [ ] Vinmec   [ ] Khác: _________________ │
## │                                                             │
## │ Ai đang đau (Actor)? Tài xế lái xe và Hãng bảo hiểm đối tác của VinFast │
## │                                                             │
## │ Workflow thủ công hiện tại:                                 │
## │   1. Xe di chuyển trên đường gặp chướng ngại vật khuất tầm nhìn. │
## │   2. Tài xế quan sát bằng mắt thường và nhận diện rủi ro tiềm ẩn. │
## │   3. Tài xế phân tích tình huống và đưa ra quyết định xử lý (phanh/lái). │
## │   4. Xảy ra va chạm (nếu không kịp) -> Chờ bảo hiểm đến giám định thủ công. │
## │                                                             │
## │ Bước lỗi/tốn thời gian nhất: Bước 2 (Mất ~3 đến 5 giây phản xạ sinh học) │
## │ AI hỗ trợ ở bước nào: Bước 1 & 2 (Camera/Radar AI quét liên tục góc khuất) │
## │                                                             │
## │ Đo thành công bằng (Metric): Giảm thời gian nhận diện rủi ro nguy hiểm │
## │ từ 3 giây của người xuống dưới 150 miligiây (0.15s), giảm 40% vụ va chạm. │
## │                                                             │
## │ Quick Architecture: [ ] No AI  [x] Rule  [ ] LLM  [x] Deep Learning/Vision │
## └─────────────────────────────────────────────────────────────┘

## ┌─────────────────────────────────────────────────────────────┐
## │ QUICK PROBLEM CARD #02                                      │
## │                                                             │
## │ Bài toán: Hệ thống tối ưu hóa điều phối lắp đặt hạ tầng trạm sạc   │
## │ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
## │                     [ ] Vinmec   [x] V-Green                │
## │                                                             │
## │ Ai đang đau (Actor)? Chuyên viên quy hoạch mạng lưới trạm sạc V-Green │
## │                                                             │
## │ Workflow thủ công hiện tại:                                 │
## │   1. Nhận yêu cầu khảo sát địa điểm/mặt bằng từ đối tác hoặc cư dân. │
## │   2. Chuyên viên đối chiếu thủ công bản đồ lưới điện, mật độ xe và hạ tầng. │
## │   3. Lên phương án điều phối kỹ sư kỹ thuật xuống thực địa kiểm tra. │
## │   4. Thiết lập lịch trình thi công và sắp xếp nhân sự thủ công trên Excel. │
## │                                                             │
## │ Bước lỗi/tốn thời gian nhất: Bước 2 (Mất từ 2 - 4 tiếng/địa điểm khảo sát) │
## │ AI hỗ trợ ở bước nào: Bước 2 & 3 (Tự động hóa đối chiếu lớp dữ liệu GIS) │
## │                                                             │
## │ Đo thành công bằng (Metric): Giảm thời gian kiểm tra tính khả thi địa điểm │
## │ từ 180 phút xuống dưới 3 phút; tăng 30% độ chính xác quy hoạch lưới điện. │
## │                                                             │
## │ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [x] Agent │
## └─────────────────────────────────────────────────────────────┘

## ┌─────────────────────────────────────────────────────────────┐
## │ QUICK PROBLEM CARD #03                                      │
## │                                                             │
## │ Bài toán: Trợ lý Co-pilot gợi ý bảo trì chủ động và hỗ trợ xưởng dịch vụ │
## │ Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
## │                     [ ] Vinmec   [ ] Khác: _________________ │
## │                                                             │
## │ Ai đang đau (Actor)? Khách hàng lái xe và Kỹ thuật viên tại xưởng dịch vụ │
## │                                                             │
## │ Workflow thủ công hiện tại:                                 │
## │   1. Khách hàng đợi xe hỏng hóc hẳn hoặc đến mốc KM cố định mới đi kiểm tra. │
## │   2. Mang xe đến xưởng -> Kỹ thuật viên dùng máy quét log lỗi OBD thủ công. │
## │   3. Tra cứu sách hướng dẫn sửa chữa (SOP) để tìm linh kiện thay thế. │
## │   4. Tiến hành sửa chữa, bảo dưỡng và viết báo cáo hoàn thành thủ công. │
## │                                                             │
## │ Bước lỗi/tốn thời gian nhất: Bước 1 & 3 (Khách bị động; thợ mất thời gian tra SOP) │
## │ AI hỗ trợ ở bước nào: Bước 1 (Gợi ý trước) và Bước 3 (RAG tra cứu cẩm nang lỗi) │
## │                                                             │
## │ Đo thành công bằng (Metric): Chuyển đổi 50% số ca sửa chữa bị động sang │
## │ chủ động (Predictive Maintenance); giảm thời gian tra cứu mã lỗi của thợ │
## │ từ 45 phút xuống dưới 30 giây bằng RAG.                     │
## │                                                             │
## │ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [x] Agent (RAG Assisted) │
## └─────────────────────────────────────────────────────────────┘