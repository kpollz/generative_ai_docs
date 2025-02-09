## 🐋 DeepSeek-V2


### 1. DeepSeek-V2 là gì?

- **DeepSeek-V2** là một mô hình ngôn ngữ lớn (Large Language Model – LLM) tiên tiến, được xây dựng theo kiến trúc **Mixture-of-Experts (MoE)**.
- Tổng số tham số của mô hình lên đến **236 tỷ (236B)**, nhưng chỉ kích hoạt **21 tỷ (21B)** tham số cho mỗi token trong quá trình suy diễn.
- Mô hình này được thiết kế với những cải tiến đột phá nhằm **giảm chi phí huấn luyện** và **tăng tốc quá trình suy diễn (inference)**, đồng thời hỗ trợ xử lý các ngữ cảnh dài lên đến **128K token**.

---

### 2. Mục tiêu và lĩnh vực ứng dụng của DeepSeek-V2

- **Bài toán trọng tâm:** Khi các mô hình LLM được mở rộng về số lượng tham số, hiệu năng thường cải thiện nhưng đi kèm với chi phí tính toán lớn (cả trong giai đoạn huấn luyện lẫn suy diễn). Đặc biệt, việc lưu trữ và xử lý bộ nhớ cache (Key-Value cache) trong quá trình suy diễn là một trong những nút thắt lớn.
- **DeepSeek-V2 ra đời để:**  
  - **Tiết kiệm chi phí huấn luyện:** Bằng cách chỉ kích hoạt một phần nhỏ các tham số (21B trên 236B tổng số) và sử dụng kiến trúc MoE hiệu quả.
  - **Tăng tốc suy diễn:** Thông qua việc giảm đáng kể kích thước bộ nhớ KV cache và tối ưu các phép tính liên quan đến attention.
  - **Hỗ trợ xử lý các ngữ cảnh cực dài:** Lên đến 128K tokens, mở rộng khả năng ứng dụng trong các tác vụ cần lưu giữ thông tin dài hạn.

---

### 3. Các stage-of-the-art trước DeepSeek-V2

Trước DeepSeek-V2, đã có một số mô hình và kỹ thuật nổi bật nhằm giải quyết các thách thức trong huấn luyện và suy diễn của LLM:

- **Các mô hình dense (đặc):**  
  - **LLaMA, LLaMA 2, LLaMA 3:** Những mô hình này tập trung vào việc tăng số lượng tham số để cải thiện hiệu năng, nhưng lại gặp hạn chế về chi phí tính toán và tốc độ suy diễn.
  
- **Các mô hình MoE khác:**  
  - **DeepSeek 67B:** Phiên bản trước của DeepSeek với kiến trúc MoE, đã cho thấy khả năng tiết kiệm chi phí huấn luyện so với mô hình dense.
  - **Mixtral, Qwen:** Các mô hình MoE và hybrid khác cũng đã thử nghiệm để tối ưu chi phí và tăng tốc suy diễn.
  
- **Các cải tiến trong cơ chế attention:**  
  - **Multi-Head Attention (MHA):** Phổ biến trong hầu hết các mô hình Transformer nhưng lại có bộ nhớ KV cache nặng.
  - **Multi-Query Attention (MQA) và Grouped-Query Attention (GQA):** Được phát triển nhằm giảm bớt kích thước KV cache nhưng thường đánh đổi phần nào về mặt hiệu năng.

---

### 4. Hạn chế của SOTA trước đó và điểm mới của DeepSeek-V2

#### Hạn chế của các phương pháp SOTA:
- **Chi phí huấn luyện cao:** Mô hình dense đòi hỏi tài nguyên tính toán lớn khi tăng số lượng tham số.
- **Bottleneck ở KV cache:** Các cơ chế attention như MHA cần phải lưu trữ một lượng lớn dữ liệu (keys và values) cho từng token, dẫn đến hiệu năng suy diễn thấp khi xử lý ngữ cảnh dài.
- **Khó mở rộng ngữ cảnh:** Các mô hình trước đây thường bị giới hạn bởi chiều dài ngữ cảnh xử lý, không hỗ trợ tốt các tác vụ đòi hỏi ngữ cảnh dài.

#### Điểm mới và giải pháp của DeepSeek-V2:
- **Multi-head Latent Attention (MLA):**  
  - Áp dụng kỹ thuật **low-rank key-value joint compression** để giảm kích thước KV cache xuống tới 93,3% so với MHA truyền thống.
  - Kết hợp với chiến lược **decoupled Rotary Position Embedding (RoPE)** giúp tách biệt phần chịu tác động của vị trí, từ đó tối ưu hóa quá trình suy diễn.
  
- **DeepSeekMoE:**  
  - Kiến trúc MoE với **phân đoạn chuyên môn (fine-grained expert segmentation)** và cơ chế **chia sẻ expert (shared expert isolation)** giúp mô hình huấn luyện với chi phí thấp hơn mà vẫn đạt hiệu năng cao.
  - Các cải tiến trong **device-limited routing** và các hàm mất mát phụ trợ (auxiliary losses) đảm bảo sự cân bằng tải và giảm thiểu overhead trong giao tiếp giữa các thiết bị.
  
- **Kết quả:**  
  - Tiết kiệm được khoảng **42,5% chi phí huấn luyện** so với phiên bản DeepSeek 67B.
  - Tốc độ suy diễn (throughput) được tăng lên tới **5.76 lần** so với DeepSeek 67B.
  - Hỗ trợ context lên đến 128K tokens, mở rộng khả năng ứng dụng trong các tác vụ cần lưu giữ thông tin dài hạn.

---

### 5. Tổng kết: Các cải tiến, hạn chế tồn đọng và hướng phát triển trong tương lai

#### Các cải tiến nổi bật:
- **Tiết kiệm chi phí huấn luyện:** Chỉ kích hoạt 21B tham số trong tổng số 236B, giúp giảm chi phí tính toán mà vẫn duy trì hiệu năng cao.
- **Tăng tốc suy diễn:** Nhờ vào kiến trúc MLA giúp giảm đáng kể kích thước KV cache và tối ưu hóa quá trình tính toán.
- **Hỗ trợ ngữ cảnh cực dài:** Có thể xử lý các tác vụ với context lên đến 128K tokens, mở rộng phạm vi ứng dụng.
- **Kiến trúc MoE tiên tiến (DeepSeekMoE):** Giúp huấn luyện hiệu quả hơn và khả năng chuyên môn hóa của các “expert” được cải thiện thông qua các cơ chế routing và cân bằng tải mới.

#### Hạn chế còn tồn đọng:
- **Độ phức tạp của kiến trúc:** Việc tích hợp các cơ chế MoE và các cải tiến trong attention có thể khiến quá trình triển khai và bảo trì trở nên phức tạp.
- **Cân bằng tải và giao tiếp giữa các expert:** Dù đã có các cơ chế giảm tải và cân bằng, nhưng việc tối ưu hoá giao tiếp giữa các thiết bị trong môi trường phân tán vẫn là một thách thức.
- **Khả năng ứng dụng đa ngôn ngữ:** Mặc dù đã hỗ trợ cả tiếng Anh và tiếng Trung, nhưng có thể cần cải thiện thêm để mở rộng sang các ngôn ngữ khác.

#### Hướng phát triển trong tương lai:
- **Tối ưu hóa kiến trúc MoE:** Nghiên cứu thêm các kỹ thuật mới để cải thiện sự cân bằng tải và giảm thiểu overhead giao tiếp giữa các expert.
- **Mở rộng khả năng đa ngôn ngữ:** Tăng cường dữ liệu huấn luyện và điều chỉnh kiến trúc để đáp ứng tốt hơn cho các ngôn ngữ ngoài tiếng Anh và tiếng Trung.
- **Cải tiến hiệu năng suy diễn:** Tìm kiếm các giải pháp phần cứng và thuật toán mới nhằm tối ưu hoá quá trình suy diễn, đặc biệt trong các ứng dụng thời gian thực.
- **Nghiên cứu hướng hợp nhất các kỹ thuật hiện có:** Kết hợp các cải tiến từ MLA, DeepSeekMoE với các tiến bộ mới trong lĩnh vực học sâu để tiếp tục nâng cao hiệu năng và khả năng ứng dụng của LLM.

---

## 🔍 APPENDIX

### 1. Giải thích sơ bộ về Multi-Query Attention (MQA) và Grouped-Query Attention (GQA)

Trong kiến trúc Transformer, **Multi-Head Attention (MHA)** truyền thống tính toán các vector truy vấn (query), khóa (key) và giá trị (value) riêng cho mỗi “đầu” (head). Điều này có nghĩa là đối với mỗi token, ta phải lưu trữ một bộ key và value riêng biệt cho từng head, dẫn đến việc bộ nhớ cache (KV cache) trở nên khá lớn, đặc biệt là khi số lượng head tăng lên.

**Multi-Query Attention (MQA):**
- **Ý tưởng chính:** Thay vì tính toán riêng biệt keys và values cho từng head, MQA sử dụng **một bộ key và value chung cho tất cả các head** trong attention.
- **Ưu điểm:** Giảm đáng kể kích thước của KV cache, vì chỉ cần lưu trữ một bộ key và value duy nhất cho mỗi token.
- **Nhược điểm:** Việc chia sẻ chung keys và values có thể làm mất đi tính đa dạng mà mỗi head riêng lẻ mang lại, dẫn đến một chút giảm hiệu năng (khả năng biểu diễn thông tin có thể không phong phú như khi có keys/values riêng cho mỗi head).

**Grouped-Query Attention (GQA):**
- **Ý tưởng chính:** GQA là một giải pháp trung gian giữa MHA và MQA. Ở đây, các head được **chia thành các nhóm** và trong mỗi nhóm, các head sẽ chia sẻ một bộ key và value chung.
- **Ưu điểm:** So với MHA, GQA vẫn giảm được kích thước của KV cache (vì không phải mỗi head đều có riêng một bộ key và value) nhưng đồng thời vẫn cho phép duy trì một phần tính đa dạng bằng cách không chia sẻ chung giữa tất cả các head.
- **Nhược điểm:** Mặc dù giảm kích thước cache, việc chia sẻ này vẫn có thể làm mất đi một phần khả năng mô hình hóa các mối quan hệ phức tạp giữa các token so với MHA truyền thống – do đó, hiệu năng có thể không bằng MHA nhưng lại tốt hơn MQA.

Tóm lại, cả MQA và GQA đều được phát triển với mục tiêu **giảm bớt bộ nhớ lưu trữ KV cache** trong quá trình suy diễn, nhưng điều này có thể đi kèm với một sự đánh đổi về mặt hiệu năng biểu diễn so với cách tính truyền thống của MHA, vốn cho mỗi head một bộ key và value riêng biệt.

---

### 2. So sánh chi tiết giữa LLM dựa trên MoE và Dense

Theo kiến thức hiện nay, các mô hình LLM chủ yếu có hai loại kiến trúc:

- **Dense (đặc):**  
  - Tất cả các tham số của mô hình đều được kích hoạt và sử dụng trong quá trình huấn luyện và suy diễn.
  - Ưu điểm: Đơn giản, hiệu năng ổn định và thường cho kết quả biểu diễn tốt.
  - Nhược điểm: Khi mô hình có số lượng tham số rất lớn, chi phí tính toán và bộ nhớ cũng tăng đáng kể.

- **MoE (Mixture-of-Experts – hỗn hợp chuyên gia):**  
  - Mô hình có rất nhiều “expert” (nhóm con) nhưng chỉ một số nhỏ được kích hoạt cho mỗi token. Ví dụ, một mô hình có tổng 236B tham số nhưng chỉ kích hoạt khoảng 21B tham số cho mỗi token.
  - Ưu điểm: Giảm chi phí tính toán và bộ nhớ (vì chỉ một phần nhỏ tham số được sử dụng mỗi lần) mà vẫn duy trì được hiệu năng cao nhờ vào khả năng chuyên môn hóa của từng expert.
  - Nhược điểm: Kiến trúc phức tạp hơn, đòi hỏi các cơ chế routing và cân bằng tải giữa các expert; việc triển khai và tối ưu hóa giao tiếp giữa các thiết bị phân tán có thể gặp thách thức.

Dưới đây là một bảng so sánh minh họa giữa một số mô hình LLM dựa trên Dense và MoE:

| **Model**                | **Kiểu kiến trúc** | **Tổng số tham số** | **Tham số kích hoạt** | **Ghi chú**                                      |
|--------------------------|--------------------|---------------------|-----------------------|--------------------------------------------------|
| **Dense Models**         |                    |                     |                       |                                                  |
| GPT-3                    | Dense              | 175B                | 175B                  | Mô hình dense truyền thống                       |
| LLaMA 2                  | Dense              | 70B                 | 70B                   | Dense, được tối ưu cho hiệu năng tốt             |
| LLaMA 3                  | Dense              | 70B                 | 70B                   | Dense, phiên bản mới với cải tiến                  |
| Qwen1.5                  | Dense              | 72B                 | 72B                   | Dense, hỗ trợ đa ngôn ngữ                          |
| DeepSeek 67B             | Dense              | 67B                 | 67B                   | Phiên bản dense của DeepSeek (trước DeepSeek-V2)   |
|                          |                    |                     |                       |                                                  |
| **MoE Models**           |                    |                     |                       |                                                  |
| Switch Transformer       | MoE                | ~1.6T               | Chỉ kích hoạt ~1/16 tổng (sparse) | Mô hình MoE của Google, với số lượng expert rất lớn    |
| GLaM                     | MoE                | ~1.2T               | Khoảng 100B (kích hoạt thưa) | Mô hình MoE của Google, sử dụng kích hoạt thưa          |
| Mixtral 8x22B            | MoE                | ~141B               | 39B                   | MoE, sử dụng 8 expert, kích hoạt một số expert nhất định|
| DeepSeek-V2              | MoE                | 236B                | 21B                   | MoE tiên tiến, tích hợp các cải tiến như MLA & DeepSeekMoE  |

---

### Tóm tắt

- **Dense LLM:**  
  - Sử dụng toàn bộ tham số cho mỗi token.  
  - Ví dụ: GPT-3, LLaMA 2, LLaMA 3, Qwen1.5, DeepSeek 67B.

- **MoE LLM:**  
  - Chỉ kích hoạt một phần nhỏ các expert (với tổng số tham số lớn) cho mỗi token, giúp tiết kiệm chi phí tính toán và bộ nhớ.  
  - Ví dụ: Switch Transformer, GLaM, Mixtral 8x22B, DeepSeek-V2.
