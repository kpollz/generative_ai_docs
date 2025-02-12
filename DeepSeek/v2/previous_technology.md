Dưới đây là bảng phân tích chi tiết về các kỹ thuật & công nghệ trong các mô hình trước (prior art), hạn chế của chúng, và cách DeepSeek-V2 cải tiến để khắc phục những yếu điểm này.


---

1. Các kỹ thuật và công nghệ trong các mô hình trước (Prior Art)


---

2. Cách DeepSeek-V2 cải tiến so với các mô hình trước


---

Tóm tắt điểm khác biệt của DeepSeek-V2 so với các SOTA trước đó:

1. Sử dụng DeepSeekMoE thay vì MoE thông thường → Giữ hiệu suất cao nhưng giảm chi phí tính toán.


2. Multi-Head Latent Attention (MLA) thay thế MHA/GQA/MQA → Giảm KV cache 93.3%, nhưng vẫn giữ hiệu suất cao.


3. Device-Limited Routing & Load Balance Losses → Giảm giao tiếp giữa các GPU, tránh bottleneck khi huấn luyện MoE.


4. Áp dụng YaRN với Decoupled RoPE → Hỗ trợ 128K tokens context length mà không làm chậm suy luận.


5. Kết hợp FlashAttention-2 & FP8 Precision → Tăng tốc độ sinh token lên 5.76 lần so với DeepSeek 67B.




---

DeepSeek-V2 không chỉ giữ lại những ưu điểm của các mô hình trước mà còn giải quyết những điểm yếu của chúng, giúp giảm chi phí huấn luyện, tăng tốc suy luận, và mở rộng ngữ cảnh. Nếu bạn cần phân tích chi tiết hơn một phần nào đó, hãy cho mình biết nhé!

