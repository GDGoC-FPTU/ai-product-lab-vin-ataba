# 02-deep-dive-report — Vin Smart Future (Vincom Lost Child Use Case)

> **Báo cáo nhóm cho Phase 3 (DEEP-DIVE) và Phase 5 (EVALUATE).**
>
> * **Tên nhóm:** VinAtaba
> * **Thành viên:** Lý Hải Long - 2A202600568, Nguyễn Trung Kiên - 2A202600969, Hoàng Thanh Chiến - 2A202600861, Vũ Xuân Bách - 2A202600776
> * **Mảng kinh doanh lựa chọn:** **Vincom / Trung tâm thương mại — An toàn khách hàng & vận hành an ninh.**

---

## 🏛️ Bối cảnh: Nhóm chúng tôi đang giải quyết vấn đề gì?

Nhóm chúng tôi đóng vai trò **AI Product Engineer tại Vin Smart Future**, phối hợp với đội vận hành và an ninh tại **Vincom** để phân tích một tình huống nhạy cảm nhưng có khả năng xảy ra trong trung tâm thương mại: **phụ huynh báo trẻ bị lạc trong khu vực Vincom đông người**.

Quy trình hiện tại phụ thuộc vào việc phụ huynh mô tả đặc điểm nhận diện, bảo vệ truyền thông tin qua bộ đàm, nhân viên đi tìm trực tiếp, đồng thời bộ phận camera phải quan sát nhiều màn hình bằng mắt thường. Trong giờ cao điểm, trẻ có thể di chuyển rất nhanh qua thang cuốn, thang máy, cửa hàng, khu vui chơi hoặc lối ra. Vì vậy, bottleneck lớn nhất không nằm ở việc "có camera hay không", mà nằm ở việc **tìm đúng camera, đúng khung thời gian và đúng người nghi vấn đủ nhanh**.

---

# 🗳️ Quyết định lựa chọn của nhóm

Nhóm quyết định chọn bài toán **"Hỗ trợ tìm trẻ lạc trong trung tâm thương mại Vincom bằng AI nhận diện theo ảnh/mô tả và theo dấu qua camera"** để thực hiện Deep-Dive.

## Lý do lựa chọn

* **Tác động vận hành rõ ràng:** Mỗi phút chậm trễ làm phụ huynh hoảng loạn hơn, kéo nhiều nhân viên khỏi vị trí trực và tăng nguy cơ trẻ đi ra khỏi khu vực an toàn.
* **Có workflow thủ công cụ thể:** Phụ huynh báo bảo vệ → mô tả trẻ → báo bộ phận camera/nhân viên tầng → tìm bằng mắt thường/camera → giữ trẻ lại → dẫn phụ huynh đến xác nhận.
* **AI có vai trò phù hợp:** AI không cần tự ra quyết định cuối cùng, nhưng có thể giúp chuẩn hóa mô tả, tìm frame/camera nghi vấn, dự đoán hướng di chuyển và gợi ý khu vực ưu tiên cho nhân viên.
* **Ranh giới vận hành bắt buộc phải rõ:** Vì liên quan đến trẻ em, AI chỉ được hỗ trợ nội bộ, không tự kết luận danh tính, không tự công bố thông tin và luôn cần con người xác nhận.

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm)

## 3.1. Current-State Workflow

Quy trình xử lý hiện tại khi phụ huynh báo trẻ lạc tại Vincom:

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Phụ huynh    │     │ Bảo vệ ghi   │     │ Chuyển tin   │     │ Nhân viên    │
│ báo trẻ lạc  │ ──→ │ mô tả trẻ &  │ ──→ │ cho camera,  │ ──→ │ các tầng đi  │
│ tại quầy/    │     │ nơi thấy cuối│     │ sảnh, tầng   │     │ tìm trực tiếp│
│ bảo vệ       │     │              │     │              │     │              │
│ Ai: Parent   │     │ Ai: Security │     │ Ai: Security │     │ Ai: Floor    │
│ ⏱ 3 phút     │     │ ⏱ 5 phút 🔄  │     │ ⏱ 2 phút 🔄  │     │ ⏱ 10 phút 🔴 │
│ In: Báo mất  │     │ In: Mô tả    │     │ In: Mô tả    │     │ In: Bộ đàm   │
│ Out: Sự cố   │     │ Out: Phiếu   │     │ Out: Alert   │     │ Out: Kết quả │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 8       │     │ Bước 7       │     │ Bước 6       │     │ Bước 5       │
│ Phụ huynh    │     │ Nhân viên    │     │ Nhân viên    │     │ Bộ phận      │
│ đến xác nhận │ ←── │ giữ bé tại   │ ←── │ báo vị trí   │ ←── │ camera rà    │
│ và nhận bé   │     │ điểm an toàn │     │ nghi vấn     │     │ bằng mắt     │
│ Ai: Parent   │     │ Ai: Floor    │     │ Ai: Floor    │     │ Ai: Camera   │
│ ⏱ 5 phút     │     │ ⏱ 3 phút     │     │ ⏱ 2 phút 🔄  │     │ ⏱ 15 phút 🔴 │
│ In: Vị trí   │     │ In: Trẻ thấy │     │ In: Quan sát │     │ In: CCTV     │
│ Out: Bàn giao│     │ Out: Giữ bé  │     │ Out: Bộ đàm  │     │ Out: Camera  │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
```

🔴 = Bottleneck  
🔄 = Handoff  
⏱ **Tổng thời gian xử lý thủ công ước tính: 45 phút/lượt** trong giờ cao điểm.

## Điểm handoff quan trọng

* **Phụ huynh → bảo vệ:** Phụ huynh mô tả trẻ bằng lời, có thể thiếu thông tin hoặc bị hoảng loạn nên mô tả không nhất quán.
* **Bảo vệ → camera/nhân viên tầng:** Mô tả truyền qua bộ đàm dễ bị rút gọn, thiếu ảnh, thiếu vị trí thấy lần cuối.
* **Camera → nhân viên tầng:** Nhân viên camera phải vừa nhìn màn hình vừa báo vị trí nghi vấn cho người ở hiện trường.
* **Nhân viên tầng → phụ huynh:** Chỉ được bàn giao khi phụ huynh xác nhận trực tiếp, tránh nhận nhầm trẻ.

## Bottleneck chính

* **Bước 5 — Rà camera bằng mắt thường:** mất khoảng **15 phút/lượt**, vì phải xem nhiều camera, nhiều tầng và nhiều khung thời gian.
* **Bước 4 — Nhân viên đi tìm trực tiếp:** mất khoảng **10 phút/lượt**, vì mô tả ban đầu có thể mơ hồ: "áo vàng", "bé khoảng 5 tuổi", "gần khu ăn uống".
* **Bước 2 — Ghi mô tả trẻ:** mất khoảng **5 phút/lượt**, nhưng ảnh hưởng lớn đến toàn bộ quy trình nếu mô tả thiếu màu áo, phụ kiện, chiều cao, hướng di chuyển hoặc vị trí thấy cuối.

---

## 3.2. Problem Statement (6-field) — Vin Smart Future Standard

| Field | Nội dung |
|---|---|
| **1. Actor / Operator** | Bảo vệ/quầy thông tin Vincom, bộ phận camera an ninh, nhân viên sảnh/tầng, quản lý ca và phụ huynh báo trẻ lạc. |
| **2. Current Workflow** | Phụ huynh báo trẻ lạc cho bảo vệ. Bảo vệ ghi nhận mô tả nhận diện như tuổi ước tính, màu áo/quần, phụ kiện, ảnh gần nhất nếu có và vị trí nhìn thấy lần cuối. Sau đó bảo vệ báo cho bộ phận camera và nhân viên các tầng. Nhân viên đi tìm trực tiếp, có thể phát loa nội bộ hoặc loa trung tâm nếu cần. Bộ phận camera rà nhiều màn hình bằng mắt thường. Khi thấy trẻ nghi vấn, nhân viên tại vị trí giữ bé ở điểm an toàn rồi dẫn phụ huynh đến xác nhận. |
| **3. Bottleneck** | Rà camera thủ công và truyền mô tả qua nhiều người. Camera có nhiều luồng, trẻ di chuyển nhanh, mô tả có thể không đủ chi tiết, nhân viên dễ bỏ sót frame quan trọng. Bottleneck lớn nhất là bước tìm frame/khu vực nghi vấn trong 10-20 phút đầu. |
| **4. Business Impact** | Đây là sự cố an toàn khách hàng có độ ưu tiên cao. Nếu xử lý chậm, phụ huynh hoảng loạn, nhiều nhân sự phải rời vị trí trực, trung tâm có nguy cơ phải phát loa nhiều lần và trải nghiệm khách hàng bị ảnh hưởng. Với mỗi ca mất khoảng 45 phút và cần 5-8 nhân sự phối hợp, chi phí vận hành và rủi ro uy tín đều tăng. |
| **5. Success Metric** | 1. Giảm thời gian khoanh vùng camera/khu vực nghi vấn từ 25 phút xuống dưới 5 phút.<br>2. 90% ca có ảnh hoặc mô tả đủ rõ được tạo danh sách 3 khu vực ưu tiên trong dưới 2 phút.<br>3. 100% trường hợp phải có nhân viên Vincom xác nhận trực tiếp trước khi báo phụ huynh đến nhận trẻ.<br>4. Không lưu ảnh/mô tả trẻ quá thời gian xử lý sự cố, trừ khi có yêu cầu pháp lý hoặc biên bản được phê duyệt. |
| **6. Operational Boundary** | AI được phép nhận ảnh tham chiếu/mô tả từ phụ huynh, chuẩn hóa đặc điểm nhận diện, tìm frame/camera nghi vấn, gợi ý hướng di chuyển và tạo bản tin nội bộ cho nhân viên. **CẤM:** AI không được tự khẳng định danh tính trẻ, không tự phát loa, không tự gửi ảnh trẻ ra ngoài hệ thống nội bộ, không tự bàn giao trẻ, không dùng dữ liệu cho mục đích marketing, không lưu ảnh lâu hơn chính sách sự cố. Mọi kết quả AI phải được nhân viên camera/bảo vệ xác nhận trước khi điều phối người đến vị trí. |

---

## 3.3. Future-State Flow & AI Fit

* **AI Fit:** Chọn **LLM Feature + Vision Retrieval**, kết hợp rule-based workflow. Chưa chọn Agentic Loop tự trị vì tình huống liên quan trẻ em và an toàn tại không gian công cộng.
* **Vai trò của AI:** Hỗ trợ nội bộ để tăng tốc khoanh vùng, không thay thế quyết định của bảo vệ hoặc phụ huynh.

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Phụ huynh    │     │ 🟢 Bảo vệ    │     │ 🔵 AI chuẩn  │     │ 🔵 AI tìm    │
│ báo trẻ lạc  │ ──→ │ nhập mô tả & │ ──→ │ hóa mô tả    │ ──→ │ camera/frame │
│              │     │ ảnh nếu có   │     │ nhận diện    │     │ nghi vấn     │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 8       │     │ Bước 7       │     │ Bước 6       │     │ Bước 5       │
│ Phụ huynh    │     │ Nhân viên    │     │ 🟢 Nhân viên │     │ 🟢 Camera    │
│ xác nhận &   │ ←── │ giữ bé tại   │ ←── │ tới khu vực  │ ←── │ xác nhận     │
│ nhận bé      │     │ điểm an toàn │     │ ưu tiên      │     │ frame nghi   │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
                                                              ↩️ Fallback:
                                                              Nếu AI không tự tin,
                                                              quay lại tìm thủ công
                                                              và kiểm tra lối ra.
```

## AI Step

* **🔵 AI chuẩn hóa mô tả:** Chuyển lời kể của phụ huynh thành checklist: giới tính/tuổi ước tính, màu áo, màu quần, giày dép, balo/mũ, chiều cao tương đối, vị trí thấy lần cuối, thời điểm mất dấu.
* **🔵 AI truy xuất camera/frame:** Dựa trên vị trí thấy cuối và thời gian mất dấu để ưu tiên camera gần đó, thang cuốn, thang máy, cửa ra vào, khu vui chơi và khu ăn uống.
* **🔵 AI xếp hạng khu vực:** Trả về danh sách 3-5 khu vực/camera nghi vấn kèm mức tự tin và timestamp.
* **🔵 AI tạo bản tin nội bộ:** Ví dụ: `[NỘI BỘ] Trẻ nghi vấn áo vàng, quần jean, balo đỏ, xuất hiện gần thang cuốn tầng 2 lúc 15:24. Cần nhân viên tầng 2 xác minh.`

## Human Step (HITL)

* **🟢 Bảo vệ xác nhận đầu vào:** Xác nhận mô tả với phụ huynh trước khi đưa vào hệ thống.
* **🟢 Nhân viên camera xác nhận frame:** Kiểm tra frame nghi vấn trước khi báo nhân viên tầng tiếp cận.
* **🟢 Nhân viên tầng xác minh tại chỗ:** Tiếp cận nhẹ nhàng, giữ trẻ tại điểm an toàn, không bàn giao cho bất kỳ ai nếu chưa có xác nhận.
* **🟢 Phụ huynh xác nhận:** Phụ huynh trực tiếp xác nhận trẻ trước khi bàn giao.

## Fallback

* Nếu ảnh tham chiếu mờ hoặc mô tả thiếu: hệ thống chuyển sang checklist thủ công và ưu tiên kiểm tra lối ra, thang cuốn, thang máy, khu vui chơi.
* Nếu AI trả nhiều kết quả gần giống nhau: nhân viên camera xác nhận từng frame theo thứ tự gần vị trí thấy cuối nhất.
* Nếu sau **10 phút** chưa có kết quả đáng tin cậy: kích hoạt quy trình khẩn cấp, tăng nhân sự kiểm soát lối ra và báo quản lý ca.
* Nếu hệ thống AI/camera lỗi: quay lại quy trình hiện tại bằng bộ đàm, sơ đồ tầng và chia khu vực tìm kiếm.

---

# 🏁 Phase 5 — EVALUATE

## AI Readiness Checklist

| Checklist | Trạng thái | Nhận xét |
|---|---|---|
| Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test? | [x] có đủ | Hình ảnh, dữ liệu về con người có nhiều trên mạng xã hội, đủ để nhận diện hình dáng, khuôn mặt đặc trưng. |
| Rủi ro khi AI sai có nằm trong tầm kiểm soát? | [x] Có, nếu bắt buộc HITL | AI chỉ tạo danh sách nghi vấn. Bảo vệ/camera/nhân viên tầng và phụ huynh luôn xác nhận trước mọi hành động. |
| Stakeholders sẵn sàng thay đổi quy trình làm việc cũ? | [x] Có thể | Đội bảo vệ và camera có động lực vì giảm thời gian rà camera, nhưng cần training cách nhập mô tả, dùng ảnh tham chiếu và xử lý kết quả AI. |

## Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future

[x] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.  
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.  
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

## Justification

Nhóm chọn **NOT YET** vì bài toán có giá trị vận hành rõ ràng nhưng liên quan trực tiếp đến **trẻ em, dữ liệu camera, quyền riêng tư và an toàn tại nơi công cộng**. Về mặt kỹ thuật, AI vision và LLM có thể giúp giảm đáng kể thời gian khoanh vùng trẻ lạc, nhưng nếu triển khai vội, rủi ro sai nhận diện hoặc lạm dụng dữ liệu sẽ lớn hơn lợi ích ban đầu.

Quyết định hợp lý là chuẩn bị một prototype nội bộ với phạm vi hẹp:

* Chỉ dùng dữ liệu mô phỏng hoặc video diễn tập đã được cho phép.
* Chỉ chạy trong môi trường nội bộ, không gửi ảnh hoặc kết quả ra ngoài.
* Chỉ đo khả năng khoanh vùng camera/khu vực, chưa tự động điều phối toàn bộ quy trình.
* Luôn giữ quy định **AI gợi ý, con người xác nhận**.

## Ước lượng chi phí và effort

| Hạng mục | Ước lượng |
|---|---:|
| AI/backend prototype nhận mô tả, ảnh tham chiếu và trả danh sách camera nghi vấn | 2 kỹ sư x 3 tuần |
| Tích hợp dữ liệu camera mẫu hoặc video diễn tập | 1 kỹ sư x 2 tuần |
| Thiết kế quy trình vận hành, checklist HITL và logging | 1 PM/Operations x 1 tuần |
| Kiểm thử tình huống tại 1 Vincom giả lập hoặc sau giờ vận hành | 2-3 buổi test |
| Chi phí cloud/API cho prototype nhỏ | Thấp đến trung bình, phụ thuộc số giờ video test |

## Điều kiện để chuyển từ NOT YET sang GO

* Có baseline hiện tại: số ca/tháng, thời gian tìm trung bình, số nhân sự tham gia, tỉ lệ phát hiện qua camera.
* Có bộ dữ liệu test an toàn: mô phỏng hoặc đã ẩn danh, không dùng dữ liệu trẻ em thật tùy tiện.
* Có chính sách lưu/xóa ảnh tham chiếu, mô tả trẻ và log camera sau khi sự cố kết thúc.
* Có quy trình HITL bắt buộc ở 4 điểm: nhập mô tả, xác nhận frame, tiếp cận trẻ, bàn giao cho phụ huynh.
* Có hướng dẫn fallback nếu AI không tự tin, camera lỗi hoặc có nhiều trẻ giống mô tả.

## Kết luận

Dự án **chưa nên GO ngay**, nhưng rất đáng để chuẩn bị prototype có kiểm soát. Nếu nhóm thu thập được dữ liệu mô phỏng an toàn và thiết kế tốt ranh giới vận hành, bài toán này có thể trở thành một công cụ hỗ trợ an ninh thực tế cho Vincom: giảm thời gian khoanh vùng trẻ lạc, giảm áp lực cho phụ huynh và giúp nhân viên xử lý sự cố có hệ thống hơn.
