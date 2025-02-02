Dưới đây là bảng phân tích chi tiết **input/output** và **nhiệm vụ của từng module** trong workflow của các mô hình **Stable Diffusion (SD)**, **ControlNet**, **DreamBooth**, **Kosmos-G** và **OmniGen**. Bạn có thể dùng thông tin này để vẽ sơ đồ module chính xác!

---

### **1. Stable Diffusion (SD)**
| **Module**          | **Input**                     | **Output**                    | **Nhiệm vụ**                                                                 |
|----------------------|-------------------------------|-------------------------------|------------------------------------------------------------------------------|
| **CLIP Text Encoder**| Văn bản (text prompt)         | Text Embeddings               | Mã hóa văn bản thành vector đặc trưng để điều khiển quá trình sinh ảnh.      |
| **U-Net**            | Text Embeddings + Noise       | Latent Features               | Khử nhiễu và sinh latent features từ text embeddings và nhiễu ban đầu.       |
| **VAE Decoder**      | Latent Features               | Ảnh (RGB)                     | Giải mã latent features thành ảnh RGB.                                      |

**Workflow**:  
`Text → CLIP Text Encoder → U-Net → VAE Decoder → Ảnh`

---

### **2. ControlNet**
| **Module**               | **Input**                     | **Output**                    | **Nhiệm vụ**                                                                 |
|--------------------------|-------------------------------|-------------------------------|------------------------------------------------------------------------------|
| **Condition Extractor**  | Ảnh gốc (pose/depth/seg)      | Điều kiện không gian (map)    | Trích xuất thông tin điều kiện (pose, depth, segmentation) từ ảnh đầu vào.   |
| **CLIP Text Encoder**    | Văn bản (text prompt)         | Text Embeddings               | Mã hóa văn bản thành vector đặc trưng.                                       |
| **ControlNet Plugin**    | Điều kiện không gian + Text   | Adjusted Latent Features      | Kết hợp điều kiện không gian với text embeddings để điều chỉnh latent.       |
| **U-Net**                | Adjusted Latent Features      | Latent Features               | Khử nhiễu và sinh latent features dựa trên điều kiện đã điều chỉnh.          |
| **VAE Decoder**          | Latent Features               | Ảnh (RGB)                     | Giải mã latent features thành ảnh RGB.                                      |

**Workflow**:  
`Ảnh → Condition Extractor → ControlNet Plugin → U-Net → VAE Decoder → Ảnh`  
`Text → CLIP Text Encoder → ControlNet Plugin`

---

### **3. DreamBooth**
| **Module**               | **Input**                     | **Output**                    | **Nhiệm vụ**                                                                 |
|--------------------------|-------------------------------|-------------------------------|------------------------------------------------------------------------------|
| **Data Preparation**     | Ảnh chủ đề (3–5 ảnh)          | Fine-tuning Dataset           | Chuẩn bị dữ liệu để fine-tuning mô hình trên chủ đề cụ thể.                   |
| **CLIP Text Encoder**    | Văn bản (text prompt)         | Text Embeddings               | Mã hóa văn bản thành vector đặc trưng.                                       |
| **Fine-Tuned U-Net**     | Text Embeddings + Noise       | Latent Features               | Khử nhiễu và sinh latent features đã được điều chỉnh cho chủ đề cụ thể.      |
| **VAE Decoder**          | Latent Features               | Ảnh (RGB)                     | Giải mã latent features thành ảnh RGB.                                      |

**Workflow**:  
`Text → CLIP Text Encoder → Fine-Tuned U-Net → VAE Decoder → Ảnh`

---

### **4. Kosmos-G**
| **Module**          | **Input**                     | **Output**                    | **Nhiệm vụ**                                                                 |
|----------------------|-------------------------------|-------------------------------|------------------------------------------------------------------------------|
| **CLIP Encoder**     | Văn bản + Ảnh                 | Multimodal Embeddings         | Mã hóa văn bản và ảnh thành vector đặc trưng chung.                          |
| **U-Net**            | Multimodal Embeddings + Noise | Latent Features               | Khử nhiễu và sinh latent features dựa trên đặc trưng đa phương thức.          |
| **VAE Decoder**      | Latent Features               | Ảnh (RGB)                     | Giải mã latent features thành ảnh RGB.                                      |

**Workflow**:  
`Text/Ảnh → CLIP Encoder → U-Net → VAE Decoder → Ảnh`

---

### **5. OmniGen**
| **Module**          | **Input**                     | **Output**                    | **Nhiệm vụ**                                                                 |
|----------------------|-------------------------------|-------------------------------|------------------------------------------------------------------------------|
| **Tokenizer**        | Văn bản (text prompt)         | Text Tokens                   | Token hóa văn bản thành chuỗi tokens.                                        |
| **VAE Encoder**      | Ảnh (điều kiện)               | Latent Vectors                | Mã hóa ảnh thành latent vectors.                                             |
| **Transformer**      | Text Tokens + Latent Vectors  | Adjusted Latent Features      | Xử lý kết hợp text và image tokens để sinh latent features.                  |
| **VAE Decoder**      | Adjusted Latent Features      | Ảnh (RGB)                     | Giải mã latent features thành ảnh RGB.                                      |

**Workflow**:  
`Text/Ảnh → Tokenizer/VAE Encoder → Transformer → VAE Decoder → Ảnh`

---

### **Bảng So Sánh Tổng Hợp**
| **Mô hình**       | **Số Module** | **Input**                     | **Output**        | **Phức Tạp** |
|--------------------|---------------|-------------------------------|-------------------|-------------|
| **Stable Diffusion** | 3            | Text/Image                    | Ảnh              | Trung bình  |
| **ControlNet**      | 5+           | Text + Image + Điều kiện      | Ảnh              | Cao         |
| **DreamBooth**      | 4            | Text + Ảnh chủ đề             | Ảnh              | Cao         |
| **Kosmos-G**        | 3            | Text + Image                  | Ảnh              | Trung bình  |
| **OmniGen**         | 4            | Text + Image (linh hoạt)      | Ảnh              | Thấp        |

---

### **Gợi ý Vẽ Module Diagram**
1. **Ký hiệu module**:
   - **Encoder/Decoder**: Hình chữ nhật bo góc.  
   - **Condition Extractor/Plugin**: Hình thoi.  
   - **Transformer/U-Net**: Hình tròn.  
2. **Mũi tên**:
   - Input → Module → Output: Mũi tên liền.  
   - Plugin/Adapter: Mũi tên đứt nét.  
3. **Màu sắc**:
   - Màu xanh dương: Module xử lý text.  
   - Màu xanh lá: Module xử lý ảnh.  
   - Màu cam: Module kết hợp đa phương thức.  

**Ví dụ sơ đồ ControlNet**:  
`[Ảnh] → (Condition Extractor) → [Pose Map] → (ControlNet Plugin) → [U-Net] → [VAE Decoder] → [Ảnh Output]`  
`[Text] → (CLIP Encoder) → [Text Embeddings] → (ControlNet Plugin)`

---

Hy vọng thông tin này giúp bạn vẽ sơ đồ module rõ ràng và chính xác! 😊