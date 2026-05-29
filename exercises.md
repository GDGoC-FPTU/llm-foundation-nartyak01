# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python starter-code/template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o, GPT-4o-mini và Gemini 2.5 Flash.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Temperature càng thấp (0.0–0.5), câu trả lời càng ổn định, súc tích và lặp lại nội dung quen thuộc. Temperature càng cao (1.0–1.5), mô hình chọn token ngẫu nhiên hơn nên câu chuyện đa dạng, sáng tạo hơn nhưng đôi khi lệch chủ đề hoặc kém nhất quán.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Khoảng **0.2–0.4**. Mức này giữ câu trả lời nhất quán, đúng chính sách và ít “bịa” thông tin, phù hợp hỗ trợ khách hàng; vẫn đủ linh hoạt để diễn đạt tự nhiên hơn temperature 0.0.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Tổng **30.000 lần gọi/ngày** × **350 token** ≈ **10,5 triệu token/ngày**.  
> Giả sử mỗi lần gọi ~100 token input và 250 token output (theo `PRICING_1M_TOKENS` trong `template.py`):  
> - Chi phí/lần GPT-4o: (100×5 + 250×20) / 10⁶ ≈ **$0,0055**  
> - Chi phí/lần GPT-4o-mini: (100×0,15 + 250×0,6) / 10⁶ ≈ **$0,000165**  
> → GPT-4o đắt hơn khoảng **33 lần** (~$165/ngày so với ~$5/ngày cho cùng workload).

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> **GPT-4o xứng đáng** khi cần suy luận phức tạp, phân tích tài liệu dài hoặc soạn nội dung quan trọng (hợp đồng, báo cáo y tế) — sai sót tốn kém hơn tiền API. **GPT-4o-mini phù hợp** cho phân loại intent, FAQ, tóm tắt ngắn hoặc chatbot khối lượng lớn — đủ tốt với chi phí thấp hơn nhiều lần.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất khi người dùng tương tác trực tiếp (chatbot, trợ lý ảo): token hiển thị dần giúp cảm giác phản hồi nhanh và giảm tỷ lệ bỏ phiên chờ đợi. Non-streaming phù hợp hơn khi chạy batch qua đêm, pipeline ETL, hoặc cần toàn bộ JSON/structured output trước khi xử lý bước tiếp theo — logic đơn giản hơn và dễ validate kết quả một lần.

---

## Danh Sách Kiểm Tra Nộp Bài
- [x] Tất cả tests pass: `pytest tests/ -v`
- [x] `call_openai` đã triển khai và kiểm thử
- [x] `call_gemini` / GPT-4o-mini (qua `call_openai` với `gpt-4o-mini`) đã triển khai và kiểm thử
- [x] `compare_models` đã triển khai và kiểm thử
- [x] `streaming_chatbot` đã triển khai và kiểm thử
- [x] `retry_with_backoff` đã triển khai và kiểm thử
- [x] `batch_compare` đã triển khai và kiểm thử
- [x] `format_comparison_table` đã triển khai và kiểm thử
- [x] `exercises.md` đã điền đầy đủ
- [x] Sao chép bài làm vào folder `solution-code/solution.py`
