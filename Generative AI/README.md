Cảm ơn bạn đã làm rõ. Mình sẽ điều chỉnh lại lộ trình học Generative AI đã xây dựng trước đó theo đúng thứ tự thời gian phát triển của các phương pháp trong ảnh mà bạn cung cấp: bắt đầu từ Bayesian Networks, Restricted Boltzmann Machines, Variational Autoencoders, GANs, Normalizing Flows, Autoregressive Models, Energy-based Models và cuối cùng là Diffusion Models.

Mình sẽ giữ nguyên cấu trúc lý thuyết - notebook - ứng dụng thực tế như trước, và cập nhật thứ tự sao cho phù hợp với tiến trình phát triển học thuật.
Mình sẽ quay lại sớm với bản cập nhật hoàn chỉnh.


# Lộ trình học Generative AI (Theo tiến trình lịch sử)

Để nắm vững Generative AI, người học cần hiểu sâu các mô hình sinh từ cổ điển đến hiện đại. Lộ trình dưới đây trình bày 8 nhóm mô hình quan trọng theo thứ tự lịch sử: **Bayesian Networks**, **Restricted Boltzmann Machines (RBM)**, **Variational Autoencoders (VAE)**, **Generative Adversarial Networks (GAN)**, **Normalizing Flows**, **Autoregressive Models**, **Energy-based Models (EBM)**, và **Denoising Diffusion Models**. Mỗi mục gồm phần **lý thuyết chi tiết** (cơ chế sinh dữ liệu), **trực giác toán học**, **tài liệu đọc tham khảo** (các paper gốc, sách, blog kỹ thuật), **notebook/mã mẫu thực hành**, và **ứng dụng nổi bật**. Lộ trình này giúp học viên hiểu rõ lý thuyết và triển khai được mô hình, phục vụ nghiên cứu hoặc phát triển sản phẩm.

---

## Bayesian Networks (Mạng Bayes)

* **Lý thuyết chi tiết:** Mạng Bayes là mô hình đồ thị xác suất có hướng (Directed Acyclic Graphs – DAG) mô tả quá trình sinh dữ liệu. Mỗi nút trong đồ thị biểu diễn một biến ngẫu nhiên, và các cạnh có hướng biểu thị quan hệ điều kiện. Phân phối xác suất chung của tập hợp các biến được phân tích thành tích của các phân phối có điều kiện tại mỗi nút:

  $$
  P(X_1,\dots,X_n) = \prod_{i=1}^n P(X_i \mid \mathrm{Parents}(X_i))
  $$
  
  Điều này tương đương việc coi các biến được sinh theo thứ tự topological của đồ thị, mỗi biến phụ thuộc ngẫu nhiên vào các nút cha của nó. Mạng Bayes cho phép **mô phỏng (sampling)** dữ liệu bằng cách sinh từng nút lần lượt theo phân phối điều kiện, do đó thực sự là mô hình sinh (generative). Ví dụ tiêu biểu là mô hình Naive Bayes (một trường hợp đặc biệt, cho dữ liệu đa biến độc lập có liên quan qua lớp nhãn).
* **Trực giác toán học:** Về toán học, mạng Bayes thể hiện quan hệ độc lập có điều kiện (conditional independence) theo giả thiết Markov cục bộ: mỗi biến độc lập với các biến không có hậu duệ (non-descendants) trong DAG, khi biết giá trị của các cha (parents). Điều này giảm thiểu số lượng tham số cần học so với mô hình liền mạch, nhưng vẫn cho phép biểu diễn phân phối chung của dữ liệu. Các bảng xác suất điều kiện (CPTs) tại mỗi nút cung cấp phân phối của biến đó dựa vào từng kết hợp giá trị của cha. Trong thực nghiệm, phần học mạng Bayes thường là bài toán ước lượng tham số (từ dữ liệu có gắn nhãn hoặc không nhãn) và đôi khi cả cấu trúc đồ thị.
* **Tài liệu đọc:** Sách tiêu chuẩn về lý thuyết Đồ thị xác suất như *Probabilistic Graphical Models* của Koller & Friedman (2009) hoặc chương về Mạng Bayes trong sách *Pattern Recognition and Machine Learning* của Bishop. Các bài báo kinh điển như Judea Pearl (1988) giới thiệu nền tảng Mạng Bayes. Ngoài ra, tìm hiểu các tutorial như Stanford CS221 về mạng Bayes sẽ rất hữu ích.
* **Notebook/Mã mẫu:** Có thể triển khai demo bằng thư viện PGM như **pgmpy** hoặc **Pyro** (Python) để xây dựng mô hình mạng Bayes và thực hiện suy luận, sinh mẫu (inference và sampling). Ví dụ, xây mô hình Naive Bayes tự viết (với CPT học từ dữ liệu) để sinh các ví dụ giả lập.
* **Ứng dụng nổi bật:** Mạng Bayes được dùng rộng rãi trong chẩn đoán y khoa (hội chứng bệnh), hệ khuyến nghị (cộng tác lọc), nhận dạng mẫu, và phân tích nguyên nhân hệ thống. Ví dụ, mô hình Naive Bayes (có cấu trúc đầy đủ đặc biệt) là bộ phân loại sinh đơn giản nhưng mạnh mẽ cho văn bản (spam filtering) và y sinh.

---

## Restricted Boltzmann Machines (RBM)

* **Lý thuyết chi tiết:** RBM là mô hình sinh dạng hai lớp (visible và hidden) không có kết nối ngang trong cùng lớp (không dây chéo), đề xuất bởi Smolensky (1986) và phát triển bởi Hinton và cộng sự (2002). Nó định nghĩa năng lượng của mỗi cấu hình (v,h) theo công thức:

  $$
  E(v,h) = -\sum_{i}a_i v_i - \sum_{j}b_j h_j - \sum_{i,j} v_i w_{ij} h_j,
  $$

  trong đó $v_i$, $h_j$ thuộc ${0,1}$ là trạng thái của đơn vị visible và hidden, \$a\_i,b\_j\$ là bias, \$w\_{ij}\$ là trọng số kết nối. Xác suất liên hợp của (v,h) là \$P(v,h)\propto\exp(-E(v,h))\$. Vì hai lớp tách biệt, RBM cho phép tính xác suất biên của latent và huấn luyện tương đối dễ thông qua thuật toán *Contrastive Divergence* để xấp xỉ gradient log-likelihood. RBM thường được dùng làm mô-đun tiền huấn luyện trong mạng sâu (deep belief networks).
* **Trực giác toán học:** Về trực giác, RBM học phân phối (latent) qua cách cập nhật trọng số để giảm năng lượng cho cấu hình dữ liệu và tăng năng lượng cho cấu hình khác (chiến lược học gradient). Do cách thiết kế bipartite, ta có thể tách quá trình lấy mẫu (gibbs sampling song song) cho các lớp. Tính gradient của log-độ khả dĩ đơn giản: \$\frac{\partial \log P(v)}{\partial w\_{ij}} = \langle v\_i h\_j\rangle\_{\text{data}} - \langle v\_i h\_j\rangle\_{\text{model}}\$ (hiệu giữa kỳ vọng dưới phân phối dữ liệu và mô hình).
* **Tài liệu đọc:**

  * Geoffrey Hinton (2002), *A Practical Guide to Training Restricted Boltzmann Machines*, tech report (giới thiệu kỹ thuật CD).
  * G. E. Hinton & R. Salakhutdinov (2006), *Science* 313:504, "Reducing the Dimensionality of Data with Neural Networks" (áp dụng RBM vào giảm kích thước dữ liệu).
  * Bài viết hướng dẫn của Lilian Weng hoặc các tutorial về RBM trên Medium, Paperspace.
* **Notebook/Mã mẫu:** Có nhiều triển khai mẫu RBM. Ví dụ, blog Paperspace hướng dẫn RBM bằng PyTorch, hoặc kho GitHub **bacnguyencong/rbm-pytorch**. Bạn cũng có thể tìm các notebook Colab/Demo đơn giản: ví dụ huấn luyện RBM trên tập MNIST với PyTorch hoặc TensorFlow để sinh ảnh số mới.
* **Ứng dụng nổi bật:** RBM được dùng cho **học đặc trưng** (feature learning), **giảm chiều dữ liệu**, tiền huấn luyện mạng sâu, và trong các hệ thống đề xuất (collaborative filtering, như đề xuất phim). Theo Hinton, RBM được áp dụng trong nhận dạng mẫu (classification), lọc cộng tác, học đặc trưng, mô hình chủ đề (topic modelling) và thậm chí trong cơ học lượng tử. Ví dụ Netflix từng sử dụng mô hình RBM để gợi ý phim.

---

## Variational Autoencoders (VAE)

* **Lý thuyết chi tiết:** VAE (Kingma & Welling, 2014) là một mô hình sinh cấu trúc (deep generative model) kết hợp ý tưởng autoencoder với phương pháp biến phân. Mạng gồm hai phần chính: *encoder* và *decoder*. Encoder học ánh xạ đầu vào \$x\$ sang một phân phối *latent* \$q\_\phi(z|x)\$ (thường chọn Gaussian), thay vì một điểm cố định như autoencoder thông thường. Decoder sau đó giải nén ngẫu nhiên từ \$z \sim q\_\phi(z|x)\$ để sinh ngược ra \$x’\$ sao cho \$p\_\theta(x|z)\$ khớp dữ liệu. Hai mạng này cùng học thông qua tối đa hóa Hàm *evidence lower bound* (ELBO) của log-likelihood dữ liệu, sử dụng *kỹ thuật tái tham số hóa (reparameterization trick)* để chạy lan truyền ngược trên sampling layer. Kết quả, VAE học được phân phối dữ liệu tiệm cận (mô hình sinh) và tạo mẫu mới bằng cách lấy \$z\sim p(z)\$ (ví dụ chuẩn), rồi decode sang dữ liệu.
* **Trực giác toán học:** Cách suy nghĩ: Encoder biến dữ liệu thành khoảng không gian ẩn xác suất (gaussian), thay vì điểm xác định. Điều này cho phép học latent space có cấu trúc, tránh overfitting. Hàm mục tiêu là ELBO:

  $$
  \mathcal{L}(x) = \mathbb{E}_{q_\phi(z|x)}[\ln p_\theta(x|z)] - D_{KL}(q_\phi(z|x)\parallel p(z)),
  $$

  trong đó \$p(z)\$ thường là chuẩn đa biến. Hồi quy phân phối biến phân đảm bảo decoder sinh ra ví dụ thực tế, đồng thời đưa phân phối \$q\_\phi(z|x)\$ tiệm cận \$p(z)\$ qua phần KL. Bằng cách tối đa ELBO, VAE tối ưu hóa gần đúng log-likelihood dữ liệu.
* **Tài liệu đọc:**

  * Bài báo gốc: Kingma & Welling (2014), *Auto-Encoding Variational Bayes*.
  * Tutorial hiện đại, ví dụ *"An Introduction to Variational Autoencoders"* (Ardizzone et al., 2019), hoặc bài hướng dẫn của Arxiv Sanity.
  * Các blog giải thích VAE như Jaan Nystr"om: “What is a Variational Autoencoder?” giới thiệu trực quan cấu trúc.
* **Notebook/Mã mẫu:** Thư viện Keras, PyTorch đều có ví dụ VAE. Ví dụ, Keras cung cấp tutorial Autoencoder (hãy điều chỉnh thành VAE). Các repository trên GitHub (ví dụ *martinarjovsky/VAE*) có code mẫu. Ngoài ra, Google Colab và Kaggle có nhiều notebook hướng dẫn học VAE tạo ảnh MNIST, CelebA.
* **Ứng dụng nổi bật:** VAE thường dùng trong sinh ảnh (hình ảnh, mẫu), học biểu diễn ẩn (representation learning) và tăng cường dữ liệu. Ngoài sinh ảnh, VAE áp dụng cho bán giám sát (semi-supervised learning) khi gắn nhãn dữ liệu kèm latent, điều chỉnh style chuyển đổi (ví dụ  biến đổi phong cách hình ảnh), và cả sinh văn bản/speech. VAE được chứng minh hữu hiệu trong nhiều domain: từ tách chủ đề văn bản (topic modeling) đến mô hình ẩn trong nhịp sinh học.

---

## Generative Adversarial Networks (GAN)

* **Lý thuyết chi tiết:** GAN (Goodfellow et al., 2014) là khuôn khổ generative mới, gồm hai mạng neural đối kháng: *Generator* và *Discriminator*. Generator cố gắng sinh dữ liệu giả trông như thật bằng cách biến noise ngẫu nhiên \$z\$ thành đầu ra \$G(z)\$. Discriminator học phân biệt thật/giả, gán xác suất \$D(x)\$ rằng \$x\$ là thật. Hai mạng được huấn luyện cùng nhau trong một trò chơi zero-sum: Generator được huấn luyện để *lừa* Discriminator (minimize \$\log(1-D(G(z)))\$), còn Discriminator thì maximize khả năng phân biệt (maximize \$\log D(x)\$). Mục tiêu tối hậu là hướng xác suất phân phối sinh của generator tiến tới phân phối thực của dữ liệu.
* **Trực giác toán học:** GAN tối đa hóa hàm mục tiêu min-max:

  $$
  \min_G \max_D \, \mathbb{E}_{x\sim p_{\text{data}}}[\log D(x)] + \mathbb{E}_{z\sim p(z)}[\log (1 - D(G(z)))].
  $$

  Discriminator cải thiện khả năng nhận biết mẫu giả, còn Generator học cải thiện để Discriminator đưa ra sai lầm. Khi huấn luyện hội tụ lý tưởng, Discriminator không thể phân biệt (kết quả \$D(x)=0.5\$). Thuật toán đòi hỏi cân bằng và dễ gặp các vấn đề như **mode collapse** (mất đa dạng) hay **mất ổn định** trong huấn luyện.
* **Tài liệu đọc:**

  * Bài báo gốc Ian Goodfellow và cs (2014) *Generative Adversarial Nets*.
  * Tutorial và survey: e.g. *NIPS 2016 Tutorial on GANs* (Goodfellow) hay blog tổng hợp (như V7 Labs guide).
  * Các biến thể quan trọng: Wasserstein GAN (Arjovsky et al., 2017), LSGAN, StyleGAN (Karras et al., 2018-2019) với kỹ thuật cải tiến.
* **Notebook/Mã mẫu:** Có vô số code mẫu GAN. Thư viện PyTorch và TensorFlow đều có các ví dụ chính thức (ví dụ PyTorch DCGAN tutorial). Trên GitHub còn các mẫu như **awesome-gan** hoặc các notebook Triển khai GAN tạo ảnh (MNIST, CelebA). Ngoài ra, Colab “Deep Convolutional GAN (DCGAN)” hay “CycleGAN” để tạo ảnh phong cách (style transfer) cũng hữu ích.
* **Ứng dụng nổi bật:** GAN đã cách mạng sinh ảnh: từ tạo ảnh chân dung, phong cảnh (StyleGAN cho khuôn mặt photorealistic) đến tạo ảnh chuyển đổi kiểu dáng (CycleGAN biến đổi phong cảnh giữa mùa, Pix2Pix chuyển ảnh đen trắng thành màu). Ngoài ảnh, GAN dùng trong sinh nhạc, tạo văn bản (GAN văn bản ít phổ biến do tính rời rạc của từ), và trong y sinh (tạo mô hình kết cấu y tế). GAN cũng ứng dụng trong tăng cường dữ liệu (data augmentation) và tạo nội dung (ví dụ DALL-E sử dụng biến thể diffusion/GAN cho ảnh từ văn bản). Theo Wikipedia, GAN là “một khung học máy nổi bật tiếp cận trí tuệ nhân tạo tạo sinh” được giới thiệu năm 2014.

---

## Normalizing Flows (Luồng Hoá Phân phối)

&#x20;*Hình: So sánh sơ đồ hoạt động của GAN, VAE và Flow-based models. Flow-based learning trực tiếp tối ưu xác suất thông qua biến đổi khả nghịch và các hàm density cao cấp.*

* **Lý thuyết chi tiết:** Normalizing Flows (Dinh et al. 2014–2018, Rezende & Mohamed 2015) là lớp mô hình sinh học thống kê học biểu diễn phân phối phức tạp thông qua chuỗi các biến đổi khả nghịch từ một phân phối đơn giản (ví dụ Gaussian chuẩn). Cụ thể, khởi đầu từ \$z\sim \mathcal{N}(0,I)\$, một dãy các phép biến đổi khả nghịch \$f\$ liên tiếp biến \$z\$ thành \$x=f(z)\$ sao cho xác suất \${p\_x(x) = p\_z(f^{-1}(x));\big|\det(\partial f^{-1}/\partial x)\big|}\$. Mỗi biến đổi trong luồng (flow) được thiết kế để có đạo hàm tốt và xác định định thức Jacobian đơn giản (để tính log-likelihood hiệu quả). Khác với GAN/VAE, mô hình này học trực tiếp mật độ xác suất dữ liệu bằng **tối đa hóa log-likelihood**.
* **Trực giác toán học:** Giải thích trực quan của Lilian Weng: Flow-based models “chinh phục vấn đề khó này với sự trợ giúp của *normalizing flows*, một công cụ thống kê mạnh cho ước lượng mật độ”. Ý tưởng là áp dụng một biến đổi khả nghịch \$f\$ sao cho phân phối mới \$p\_X\$ thu được phức tạp hơn phân phối gốc; toàn bộ hàm mất là \$-\log p\_X(x)\$. Ưu điểm của flows là có thể tính mật độ và sinh mẫu trực tiếp, nhưng cần duy trì tính khả nghịch của mỗi bước biến đổi.
* **Tài liệu đọc:**

  * Danilo Rezende & Mohamed (2015), *Variational Inference with Normalizing Flows* (ý tưởng chính về flows).
  * Laurent Dinh et al. (2016), *Density Estimation using Real NVP* (KDD) – giới thiệu biến thể RealNVP.
  * Kingma et al. (2018), *Glow* – cải thiện luồng với invertible 1x1 conv.
  * Bài viết blog Lilian Weng (2018) về Flow-based models với giải thích chi tiết và ví dụ (trích nguồn ở trên).
* **Notebook/Mã mẫu:** UvA DL Notebooks có tutorial Flow-based modeling, bao gồm code PyTorch để xây dựng và huấn luyện flows với MNIST/ CIFAR. Các thư viện như PyTorch Lightning và TensorFlow Probability đều hỗ trợ flows (e.g. RealNVP, Masked Autoregressive Flow). GitHub có nhiều mẫu: ví dụ **pytorch-flows**, hoặc thư viện **nflows** (PyTorch). Bạn có thể thử triển khai RealNVP từ đầu theo hướng dẫn trên.
* **Ứng dụng nổi bật:** Flows phù hợp với những tác vụ cần ước lượng mật độ chính xác: ví dụ tạo mẫu ảnh chất lượng (likelihood cao) và nén dữ liệu. Chúng được dùng cho **tổng hợp mẫu** (sampling), **ước lượng mật độ** (density estimation) và **suy diễn latent**. Flows ít được dùng trong ứng dụng văn bản vì chi phí tính toán, nhưng có trong model time-series (như WaveFlow cho audio). Ứng dụng điển hình là trong compress và rareness score (đánh giá độ hiếm của mẫu).

---

## Autoregressive Models (Mô hình Tự hồi quy)

* **Lý thuyết chi tiết:** Các mô hình tự hồi quy (AR) mô hình xác suất chung bằng cách phân tích liên tiếp từng thành phần của dữ liệu với quan hệ điều kiện. Cụ thể, với dữ liệu đa chiều \$\mathbf{x} = (x\_1,\dots,x\_D)\$, ta có:

  $$
    p(\mathbf{x}) = \prod_{i=1}^D p(x_i \mid x_1,\dots,x_{i-1}),
  $$

  áp dụng định lý chuỗi. Mỗi điều kiện được ước lượng bằng mạng neural nhận các giá trị trước đó làm đầu vào (ví dụ MLP hoặc CNN có che chắn). Nhờ đó mô hình này luôn tính được log-likelihood chính xác và sinh mẫu từng bước (predict từng biến). Ví dụ nổi tiếng: **PixelRNN/PixelCNN** (Oord et al. 2016) sinh ảnh pixel theo quy tắc scanline, và **WaveNet** sinh sóng âm thanh mẫu-timestep.
* **Trực giác toán học:** Quan trọng nhất là đảm bảo tách bạch thông tin: mỗi phần (pixel, token…) chỉ phụ thuộc vào các phần đã sinh trước đó. Trực giác là biến số \$x\_1\$ sinh đầu tiên, sau đó \$x\_2\$ dựa vào \$x\_1\$, v.v. (hình mô tả mạng Bayesian fully-visible). Tính toán có thể rất đắt khi sinh mẫu (phải dự đoán tuần tự), nhưng dễ huấn luyện vì log-likelihood có thể ước lượng xấp xỉ. Một số biến thể (MADE, PixelCNN++) tăng tốc bằng masking hoặc học tuần tự có điều chỉnh.
* **Tài liệu đọc:**

  * Aaron van den Oord et al. (2016), *PixelRNN/PixelCNN* (ICML) – tài liệu quan trọng về AR cho ảnh.
  * Nal Kalchbrenner et al. (2016), *Video Pixel Networks* (AR cho video).
  * Yu Zhang et al. (2017), *PixelCNN++*.
  * Bài viết tổng quan như Tu Nguyen (blog) về Autoregressive Models (bao gồm MADE, WaveNet, Self-Attention AR).
* **Notebook/Mã mẫu:** Ví dụ trên Github: **pytorch-pixel-cnn** hoặc TensorFlow models, *WaveNet for audio*. Trên UvA Deep Learning có Tutorial 12 về AR image modeling. Thư viện **PyTorch/TF Distributions** cung cấp lớp *MADE* hay *Autoregressive Flow* triển khai AR networks. Bạn có thể thử train PixelCNN++ trên MNIST hoặc CIFAR.
* **Ứng dụng nổi bật:** AR thường dùng trong sinh chuỗi tuần tự: **sinh ảnh pixel-thuật toán**, **sinh văn bản** (ví dụ chuỗi từ, như GPT là AR trong không gian embedding), **sinh âm thanh** (WaveNet cho speech). Ngoài ra AR áp dụng trong model ranking (language modeling) hay anomaly detection: ví dụ PixelCNN++ được dùng cho phát hiện bất thường trong ảnh.

---

## Energy-based Models (Mô hình dựa trên năng lượng)

* **Lý thuyết chi tiết:** Energy-based Models (EBM) định nghĩa một hàm năng lượng \$E\_\theta(x)\$ cho mỗi cấu hình dữ liệu \$x\$, và xác suất được cho bởi \$p\_\theta(x)\propto \exp(-E\_\theta(x))\$ (có thêm hằng số chuẩn hóa \$Z\$). Một ví dụ cổ điển là Mạng Boltzmann đầy đủ (không hạn chế) và Deep Boltzmann Machines, nhưng EBM hiện đại coi neural network là hàm năng lượng (Vi. Francis, Lecun et al.). Mục tiêu là học để \$E(x)\$ thấp cho dữ liệu thật và cao cho dữ liệu không phải mẫu thật. Huấn luyện thường phức tạp do không thể tính \$Z\$; ta dùng các kỹ thuật như MCMC (Gibbs sampling), Contrastive Divergence, hay training mô phỏng (score matching, JEM...).
* **Trực giác toán học:** EBMs nhìn từ góc độ học xác suất: mô hình không xác định phân phối ngầm định mà chỉ học năng lượng. Sự khác biệt với GAN hay VAE là không có quá trình sinh dữ liệu trực tiếp; thay vào đó, ta thực hiện sampling từ \$p\_\theta(x)\propto e^{-E(x)}\$ (dùng MCMC hoặc Langevin dynamics). Điều này giống mô hình tương tác các hạt dao động trong thế năng (Maxwell-Boltzmann). EBMs có thể coi là tổng quát, cho phép xây dựng các mạng complex làm hàm năng lượng. Gần đây, EBMs có khả năng cạnh tranh với GAN về chất lượng mẫu nếu huấn luyện tốt.
* **Tài liệu đọc:**

  * Tutorial UvA về Energy-based models (Tutorial 8), cung cấp giới thiệu và ví dụ.
  * Yann LeCun (2006+), *A Tutorial on Energy-Based Learning* – nền tảng EBM.
  * Forney & Yuille, *Probabilistic Inference and Energy Minimization in Structured Models*.
  * Blog phân tích EBM: ví dụ blog “Strong EBMs vs GANs” (A. Jolicoeur), “Implicit energy-based models” (Song & Ermon).
* **Notebook/Mã mẫu:** Có mã mẫu EBM trong kho GitHub của tác giả (ví dụ Xie et al. “Cooperative Networks” code). Một số tutorial dùng EBM để sinh mẫu điểm điểm (toy data). Các framework như PyTorch không có sẵn hàm EBM, nhưng bạn có thể định nghĩa module với logit = -Energy và sử dụng MCMC sampling (như function pytorch LPM). Các bài demo thường chạy sampling Langevin từ noise.
* **Ứng dụng nổi bật:** EBMs được nghiên cứu cho **sinh ảnh** (NCSN/Diffusion ban đầu được xem dưới góc độ score matching – một dạng EBM ẩn), phát hiện bất thường (anomaly detection) do tính linh hoạt trong ước lượng mật độ, và trong xử lý dữ liệu phi cấu trúc (do EBMs không cần xấp xỉ explicit distribution form). Theo \[47], EBMs “đã thể hiện vượt trội so với các GAN mạnh trong một số trường hợp” khi được huấn luyện đúng kỹ thuật. Ví dụ, EBMs đã được thử nghiệm cho sinh ảnh khuôn mặt (Convolutional EBMs) và liên tục được nghiên cứu để kết hợp với mô hình lai GAN/Flow.

---

## Denoising Diffusion Models (Mô hình Khuếch tán Khử nhiễu)

* **Lý thuyết chi tiết:** Đây là thế hệ mới nhất của mô hình sinh hình ảnh chất lượng cao. Như định nghĩa trong Diffusion Models (2015 từ Sohl-Dickstein et al.), ý tưởng là mô hình hóa quá trình khuếch tán ngược: bắt đầu từ một phân phối thực (các ảnh thật), lặp lại thêm nhiễu Gaussian nhỏ qua nhiều bước để chuyển thành phân phối Gaussian thuần túy (nhiễu trắng). Sau đó, học một mạng neural (**noise predictor**) để học quá trình ngược (removal) từng bước, tức học cách từ ảnh nhiễu dự đoán ảnh ít nhiễu hơn. Kết quả, ta có thể sinh ảnh mới bằng cách bắt đầu từ ảnh noise hoàn toàn và lặp lại bước denoising nhiều lần. Phiên bản phổ biến là Denoising Diffusion Probabilistic Model (DDPM, Ho et al. 2020), được huấn luyện tối đa ELBO tương tự VAE, kết hợp với ý tưởng score matching (gần gũi với EBMs).
* **Trực giác toán học:** Một cách hình dung: giả sử tập dữ liệu ảnh “cloud” trong không gian ảnh. Thêm nhiễu liên tục sẽ làm nó lan dần đến phân phối Gaussian (nhiệt độ cao). Mạng học khuếch tán là học mô phỏng ngược quá trình này (như chơi trò ú tim trên không gian ảnh) – mạng học cách “nhìn thấy” noise và phục hồi tín hiệu. Từng bước, mạng cố gắng tối đa log-likelihood mẫu (bằng huấn luyện biến phân). Bài báo gốc chứng minh diffusion models có thể đạt chất lượng ảnh vượt trội (FID, IS) so với GAN cổ điển.
* **Tài liệu đọc:**

  * Jonathan Ho et al. (2020), *Denoising Diffusion Probabilistic Models* – paper nền tảng.
  * Song et al. (2020), *Score-Based Generative Modeling through SDEs* – mô hình score-based tương đương.
  * Tutorial CVPR 2022: *Denoising Diffusion-based Generative Modeling* (Arash Vahdat) – slide và video lecture.
  * Bài blog “DDPM from scratch” (learnopencv), “Diffusion models explained” (medium).
* **Notebook/Mã mẫu:** Nhiều công cụ và thư viện hỗ trợ diffusion như **Hugging Face Diffusers**, **OpenAI guided-diffusion**. Ví dụ, Google Colab mẫu chạy Stable Diffusion (đã tích hợp text-to-image). Các tác giả DDPM cũng công bố code. Ngoài ra, thư viện PyTorch có ví dụ đơn giản: học khử nhiễu MNIST, CelebA.
* **Ứng dụng nổi bật:** Đã tạo ra cuộc cách mạng trong sinh ảnh: các mô hình như **Stable Diffusion**, **DALL·E 2**, **Imagen** là ứng dụng diffusion kết hợp học có điều kiện (text, depth, mask). Chúng cho chất lượng ảnh photorealistic cực cao và đang được ứng dụng rộng rãi trong tạo nội dung (AI art). Ngoài ảnh, diffusion cũng mở rộng sang **sinh văn bản** (đã xuất hiện diffusion text), **sinh âm thanh** (WaveGrad, DiffWave), xử lý y tế (hồi phục ảnh MRI) và các bài toán tăng cường dữ liệu. Khác với GAN, diffusion dễ huấn luyện ổn định hơn và cho phép điều khiển sâu (như kết hợp với attention, guidance).

**Tóm lại**, lộ trình trên cung cấp cái nhìn chi tiết từng bước phát triển của các phương pháp tạo sinh: từ mô hình xác suất truyền thống đến các mạng nơ-ron sâu tiên tiến. Mỗi phương pháp đều kèm theo giải thích trực quan, cơ sở toán học, và tài liệu tham khảo hàng đầu (paper, sách, blog), kèm ví dụ thực hành. Người học với nền tảng ML/DL có thể sử dụng roadmap này để đào sâu lý thuyết, triển khai mã mẫu (notebook), và nghiên cứu, phát triển ứng dụng Generative AI một cách hệ thống.
