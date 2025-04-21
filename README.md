
### **Bài toán 1: Tối ưu đa nhiệm xuyên thiết bị khi họp trực tuyến**  

**Solution**:  
- **AI Task Migrator**: Sử dụng mô hình AI để phân tích tải từng thiết bị và đề xuất chuyển task tối ưu. Ví dụ: Khi điện thoại quá nóng, AI tự động chuyển việc render slide sang laptop.  

---

### **Bài toán 2: Trợ lý ảo cá nhân hóa đa thiết bị nhưng không xâm phạm riêng tư**  
**User Scenario**:  
- *Bình, một bác sĩ, dùng trợ lý ảo trên smartwatch để nhắc lịch khám bệnh, đồng thời dùng loa thông minh ở nhà để đọc tin tức y khoa. Tuy nhiên, anh lo ngại lịch trình làm việc chứa thông tin bệnh nhân nhạy cảm có thể bị rò rỉ khi đồng bộ qua cloud.*  

**User Problem**:  
- Dữ liệu cá nhân được lưu trữ tập trung trên cloud, dễ bị tấn công hoặc sử dụng sai mục đích.  
- Trợ lý ảo không nhất quán khi chuyển đổi giữa các thiết bị (ví dụ: smartwatch không nhớ lịch sử tương tác từ loa).  

**User Expectation**:  
- Trợ lý ảo học tập thói quen từ mọi thiết bị nhưng không lưu dữ liệu nhạy cảm lên server.  

**Research**:  
- Báo cáo của McKinsey (2022) cho thấy 72% người dùng ngành y tế từ chối dùng AI vì lo ngại bảo mật.  
- Công nghệ Federated Learning (FL) của Google chỉ áp dụng cho dữ liệu phi cấu trúc, chưa xử lý được thông tin có ngữ cảnh phức tạp.  

**Solution**:  
- **On-Device AI Trainer**: Mỗi thiết bị huấn luyện model cục bộ, sau đó tổng hợp tri thức qua blockchain để đảm bảo tính minh bạch và không lưu trữ dữ liệu gốc.  

---

### **Bài toán 3: Phục hồi kết nối tự động khi chơi game đa thiết bị**  
**User Scenario**:  
- *Nhóm bạn của Minh chơi game AR Pokémon GO cùng lúc trên smartphone, tablet và kính AR. Khi đi vào khu vực sóng yếu, smartphone mất kết nối, khiến cả nhóm không thể cùng săn Pokémon. Họ phải thoát game và kết nối lại thủ công.*  

**User Problem**:  
- Ứng dụng đa thiết bị không tự động phục hồi phiên làm việc khi mất kết nối tạm thời.  
- Người dùng phải thiết lập lại từ đầu, gây gián đoạn trải nghiệm.  

**User Expectation**:  
- Game tự động chuyển vai trò host sang thiết bị có kết nối ổn định nhất mà không cần can thiệp thủ công.  

**Research**:  
- Nghiên cứu từ ĐH Carnegie Mellon (2021) chỉ ra rằng 30% người dùng game AR từ bỏ trận đấu nếu mất kết nối quá 10 giây.  
- Công nghệ Mesh Networking (như GoTenna) mới chỉ áp dụng cho IoT, chưa tích hợp vào nền tảng giải trí.  

**Solution**:  
- **Decentralized Connection Pool**: Tạo mạng lưới P2P giữa các thiết bị, sử dụng AI để dự đoán thiết bị có kết nối ổn định nhất làm host dự phòng.  

---

### **Bài toán 4 (MDE Standalone): Đồng bộ clipboard đa nền tảng**  
**User Scenario**:  
- *Hạnh, một nhà báo, copy đoạn văn bản từ điện thoại Android để dán vào bài viết trên MacBook. Cô phải mở email để gửi cho chính mình vì tính năng Universal Clipboard của Apple không hỗ trợ Android.*  

**User Problem**:  
- Không có giải pháp đồng bộ clipboard hiệu quả giữa các hệ điều hành khác nhau (iOS, Android, Windows).  
- Người dùng phải dùng ứng dụng trung gian (email, messenger), tốn thời gian và tiềm ẩn rủi ro bảo mật.  

**User Expectation**:  
- Sao chép nội dung từ thiết bị này và dán trực tiếp lên thiết bị khác, bất kể nền tảng.  

**Research**:  
- Công cụ như KDE Connect chỉ hoạt động trên Linux/Android, không hỗ trợ iOS.  
- Khảo sát của Gartner (2023): 45% người dùng đa nền tảng đánh mất dữ liệu khi chuyển thiết bị.  

**Solution**:  
- **Cross-OS Clipboard Protocol**: Giao thức mã nguồn mở, sử dụng mã hóa end-to-end và quét QR code để thiết lập kết nối trực tiếp giữa các thiết bị.  

---

### **Bài toán 5 (AI Standalone): Tối ưu pin điện thoại theo thói quen cá nhân**  
**User Scenario**:  
- *Tuấn, một tài xế công nghệ, thường xuyên hết pin điện thoại vào giờ cao điểm do ứng dụng gọi xe chạy ngầm. Anh phải mang theo pin dự phòng cồng kềnh vì chế độ tiết kiệm pin mặc định tắt hết tính năng cần thiết.*  

**User Problem**:  
- Chế độ tiết kiệm pin không thông minh, tắt bừa bãi các ứng dụng quan trọng.  
- Người dùng không thể cá nhân hóa ứng dụng được ưu tiên khi pin yếu.  

**User Expectation**:  
- Hệ thống học thói quen sử dụng để tối ưu pin mà không vô hiệu hóa ứng dụng thiết yếu.  

**Research**:  
- Tính năng Adaptive Battery của Android chỉ dựa trên hành vi chung, không cá nhân hóa.  
- Theo Battery University, việc sạc không tối ưu làm giảm 20% tuổi thọ pin sau 1 năm.  

**Solution**:  
- **Context-Aware Battery AI**: Kết hợp Reinforcement Learning và dữ liệu sensor (GPS, thời gian) để dự đoán ứng dụng cần ưu tiên (ví dụ: ứng dụng gọi xe được giữ chạy nếu người dùng thường làm việc từ 5-7 PM).  

---

### **Bài toán 6 (AI + MDE): Tự động chuyển chế độ thiết bị theo ngữ cảnh**  
**User Scenario**:  
- *Trang, một người mẹ, thường xuyên quên chuyển điện thoại sang chế độ im lặng khi vào họp hoặc chuyển sang chế độ báo thức lớn khi dậy cho con đi học. Cô phải thao tác thủ công nhiều lần trong ngày.*  
Chào bạn,

Rất vui được hỗ trợ bạn với vai trò chuyên gia Generative AI. Ý tưởng của bạn về việc tự động hóa quy trình Approval bằng LLM và Tool Calling là rất thực tế và có tiềm năng lớn trong môi trường công ty A. Dưới đây là cách bạn có thể hoàn thiện ý tưởng này theo form của cuộc thi:

---

**Đề xuất Dự án: Trợ lý Phê duyệt Thông minh (AI Approval Assistant)**

**1. Overview (Tổng quan)**

* **1.1. Background: Current work process status and problem definition (AS-IS)**
    * **Hiện trạng (AS-IS):** Tại công ty A, quy trình yêu cầu phê duyệt (Approval) cho các tác vụ liên quan đến IT và vận hành (như xin cấp IP, mở firewall, truy cập web, yêu cầu tài nguyên, v.v.) được quản lý chặt chẽ và đòi hỏi nhiều thủ tục. Hiện tại, nhân viên phải tự tìm kiếm thông tin hướng dẫn trong một kho tài liệu lớn bao gồm nhiều định dạng (PPT, Word, PDF), nằm rải rác ở nhiều nơi. Quá trình này tốn nhiều thời gian, dễ gây nhầm lẫn do có quá nhiều loại Approval với các bước thực hiện khác nhau, khó ghi nhớ và dễ dẫn đến sai sót khi điền form hoặc thực hiện thủ công. Việc này làm giảm hiệu suất làm việc và gây khó khăn không cần thiết cho nhân viên.
    * **Vấn đề:**
        * Tốn thời gian tìm kiếm thông tin và thực hiện thủ tục.
        * Khó khăn trong việc ghi nhớ và tuân thủ đúng quy trình cho từng loại Approval.
        * Nguy cơ sai sót cao khi thực hiện thủ công.
        * Trải nghiệm không tốt của nhân viên khi phải xử lý các thủ tục phức tạp, lặp đi lặp lại.
        * Kiến thức về quy trình bị phân mảnh, khó cập nhật và quản lý.

* **1.2. Purpose: Goals and objectives to be achieved through AI (TO-BE)**
    * **Mục tiêu chính (Goal):** Xây dựng một giải pháp ứng dụng Generative AI (sử dụng LLM được cung cấp) để đơn giản hóa và tự động hóa quy trình tạo yêu cầu Approval tại công ty A.
    * **Mục tiêu cụ thể (Objectives):**
        * Giảm đáng kể thời gian nhân viên bỏ ra để tìm hiểu và tạo yêu cầu Approval (ước tính giảm >70% thời gian so với hiện tại).
        * Tăng độ chính xác và tính tuân thủ của các yêu cầu Approval bằng cách tự động hóa việc điền thông tin và chọn đúng quy trình.
        * Cải thiện trải nghiệm của nhân viên bằng cách cung cấp một giao diện tương tác trực quan (ví dụ: chatbot) thay vì phải đọc tài liệu và làm thủ công.
        * Trung tâm hóa nguồn kiến thức về quy trình Approval, giúp dễ dàng truy cập và cập nhật.
        * Giải phóng thời gian cho nhân viên để tập trung vào các công việc có giá trị cao hơn.

* **1.3. Overview: Name and main feature of the AI service to be developed**
    * **Tên dịch vụ AI:** **Trợ lý Phê duyệt Thông minh (AI Approval Assistant)** hoặc **AutoApprover**.
    * **Tính năng chính:**
        * **Hỏi đáp về quy trình:** Cho phép người dùng hỏi bằng ngôn ngữ tự nhiên về bất kỳ quy trình Approval nào (VD: "Làm thế nào để xin mở cổng firewall cho ứng dụng X?", "Tôi cần xin quyền truy cập vào trang web Y, phải làm gì?"). AI sẽ dựa trên kho kiến thức (tài liệu đã được xử lý) để trả lời chính xác.
        * **Tự động tạo yêu cầu Approval:** Dựa trên yêu cầu của người dùng (qua chat hoặc điền form đơn giản), AI sẽ xác định đúng loại Approval, thu thập thông tin cần thiết (có thể hỏi thêm người dùng nếu thiếu) và tự động điền vào form/hệ thống Approval tương ứng thông qua cơ chế **Tool Calling** được tích hợp với API của LLM.

* **1.4. Target user group and expected number of users**
    * **Nhóm người dùng mục tiêu:** Toàn bộ nhân viên tại công ty A có nhu cầu thực hiện các yêu cầu Approval liên quan đến công việc (VD: IT, Vận hành, Nhân sự, Mua hàng...).
    * **Số lượng người dùng dự kiến:** Phụ thuộc vào quy mô công ty A (ví dụ: nếu công ty có 500 nhân viên, có thể ước tính 400-500 người dùng tiềm năng). Trong giai đoạn PoC (Proof of Concept), có thể thử nghiệm với một phòng ban cụ thể (khoảng 50-100 người).

* **1.5. Expected benefits (estimated cost saving, target business metrics, etc.)**
    * **Tiết kiệm chi phí:**
        * **Giảm thời gian làm việc:** Giả sử trung bình mỗi nhân viên tiết kiệm được 1-2 giờ/tháng cho việc xử lý Approvals. Với N nhân viên, tổng thời gian tiết kiệm hàng năm là (1-2) * N * 12 giờ. Quy đổi ra chi phí nhân sự (dựa trên mức lương trung bình) sẽ là một con số đáng kể.
        * **Giảm chi phí do sai sót:** Hạn chế các lỗi trong quá trình Approval có thể dẫn đến trì hoãn công việc hoặc vi phạm quy định.
    * **Cải thiện chỉ số kinh doanh/vận hành:**
        * **Tăng tốc độ xử lý yêu cầu:** Giúp các yêu cầu được tạo và gửi đi nhanh hơn, đẩy nhanh tiến độ công việc liên quan.
        * **Tăng năng suất nhân viên:** Nhân viên dành ít thời gian hơn cho thủ tục hành chính, tập trung hơn vào chuyên môn.
        * **Tăng mức độ hài lòng của nhân viên (Employee Satisfaction Score):** Giảm sự phiền phức trong công việc hàng ngày.
        * **Tăng tính tuân thủ (Compliance Rate):** Đảm bảo các yêu cầu luôn được tạo đúng quy trình.

* **1.6. Expected potential to scale-up the service scope and value through increased user base (departments, businesses)**
    * **Mở rộng người dùng:** Sau PoC thành công, dễ dàng triển khai cho toàn bộ các phòng ban trong công ty A.
    * **Mở rộng loại Approval:** Bổ sung thêm các loại tài liệu hướng dẫn cho các quy trình Approval khác (không chỉ IT mà còn HR, Finance, Legal...) vào kho kiến thức của AI.
    * **Mở rộng chức năng:**
        * Tích hợp sâu hơn với các hệ thống backend (ERP, ITSM) để không chỉ tạo yêu cầu mà còn theo dõi trạng thái, tự động cập nhật.
        * Phân tích dữ liệu Approval để đưa ra các đề xuất cải tiến quy trình.
        * Áp dụng mô hình tương tự cho các loại tài liệu và quy trình nội bộ khác (VD: hướng dẫn sử dụng phần mềm, chính sách công ty...).
    * **Mở rộng quy mô công ty:** Có thể triển khai cho các chi nhánh hoặc công ty con khác (nếu có).

**2. PoC Plan (Kế hoạch Proof of Concept)**

* **2.1. List of data to be utilized (type, source, update frequency, etc.)**
    * **Loại dữ liệu:** Tài liệu hướng dẫn quy trình Approval dạng phi cấu trúc (chủ yếu là văn bản, có thể kèm hình ảnh minh họa).
    * **Nguồn dữ liệu:** Kho tài liệu nội bộ hiện có của công ty A (thư mục chia sẻ, Sharepoint, Confluence, v.v.).
    * **Định dạng:** PP- **AI Task Migrator**: Sử dụng mô hình AI để phân tích tải từng thiết bị và đề xuất chuyển task tốụ: Khi điện thoại quá nóng, AI tự động chuyển việc render slide sang laptop.  cập nhật tài liệu vào hệ thống AI khi có thay đổi. Ban đầu, có thể cập nhật thủ công theo đợt (VD: hàng quý), sau đó có thể tự động hóa việc theo dõi thay đổi.

* **2.2. Data collection, preprocessing, and AI utilization Plan**
    * **Thu thập dữ liệu:** Tập hợp toàn bộ các file tài liệu hướng dẫn Approval liên quan từ các nguồn đã xác định.
    * **Tiền xử lý (Preprocessing):**
        * **Chuyển đổi định dạng:** Sử dụng các thư viện/công cụ để trích xuất nội dung text từ các file PPT, Word, PDF sang định dạng văn bản thuần túy (plain text) hoặc Markdown.
        * **Phân đoạn (Chunking):** Chia nhỏ các tài liệu dài thành các đoạn văn bản có ý nghĩa, kích thước phù hợp để LLM xử lý hiệu quả (VD: chia theo section, heading, hoặc số lượng token nhất định).
        * **Làm sạch dữ liệu:** Loại bỏ các thông tin thừa, định dạng không cần thiết.
        * **(Quan trọng) Vector hóa (Embedding):** Sử dụng một mô hình embedding phù hợp (có thể là mô hình riêng hoặc được cung cấp) để chuyển đổi các đoạn văn bản thành các vector số học. Lưu trữ các vector này vào một cơ sở dữ liệu vector (Vector Database).
    * **Kế hoạch sử dụng AI (LLM):**
        * **Kiến trúc RAG (Retrieval-Augmented Generation):**
            1.  Khi người dùng đặt câu hỏi hoặc yêu cầu tạo Approval, hệ thống sẽ chuyển đổi yêu cầu đó thành vector.
            2.  Tìm kiếm các đoạn văn bản (chunk) có vector gần giống nhất với vector yêu cầu trong Vector Database (đây là bước Retrieval).
            3.  Ghép nối yêu cầu gốc của người dùng và các đoạn văn bản liên quan đã tìm được thành một prompt hoàn chỉnh.
            4.  Gửi prompt này đến LLM (thông qua API được cung cấp) để tạo ra câu trả lời hoặc xác định hành động cần thực hiện (Generation).
        * **Sử dụng Tool Calling:**
            1.  Định nghĩa các "tools" (thực chất là các function/API call) tương ứng với các hành động tạo Approval cụ thể (VD: `create_firewall_request(ip_address, port, reason)`, `request_website_access(url, justification)`).
            2.  Trong prompt gửi đến LLM, mô tả rõ các tool này và cách sử dụng.
            3.  Khi LLM nhận diện được yêu cầu cần tạo Approval cụ thể từ người dùng và thông tin liên quan (từ RAG hoặc hỏi thêm người dùng), nó sẽ quyết định gọi tool tương ứng với các tham số cần thiết.
            4.  Hệ thống của bạn sẽ nhận lệnh gọi tool từ LLM, thực thi hành động (VD: gọi API của hệ thống Approval nội bộ, tạo một file yêu cầu...) và trả kết quả về cho LLM (và người dùng).

* **2.3. AI implementation features and applied tasks**
    * **Các tính năng AI cần triển khai:**
        * NLU (Natural Language Understanding): Hiểu yêu cầu người dùng bằng ngôn ngữ tự nhiên.
        * Information Retrieval: Tìm kiếm thông tin chính xác từ kho tài liệu đã xử lý.
        * Text Generation: Sinh ra câu trả lời, giải thích quy trình.
        * Tool/Function Calling: Khả năng nhận biết và gọi các hàm/API bên ngoài để thực hiện tác vụ cụ thể (tạo Approval).
        * Conversational AI: Duy trì ngữ cảnh hội thoại, đặt câu hỏi làm rõ nếu cần.
    * **Các tác vụ ứng dụng:**
        * Question Answering (Trả lời câu hỏi về quy trình).
        * Automated Form Filling / Request Generation (Tự động điền form/tạo yêu cầu).
        * Task Automation (Tự động hóa tác vụ thông qua gọi tool).

* **2.4. Final output type (Chatbot, Copilot)**
    * **Loại hình sản phẩm cuối:** **Chatbot**. Đây là hình thức phù hợp nhất cho phép người dùng tương tác hỏi đáp và yêu cầu tạo Approval một cách tự nhiên. Chatbot này có thể được triển khai dưới dạng một ứng dụng web nội bộ hoặc tích hợp vào các nền tảng giao tiếp hiện có của công ty (VD: Microsoft Teams, Slack...).

* **2.5. Required technology and technology acquisition plan**
    * **Công nghệ cần thiết:**
        * **LLM & API:** Đã được cung cấp bởi cuộc thi.
        * **Ngôn ngữ lập trình:** Python (phổ biến cho AI/ML và có nhiều thư viện hỗ trợ).
        * **Thư viện/Framework:**
            * LangChain hoặc LlamaIndex (hỗ trợ xây dựng ứng dụng LLM, RAG, Tool Calling).
            * Thư viện xử lý file: `python-pptx`, `python-docx`, `PyPDF2` hoặc `pdfminer.six`.
            * Vector Database: ChromaDB, FAISS (chạy local/on-premise), hoặc các dịch vụ cloud nếu được phép.
            * Web Framework (cho backend chatbot): FastAPI hoặc Flask.
            * Frontend Framework (cho giao diện chatbot - tùy chọn): React, Vue, hoặc Gradio/Streamlit (để làm PoC nhanh).
        * **Hạ tầng:** Máy chủ nội bộ hoặc cloud (tuân thủ quy định công ty A) để host ứng dụng backend và Vector DB.
    * **Kế hoạch tiếp cận công nghệ:**
        * LLM/API: Sử dụng theo tài liệu và hướng dẫn của cuộc thi.
        * Thư viện Python: Cài đặt qua pip (cần kiểm tra chính sách firewall/proxy của công ty, có thể cần Approval để truy cập PyPI hoặc cần sử dụng kho artifact nội bộ nếu có).
        * Vector Database: Ưu tiên các giải pháp có thể chạy on-premise (như FAISS, ChromaDB) để tránh phụ thuộc cloud và tuân thủ quy định bảo mật.
        * Hạ tầng: Đề xuất sử dụng môi trường development/staging hiện có của công ty hoặc xin cấp phép tài nguyên cần thiết (có thể lại là một quy trình Approval!).
        * Kiến thức/Nhân lực: Tận dụng kỹ năng của thành viên dự án. Nếu thiếu, đề xuất tham gia training hoặc tìm kiếm sự hỗ trợ từ các chuyên gia trong/ngoài công ty (nếu được phép).

---

Hy vọng bản phác thảo chi tiết này sẽ giúp bạn hoàn thiện hồ sơ dự thi một cách tốt nhất. Ý tưởng của bạn rất tiềm năng và giải quyết đúng vấn đề thực tế của công ty. Chúc bạn thành công trong cuộc thi!
