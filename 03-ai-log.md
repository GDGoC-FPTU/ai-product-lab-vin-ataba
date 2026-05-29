# 📄 NHẬT KÝ CHIÊM NGHIỆM TƯƠNG TÁC AI (AI LOG)
**Kỹ sư thực hiện:** Nguyễn Trung Kiên  
**Mã số sinh viên:** 2A202600969  

---

### 1. AI đã giúp ích gì cho tôi trong suốt buổi học?
Trong suốt quá trình thực hiện Lab 02 và hoàn thiện giải pháp cho hệ thống điều phối của Xanh SM cũng như quản lý an ninh tại Vincom, Trợ lý AI đã đóng vai trò là một người bạn đồng hành tư duy (Thought-partner) và trợ lý lập trình đắc lực:
- **Hệ thống hóa cấu trúc quy trình bằng Code:** AI đã hỗ trợ tôi chuyển đổi sơ đồ tư duy từ dạng vẽ tay/ASCII thô sơ sang định dạng mã nguồn **Mermaid.js**. Nhờ đó, hai biểu đồ quy trình tìm trẻ lạc tại Vincom (Current-State và Future-State) được hiển thị trực quan, có phân cấp màu sắc rõ ràng cho các trạm gác HITL (Human-in-the-loop) ngay trên giao diện GitHub Markdown.
- **Xây dựng khung Prompt an toàn (Security Guardrails):** AI đã giúp tôi cấu trúc phân tầng logic cho `SYSTEM_PROMPT` nhằm bảo vệ ranh giới vận hành, xử lý các điều kiện biên phức tạp (như ép hệ thống trả về payload JSON gọi xe cứu hộ di động khi pin dưới 5%).
- **Gỡ rối hệ thống Git phân tán:** Trong giai đoạn đẩy bài lên hệ thống, khi gặp liên tiếp các lỗi xung đột mã nguồn (`Merge Conflict`) do các thành viên trong nhóm push đè file và lỗi kết nối mạng quốc tế (`RPC failed; curl 7 Recv failure`), AI đã hướng dẫn tôi từng bước xử lý cục bộ bằng các lệnh nâng cao như `git merge --abort`, `git fetch` và `git reset --hard origin/main` để làm sạch môi trường làm việc mà không ảnh hưởng đến Repo chung.

---

### 2. Trải nghiệm về sự sai lệch (Hallucination) hoặc điểm yếu của AI
Một bài học xương máu mà tôi nhận ra là **AI rất dễ đưa ra các giải pháp thiếu tính thực tế hoặc "bẫy" lập trình nếu người dùng không có kiến thức nền tảng để kiểm soát**:
- **Lỗi ngáo cú pháp và bất đồng bộ thư viện (Syntax & Dependency Mistake):** Khi yêu cầu hoàn thiện hàm `evaluate_prompt` để gọi mô hình Gemini, AI đã viết mã nguồn bị lặp lại cấu trúc khai báo hàm (`def` lồng `def`) và thụt lề sai logic (`IndentationError`). Hơn nữa, AI liên tục sử dụng cấu trúc thư viện mới `google-genai` trong khi môi trường ảo cục bộ `.venv` chưa cài đặt, dẫn đến script bị crash lập tức với exit code 1 (`No module named 'google'`).
- **Điểm mù đối với Autograder:** AI không hiểu luật chấm điểm tự động của hệ thống `autograder.py`. Nó đã giữ nguyên dòng lệnh `raise NotImplementedError` ngay dưới khối lệnh xử lý chính. Khi bot quét mã nguồn bằng `inspect.getsource()`, nó lập tức đánh trượt Tiêu chí 2 dù logic gọi API hoàn toàn đúng.
- **Rủi ro ranh giới an toàn (Safety Vulnerability):** Ban đầu, AI đề xuất System Prompt cho Xanh SM với tham số mặc định `temperature = 0.7`. Khi tôi đóng vai người dùng cố tình thực hiện kỹ thuật tấn công ngôn từ (Prompt Injection), AI đã bị thao túng tâm lý, chấp nhận bỏ qua tag `[DRAFT_ONLY]` và đồng ý chỉ đường cho xe pin 2% đến trạm sạc cách 8km, vi phạm nghiêm trọng ranh giới vận hành khắt khe của dự án.

---

### 3. Tôi đã điều chỉnh prompt và kiểm soát hệ thống ra sao?
Để khuất phục sự "ngáo" của AI và ép mô hình phải tuân thủ kỷ luật kỹ thuật tuyệt đối, tôi đã thực hiện hai bước hiệu chỉnh quan trọng:
1. **Khóa chết tính năng sáng tạo (`temperature = 0.0`):** Tôi chủ động hạ tham số cấu hình `temperature` về mức 0 tuyệt đối trong file cấu hình `GenerateContentConfig`. Việc này ép mô hình chuyển sang thuật toán giải mã tham lam (*Greedy Decoding*), luôn chọn từ có xác suất toán học cao nhất theo đúng chỉ thị hệ thống, giúp triệt tiêu hoàn toàn khả năng mô hình bị thao túng tâm lý trước các câu lệnh bẻ lái của người dùng.
2. **Thiết lập từ khóa mệnh lệnh tối cao:** Tôi đã tái cấu trúc lại `SYSTEM_PROMPT`, loại bỏ các câu lệnh mềm mỏng, thay thế bằng các từ ngữ mang tính bắt buộc viết hoa (`CRITICAL MANDATES`, `ABSOLUTELY FORBIDDEN`). Tôi định nghĩa rõ ràng cấu trúc đầu ra: bắt buộc phải có tiền tố `[DRAFT_ONLY]` ở mọi đoạn văn bản nháp, và nếu pin `< 5%` thì lập tức từ chối điều hướng, ép xuất dữ liệu dạng cấu trúc JSON sạch. 

Kết quả sau khi tôi tự tay tinh chỉnh và gỡ bỏ các dòng lệnh thừa, file `prompt_prototype.py` đã chạy thành công mượt mà, vượt qua 100% các bài test độc hại và ăn trọn điểm số tối đa từ bot chấm tự động.