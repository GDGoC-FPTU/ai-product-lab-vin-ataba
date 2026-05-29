# 03-ai-log — Reflection cá nhân

Trong buổi lab này, tôi dùng AI như một **thought-partner** để hỗ trợ quá trình tìm bài toán, viết báo cáo và kiểm tra lại logic sản phẩm. Thay vì chỉ yêu cầu AI viết hộ, tôi dùng AI để đặt câu hỏi ngược lại: bài toán nào đủ thực tế, workflow nào có bottleneck rõ, metric nào đo được, và ranh giới vận hành nào cần khóa chặt trước khi đưa AI vào quy trình thật.

## AI đã giúp gì?

AI giúp tôi brainstorm các pain point vận hành trong hệ sinh thái Vingroup, sau đó chọn lọc lại thành các bài toán cụ thể hơn cho Phase 1 và Phase 2. Ví dụ, tôi dùng AI để chuyển các ý tưởng chung như "tối ưu vận hành trung tâm thương mại" thành một bài toán rõ hơn: **hỗ trợ tìm trẻ lạc trong Vincom bằng AI nhận diện theo ảnh/mô tả và theo dấu qua camera**.

AI cũng hỗ trợ tôi viết cấu trúc báo cáo theo format của bài mẫu: có current-state workflow, handoff, bottleneck, Problem Statement 6-field, future-state flow, Human-in-the-loop, fallback và checklist đánh giá. Nhờ đó, tôi không chỉ mô tả "dùng AI để nhận diện trẻ", mà còn phải chỉ ra AI được phép làm gì, không được phép làm gì, bước nào con người bắt buộc xác nhận.

Ngoài ra, AI giúp tôi nghĩ kỹ hơn về metric. Ban đầu tôi chỉ nghĩ chung là "tìm trẻ nhanh hơn", nhưng sau khi trao đổi với AI, metric được cụ thể hóa thành: giảm thời gian khoanh vùng camera/khu vực nghi vấn từ khoảng 25 phút xuống dưới 5 phút, và 100% trường hợp phải có nhân viên xác nhận trước khi báo phụ huynh đến nhận trẻ.

## AI đã sai hoặc chưa phù hợp ở đâu?

Một điểm AI làm chưa tốt là ban đầu đề xuất một số bài toán khá giống với ví dụ trong `03-inspiration-kit.md`, ví dụ như phân loại phản ánh cư dân, phân loại lịch hẹn khám hoặc xử lý review khách sạn. Các ý tưởng này không sai hoàn toàn, nhưng chưa đủ "riêng" và dễ bị xem là copy từ tài liệu gợi ý thay vì tự phát triển từ bối cảnh thực tế.

Với bài toán tìm trẻ lạc, AI cũng có xu hướng đề xuất giải pháp vision/face recognition khá mạnh, như thể hệ thống có thể tự nhận diện và kết luận ngay trẻ đang ở đâu. Đây là điểm rủi ro, vì bài toán liên quan đến trẻ em, dữ liệu camera và quyền riêng tư. Nếu để AI tự kết luận danh tính hoặc tự gửi thông tin cho nhân viên mà không có xác nhận, hệ thống có thể gây nhầm lẫn hoặc vi phạm ranh giới an toàn.

Một điểm nữa là AI ban đầu hơi thiên về "GO" vì thấy bài toán có giá trị và công nghệ có vẻ khả thi. Sau khi suy nghĩ lại, tôi thấy quyết định phù hợp hơn là **NOT YET**, vì nhóm cần dữ liệu mô phỏng an toàn, baseline hiện tại và quy trình bảo mật trước khi prototype trên camera thật.

## Tôi đã sửa prompt và ranh giới như thế nào?

Tôi điều chỉnh prompt theo hướng yêu cầu AI không chỉ đưa ý tưởng, mà phải kiểm tra theo rubric của README: có workflow hiện tại, thời gian từng bước, bottleneck, business impact, metric có số, operational boundary, HITL và fallback. Điều này giúp câu trả lời bám vào bài nộp hơn, thay vì chỉ là brainstorm chung chung.

Tôi cũng bổ sung ranh giới rõ cho bài toán Vincom:

- AI chỉ được dùng để **gợi ý nội bộ** camera/frame/khu vực nghi vấn.
- AI không được tự khẳng định danh tính trẻ.
- AI không được tự phát loa hoặc gửi hình ảnh trẻ ra ngoài hệ thống.
- AI không được tự bàn giao trẻ cho bất kỳ ai.
- Nhân viên camera, nhân viên hiện trường và phụ huynh đều phải xác nhận ở các bước quan trọng.
- Nếu AI không tự tin hoặc dữ liệu đầu vào kém, hệ thống phải fallback về quy trình thủ công.

Sau khi thêm các ranh giới này, bài toán trở nên thực tế hơn: AI không còn là "người quyết định", mà là công cụ giúp nhân viên Vincom khoanh vùng nhanh hơn trong một tình huống khẩn cấp. Qua bài lab, tôi nhận ra AI hữu ích nhất khi được đặt trong một workflow có con người kiểm soát, metric rõ ràng và giới hạn vận hành cụ thể.
