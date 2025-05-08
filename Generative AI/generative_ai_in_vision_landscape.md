# Tổng quan về Generative AI trong Vision

Dưới đây sẽ làm trình bày chi tiết hiện trạng các bài toán trong lĩnh vực Generative AI in Vision dưới hai góc nhìn:

- **Nghiệp vụ, bài toán**: Được định nghĩa theo đầu ra và đầu vào của thuật toán, bao gồm hai bài toán chính Image Generation và Video Generation.
- **Kỹ thuật tăng cường**: Được định nghĩa theo các nhóm kỹ thuật giúp tăng cường hiệu suất của các tác vụ sinh như *Triển khai thiết bị biên*, *Giảm thời gian suy luận*, *Giảm kích thước mô hình*, *Tăng cường chất lượng sinh*,...

Đồng thời nêu ra một số ví dụ về tiềm năng nghiên cứu trong lĩnh vực này. Chi tiết mục lục của báo cao như sau:

- [Tổng quan về Generative AI trong Vision](#tổng-quan-về-generative-ai-trong-vision)
  - [1. Nghiệp vụ, bài toán](#1-nghiệp-vụ-bài-toán)
    - [1.1. Image Generation](#11-image-generation)
      - [A. Text-to-Image](#a-text-to-image)
      - [B. Image-to-Image](#b-image-to-image)
      - [C. Multimodal-to-Image](#c-multimodal-to-image)
    - [1.2. Video Generation](#12-video-generation)
      - [A. Text-to-Video](#a-text-to-video)
      - [B. Video-to-Video](#b-video-to-video)
      - [C. Multimodal-to-Video](#c-multimodal-to-video)
      - [D. Các bài toán đặc thù của Video Generation](#d-các-bài-toán-đặc-thù-của-video-generation)
  - [2. Kỹ thuật tăng cường](#2-kỹ-thuật-tăng-cường)
    - [2.1. Tối ưu mô hình để triển khai trên thiết bị biên](#21-tối-ưu-mô-hình-để-triển-khai-trên-thiết-bị-biên)
    - [2.2. Tối ưu khả năng sinh sát với prompt hay condition đầu vào](#22-tối-ưu-khả-năng-sinh-sát-với-prompt-hay-condition-đầu-vào)
    - [2.3. Tối ưu hiệu quả sinh, chất lượng đầu ra của mô hình](#23-tối-ưu-hiệu-quả-sinh-chất-lượng-đầu-ra-của-mô-hình)
    - [2.4. Cải thiện kiến trúc mô hình](#24-cải-thiện-kiến-trúc-mô-hình)
    - [2.5. Kỹ thuật huấn luyện](#25-kỹ-thuật-huấn-luyện)
    - [2.6. Khả năng mở rộng](#26-khả-năng-mở-rộng)
    - [2.7. Tính kiểm soát và khả năng diễn giải](#27-tính-kiểm-soát-và-khả-năng-diễn-giải)
    - [2.8. Xử lý vấn đề đạo đức](#28-xử-lý-vấn-đề-đạo-đức)
  - [3. Hướng nghiên cứu tiềm năng trong Generative AI cho Vision](#3-hướng-nghiên-cứu-tiềm-năng-trong-generative-ai-cho-vision)
    - [3.1. Nghiên cứu học thuật (Publish Paper)](#31-nghiên-cứu-học-thuật-publish-paper)
      - [A. Mô hình đa nhiệm cho Image và Video Generation](#a-mô-hình-đa-nhiệm-cho-image-và-video-generation)
      - [B. Học không giám sát cho Video Generation](#b-học-không-giám-sát-cho-video-generation)
      - [C. Kiểm soát chi tiết trong Conditional Video Generation](#c-kiểm-soát-chi-tiết-trong-conditional-video-generation)
      - [D. Phát hiện deepfake trong Video Generation](#d-phát-hiện-deepfake-trong-video-generation)
    - [3.2. Nghiên cứu sáng chế (Patent)](#32-nghiên-cứu-sáng-chế-patent)
      - [A. Mô hình Generative AI nhẹ cho thiết bị biên](#a-mô-hình-generative-ai-nhẹ-cho-thiết-bị-biên)
      - [B. Hệ thống sinh video tương tác thời gian thực](#b-hệ-thống-sinh-video-tương-tác-thời-gian-thực)
      - [C. Công cụ chỉnh sửa video dựa trên AI với giao diện trực quan](#c-công-cụ-chỉnh-sửa-video-dựa-trên-ai-với-giao-diện-trực-quan)

## 1. Nghiệp vụ, bài toán

### 1.1. Image Generation

#### A. Text-to-Image

- **Định nghĩa**: Tạo ra hình ảnh từ mô tả văn bản, ví dụ: "một ngôi nhà gỗ bên hồ nước". Mục tiêu là tạo ra hình ảnh chân thực, phù hợp với mô tả.
- **Kỹ thuật**:
  - **GANs**: Sử dụng generator và discriminator để tạo ảnh, như trong DALL-E.
  - **VAEs**: Mã hóa văn bản và ảnh vào không gian ẩn để tái tạo.
  - **Diffusion Models**: Hiện là phương pháp chủ đạo, sử dụng quá trình khử nhiễu để tạo ảnh chất lượng cao, như trong Stable Diffusion.
  - **Language-Vision Models**: Kết hợp mô hình ngôn ngữ (như CLIP) để hiểu văn bản và hướng dẫn quá trình sinh.
- **SOTA**:
  - **Stable Diffusion** ([Stable Diffusion](https://www.stability.ai/stable-diffusion)): Mô hình mã nguồn mở, được sử dụng rộng rãi nhờ hiệu quả và chất lượng.
  - **DALL-E 3** ([DALL-E](https://openai.com/dall-e)): Cải tiến từ DALL-E 2, với khả năng hiểu prompt phức tạp.
  - **Imagen** ([Imagen](https://cloud.google.com/blog/products/ai-machine-learning/imagen-2)): Mô hình của Google, nổi bật với độ chân thực.
  - **FLUX.1** ([FLUX.1](https://blackforestlabs.ai/)): Mô hình mới từ Black Forest Labs, được đánh giá cao về chi tiết và tuân thủ prompt.
- **Thách thức**:
  - **Độ chính xác với prompt**: Mô hình có thể bỏ qua các chi tiết trong mô tả phức tạp.
  - **Xử lý cảnh phức tạp**: Khó tạo ra các cảnh có nhiều đối tượng hoặc tương tác phức tạp.
  - **Tính chân thực**: Một số hình ảnh vẫn có artifacts hoặc thiếu tính tự nhiên.
  - **Chi phí tính toán**: Huấn luyện và sinh ảnh đòi hỏi tài nguyên lớn.
- **Cơ hội**:
  - Cải thiện hiểu biết đa phương thức để xử lý các prompt phức tạp hơn.
  - Ứng dụng trong thiết kế, quảng cáo, và giáo dục.
  - Tích hợp với các công cụ sáng tạo để hỗ trợ người dùng không chuyên.
  - Kiểm soát chi tiết hơn quá trình sinh, như điều chỉnh phong cách hoặc bố cục.
  - Sinh ảnh theo thời gian thực để sử dụng trong ứng dụng tương tác.
  - Tăng độ phân giải và chất lượng để đáp ứng nhu cầu chuyên nghiệp.

#### B. Image-to-Image

- **Định nghĩa**: Chuyển đổi hay sinh ảnh từ ảnh đầu vào là các tác vụ liên quan đến việc khôi phục, nâng cấp độ phân giải hay chỉnh sửa ảnh.
- **Bài toán con**:
  - **Super-Resolution**: Tăng độ phân giải hình ảnh từ thấp lên cao, ví dụ: từ 64x64 lên 256x256 pixel, nhằm khôi phục chi tiết và cấu trúc.
    - **Kỹ thuật**:
      - **CNNs**: Các mạng tích chập học ánh xạ từ ảnh độ phân giải thấp sang cao, như SRCNN.
      - **GANs**: Sử dụng adversarial loss để tạo ảnh chân thực, như SRGAN, ESRGAN.
      - **Transformer-based Models**: Sử dụng attention để xử lý đặc trưng toàn cục, như SwinIR.
      - **Mamba-based Models**: Kết hợp Mamba state-space model để khai thác phụ thuộc dài hạn, như MambaSR.
    - **SOTA**:
      - **MambaSR** ([MambaSR Paper](https://ideas.repec.org/a/gam/jmathe/v12y2024i15p2370-d1445987.html)): Đạt hiệu suất vượt trội trên Urban100 (PSNR cao hơn MetaSR 0.93 dB) và Manga109, hỗ trợ siêu phân giải ở mọi tỷ lệ.
      - **DRCT-L** ([DRCT Paper](https://arxiv.org/abs/2404.00722)): Sử dụng kết nối dư dày đặc trong Transformer, đạt SOTA trên Set14 x4 upscaling.
      - **SwinIR**: Vẫn là chuẩn mực nhờ hiệu suất ổn định trên các bộ dữ liệu như Set5, Set14.
    - **Thách thức**:
      - **Xử lý suy giảm thực tế**: Hầu hết mô hình được huấn luyện trên suy giảm bicubic, nhưng ảnh thực tế có nhiễu, mờ, hoặc nén JPEG.
      - **Tính tổng quát hóa**: Mô hình huấn luyện trên một loại hình ảnh (như khuôn mặt) thường không hoạt động tốt trên các loại khác (như cảnh quan).
      - **Hiệu quả tính toán**: Các mô hình như MambaSR yêu cầu tài nguyên lớn, khó triển khai trên thiết bị biên.
      - **Chất lượng cảm quan**: Tối ưu PSNR thường dẫn đến ảnh thiếu tự nhiên, trong khi tối ưu cảm quan có thể làm mất chi tiết.
      - **Siêu phân giải tỷ lệ bất kỳ**: Hầu hết mô hình chỉ hỗ trợ các tỷ lệ cố định (2x, 4x).
    - **Cơ hội**:
      - **Mô hình xử lý đa suy giảm**: Phát triển mô hình có thể xử lý nhiễu, mờ, và nén đồng thời, ví dụ: kết hợp Mamba với các mô hình vật lý của suy giảm ([Image Super-Resolution Review](https://www.digitalocean.com/community/tutorials/image-super-resolution)).
      - **Học không giám sát**: Sử dụng dữ liệu không ghép đôi để cải thiện tổng quát hóa, như trong các phương pháp tự giám sát.
      - **Kiến trúc nhẹ**: Thiết kế mô hình hiệu quả hơn, như kết hợp Mamba với quantization hoặc pruning, để triển khai trên thiết bị biên.
      - **Tối ưu cảm quan**: Phát triển hàm mất mới kết hợp PSNR, SSIM, và các chỉ số cảm quan như LPIPS để cải thiện chất lượng hình ảnh.
      - **Siêu phân giải đa nhiệm**: Kết hợp siêu phân giải với các tác vụ khác như khử nhiễu hoặc khử mờ trong một mô hình duy nhất.

  - **Inpainting**: Điền vào các phần thiếu hoặc bị hỏng của hình ảnh, ví dụ: xóa một đối tượng và tái tạo nền.
    - **Kỹ thuật**:
      - **GANs**: Sử dụng generator để tạo nội dung, như DeepFill.
      - **Diffusion Models**: Sử dụng khử nhiễu để tái tạo vùng thiếu, như Stable Diffusion.
      - **Transformer-based Models**: Tập trung vào vùng lân cận để đảm bảo tính nhất quán, như MAT.
    - **SOTA**:
      - **PixelHacker** ([PixelHacker Paper](https://arxiv.org/abs/2504.20438)): Sử dụng hướng dẫn danh mục tiềm ẩn, đạt hiệu suất vượt trội trên Places2, CelebA-HQ, và FFHQ.
      - **LaMa** ([LaMa Paper](https://www.producthunt.com/products/lama-cleaner)): Sử dụng Fast Fourier Convolutions để xử lý vùng thiếu lớn.
      - **MAT**: Sử dụng Transformer để cải thiện tính liên kết.
    - **Thách thức**:
      - **Vùng thiếu lớn**: Khó tái tạo các vùng lớn mà không làm mất tính nhất quán toàn cục.
      - **Tính liên kết ngữ nghĩa**: Đảm bảo vùng được điền khớp với ngữ cảnh của hình ảnh.
      - **Bảo toàn texture**: Đặc biệt khó với các mẫu phức tạp như khuôn mặt hoặc cảnh tự nhiên.
      - **Hiệu quả tính toán**: Các mô hình diffusion như PixelHacker yêu cầu thời gian sinh lâu.
    - **Cơ hội**:
      - **Hướng dẫn ngữ nghĩa**: Tích hợp thông tin ngữ nghĩa từ mô hình ngôn ngữ hoặc phân đoạn để cải thiện tính liên kết ([Large-scale Inpainting Benchmark](https://arxiv.org/abs/2502.06593)).
      - **Mô hình đa cấp**: Phát triển các phương pháp đa cấp để xử lý vùng thiếu lớn và nhỏ đồng thời.
      - **Học tương tác**: Tạo công cụ inpainting cho phép người dùng cung cấp hướng dẫn bổ sung (văn bản, phác thảo).
      - **Tăng tốc diffusion**: Nghiên cứu các phương pháp lấy mẫu nhanh hơn cho mô hình diffusion để áp dụng thời gian thực.
      - **Inpainting đa phương thức**: Kết hợp văn bản, hình ảnh, và các điều kiện khác để kiểm soát tốt hơn kết quả.

  - **Outpainting**: Mở rộng hình ảnh ra ngoài biên giới ban đầu, tạo nội dung mới liền mạch.
    - **Kỹ thuật**:
      - **GANs**: Sử dụng generator để tạo nội dung mở rộng, như Boundless.
      - **Diffusion Models**: Sử dụng khử nhiễu để tạo nội dung mới, như Infinite Nature.
    - **SOTA**:
      - **Boundless**: Một trong những mô hình đầu tiên cho outpainting, tạo nội dung mở rộng tự nhiên.
      - **Infinite Nature**: Tạo cảnh quan mở rộng với tính liên kết cao.
    - **Thách thức**:
      - **Tính liên kết toàn cục**: Đảm bảo nội dung mới khớp với phong cách và ngữ cảnh của hình ảnh gốc.
      - **Độ đa dạng nội dung**: Khó tạo ra nội dung đa dạng mà không lặp lại mẫu.
      - **Hiệu quả tính toán**: Yêu cầu tài nguyên lớn để xử lý hình ảnh độ phân giải cao.
    - **Cơ hội**:
      - **Hướng dẫn điều kiện**: Tích hợp văn bản hoặc hình ảnh tham chiếu để kiểm soát nội dung mở rộng.
      - **Mô hình đa phương thức**: Kết hợp thông tin từ nhiều nguồn (văn bản, âm thanh) để tạo nội dung phong phú hơn.
      - **Outpainting 3D**: Mở rộng sang không gian 3D hoặc video để áp dụng trong thực tế ảo.
      - **Tối ưu hiệu quả**: Phát triển mô hình nhẹ hơn để áp dụng trên thiết bị biên.

  - **Style Transfer**: Áp dụng phong cách nghệ thuật của một hình ảnh vào nội dung của hình ảnh khác.
    - **Kỹ thuật**:
      - **CNNs**: Sử dụng các lớp tích chập để trích xuất đặc trưng phong cách và nội dung.
      - **GANs**: Sử dụng adversarial loss để tạo kết quả chân thực.
    - **SOTA**:
      - **Arbitrary Style Transfer**: Cho phép chuyển đổi phong cách mà không cần huấn luyện lại.
      - **Fast Style Transfer**: Tối ưu cho xử lý thời gian thực.
    - **Thách thức**:
      - **Bảo toàn nội dung**: Đảm bảo cấu trúc nội dung không bị biến dạng khi áp dụng phong cách.
      - **Phong cách bất kỳ**: Khó xử lý các phong cách mới mà không cần huấn luyện lại.
      - **Hiệu quả thời gian thực**: Yêu cầu tốc độ cao cho ứng dụng tương tác.
    - **Cơ hội**:
      - **Mô hình phong cách tổng quát**: Phát triển mô hình có thể xử lý mọi phong cách mà không cần huấn luyện lại.
      - **Kết hợp đa nhiệm**: Tích hợp style transfer với các tác vụ như siêu phân giải hoặc inpainting.
      - **Style transfer video**: Mở rộng sang video với tính nhất quán thời gian.
      - **Học không giám sát**: Sử dụng dữ liệu không ghép đôi để cải thiện tính linh hoạt.

  - **Restoration**: Khôi phục hình ảnh bị suy giảm (nhiễu, mờ, hiện vật) để cải thiện chất lượng tổng thể.
    - **Kỹ thuật**:
      - **CNNs**: Sử dụng tích chập để học ánh xạ từ ảnh suy giảm sang ảnh sạch.
      - **GANs**: Sử dụng adversarial loss để tạo kết quả chân thực.
      - **Diffusion Models**: Sử dụng khử nhiễu để khôi phục hình ảnh.
    - **SOTA**:
      - **NAFNet** ([NAFNet Paper](https://link.springer.com/chapter/10.1007/978-3-031-20071-7_2)): Mạng không có hàm kích hoạt phi tuyến, đạt SOTA trên nhiều tác vụ khôi phục.
      - **Restormer**: Sử dụng Transformer để cải thiện hiệu suất.
    - **Thách thức**:
      - **Xử lý đa suy giảm**: Khó xử lý nhiễu, mờ, và nén đồng thời.
      - **Bảo toàn chi tiết**: Tránh làm mất texture hoặc cạnh khi khôi phục.
      - **Hiệu quả tính toán**: Yêu cầu tài nguyên lớn cho hình ảnh độ phân giải cao.
    - **Cơ hội**:
      - **Mô hình thống nhất**: Phát triển mô hình có thể xử lý nhiều loại suy giảm trong một kiến trúc duy nhất.
      - **Học tự giám sát**: Sử dụng dữ liệu không ghép đôi để cải thiện tổng quát hóa.
      - **Tích hợp mô hình vật lý**: Kết hợp các mô hình vật lý của suy giảm để cải thiện độ chính xác.
      - **Khôi phục thời gian thực**: Tối ưu mô hình cho ứng dụng video hoặc tương tác.

  - **Colorization**: Thêm màu sắc cho hình ảnh đơn sắc, tạo ra kết quả thực tế.
    - **Kỹ thuật**:
      - **CNNs**: Sử dụng tích chập để dự đoán màu sắc.
      - **GANs**: Sử dụng adversarial loss để tạo màu sắc chân thực.
    - **SOTA**:
      - **DeOldify**: Kết hợp CNN và GAN để tạo màu sắc tự nhiên.
      - **ChromaGAN**: Tối ưu cho màu sắc thực tế.
    - **Thách thức**:
      - **Độ chính xác màu sắc**: Khó dự đoán màu sắc chính xác cho các đối tượng đa dạng.
      - **Tính nhất quán ngữ nghĩa**: Đảm bảo màu sắc phù hợp với ngữ cảnh.
      - **Xử lý cảnh phức tạp**: Khó với các cảnh có nhiều đối tượng hoặc ánh sáng thay đổi.
    - **Cơ hội**:
      - **Hướng dẫn người dùng**: Tích hợp gợi ý màu sắc từ người dùng hoặc hình ảnh tham chiếu.
      - **Colorization video**: Mở rộng sang video với tính nhất quán thời gian.
      - **Học đa phương thức**: Kết hợp văn bản hoặc ngữ cảnh để cải thiện độ chính xác màu sắc.
      - **Tối ưu hiệu quả**: Phát triển mô hình nhẹ hơn cho ứng dụng thời gian thực.

  - **Denoising**: Loại bỏ nhiễu (Gaussian, Poisson, hoặc nhiễu thực tế) từ hình ảnh để khôi phục nội dung gốc.
  - **Kỹ thuật**:
    - **CNNs**: Sử dụng tích chập để học ánh xạ từ ảnh nhiễu sang ảnh sạch, như DnCNN.
    - **Autoencoders**: Mã hóa và giải mã để tái tạo hình ảnh sạch.
    - **GANs**: Sử dụng adversarial loss để tạo kết quả chân thực.
    - **Diffusion Models**: Sử dụng khử nhiễu để khôi phục hình ảnh.
  - **SOTA**:
    - **CGNet** ([SIDD Benchmark](https://paperswithcode.com/sota/image-denoising-on-sidd)): Đạt SOTA trên bộ dữ liệu SIDD, tập trung vào nhiễu thực tế từ điện thoại thông minh.
    - **DnCNN**: Chuẩn mực cho nhiễu Gaussian, hiệu quả và đơn giản.
    - **Restormer**: Sử dụng Transformer để cải thiện hiệu suất trên nhiễu thực tế.
  - **Thách thức**:
    - **Nhiễu thực tế**: Hầu hết mô hình được huấn luyện trên nhiễu tổng hợp (Gaussian), nhưng nhiễu thực tế phức tạp hơn (nhiễu cảm biến, nén).
    - **Bảo toàn chi tiết**: Loại bỏ nhiễu mà không làm mất texture hoặc cạnh.
    - **Tổng quát hóa**: Khó áp dụng mô hình trên các mức nhiễu và loại hình ảnh khác nhau.
    - **Hiệu quả tính toán**: Các mô hình như Restormer yêu cầu tài nguyên lớn.
    - **Dữ liệu ghép đôi**: Cần dữ liệu sạch-nhiễu lớn, khó thu thập trong thực tế.
  - **Cơ hội**:
    - **Mô hình nhiễu thực tế**: Phát triển mô hình chuyên biệt cho nhiễu thực tế, như nhiễu cảm biến trong y tế hoặc nhiếp ảnh ([Image Denoising Survey](https://epubs.siam.org/doi/10.1137/23M1545859)).
    - **Học không giám sát**: Sử dụng dữ liệu không ghép đôi hoặc tự giám sát để giảm phụ thuộc vào dữ liệu sạch.
    - **Mô hình đa nhiệm**: Kết hợp khử nhiễu với siêu phân giải hoặc khử mờ để xử lý đa suy giảm.
    - **Kiến trúc nhẹ**: Thiết kế mô hình hiệu quả hơn, như sử dụng Mamba hoặc attention tối ưu, để triển khai trên thiết bị biên.
    - **Tích hợp mô hình vật lý**: Kết hợp các mô hình vật lý của nhiễu (như Poisson) để cải thiện độ chính xác.

  - **Deblur**: Loại bỏ mờ (do chuyển động, mất nét, hoặc các yếu tố khác) để khôi phục hình ảnh sắc nét.
    - **Kỹ thuật**:
      - **Deconvolution**: Ước lượng kernel mờ và khôi phục hình ảnh.
      - **CNNs**: Học ánh xạ từ ảnh mờ sang ảnh sắc nét, như DeblurGAN.
      - **GANs**: Sử dụng adversarial loss để tạo kết quả chân thực.
      - **Transformer-based Models**: Sử dụng attention để xử lý đặc trưng toàn cục, như DeblurDiNAT.
    - **SOTA**:
      - **DeblurDiNAT** ([DeblurDiNAT Paper](https://arxiv.org/abs/2403.13163)): Sử dụng Dilated Neighborhood Attention, đạt hiệu suất cao và tổng quát hóa tốt trên các miền chưa thấy.
      - **NAFNet** ([NAFNet Paper](https://link.springer.com/chapter/10.1007/978-3-031-20071-7_2)): Đạt SOTA trên GoPro với PSNR 33.69 dB, hiệu quả tính toán.
      - **DeblurGAN-v2**: Cải tiến từ DeblurGAN, hiệu quả và linh hoạt.
    - **Thách thức**:
      - **Ước lượng kernel mờ**: Khó với mờ không đồng nhất hoặc phức tạp.
      - **Xử lý đa loại mờ**: Mô hình thường chỉ tối ưu cho một loại mờ (chuyển động hoặc mất nét).
      - **Bảo toàn chi tiết**: Loại bỏ mờ mà không làm mất texture hoặc tạo hiện vật.
      - **Hiệu quả thời gian thực**: Yêu cầu tốc độ cao cho ứng dụng video hoặc tương tác.
      - **Dữ liệu huấn luyện**: Cần dữ liệu ghép đôi mờ-sắc nét, khó thu thập trong thực tế.
    - **Cơ hội**:
      - **Mô hình đa loại mờ**: Phát triển mô hình có thể xử lý cả mờ chuyển động và mất nét ([MC-Blur Dataset](https://ieeexplore.ieee.org/document/10264126)).
      - **Học không giám sát**: Sử dụng dữ liệu không ghép đôi hoặc tự giám sát để giảm phụ thuộc vào dữ liệu huấn luyện.
      - **Phương pháp miền tần số**: Khai thác miền tần số để ước lượng kernel mờ chính xác hơn.
      - **Deblur thời gian thực**: Tối ưu mô hình cho video hoặc ứng dụng tương tác, như sử dụng kiến trúc nhẹ hoặc lấy mẫu nhanh.
      - **Tích hợp đa nhiệm**: Kết hợp khử mờ với khử nhiễu hoặc siêu phân giải để xử lý đa suy giảm.
  
#### C. Multimodal-to-Image

- **Định nghĩa**: Tạo hoặc chỉnh sửa ảnh dựa trên cả văn bản và ảnh đầu vào, ví dụ: chỉnh sửa ảnh theo hướng dẫn "thêm một chiếc mũ vào người trong ảnh" hoặc tạo ảnh dựa trên bản phác thảo và mô tả.
- **Kỹ thuật**:
  - **CLIP-guided Diffusion**: Sử dụng CLIP để hướng dẫn quá trình sinh dựa trên văn bản, như trong GLIDE.
  - **GANs**: Kết hợp điều kiện văn bản và ảnh để chỉnh sửa, như trong StyleCLIP.
  - **Hybrid Models**: Kết hợp diffusion và Transformer để cải thiện chất lượng và kiểm soát.
- **SOTA**:
  - **GLIDE** ([GLIDE](https://arxiv.org/abs/2112.10741)): Mô hình của OpenAI, hỗ trợ chỉnh sửa ảnh dựa trên văn bản.
  - **DALL-E 2 Editing** ([DALL-E](https://openai.com/dall-e)): Cho phép chỉnh sửa ảnh với hướng dẫn văn bản.
  - **Stable Diffusion with Text Guidance** ([Stable Diffusion](https://www.stability.ai/stable-diffusion)): Hỗ trợ chỉnh sửa dựa trên văn bản và ảnh.
- **Thách thức**:
  - **Hiểu hướng dẫn phức tạp**: Xử lý các mô tả văn bản mơ hồ hoặc chi tiết.
  - **Duy trì consistency**: Đảm bảo các chỉnh sửa không làm mất tính nhất quán của ảnh gốc.
  - **Tính linh hoạt**: Xử lý nhiều loại chỉnh sửa (thêm đối tượng, thay đổi phong cách, v.v.).
- **Cơ hội**:
  - Phát triển các công cụ chỉnh sửa ảnh intuitive cho người dùng không chuyên.
  - Ứng dụng trong thiết kế, quảng cáo, và nghệ thuật số.
  - Hiểu các hướng dẫn compositional (ví dụ: "đặt một con chim trên cành cây bên trái").
  - Chỉnh sửa tương tác theo thời gian thực.
  - Tích hợp với các nền tảng sáng tạo để hỗ trợ quy trình làm việc.

### 1.2. Video Generation

#### A. Text-to-Video

- **Định nghĩa**: Tạo video từ mô tả văn bản, ví dụ: "một con tàu vũ trụ bay qua dải ngân hà". Mục tiêu là tạo ra video chân thực, phù hợp với mô tả, với các khung hình liên kết mượt mà.
- **Kỹ thuật**:
  - **Diffusion Models**: Mở rộng từ text-to-image, thêm cơ chế đảm bảo tính nhất quán thời gian, như trong Make-A-Video.
  - **GANs**: Sử dụng temporal generators để tạo chuỗi khung hình, như trong MoCoGAN.
  - **Transformer-based Models**: Sử dụng attention để mô hình hóa động lực thời gian, như trong Phenaki.
- **SOTA**:
  - **Sora** ([Sora](https://openai.com/sora)): Mô hình của OpenAI, nổi bật với chất lượng cao và khả năng tạo video linh hoạt từ văn bản.
  - **Make-A-Video** ([Make-A-Video](https://makeavideo.studio/)): Mô hình của Meta AI, tạo video ngắn chất lượng cao từ mô tả văn bản.
  - **Imagen Video** ([Imagen Video](https://cloud.google.com/blog/products/ai-machine-learning/imagen-2)): Mô hình của Google, được đánh giá cao về độ chân thực.
  - **Phenaki** ([Phenaki Paper](https://arxiv.org/abs/2210.11618)): Hỗ trợ tạo video dài hơn với văn bản điều kiện.
- **Thách thức**:
  - **Tính nhất quán thời gian**: Đảm bảo các khung hình liên kết mượt mà, tránh hiện tượng giật hoặc không tự nhiên.
  - **Sinh video dài**: Hầu hết các mô hình chỉ tạo được video ngắn (vài giây), khó mở rộng sang video dài hơn.
  - **Chi phí tính toán**: Huấn luyện và sinh video đòi hỏi tài nguyên lớn, đặc biệt với độ phân giải cao.
  - **Hiểu prompt phức tạp**: Xử lý các mô tả văn bản chi tiết hoặc mơ hồ là một thách thức.
- **Cơ hội**:
  - **Sinh video dài**: Phát triển các mô hình có thể tạo video dài hơn với tính nhất quán cao, như sử dụng các kỹ thuật học tuần tự hoặc memory-augmented networks.
  - **Tăng tốc độ sinh**: Nghiên cứu các phương pháp lấy mẫu nhanh hơn cho diffusion models để áp dụng thời gian thực.
  - **Tích hợp điều kiện phức tạp**: Cho phép người dùng kiểm soát chi tiết hơn qua prompt văn bản hoặc hình ảnh, như chỉ định chuyển động cụ thể.
  - **Học không giám sát**: Sử dụng dữ liệu không ghép đôi để cải thiện khả năng tổng quát hóa của mô hình.

#### B. Video-to-Video

- **Định nghĩa**: Chuyển đổi video để thực hiện các tác vụ như khôi phục, nâng cấp độ phân giải, hoặc chỉnh sửa, tương tự như Image-to-Image nhưng với yêu cầu thêm về tính nhất quán thời gian.
- **Bài toán con**:
  - **Video Restoration**: Loại bỏ nhiễu, khôi phục video cũ hoặc bị suy giảm chất lượng.
    - **Kỹ thuật**: CNNs với temporal convolutions, GANs để tạo khung hình chân thực.
    - **SOTA**: EDVR ([EDVR Paper](https://arxiv.org/abs/1905.02716)), sử dụng deformable convolutions để cải thiện chất lượng.
    - **Thách thức**: Xử lý nhiễu phức tạp (như nhiễu thực tế từ cảm biến), duy trì tính liên kết giữa các khung hình.
    - **Cơ hội**: Ứng dụng trong khôi phục phim cũ, cải thiện chất lượng video streaming, hoặc xử lý video giám sát.
  - **Video Super-Resolution**: Tăng độ phân giải video từ thấp lên cao.
    - **Kỹ thuật**: Recurrent networks để xử lý chuỗi khung hình, attention mechanisms để tập trung vào chi tiết.
    - **SOTA**: DUF ([DUF Paper](https://arxiv.org/abs/1804.07709)), EDVR.
    - **Thách thức**: Xử lý motion blur, occlusions, và duy trì tính nhất quán thời gian.
    - **Cơ hội**: Cải thiện chất lượng video surveillance, streaming, hoặc video y tế.
  - **Video Inpainting**: Điền vào các phần thiếu hoặc bị hỏng trong video.
    - **Kỹ thuật**: GANs, diffusion models, Transformer-based models như STTN để đảm bảo tính liên kết.
    - **SOTA**: FGVC ([FGVC Paper](https://arxiv.org/abs/2002.08038)), STTN ([STTN Paper](https://arxiv.org/abs/2004.00334)).
    - **Thách thức**: Đảm bảo tính nhất quán thời gian, xử lý occlusions do đối tượng di chuyển.
    - **Cơ hội**: Chỉnh sửa video chuyên nghiệp, xóa đối tượng không mong muốn trong sản xuất phim.
  - **Video Outpainting**: Mở rộng biên giới video để tạo nội dung mới.
    - **Kỹ thuật**: GANs, diffusion models, mở rộng từ các phương pháp image outpainting.
    - **SOTA**: Ít nghiên cứu, nhưng các mô hình như Infinite Nature có thể được thích nghi.
    - **Thách thức**: Duy trì nội dung tự nhiên, xử lý khối lượng tính toán lớn.
    - **Cơ hội**: Tạo video toàn cảnh, ứng dụng trong thực tế ảo (VR) hoặc sản xuất nội dung sáng tạo.
  - **Video Style Transfer**: Áp dụng phong cách nghệ thuật cho video.
    - **Kỹ thuật**: Temporal GANs, flow-based methods để đảm bảo tính nhất quán thời gian.
    - **SOTA**: ReCoNet ([ReCoNet Paper](https://arxiv.org/abs/1803.02287)), MCCNet.
    - **Thách thức**: Đảm bảo tính nhất quán thời gian, tránh hiện tượng nhấp nháy giữa các khung hình.
    - **Cơ hội**: Sản xuất nội dung sáng tạo, như video nghệ thuật hoặc quảng cáo.
  - **Video Colorization**: Thêm màu cho video đen trắng.
    - **Kỹ thuật**: GANs, deep learning-based color propagation để lan truyền màu sắc qua các khung hình.
    - **SOTA**: DeOldify ([DeOldify](https://github.com/jantic/DeOldify)), ChromaGAN.
    - **Thách thức**: Xử lý chuyển động, duy trì màu sắc tự nhiên qua các khung hình.
    - **Cơ hội**: Khôi phục phim lịch sử, cải thiện trải nghiệm xem video cũ.

#### C. Multimodal-to-Video

- **Định nghĩa**: Tạo hoặc chỉnh sửa video dựa trên văn bản, hình ảnh, hoặc các điều kiện khác, ví dụ: chỉnh sửa video theo hướng dẫn "thêm một chiếc mũ cho người trong video" hoặc tạo video từ bản phác thảo.
- **Kỹ thuật**:
  - **CLIP-guided Diffusion**: Sử dụng CLIP để hướng dẫn quá trình sinh dựa trên văn bản hoặc hình ảnh.
  - **Conditional GANs**: Kết hợp điều kiện văn bản hoặc hình ảnh để chỉnh sửa video.
  - **Transformer-based Models**: Sử dụng attention để xử lý các điều kiện phức tạp.
- **SOTA**:
  - **ControlNet** ([ControlNet Paper](https://arxiv.org/abs/2302.05543)): Cho phép kiểm soát chi tiết các mô hình diffusion với các điều kiện như bản đồ cạnh, tư thế, hoặc phân đoạn.
  - **Phenaki** ([Phenaki Paper](https://arxiv.org/abs/2210.11618)): Hỗ trợ tạo video dài hơn với văn bản điều kiện.
  - **Video Diffusion Models** ([Video Diffusion Models](https://arxiv.org/abs/2204.03458)): Mô hình diffusion có điều kiện, cải thiện khả năng chỉnh sửa video.
- **Thách thức**:
  - **Hiểu hướng dẫn phức tạp**: Xử lý các prompt văn bản hoặc điều kiện hình ảnh chi tiết hoặc mơ hồ.
  - **Duy trì consistency**: Đảm bảo các chỉnh sửa không làm mất tính nhất quán của video gốc.
  - **Tính linh hoạt**: Xử lý nhiều loại chỉnh sửa (thêm đối tượng, thay đổi phong cách, v.v.).
- **Cơ hội**:
  - **Kiểm soát chi tiết**: Phát triển các mô hình cho phép kiểm soát từng phần của video, như chỉnh sửa một đối tượng cụ thể.
  - **Tích hợp đa phương thức**: Kết hợp văn bản, hình ảnh, và âm thanh để sinh video phong phú hơn.
  - **Chỉnh sửa tương tác**: Tạo công cụ chỉnh sửa video intuitive cho người dùng không chuyên.
  - **Học không giám sát**: Sử dụng dữ liệu không ghép đôi để cải thiện khả năng tổng quát hóa.

#### D. Các bài toán đặc thù của Video Generation

- **Video Prediction**:
  - **Định nghĩa**: Dự đoán các khung hình tương lai từ các khung hình trước, ví dụ: dự đoán chuyển động của một chiếc xe từ video giao thông.
  - **Kỹ thuật**: Autoregressive models, VAEs, GANs như SAVP để xử lý uncertainty.
  - **SOTA**: SAVP ([SAVP Paper](https://arxiv.org/abs/1803.01465)), PredRNN ([PredRNN Paper](https://arxiv.org/abs/2103.09504)).
  - **Thách thức**: Xử lý uncertainty trong các sự kiện tương lai, dự đoán dài hạn mà không làm mất chất lượng.
  - **Cơ hội**: Ứng dụng trong lái xe tự động, giám sát, hoặc dự báo thời tiết.
- **Video Interpolation**:
  - **Định nghĩa**: Tạo các khung hình trung gian để tăng độ mượt mà, ví dụ: chuyển video 30fps thành 60fps.
  - **Kỹ thuật**: Optical flow, deep learning-based methods như DAIN.
  - **SOTA**: DAIN ([DAIN Paper](https://arxiv.org/abs/1904.00830)).
  - **Thách thức**: Xử lý chuyển động nhanh, occlusions, và duy trì tính tự nhiên.
  - **Cơ hội**: Tăng frame rate, tạo hiệu ứng slow motion, cải thiện trải nghiệm xem video.
- **Talking Head Generation**:
  - **Định nghĩa**: Tạo video của một người nói dựa trên âm thanh hoặc văn bản, ví dụ: tạo video từ giọng nói hoặc kịch bản.
  - **Kỹ thuật**: GANs, neural rendering để tạo biểu cảm và đồng bộ môi.
  - **SOTA**: First Order Motion Model ([First Order Motion](https://arxiv.org/abs/2003.00196)).
  - **Thách thức**: Tạo biểu cảm tự nhiên, đồng bộ môi chính xác, xử lý các góc nhìn khác nhau.
  - **Cơ hội**: Ứng dụng trong trợ lý ảo, lồng tiếng, hoặc sản xuất nội dung giáo dục.
- **Motion Transfer**:
  - **Định nghĩa**: Chuyển động từ một video sang video khác, ví dụ: áp dụng điệu nhảy từ một người sang người khác.
  - **Kỹ thuật**: Pose estimation, GANs để ánh xạ chuyển động.
  - **SOTA**: Everybody Dance Now ([Everybody Dance Now](https://arxiv.org/abs/1808.07371)).
  - **Thách thức**: Xử lý các loại cơ thể khác nhau, đảm bảo chuyển động tự nhiên.
  - **Cơ hội**: Ứng dụng trong hoạt hình, thể thao, hoặc sản xuất nội dung sáng tạo.

## 2. Kỹ thuật tăng cường

### 2.1. Tối ưu mô hình để triển khai trên thiết bị biên

- **Định nghĩa**: Tối ưu hóa các mô hình Generative AI để chạy trên các thiết bị có tài nguyên hạn chế như điện thoại thông minh, thiết bị IoT, hoặc máy chủ biên, thay vì phụ thuộc vào các máy chủ đám mây mạnh mẽ. Điều này nhằm giảm độ trễ, tăng quyền riêng tư, và tiết kiệm chi phí.
- **Kỹ thuật**:
  - **Nén mô hình**: Sử dụng cắt tỉa (pruning) để loại bỏ các trọng số không cần thiết, lượng tử hóa (quantization) để giảm độ chính xác số học (ví dụ: từ 32-bit xuống 8-bit), và chưng cất kiến thức (knowledge distillation) để huấn luyện mô hình nhỏ hơn bắt chước mô hình lớn.
  - **Kiến trúc hiệu quả**: Thiết kế các mô hình nhẹ hơn, như sử dụng tích chập riêng biệt (depthwise separable convolutions) hoặc các biến thể transformer tối ưu hóa cho thiết bị biên.
  - **Tối ưu hóa suy luận**: Tận dụng các tối ưu hóa phần cứng, như sử dụng Neural Processing Units (NPUs) hoặc TensorFlow Lite, để tăng tốc suy luận trên thiết bị.
- **SOTA**:
  - **Ministral 3B và 8B** ([Qualcomm and Mistral AI Partnership](https://www.edge-ai-vision.com/2024/10/qualcomm-and-mistral-ai-partner-to-bring-new-generative-ai-models-to-edge-devices/)): Các mô hình của Mistral AI được thiết kế cho thiết bị biên, chạy trên nền tảng Snapdragon, mang lại hiệu quả năng lượng và quyền riêng tư cao.
  - **Stable Diffusion Quantized** ([Hugging Face Stable Diffusion](https://huggingface.co/stabilityai/stable-diffusion-2-1)): Phiên bản lượng tử hóa của Stable Diffusion có thể chạy trên GPU tiêu dùng hoặc CPU, phù hợp cho các ứng dụng biên.
  - **TinyML**: Các kỹ thuật chạy mô hình học máy trên thiết bị nhỏ, đang được thích nghi cho các nhiệm vụ tạo sinh như sinh ảnh đơn giản.
- **Thách thức**:
  - **Cân bằng hiệu suất và kích thước**: Giảm kích thước mô hình thường làm giảm chất lượng đầu ra, đặc biệt với các nhiệm vụ phức tạp như sinh ảnh độ phân giải cao.
  - **Ràng buộc tài nguyên**: Thiết bị biên có bộ nhớ, công suất xử lý, và năng lượng hạn chế, đòi hỏi các mô hình phải cực kỳ hiệu quả.
  - **Thời gian thực**: Nhiều ứng dụng biên yêu cầu sinh thời gian thực, nhưng các mô hình như diffusion thường chậm.
  - **Tổng quát hóa**: Mô hình tối ưu cho một thiết bị cụ thể có thể không hoạt động tốt trên các thiết bị khác.
- **Cơ hội**:
  - **Mô hình nhẹ đa nhiệm**: Phát triển các mô hình có thể xử lý nhiều nhiệm vụ (sinh ảnh, chỉnh sửa, khử nhiễu) trên thiết bị biên với tài nguyên tối thiểu.
  - **Tối ưu hóa phần cứng-AI**: Thiết kế các mô hình tận dụng tối đa các đơn vị xử lý thần kinh (NPUs) hoặc chip AI chuyên dụng.
  - **Học liên tục trên thiết bị**: Nghiên cứu các phương pháp cho phép mô hình học hoặc tinh chỉnh trên thiết bị mà không cần kết nối đám mây.
  - **Sinh thời gian thực**: Tạo các mô hình sinh ảnh hoặc video nhanh hơn, phù hợp cho các ứng dụng như thực tế tăng cường (AR) trên kính thông minh.

### 2.2. Tối ưu khả năng sinh sát với prompt hay condition đầu vào

- **Định nghĩa**: Đảm bảo rằng đầu ra của mô hình Generative AI khớp chặt chẽ với prompt văn bản, hình ảnh, hoặc các điều kiện đầu vào khác, phản ánh chính xác ý định của người dùng.
- **Kỹ thuật**:
  - **Kỹ thuật prompt**: Tạo các prompt chi tiết, sử dụng các kỹ thuật như chain-of-thought prompting để cải thiện khả năng hiểu của mô hình.
  - **Sinh có điều kiện**: Sử dụng các điều kiện bổ sung như nhãn lớp, bản đồ cạnh, hoặc tư thế để kiểm soát đầu ra.
  - **Tinh chỉnh mô hình**: Điều chỉnh các mô hình đã được huấn luyện trước trên các tập dữ liệu cụ thể để tăng độ chính xác với các prompt hoặc điều kiện nhất định.
  - **Học đa phương thức**: Kết hợp các mô hình ngôn ngữ và thị giác (như CLIP) để hiểu và sinh dựa trên cả văn bản và hình ảnh.
- **SOTA**:
  - **CLIP-Guided Diffusion** ([DALL-E 2](https://www.altexsoft.com/blog/generative-ai/)): Sử dụng CLIP để hướng dẫn các mô hình diffusion, đảm bảo hình ảnh khớp với mô tả văn bản.
  - **ControlNet** ([ControlNet Paper](https://arxiv.org/abs/2302.05543)): Cho phép kiểm soát chi tiết các mô hình diffusion bằng các điều kiện như bản đồ cạnh, tư thế, hoặc phân đoạn.
  - **InstructPix2Pix** ([InstructPix2Pix Paper](https://arxiv.org/abs/2211.09800)): Một mô hình chỉnh sửa hình ảnh dựa trên văn bản, cho phép người dùng chỉ định các thay đổi thông qua prompt.
- **Thách thức**:
  - **Prompt mơ hồ**: Các prompt ngôn ngữ tự nhiên có thể không rõ ràng, dẫn đến đầu ra không mong muốn.
  - **Xử lý điều kiện phức tạp**: Kết hợp nhiều điều kiện (ví dụ: văn bản, hình ảnh, và nhãn) mà không gây mâu thuẫn là khó khăn.
  - **Tính nhất quán**: Đảm bảo đầu ra nhất quán khi prompt hoặc điều kiện thay đổi nhẹ.
  - **Hiểu ngữ cảnh**: Mô hình có thể bỏ qua các chi tiết quan trọng trong prompt dài hoặc phức tạp.
- **Cơ hội**:
  - **Prompt tự động**: Phát triển các công cụ tự động tạo hoặc tinh chỉnh prompt dựa trên phản hồi của người dùng ([Automatic Prompt Optimization](https://cameronrwolfe.substack.com/p/automatic-prompt-optimization)).
  - **Kiểm soát đa phương thức**: Tạo các mô hình có thể xử lý và kết hợp nhiều loại điều kiện (văn bản, hình ảnh, âm thanh) để sinh đầu ra phong phú hơn.
  - **Học ngữ cảnh**: Cải thiện khả năng hiểu các prompt dài hoặc có cấu trúc phức tạp, như các mô tả compositional (ví dụ: “một con chim trên cành cây bên trái”).
  - **Giao diện người dùng**: Thiết kế các giao diện trực quan cho phép người dùng không chuyên dễ dàng chỉ định các điều kiện sinh.

### 2.3. Tối ưu hiệu quả sinh, chất lượng đầu ra của mô hình

- **Định nghĩa**: Cải thiện tốc độ sinh và chất lượng đầu ra của các mô hình Generative AI, đảm bảo rằng chúng có thể tạo ra các hình ảnh hoặc video chất lượng cao một cách nhanh chóng và hiệu quả.
- **Kỹ thuật**:
  - **Lấy mẫu nhanh hơn**: Đối với các mô hình diffusion, sử dụng các phương pháp như DDIM để giảm số bước lấy mẫu.
  - **Phát triển tiến bộ**: Trong GANs, bắt đầu với hình ảnh độ phân giải thấp và tăng dần độ phân giải trong quá trình huấn luyện và sinh.
  - **Chưng cất kiến thức**: Huấn luyện các mô hình nhỏ hơn để bắt chước các mô hình lớn, giảm chi phí tính toán mà vẫn duy trì chất lượng.
  - **Tối ưu hóa hàm mất**: Thiết kế các hàm mất kết hợp các chỉ số như PSNR, SSIM, và LPIPS để cải thiện chất lượng cảm quan.
- **SOTA**:
  - **DDIM** ([DDIM Paper](https://arxiv.org/abs/2010.02502)): Một phương pháp lấy mẫu nhanh cho các mô hình diffusion, giảm số bước từ hàng trăm xuống vài chục mà vẫn giữ chất lượng cao.
  - **StyleGAN3** ([StyleGAN3 Paper](https://arxiv.org/abs/2106.12423)): Một kiến trúc GAN tiên tiến với độ ổn định huấn luyện và tốc độ sinh được cải thiện, sản xuất hình ảnh chất lượng cao.
  - **BigGAN** ([BigGAN Paper](https://arxiv.org/abs/1809.11096)): Một mô hình GAN có khả năng mở rộng, tạo ra các hình ảnh độ phân giải cao với chất lượng vượt trội.
- **Thách thức**:
  - **Đánh đổi tốc độ và chất lượng**: Các phương pháp nhanh hơn thường làm giảm chất lượng đầu ra, đặc biệt với các mô hình diffusion.
  - **Chi phí tính toán**: Sinh chất lượng cao đòi hỏi tài nguyên lớn, đặc biệt cho video hoặc hình ảnh độ phân giải cao.
  - **Hiện vật đầu ra**: Các mô hình nhanh hơn có thể tạo ra các hiện vật (artifacts) như mờ hoặc méo mó.
  - **Tổng quát hóa**: Đảm bảo chất lượng cao trên các miền dữ liệu khác nhau (ví dụ: ảnh tự nhiên, y tế, vệ tinh).
- **Cơ hội**:
  - **Lấy mẫu hiệu quả hơn**: Phát triển các phương pháp lấy mẫu mới cho diffusion models để đạt được tốc độ thời gian thực ([Optimizing Generative AI Applications](https://navveenbalani.medium.com/optimizing-generative-ai-applications-a-strategic-guide-for-efficiency-and-performance-ebdd3fb800f9)).
  - **Mô hình đa nhiệm**: Tạo các mô hình có thể xử lý nhiều nhiệm vụ (sinh, chỉnh sửa, khử nhiễu) với hiệu quả cao.
  - **Tối ưu cảm quan**: Nghiên cứu các hàm mất mới tập trung vào chất lượng cảm quan của con người, thay vì chỉ dựa vào các chỉ số như PSNR.
  - **Sinh video thời gian thực**: Tối ưu hóa các mô hình để sinh video chất lượng cao với độ trễ thấp, phù hợp cho các ứng dụng như trò chơi hoặc VR.

### 2.4. Cải thiện kiến trúc mô hình

- **Định nghĩa**: Phát triển các kiến trúc mô hình mới hoặc cải tiến các kiến trúc hiện có để nâng cao hiệu suất, hiệu quả, và tính linh hoạt trong các nhiệm vụ tạo sinh như sinh ảnh hoặc video.
- **Kỹ thuật**:
  - **Transformer-based Models**: Sử dụng transformer với cơ chế tự chú ý (self-attention) để xử lý dữ liệu tuần tự và phụ thuộc dài hạn, phù hợp cho sinh đa phương thức.
  - **Diffusion Models**: Sinh dữ liệu bằng cách đảo ngược quá trình thêm nhiễu, nổi bật với chất lượng mẫu cao.
  - **Hybrid Models**: Kết hợp các kiến trúc như GANs với transformer hoặc diffusion để tận dụng điểm mạnh của từng loại.
  - **Autoregressive Models**: Sinh dữ liệu theo thứ tự, thường được sử dụng trong các mô hình như PixelCNN hoặc GPT.
- **SOTA**:
  - **DALL-E 2** ([DALL-E 2 Overview](https://www.altexsoft.com/blog/generative-ai/)): Kết hợp CLIP và diffusion models để sinh hình ảnh từ văn bản với chất lượng cao.
  - **Imagen** ([Imagen Paper](https://arxiv.org/abs/2205.11487)): Sử dụng một loạt các mô hình diffusion để tạo hình ảnh chất lượng cao từ văn bản.
  - **VQ-GAN** ([VQ-GAN Paper](https://arxiv.org/abs/2012.09841)): Kết hợp GANs với vector quantization để kiểm soát tốt hơn quá trình sinh.
- **Thách thức**:
  - **Độ phức tạp**: Các kiến trúc mới thường phức tạp hơn, đòi hỏi nhiều tài nguyên để huấn luyện và triển khai.
  - **Yêu cầu dữ liệu**: Các mô hình tiên tiến cần lượng dữ liệu lớn và chất lượng cao để đạt hiệu suất tối ưu.
  - **Khả năng diễn giải**: Các kiến trúc phức tạp có thể khó hiểu và kiểm soát, làm giảm tính minh bạch.
  - **Chi phí tính toán**: Huấn luyện các mô hình như transformer hoặc diffusion đòi hỏi GPU hoặc TPU mạnh mẽ.
- **Cơ hội**:
  - **Kiến trúc đa phương thức**: Phát triển các mô hình có thể xử lý và sinh dữ liệu từ nhiều phương thức (văn bản, hình ảnh, âm thanh) ([Generative AI Architecture](https://www.solulab.com/generative-ai-architecture/)).
  - **Học ít-shot**: Tạo các kiến trúc có thể sinh đầu ra chất lượng cao với lượng dữ liệu huấn luyện tối thiểu.
  - **Kiến trúc nhẹ**: Thiết kế các mô hình hiệu quả hơn, như sử dụng Mamba hoặc các biến thể transformer tối ưu, để triển khai trên thiết bị biên.
  - **Kiểm soát chi tiết**: Phát triển các kiến trúc cho phép kiểm soát chi tiết hơn, như chỉnh sửa từng phần của hình ảnh hoặc video.

### 2.5. Kỹ thuật huấn luyện

- **Định nghĩa**: Các phương pháp và chiến lược để huấn luyện các mô hình Generative AI, đảm bảo chúng học hiệu quả từ dữ liệu và tổng quát hóa tốt với các đầu vào mới.
- **Kỹ thuật**:
  - **Huấn luyện đối kháng**: Đối với GANs, sử dụng generator và discriminator cạnh tranh để cải thiện lẫn nhau.
  - **Suy luận biến phân**: Đối với VAEs, học một không gian ẩn xác suất để tái tạo và sinh dữ liệu.
  - **Khớp điểm số**: Đối với diffusion models, huấn luyện mô hình dự đoán gradient của phân phối dữ liệu.
  - **Chuyển giao học tập**: Tận dụng các mô hình đã được huấn luyện trước (như BERT, GPT) và tinh chỉnh trên các tập dữ liệu cụ thể.
  - **Tăng cường dữ liệu**: Sử dụng các kỹ thuật như xoay, lật, hoặc thêm nhiễu để tăng sự đa dạng của dữ liệu huấn luyện.
- **SOTA**:
  - **Progressive Growing of GANs** ([Progressive GANs Paper](https://arxiv.org/abs/1710.10196)): Huấn luyện GANs bằng cách tăng dần độ phân giải, cải thiện chất lượng và độ ổn định.
  - **Score Matching** ([Score Matching Paper](https://arxiv.org/abs/1905.07088)): Một kỹ thuật huấn luyện diffusion models, đạt chất lượng mẫu cao.
  - **Self-Supervised Learning** ([Self-Supervised Learning Overview](https://www.xenonstack.com/blog/generative-ai-models)): Sử dụng dữ liệu không có nhãn để tạo tín hiệu huấn luyện, giảm phụ thuộc vào dữ liệu gán nhãn.
- **Thách thức**:
  - **Độ ổn định huấn luyện**: GANs dễ gặp vấn đề như sụp đổ chế độ (mode collapse) hoặc bất ổn định.
  - **Chi phí tính toán**: Huấn luyện các mô hình lớn như diffusion hoặc transformer đòi hỏi tài nguyên lớn.
  - **Chất lượng dữ liệu**: Dữ liệu huấn luyện kém chất lượng hoặc thiên vị có thể dẫn đến đầu ra không mong muốn.
  - **Overfitting**: Mô hình có thể học quá tốt dữ liệu huấn luyện, làm giảm khả năng tổng quát hóa.
- **Cơ hội**:
  - **Huấn luyện hiệu quả**: Phát triển các phương pháp huấn luyện sử dụng ít dữ liệu hoặc tài nguyên hơn ([How to Train Generative AI](https://www.deepchecks.com/how-to-train-generative-ai-models/)).
  - **Học không giám sát**: Tạo các kỹ thuật học từ dữ liệu không có nhãn để giảm chi phí gán nhãn.
  - **Tối ưu hóa ổn định**: Nghiên cứu các phương pháp như gradient clipping hoặc spectral normalization để cải thiện độ ổn định của GANs.
  - **Huấn luyện đa nhiệm**: Phát triển các chiến lược huấn luyện cho phép mô hình học nhiều nhiệm vụ (sinh, chỉnh sửa, khử nhiễu) đồng thời.

### 2.6. Khả năng mở rộng

- **Định nghĩa**: Khả năng của các hệ thống Generative AI xử lý các tập dữ liệu lớn hơn, các nhiệm vụ phức tạp hơn, hoặc khối lượng yêu cầu cao hơn mà không làm giảm hiệu suất đáng kể.
- **Kỹ thuật**:
  - **Huấn luyện phân phối**: Sử dụng nhiều GPU hoặc máy tính để huấn luyện các mô hình lớn, chia sẻ khối lượng công việc.
  - **Song song hóa mô hình**: Phân chia mô hình qua nhiều thiết bị để xử lý các phần khác nhau đồng thời.
  - **Song song hóa dữ liệu**: Sao chép mô hình và phân chia dữ liệu qua các thiết bị để tăng tốc huấn luyện.
  - **Tính toán đám mây**: Sử dụng các nền tảng đám mây để cung cấp tài nguyên tính toán theo nhu cầu.
- **SOTA**:
  - **Megatron-LM** ([Megatron-LM Paper](https://arxiv.org/abs/1909.08053)): Hệ thống huấn luyện transformer lớn với song song hóa mô hình, tối ưu cho các mô hình ngôn ngữ và thị giác.
  - **DeepSpeed** ([DeepSpeed Website](https://www.deepspeed.ai/)): Thư viện tối ưu hóa huấn luyện với các kỹ thuật như Zero Redundancy Optimizer (ZeRO), giảm yêu cầu bộ nhớ.
  - **Cloud-Based Scaling** ([Scaling GenAI in the Cloud](https://aimagazine.com/articles/scaling-the-challenges-of-gen-ai-in-the-cloud)): Các nền tảng như AWS, Azure, và Google Cloud cung cấp cơ sở hạ tầng mở rộng cho Generative AI.
- **Thách thức**:
  - **Chi phí cao**: Mở rộng đòi hỏi đầu tư lớn vào phần cứng, cơ sở hạ tầng, và năng lượng.
  - **Quản lý phức tạp**: Các hệ thống phân phối có thể khó thiết lập và duy trì, dễ xảy ra lỗi.
  - **Quản lý dữ liệu**: Xử lý và lưu trữ các tập dữ liệu lớn một cách hiệu quả là một thách thức.
  - **Tác động môi trường**: Tính toán quy mô lớn tiêu thụ nhiều năng lượng, gây lo ngại về môi trường.
- **Cơ hội**:
  - **Tối ưu hóa tài nguyên**: Phát triển các phương pháp huấn luyện sử dụng ít tài nguyên hơn, như sparse training hoặc low-precision training ([Scaling Generative AI](https://www.pwc.com/us/en/tech-effect/ai-analytics/scaling-generative-ai.html)).
  - **Mở rộng phi tập trung**: Nghiên cứu các phương pháp huấn luyện phân phối trên các thiết bị biên hoặc mạng phi tập trung.
  - **Tích hợp dữ liệu đa nguồn**: Tạo các hệ thống có thể xử lý và tổng hợp dữ liệu từ nhiều nguồn để mở rộng khả năng học.
  - **Mô hình bền vững**: Phát triển các kỹ thuật giảm tiêu thụ năng lượng trong huấn luyện và suy luận quy mô lớn.

### 2.7. Tính kiểm soát và khả năng diễn giải

- **Định nghĩa**: Làm cho các mô hình Generative AI dễ kiểm soát hơn, cho phép người dùng chỉ định chính xác đầu ra mong muốn, và dễ diễn giải hơn, giúp hiểu tại sao mô hình tạo ra một đầu ra cụ thể.
- **Kỹ thuật**:
  - **Sinh có điều kiện**: Sử dụng các đầu vào bổ sung (như bản đồ cạnh, tư thế, hoặc nhãn) để kiểm soát đầu ra.
  - **Thao tác không gian ẩn**: Trong VAEs và GANs, chỉnh sửa không gian ẩn để thay đổi các thuộc tính cụ thể của đầu ra.
  - **Cơ chế chú ý**: Trong transformer, sử dụng trọng số chú ý để xác định phần nào của đầu vào ảnh hưởng đến đầu ra.
  - **AI có thể giải thích (XAI)**: Áp dụng các kỹ thuật như phân tích đặc trưng hoặc bản đồ chú ý để giải thích quyết định của mô hình.
- **SOTA**:
  - **ControlNet** ([ControlNet Paper](https://arxiv.org/abs/2302.05543)): Cho phép kiểm soát chi tiết các mô hình diffusion với các điều kiện như bản đồ cạnh hoặc phân đoạn.
  - **StyleCLIP** ([StyleCLIP Paper](https://arxiv.org/abs/2103.17249)): Kết hợp CLIP với các kỹ thuật chuyển phong cách để kiểm soát phong cách hình ảnh.
  - **Interpretable VAEs** ([Interpretable VAEs Paper](https://arxiv.org/abs/2102.01264)): VAEs với không gian ẩn không rối, cải thiện khả năng kiểm soát và diễn giải.
- **Thách thức**:
  - **Hộp đen**: Các mô hình phức tạp như diffusion hoặc transformer thường khó hiểu, làm giảm tính minh bạch.
  - **Giao diện người dùng**: Cung cấp các cách trực quan để người dùng kiểm soát và diễn giải mô hình là một thách thức.
  - **Đánh đổi hiệu suất**: Các mô hình dễ kiểm soát và diễn giải hơn có thể hy sinh một phần hiệu suất.
  - **Hiệu quả tính toán**: Các kỹ thuật diễn giải như phân tích đặc trưng có thể tốn kém về tính toán.
- **Cơ hội**:
  - **Kiểm soát chi tiết**: Phát triển các phương pháp cho phép kiểm soát từng phần của đầu ra, như chỉnh sửa một đối tượng cụ thể trong ảnh ([Interpretability in Generative AI](https://www.xcubelabs.com/blog/explainability-and-interpretability-in-generative-ai-systems/)).
  - **Diễn giải tự động**: Tạo các công cụ tự động giải thích quyết định của mô hình, như tạo bản đồ chú ý hoặc biểu đồ đặc trưng.
  - **Tích hợp với XAI**: Áp dụng các kỹ thuật XAI để làm cho các mô hình Generative AI minh bạch hơn, đặc biệt trong các ứng dụng nhạy cảm như y tế.
  - **Giao diện tương tác**: Thiết kế các giao diện cho phép người dùng tương tác và điều chỉnh đầu ra trong thời gian thực.

### 2.8. Xử lý vấn đề đạo đức

- **Định nghĩa**: Giải quyết các hệ quả đạo đức của Generative AI, đảm bảo rằng việc sử dụng nó công bằng, minh bạch, và tôn trọng quyền của người dùng cũng như các giá trị xã hội.
- **Kỹ thuật**:
  - **Giảm thiểu thiên vị**: Sử dụng các kỹ thuật như tái cân bằng dữ liệu hoặc điều chỉnh hàm mất để giảm thiên vị trong đầu ra.
  - **Bảo vệ quyền riêng tư**: Áp dụng quyền riêng tư khác biệt (differential privacy) hoặc mã hóa dữ liệu để bảo vệ thông tin người dùng.
  - **Phát hiện deepfake**: Phát triển các công cụ để nhận diện nội dung do AI tạo ra, như sử dụng watermarking hoặc phân tích đặc trưng.
  - **Khung đạo đức**: Áp dụng các khung như Deloitte’s Trustworthy AI Framework để hướng dẫn phát triển và triển khai AI.
- **SOTA**:
  - **Fairness-Aware Training** ([Fairness-Aware Training Paper](https://arxiv.org/abs/1908.09635)): Điều chỉnh quá trình huấn luyện để đảm bảo biểu diễn công bằng qua các nhóm dân số khác nhau.
  - **Explainable AI (XAI)** ([IBM XAI Overview](https://www.ibm.com/think/topics/interpretability)): Các kỹ thuật làm cho quyết định của AI minh bạch và dễ hiểu, tăng lòng tin của người dùng.
  - **Responsible AI Frameworks** ([Microsoft Responsible AI](https://www.microsoft.com/en-us/ai/responsible-ai-resources)): Các công cụ và hướng dẫn từ Microsoft và IBM để đảm bảo AI được phát triển và sử dụng một cách đạo đức.
- **Thách thức**:
  - **Định nghĩa đạo đức**: Không có sự đồng thuận toàn cầu về những gì tạo nên AI đạo đức, gây khó khăn trong việc thiết kế các giải pháp phổ quát.
  - **Triển khai thực tiễn**: Chuyển các nguyên tắc đạo đức thành các kỹ thuật cụ thể là một thách thức lớn.
  - **Quy định chậm trễ**: Công nghệ phát triển nhanh hơn các khung pháp lý, dẫn đến lỗ hổng trong quản lý.
  - **Tác động môi trường**: Huấn luyện và chạy các mô hình lớn tiêu thụ nhiều năng lượng, gây lo ngại về tính bền vững

## 3. Hướng nghiên cứu tiềm năng trong Generative AI cho Vision

### 3.1. Nghiên cứu học thuật (Publish Paper)

#### A. Mô hình đa nhiệm cho Image và Video Generation

- **Mô tả**: Phát triển một mô hình Generative AI duy nhất có khả năng xử lý nhiều nhiệm vụ, như sinh ảnh, sinh video, khử nhiễu, khử mờ, và siêu phân giải, với hiệu quả tính toán tối ưu.
- **Lý do tiềm năng**: Hiện tại, các mô hình thường được thiết kế cho một nhiệm vụ cụ thể, dẫn đến chi phí tính toán cao và khó triển khai trong các ứng dụng thực tế. Một mô hình đa nhiệm có thể giảm chi phí, tăng tính linh hoạt, và cải thiện hiệu suất tổng thể.
- **Thách thức cần giải quyết**:
  - Đảm bảo hiệu suất cao trên nhiều nhiệm vụ mà không làm giảm chất lượng đầu ra.
  - Tối ưu hóa kiến trúc mô hình để xử lý cả dữ liệu ảnh và video, đặc biệt là đảm bảo tính nhất quán thời gian cho video.
  - Xử lý sự khác biệt về độ phức tạp giữa các nhiệm vụ (ví dụ: sinh ảnh đơn giản hơn sinh video).
- **Phương pháp đề xuất**:
  - Kết hợp các kiến trúc như Transformer và Mamba để khai thác phụ thuộc dài hạn và giảm chi phí tính toán.
  - Sử dụng học đa nhiệm (multi-task learning) với các hàm mất tùy chỉnh để cân bằng hiệu suất giữa các nhiệm vụ.
  - Thử nghiệm trên các bộ dữ liệu như DIV2K ([DIV2K Dataset](https://data.vision.ee.ethz.ch/cvl/DIV2K/)) cho ảnh và UCF101 ([UCF101 Dataset](https://www.crcv.ucf.edu/data/UCF101.php)) cho video.
- **Tiềm năng xuất bản**:
  - **Hội nghị**: CVPR, NeurIPS, ICCV.
  - **Tạp chí**: IEEE Transactions on Pattern Analysis and Machine Intelligence (TPAMI), International Journal of Computer Vision (IJCV).
- **Ví dụ tiêu đề bài báo**: "Unified Multi-Task Generative Model for Image and Video Enhancement and Synthesis".

#### B. Học không giám sát cho Video Generation

- **Mô tả**: Phát triển các phương pháp học không giám sát hoặc tự giám sát để huấn luyện các mô hình Video Generation, giảm phụ thuộc vào dữ liệu ghép đôi (ví dụ: video thật và video giả).
- **Lý do tiềm năng**: Dữ liệu ghép đôi cho các nhiệm vụ như Video Inpainting hoặc Video Restoration rất khó thu thập, đặc biệt trong các ứng dụng thực tế như y tế hoặc giám sát. Học không giám sát có thể mở rộng khả năng huấn luyện trên dữ liệu thực tế, tăng tính tổng quát hóa.
- **Thách thức cần giải quyết**:
  - Đảm bảo chất lượng đầu ra khi không có dữ liệu ghép đôi, đặc biệt với các video có nội dung phức tạp.
  - Xử lý sự đa dạng của dữ liệu video (độ phân giải, độ dài, loại nội dung).
  - Ngăn chặn hiện tượng mode collapse trong các mô hình không giám sát.
- **Phương pháp đề xuất**:
  - Sử dụng các kỹ thuật tự giám sát như contrastive learning hoặc masked video modeling, tương tự như trong MAE ([Masked Autoencoders](https://arxiv.org/abs/2111.06377)).
  - Kết hợp các mô hình diffusion với học không giám sát để cải thiện chất lượng video.
  - Thử nghiệm trên các bộ dữ liệu như Kinetics ([Kinetics Dataset](https://deepmind.com/research/open-source/kinetics)) hoặc Vimeo-90K ([Vimeo-90K Dataset](http://toflow.csail.mit.edu/)).
- **Tiềm năng xuất bản**:
  - **Hội nghị**: CVPR, ICCV, ECCV.
  - **Tạp chí**: IJCV, Computer Vision and Image Understanding (CVIU).
- **Ví dụ tiêu đề bài báo**: "Unsupervised Video Generation with Self-Supervised Temporal Consistency".

#### C. Kiểm soát chi tiết trong Conditional Video Generation

- **Mô tả**: Phát triển các mô hình cho phép kiểm soát chi tiết hơn trong quá trình sinh video, chẳng hạn như chỉnh sửa từng phần của video (ví dụ: thay đổi biểu cảm của một người) dựa trên prompt văn bản hoặc hình ảnh.
- **Lý do tiềm năng**: Các mô hình Conditional Video Generation hiện tại, như ControlNet ([ControlNet Paper](https://arxiv.org/abs/2302.05543)), thường thiếu khả năng kiểm soát chi tiết, hạn chế ứng dụng trong sản xuất nội dung sáng tạo hoặc chỉnh sửa video chuyên nghiệp.
- **Thách thức cần giải quyết**:
  - Đảm bảo tính nhất quán thời gian khi chỉnh sửa từng phần của video.
  - Xử lý các prompt phức tạp, như các mô tả compositional (ví dụ: "thay đổi màu áo của người trong video mà không ảnh hưởng đến nền").
  - Giảm chi phí tính toán để hỗ trợ chỉnh sửa thời gian thực.
- **Phương pháp đề xuất**:
  - Mở rộng ControlNet với các điều kiện bổ sung, như bản đồ phân đoạn hoặc mô tả văn bản chi tiết.
  - Sử dụng các mô hình Transformer với cơ chế chú ý cục bộ (local attention) để tập trung vào các phần cụ thể của video.
  - Thử nghiệm trên các bộ dữ liệu như DAVIS ([DAVIS Dataset](https://davischallenge.org/)) hoặc YouTube-VOS ([YouTube-VOS Dataset](https://youtube-vos.org/)).
- **Tiềm năng xuất bản**:
  - **Hội nghị**: CVPR, NeurIPS, SIGGRAPH.
  - **Tạp chí**: ACM Transactions on Graphics (TOG), IJCV.
- **Ví dụ tiêu đề bài báo**: "Fine-Grained Control in Conditional Video Generation: Object-Level Editing with Temporal Consistency".

#### D. Phát hiện deepfake trong Video Generation

- **Mô tả**: Phát triển các phương pháp phát hiện deepfake trong video được tạo bởi các mô hình Generative AI, sử dụng các kỹ thuật như watermarking, phân tích đặc trưng, hoặc học đa phương thức.
- **Lý do tiềm năng**: Deepfake là một vấn đề đạo đức lớn trong Video Generation, đặc biệt với các mô hình như Sora ([Sora](https://openai.com/sora)). Các công cụ phát hiện hiệu quả là cần thiết để đảm bảo an toàn và minh bạch.
- **Thách thức cần giải quyết**:
  - Đảm bảo tính chính xác trong phát hiện, đặc biệt với các video chất lượng cao từ các mô hình tiên tiến.
  - Xử lý các kỹ thuật tránh phát hiện (anti-detection) mà các mô hình deepfake có thể sử dụng.
  - Tích hợp phát hiện vào các hệ thống thời gian thực.
- **Phương pháp đề xuất**:
  - Sử dụng các kỹ thuật watermarking ẩn để gắn nhãn video do AI tạo ra.
  - Kết hợp các mô hình học đa phương thức (hình ảnh, âm thanh, và đặc trưng thời gian) để phát hiện deepfake.
  - Thử nghiệm trên các bộ dữ liệu như FaceForensics++ ([FaceForensics++ Dataset](https://github.com/ondyari/FaceForensics)) hoặc DeepFake Detection Challenge ([DFDC Dataset](https://ai.facebook.com/datasets/dfdc/)).
- **Tiềm năng xuất bản**:
  - **Hội nghị**: CVPR, ICCV, ACM Multimedia.
  - **Tạp chí**: IEEE Transactions on Information Forensics and Security (TIFS), IJCV.
- **Ví dụ tiêu đề bài báo**: "Robust Deepfake Detection in Generative Video: A Multi-Modal Watermarking Approach".

### 3.2. Nghiên cứu sáng chế (Patent)

#### A. Mô hình Generative AI nhẹ cho thiết bị biên

- **Mô tả**: Thiết kế một mô hình Generative AI (cho Image hoặc Video Generation) có thể chạy trên thiết bị biên, như điện thoại thông minh, với hiệu suất cao và chi phí tính toán thấp.
- **Lý do tiềm năng**: Các mô hình Generative AI hiện tại, như Stable Diffusion ([Stable Diffusion](https://huggingface.co/stabilityai/stable-diffusion-2-1)), yêu cầu tài nguyên lớn, không phù hợp cho thiết bị di động. Một mô hình nhẹ có thể mở ra các ứng dụng như sinh ảnh/video thời gian thực trên điện thoại.
- **Thách thức cần giải quyết**:
  - Giảm kích thước mô hình mà không làm giảm chất lượng đầu ra.
  - Tối ưu hóa cho các phần cứng có hạn chế, như GPU di động hoặc NPUs.
  - Đảm bảo tính nhất quán thời gian cho các ứng dụng video.
- **Phương pháp đề xuất**:
  - Sử dụng các kỹ thuật như quantization, pruning, và chưng cất kiến thức để giảm kích thước mô hình.
  - Thiết kế kiến trúc hybrid kết hợp Mamba và Transformer để khai thác phụ thuộc dài hạn với chi phí thấp.
  - Tích hợp với các nền tảng như TensorFlow Lite ([TensorFlow Lite](https://www.tensorflow.org/lite)) để tối ưu hóa suy luận.
- **Tiềm năng patent**:
  - Giải pháp có thể liên quan đến một kiến trúc mô hình mới hoặc phương pháp tối ưu hóa suy luận trên thiết bị biên.
- **Ví dụ tiêu đề patent**: "Efficient Generative AI for Edge Devices: A Quantized Diffusion Model for Real-Time Image and Video Generation".

#### B. Hệ thống sinh video tương tác thời gian thực

- **Mô tả**: Phát triển một hệ thống cho phép người dùng tạo và chỉnh sửa video thời gian thực dựa trên prompt văn bản hoặc hình ảnh, với khả năng kiểm soát chi tiết và giao diện trực quan.
- **Lý do tiềm năng**: Sinh video thời gian thực là một thách thức lớn do yêu cầu tính toán cao. Một hệ thống như vậy có thể được sử dụng trong các ứng dụng như trò chơi, thực tế ảo, hoặc biên tập video chuyên nghiệp.
- **Thách thức cần giải quyết**:
  - Đảm bảo tốc độ sinh video cao (ví dụ: 30fps) với chất lượng cao.
  - Xử lý các prompt phức tạp trong thời gian thực, như chỉnh sửa từng phần của video.
  - Tối ưu hóa giao diện người dùng để dễ sử dụng.
- **Phương pháp đề xuất**:
  - Sử dụng các mô hình diffusion với các phương pháp lấy mẫu nhanh, như DDIM ([DDIM Paper](https://arxiv.org/abs/2010.02502)).
  - Tích hợp các mô hình như ControlNet để hỗ trợ kiểm soát chi tiết.
  - Phát triển giao diện kéo-thả hoặc nhập văn bản dựa trên các công cụ như React ([React](https://reactjs.org/)).
- **Tiềm năng patent**:
  - Giải pháp có thể liên quan đến việc tích hợp các mô hình diffusion với các kỹ thuật tăng tốc và giao diện người dùng tùy chỉnh.
- **Ví dụ tiêu đề patent**: "Real-Time Interactive Video Generation System with Fine-Grained Control and Intuitive Interface".

#### C. Công cụ chỉnh sửa video dựa trên AI với giao diện trực quan

- **Mô tả**: Phát triển một công cụ chỉnh sửa video dựa trên AI cho phép người dùng không chuyên thực hiện các chỉnh sửa phức tạp (như thay đổi phong cách, thêm đối tượng) thông qua giao diện trực quan, như kéo-thả hoặc nhập prompt văn bản.
- **Lý do tiềm năng**: Các công cụ chỉnh sửa video hiện tại, như Adobe Premiere, thường yêu cầu kỹ năng chuyên môn. Một công cụ dễ sử dụng có thể mở rộng ứng dụng của Generative AI trong chỉnh sửa video cho người dùng phổ thông.
- **Thách thức cần giải quyết**:
  - Đảm bảo giao diện trực quan và dễ hiểu cho người dùng không chuyên.
  - Xử lý các chỉnh sửa phức tạp (như thay đổi biểu cảm của người trong video) với độ chính xác cao.
  - Tối ưu hóa hiệu suất để hỗ trợ chỉnh sửa thời gian thực.
- **Phương pháp đề xuất**:
  - Tích hợp các mô hình như InstructPix2Pix ([InstructPix2Pix Paper](https://arxiv.org/abs/2211.09800)) để hỗ trợ chỉnh sửa dựa trên văn bản.
  - Phát triển giao diện người dùng dựa trên các công cụ như Tailwind CSS ([Tailwind CSS](https://tailwindcss.com/)) và React.
  - Sử dụng các kỹ thuật như mixed precision training để tăng tốc độ xử lý.
- **Tiềm năng patent**:
  - Giải pháp có thể liên quan đến việc tích hợp các mô hình Generative AI với giao diện người dùng tùy chỉnh và các kỹ thuật tối ưu hóa.
- **Ví dụ tiêu đề patent**: "User-Friendly AI-Powered Video Editing Tool with Intuitive Interface for Non-Expert Users".

