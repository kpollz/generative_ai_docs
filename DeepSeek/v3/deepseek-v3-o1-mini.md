## 🐋 DeepSeek-V3

### 1. DeepSeek-V3 là gì?  
- **DeepSeek-V3** là một mô hình ngôn ngữ quy mô lớn (Large Language Model) dựa trên kiến trúc **Mixture-of-Experts (MoE)**.  
- Tổng số tham số của mô hình đạt khoảng **671 tỷ**, tuy nhiên chỉ **37 tỷ tham số được kích hoạt** cho mỗi token, giúp tiết kiệm tài nguyên khi xử lý.  
- Mô hình được phát triển bởi DeepSeek-AI như một bước tiến so với các phiên bản trước như DeepSeek-V2 và DeepSeek-V2.5, nhằm đạt được hiệu năng cao và chi phí huấn luyện thấp.

---

### 2. DeepSeek-V3 sinh ra nhằm giải quyết bài toán gì? Lĩnh vực của nó là gì?  
- **Lĩnh vực ứng dụng:** DeepSeek-V3 thuộc lĩnh vực xử lý ngôn ngữ tự nhiên (Natural Language Processing – NLP) và trí tuệ nhân tạo (AI).  
- **Bài toán chính:**  
  - **Cải thiện khả năng sinh văn bản tự nhiên:** Hỗ trợ các ứng dụng như hội thoại, trả lời câu hỏi, tóm tắt, và sáng tạo nội dung.  
  - **Giải quyết các tác vụ chuyên sâu:** Bao gồm toán học, lập trình, suy luận logic, và các bài toán kỹ thuật (ví dụ như coding competitions, benchmarks về kiến thức, lập trình và kỹ thuật phần mềm).  
- **Mục tiêu:**  
  - Thu hẹp khoảng cách về hiệu năng giữa các mô hình mã nguồn mở và các mô hình mã nguồn đóng như GPT-4 hay Claude-3.5.  
  - Tối ưu hóa chi phí huấn luyện và inference thông qua các kỹ thuật tiên tiến.

---

### 3. Trước khi DeepSeek-V3 ra thì đã có những stage-of-the-art nào giải quyết bài toán đó?  
- **Các mô hình mã nguồn mở:**
  - **LLaMA (Meta):** Một trong những mô hình ngôn ngữ mạnh mẽ, được sử dụng rộng rãi nhưng không sử dụng kiến trúc MoE.
  - **Qwen và Mistral:** Các mô hình khác tập trung vào hiệu suất inference và tối ưu chi phí.
- **Các mô hình mã nguồn đóng:**
  - **GPT-4o (OpenAI):** Đạt hiệu năng rất cao trong nhiều tác vụ, nhưng chi phí và quyền truy cập bị giới hạn.
  - **Claude-3.5 (Anthropic):** Nổi bật về khả năng tư duy và logic, được ứng dụng trong nhiều tình huống phức tạp.
- Những mô hình này đã đạt đến một mức độ "state-of-the-art" (SOTA) nhưng thường đi kèm với các hạn chế về chi phí, khả năng mở rộng hoặc hiệu suất trên một số tác vụ chuyên biệt.

---

### 4. Những hạn chế của SOTA là gì và DeepSeek-V3 giải quyết như thế nào? (Những điểm mới của DeepSeek-V3 là gì?)  
**Hạn chế của các SOTA trước:**
- **Chi phí huấn luyện và inference cao:** Các mô hình với số tham số khổng lồ đòi hỏi tài nguyên tính toán lớn.
- **Quá trình routing và load balance trong kiến trúc MoE:** Các mô hình MoE thường gặp vấn đề về mất cân bằng tải giữa các expert, dẫn đến hiệu năng không tối ưu.
- **Hiệu suất xử lý:** Một số mô hình mã nguồn mở chưa đạt được chất lượng ngôn ngữ, khả năng suy luận và chuyên môn (toán học, lập trình) như các mô hình mã nguồn đóng.

**Cách DeepSeek-V3 giải quyết:**
- **Kiến trúc MoE thông minh:**  
  - **Chỉ kích hoạt 37 tỷ tham số trên 671 tỷ**, giúp tiết kiệm chi phí tính toán và bộ nhớ.
  - Áp dụng chiến lược **"Auxiliary-Loss-Free Load Balancing"**: Cập nhật động bias cho mỗi expert để cân bằng tải mà không phụ thuộc vào các auxiliary loss làm giảm hiệu năng.
- **Cải tiến trong kiến trúc attention:**  
  - **Multi-Head Latent Attention (MLA)** giảm kích thước bộ nhớ cache cho keys và values trong quá trình inference mà vẫn duy trì chất lượng.
- **Mục tiêu dự đoán đa token:**  
  - **Multi-Token Prediction (MTP)** giúp tăng mật độ tín hiệu huấn luyện, cải thiện khả năng dự đoán các token tiếp theo và có thể dùng cho việc dự đoán sơ bộ (speculative decoding) nhằm tăng tốc độ inference.
- **Tối ưu hóa huấn luyện:**  
  - **FP8 mixed precision training:** Sử dụng định dạng số FP8 cho các phép tính chính nhằm giảm bộ nhớ và tăng tốc độ mà vẫn đảm bảo độ chính xác trong huấn luyện.
  - **DualPipe và các chiến lược giao tiếp (all-to-all communication) hiệu quả:** Giảm bottleneck khi huấn luyện trên cụm GPU lớn.

---

### 5. Tổng kết: Các cải tiến, hạn chế còn tồn đọng và hướng phát triển về sau  
**Các cải tiến chính của DeepSeek-V3:**
- **Tiết kiệm tài nguyên tính toán:** Mô hình kích hoạt chỉ 37 tỷ tham số trong tổng số 671 tỷ thông qua kiến trúc MoE.
- **Cân bằng tải hiệu quả:** Chiến lược Auxiliary-Loss-Free giúp giảm thiểu sự mất cân bằng trong các expert.
- **Tăng tốc độ inference:** Qua MLA và Multi-Token Prediction, mô hình đạt được tốc độ và hiệu suất cao.
- **Tiết kiệm bộ nhớ và tăng tốc huấn luyện:** FP8 mixed precision training giúp giảm chi phí GPU và thời gian huấn luyện.

**Hạn chế còn tồn đọng:**
- **Độ phức tạp của hệ thống:** Yêu cầu cụm GPU lớn và hạ tầng phần cứng mạnh mẽ để triển khai hiệu quả.
- **Chưa đạt mức hoàn hảo ở một số tác vụ chuyên sâu:** Mặc dù đã tiến gần, nhưng DeepSeek-V3 vẫn cần cải thiện thêm về khả năng suy luận logic và chuyên sâu trong một số lĩnh vực (ví dụ: các bài toán mở hoặc ứng dụng thực tế yêu cầu tính chính xác cao).
- **Thách thức trong tối ưu hóa trên nhiều hạ tầng khác nhau:** Các chiến lược giao tiếp và phân bổ tài nguyên còn đòi hỏi nghiên cứu sâu hơn để áp dụng trên các hệ thống đa dạng.

**Hướng phát triển trong tương lai:**
- **Cải thiện khả năng suy luận và tư duy dài hạn:** Nâng cao chất lượng đầu ra trong các tác vụ đòi hỏi logic và reasoning phức tạp.
- **Tối ưu hóa hạ tầng inference:** Giảm độ trễ và cải thiện tốc độ phản hồi cho các ứng dụng thời gian thực.
- **Ứng dụng đa dạng lĩnh vực:** Mở rộng mô hình sang các bài toán chuyên ngành như y tế, khoa học và kỹ thuật, kết hợp thêm các kỹ thuật huấn luyện mới.
- **Nghiên cứu tiếp các chiến lược giảm chi phí:** Phát triển các giải pháp huấn luyện và inference có hiệu năng cao nhưng chi phí thấp hơn để áp dụng rộng rãi.

---


## 🔍 APPENDIX

## 1. Quá trình Routing và Load Balance trong kiến trúc MoE của DeepSeek‑V3

### **a. Kiến trúc MoE cơ bản trong DeepSeek‑V3:**
- **Mixture-of-Experts (MoE):**  
  - Mô hình MoE gồm nhiều “expert” (các mạng con chuyên biệt) và một “router” để quyết định gửi token đầu vào đến những expert nào.
  - Trong DeepSeek‑V3, có hai nhóm expert:  
    - **Shared Experts:** Các expert được sử dụng chung cho tất cả token.  
    - **Routed Experts:** Các expert mà token được chọn theo quá trình routing dựa trên “affinity” (độ tương đồng) giữa token và centroid của expert.

- **Quá trình tính toán đầu vào cho mỗi expert:**  
  - Với mỗi token, ta tính được một **affinity score** (điểm tương đồng) giữa vector đặc trưng của token (uₜ) và centroid của expert (eᵢ) thông qua hàm Sigmoid, tức:  
  $$s_{i,t} = \text{Sigmoid}(u_t^T e_i)$$

  - Sau đó, các token chỉ được gửi đến **K₍ᵣ₎** expert có điểm số cao nhất (thông qua hàm Top‑K).

### **b. Vấn đề Load Balance truyền thống và giải pháp của DeepSeek‑V3:**
- **Vấn đề load imbalance:**  
  - Trong các kiến trúc MoE trước đây, nếu quá trình routing không được cân bằng, một số expert sẽ bị “quá tải” trong khi một số khác lại “ít được sử dụng”, dẫn đến giảm hiệu năng tính toán và chất lượng mô hình.
  - Một số giải pháp truyền thống dùng **auxiliary loss** để ép buộc cân bằng, nhưng việc thêm loss phụ này có thể làm giảm hiệu suất tổng thể của mô hình.

- **Giải pháp “Auxiliary‑Loss‑Free Load Balancing”:**  
  - **Giới thiệu Bias Term:** DeepSeek‑V3 thêm một **bias term $(b_i)$** cho mỗi expert vào quá trình tính toán điểm số, theo công thức:
    $$
    g'_{i,t} = 
    \begin{cases}
    s_{i,t} & \text{nếu } s_{i,t} + b_i \text{ thuộc Top‑K của } \{s_{j,t} + b_j\} \\
    0 & \text{ngược lại}
    \end{cases}
    $$
  - **Quá trình cập nhật động:**  
    - Sau mỗi bước training, hệ thống sẽ **điều chỉnh bias $(b_i)$** dựa trên tải thực tế của từng expert:
      - Nếu một expert bị **quá tải**, bias của nó sẽ được **giảm** đi một hằng số γ.
      - Nếu expert đó bị **ít tải**, bias sẽ được **tăng** lên.
  - **Lợi ích:**  
    - Phương pháp này không cần thêm một auxiliary loss riêng biệt, nhờ đó tránh được việc làm “nhiễu” tín hiệu học của mô hình.
    - Đảm bảo mỗi expert nhận được số lượng token cân đối, tối ưu hiệu năng tính toán cũng như chất lượng đầu ra của mô hình.

---

## 2. Multi‑Token Prediction (MTP)

### **a. Ý tưởng chính của MTP:**
- **Mục tiêu:**  
  - Thay vì chỉ dự đoán **token tiếp theo** (next-token prediction) theo cách truyền thống, mô hình được huấn luyện dự đoán **nhiều token trong tương lai** cùng lúc.
  - Việc dự đoán đa token giúp “dày đặc” tín hiệu huấn luyện, cải thiện tính hiệu quả của dữ liệu và cho phép mô hình “lên kế hoạch” trước cho chuỗi ngữ cảnh dài.

### **b. Cách thức thực hiện trong DeepSeek‑V3:**
- **Kiến trúc MTP Module:**  
  - Mô hình tích hợp **D module MTP** được sắp xếp theo thứ tự tuần tự.
  - Mỗi module MTP bao gồm các thành phần:  
    - **Embedding layer:** Chia sẻ với mô hình chính.
    - **Transformer block (TRMₖ):** Xử lý thông tin ở mỗi độ sâu dự đoán.
    - **Projection matrix $(M_k)$:** Dùng để kết hợp thông tin giữa biểu diễn của token hiện tại và embedding của token mục tiêu ở độ sâu tiếp theo.
    - **Output head:** Chia sẻ với mô hình chính để chuyển đổi biểu diễn thành logits (sau đó qua Softmax để ra xác suất).

- **Quá trình dự đoán:**  
  - Với token thứ $(t_i)$, ở độ sâu dự đoán thứ $(k)$:
    1. **Kết hợp biểu diễn:**  
       - Lấy biểu diễn của token $(t_i)$ ở độ sâu $(k-1)$ (đối với $(k=1)$, sử dụng biểu diễn từ mô hình chính).
       - Lấy embedding của token thứ $(t_{i+k})$ (token mục tiêu).
       - Kết hợp hai thông tin này qua phép nhân với $(M_k)$ sau khi đưa qua RMSNorm.
       - Công thức:  
         $$
         h'_{k,i} = M_k\Big[ \text{RMSNorm}(h_{k-1,i});\, \text{RMSNorm}(\text{Emb}(t_{i+k})) \Big]
         $$
    2. **Transformer block:**  
       - Xử lý $(h'_{k,i})$ qua block TRMₖ để ra biểu diễn $(h_{k,i})$.
    3. **Output head:**  
       - Dùng $(h_{k,i})$ để dự đoán token thứ $(t_{i+k+1})$ thông qua phân phối xác suất (Softmax).
  - **Loss:**  
    - Với mỗi module MTP, tính **cross-entropy loss** giữa dự đoán và token mục tiêu.
    - Cuối cùng, trung bình các loss này (có thể nhân với hệ số λ) tạo thành một mục tiêu huấn luyện bổ sung cho mô hình.

### **c. Lợi ích của MTP:**
- **Tăng cường tín hiệu học:** Dự đoán nhiều token cùng lúc giúp mô hình học được mối liên hệ dài hạn trong ngữ cảnh.
- **Cải thiện khả năng “lên kế hoạch”:** Mô hình không chỉ dựa vào thông tin ngay trước đó mà còn học cách dự đoán các phần tiếp theo của câu, cải thiện sự mạch lạc và tính tự nhiên của văn bản.
- **Có thể áp dụng cho speculative decoding:** Trong inference, MTP có thể được dùng để dự đoán sơ bộ nhiều token nhằm tăng tốc quá trình sinh văn bản.

---

## 3. DualPipe và các chiến lược giao tiếp (All-to-All Communication)

### **a. Vấn đề trong huấn luyện mô hình phân tán:**
- Khi mô hình rất lớn và chạy trên nhiều GPU (đặc biệt là với expert parallelism trong kiến trúc MoE), **giao tiếp dữ liệu giữa các GPU** (đặc biệt là giữa các node) trở thành một điểm nghẽn nghiêm trọng.
- Tỷ lệ **computation-to-communication** có thể giảm, dẫn đến thời gian chờ đợi (pipeline bubbles) và giảm hiệu suất huấn luyện.

### **b. DualPipe – Giải pháp pipeline parallelism nâng cao:**
- **DualPipe** là một thuật toán sắp xếp pipeline được thiết kế để **chồng lấn (overlap)** các giai đoạn tính toán (computation) và giao tiếp (communication) một cách hiệu quả.
- **Phân chia chunk:**  
  - Mỗi micro-batch (chunk) được chia thành bốn phần:  
    1. **Attention:** Xử lý cơ bản của transformer.
    2. **All-to-all dispatch:** Gửi token từ GPU này sang các GPU khác dựa trên quyết định routing.
    3. **MLP (Feed-Forward Network):** Xử lý thông qua các expert.
    4. **All-to-all combine:** Gom các kết quả từ các GPU về.
  - Trong quá trình backward, các phần như **backward for input** và **backward for weights** cũng được tách riêng.

- **Chồng lấn computation và communication:**  
  - DualPipe sắp xếp lại thứ tự thực hiện sao cho trong khi một phần của micro-batch đang tính toán, các giao tiếp dữ liệu (như all-to-all) của một micro-batch khác được thực hiện song song.
  - Điều này giúp “ẩn” thời gian giao tiếp, làm giảm tối đa các khoảng trống (pipeline bubbles) – tức là thời gian chờ không cần thiết giữa các bước xử lý.

### **c. Chiến lược giao tiếp (All-to-All Communication) tối ưu:**
- **Giao tiếp giữa các node:**  
  - DeepSeek‑V3 sử dụng **InfiniBand (IB)** để giao tiếp giữa các node, kết hợp với **NVLink** cho giao tiếp nội bộ trong một node.
  - Các kernel giao tiếp (dispatch và combine) được tối ưu hóa để sử dụng tối đa băng thông của IB và NVLink.
- **Giới hạn số node tham gia:**  
  - Mỗi token được giới hạn gửi đến tối đa một số node nhất định (ví dụ: 4 node) nhằm giảm lưu lượng giao tiếp qua IB.
- **Kỹ thuật “warp specialization”:**  
  - Trong GPU, các “warp” (nhóm các luồng xử lý) được chuyên dụng cho các tác vụ giao tiếp (ví dụ: gửi/nhận dữ liệu) và được điều chỉnh động theo tải công việc.
- **Kết quả:**  
  - Với DualPipe và các chiến lược giao tiếp được cải tiến, hầu hết thời gian giao tiếp có thể được “ẩn” sau thời gian tính toán, từ đó giảm đáng kể độ trễ và tối ưu hóa hiệu suất huấn luyện trên cụm GPU lớn.

---

## **Tóm lại:**
- **Routing và Load Balance trong MoE:**  
  - DeepSeek‑V3 sử dụng một cơ chế điều chỉnh bias động (không cần auxiliary loss) để đảm bảo rằng mỗi expert nhận được số lượng token hợp lý, giúp tối ưu hóa hiệu năng mà không gây nhiễu vào tín hiệu học.
  
- **Multi-Token Prediction (MTP):**  
  - MTP giúp mô hình dự đoán nhiều token trong tương lai một cách tuần tự, từ đó tăng cường tín hiệu huấn luyện và cải thiện khả năng “lên kế hoạch” của mô hình trong việc sinh văn bản.

- **DualPipe và các chiến lược giao tiếp:**  
  - DualPipe là một thuật toán pipeline parallelism tiên tiến, cho phép chồng lấn tính toán và giao tiếp, kết hợp với các kernel giao tiếp được tối ưu (all-to-all dispatch/combine) để giảm thiểu thời gian chờ, giúp mô hình mở rộng trên cụm GPU hiệu quả hơn.

Những cải tiến này góp phần giúp DeepSeek‑V3 tiết kiệm tài nguyên, tăng tốc độ huấn luyện và cải thiện chất lượng đầu ra, từ đó tạo nên một mô hình ngôn ngữ quy mô lớn với hiệu suất vượt trội so với các giải pháp trước đó.