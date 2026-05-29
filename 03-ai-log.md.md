Trong buổi lab này, tôi sử dụng ChatGPT để hỗ trợ brainstorm các bài toán AI thực tế cho hệ sinh thái Vingroup như VinFast, Vinhomes, Vinmec và Xanh SM. AI giúp tôi nhanh chóng nghĩ ra nhiều bottleneck vận hành như phân loại phản ánh cư dân, chatbot CSKH hay hỗ trợ đặt lịch khám bệnh. Ngoài ra, tôi còn dùng AI để gợi ý workflow hiện tại, xác định bước gây bottleneck và đề xuất metric đo hiệu quả sau khi áp dụng AI.

Trong quá trình làm bài, AI cũng hỗ trợ tôi viết lại mô tả bài toán theo hướng chuyên nghiệp hơn và đề xuất loại kiến trúc phù hợp như Rule-based, LLM hoặc Agent. Đặc biệt, AI giúp tôi hiểu rõ hơn sự khác nhau giữa chatbot thông thường và Agentic AI có khả năng tự động thực hiện nhiều bước liên tiếp.

Tuy nhiên, AI không phải lúc nào cũng đưa ra câu trả lời chính xác. Có thời điểm AI đề xuất sử dụng Agent cho toàn bộ quy trình xử lý phản ánh cư dân của Vinhomes, dù thực tế bài toán này chỉ cần phân loại ticket và route đến đúng bộ phận. Giải pháp Agent khi đó quá phức tạp, tốn chi phí triển khai và khó kiểm soát hơn nhu cầu thực tế.

Ngoài ra, AI đôi lúc còn tự tạo ra các số liệu không có nguồn xác thực như “giảm 80% chi phí vận hành” hoặc “độ chính xác đạt 99%”, dù tôi chưa cung cấp dữ liệu thực tế. Điều này khiến tôi nhận ra cần phải kiểm tra lại các metric trước khi đưa vào báo cáo.

Để cải thiện kết quả, tôi đã chỉnh sửa prompt theo hướng cụ thể hơn, ví dụ:
- Giới hạn AI chỉ đề xuất giải pháp phù hợp với workflow đơn giản.
- Yêu cầu AI không tự tạo số liệu thiếu căn cứ.
- Bổ sung ràng buộc như “ưu tiên giải pháp khả thi cho MVP” và “có human-in-the-loop”.

Sau khi điều chỉnh prompt, kết quả AI trả về thực tế hơn, tập trung vào việc hỗ trợ con người thay vì thay thế hoàn toàn quy trình vận hành. Qua buổi lab này, tôi nhận thấy AI hiệu quả nhất khi đóng vai trò thought-partner hỗ trợ brainstorming, phân tích workflow và tăng tốc quá trình thiết kế sản phẩm, nhưng con người vẫn cần đánh giá tính khả thi và kiểm soát đầu ra cuối cùng.