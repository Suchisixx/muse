# AI Muse - Vietnamese LLM Chatbot with Emotional Insight & Multimodal Support

**AI Muse** là một chatbot thông minh dựa trên Large Language Model (LLM), được tối ưu hóa cho tiếng Việt, kết hợp phân tích cảm xúc (sentiment analysis) và khả năng xử lý hình ảnh (multimodal) để hỗ trợ sáng tạo, tư vấn cảm xúc và gợi ý ý tưởng.

Dự án được xây dựng hoàn toàn trên **Google Colab** (dễ replicate), sử dụng kỹ thuật quantization 4-bit để chạy mô hình lớn trên GPU miễn phí.

## Mục tiêu dự án 

- Nghiên cứu & đánh giá các mô hình LLM hiện đại (Qwen2.5-Instruct) cho tiếng Việt.
- Xây dựng chatbot đa năng: chat text + upload ảnh → mô tả ảnh + phân tích cảm xúc + gợi ý sáng tạo.
- Đánh giá hiệu quả: tốc độ phản hồi, độ chính xác cảm xúc, khả năng tiết kiệm thời gian so với chat thủ công.
- Tài liệu hóa workflow, code sạch, dễ mở rộng → sẵn sàng chia sẻ cho team nghiệp vụ.
- Kết hợp GenAI tools (Hugging Face Transformers, Gradio) với prototype giao diện web đơn giản.

## Tính năng chính

- **Chatbot tiếng Việt thông minh** sử dụng Qwen2.5-1.5B-Instruct (quantized 4-bit) – nhanh, tiết kiệm VRAM (~2-3GB).
- **Phân tích cảm xúc thời gian thực** (dùng twitter-roberta-base-sentiment-latest) để phát hiện buồn/vui/stress → gợi ý an ủi hoặc ý tưởng phù hợp.
- **Hỗ trợ multimodal**: Upload ảnh → dùng BLIP/CLIP để mô tả + tích hợp vào cuộc trò chuyện.
- **Embedding ngữ nghĩa** (all-MiniLM-L6-v2) để so sánh ý tưởng cũ/mới, tránh lặp lại.
- **Giao diện Gradio** thân thiện: chat box + upload ảnh + lịch sử chat.
- **Lưu lịch sử chat** dưới dạng JSON để phân tích sau (đánh giá use case dài hạn).

## Công nghệ & Stack sử dụng

| Phần              | Công cụ / Thư viện                          | Mô tả                                                                 |
|-------------------|---------------------------------------------|-----------------------------------------------------------------------|
| LLM Core          | Qwen/Qwen2.5-1.5B-Instruct                  | Mô hình chính, quantized 4-bit (bitsandbytes)                         |
| Tokenizer         | Hugging Face Transformers                   | Xử lý token, pad token fix                                            |
| Multimodal        | BLIP (BlipForConditionalGeneration) + CLIP  | Mô tả ảnh & hiểu ngữ nghĩa hình ảnh                                   |
| Embedding         | sentence-transformers (all-MiniLM-L6-v2)    | Vector hóa câu để so sánh ý nghĩa                                     |
| Sentiment         | twitter-roberta-base-sentiment-latest       | Phân tích cảm xúc (positive/neutral/negative)                         |
| UI/Prototype      | Gradio                                      | Giao diện web nhanh, hỗ trợ chat + file upload                        |
| Optimization      | accelerate, bitsandbytes                    | Device map auto, 4-bit/8-bit quantization                             |
| Data/Utils        | torch, numpy, PIL, json, datetime           | Xử lý tensor, ảnh, lưu trữ                                            |

Yêu cầu phần cứng: GPU T4 (Colab free) hoặc tương đương.

## Cài đặt & Chạy local/Colab

1. Clone repo:
   ```bash
   git clone https://github.com/Suchisixx/muse.git
   cd muse

2. Cài dependencies (dùng requirements.txt): pip install -r requirements.txt
Hoặc chạy trực tiếp trong Colab:
!pip install -q torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
!pip install -q --upgrade transformers accelerate bitsandbytes gradio sentence-transformers pillow numpy
