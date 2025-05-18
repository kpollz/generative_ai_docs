<h1 align="center">Bayesian Networks</h1>

Bayesian Networks (Mạng Bayes) là một công cụ mạnh mẽ trong xác suất và trí tuệ nhân tạo, cho phép biểu diễn và tính toán các mối quan hệ phụ thuộc giữa các biến ngẫu nhiên. Dưới đây là tóm tắt nhanh:

* **Định nghĩa**: Một Bayesian Network (BN) là mô hình đồ thị xác suất có hướng không chu trình (DAG) biểu diễn các biến và mối quan hệ phụ thuộc có điều kiện giữa chúng ([Wikipedia][1]).
* **Cơ chế hoạt động**: BN sử dụng tính chất Markov cục bộ để phân tách phân phối chung thành tích các phân phối có điều kiện, đồng thời áp dụng các thuật toán suy diễn (inference) như biến tiệm biến và hội tụ qua đồ thị cliques ([Wikipedia][1], [Engati][2]).
* **Chứng minh toán học**: Bắt nguồn từ quy tắc chuỗi (chain rule) và tính độc lập có điều kiện, ta chứng minh được rằng
  $$p(X_1,\dots,X_n)=\prod_{i=1}^n p(X_i \mid \mathrm{Pa}(X_i))$$
  với $Pa( )$ là tập cha của nút ([Wikipedia][1]).
* **Ví dụ lập trình**: Sử dụng thư viện [pgmpy](https://pgmpy.org/) để xây dựng mạng Bayes, định nghĩa CPD và sinh mẫu dữ liệu.

## 1. Định nghĩa

Một **Bayesian Network** (còn gọi là Bayes net, belief network) là một **probabilistic graphical model** mô tả tập hợp biến ngẫu nhiên và **mối quan hệ phụ thuộc có điều kiện** giữa chúng thông qua một **directed acyclic graph** (DAG) ([Wikipedia][1]). Mỗi nút trong đồ thị tương ứng một biến, mỗi cạnh có hướng thể hiện mối quan hệ cha–con, và mỗi nút chứa một bảng phân phối xác suất có điều kiện (CPD) cho biến đó dựa trên giá trị của các cha ([GeeksforGeeks][3]).

## 2. Cơ chế hoạt động

### 2.1 Phân tách phân phối chung

Dựa trên **chain rule** và giả thiết **độc lập có điều kiện** (Conditional Independence), ta viết được:

$$
p(X_1,\dots,X_n)
= \prod_{i=1}^n p\bigl(X_i \mid X_{1:i-1}\bigr)
= \prod_{i=1}^n p\bigl(X_i \mid \mathrm{Pa}(X_i)\bigr),
$$

trong đó $\mathrm{Pa}(X_i)$ là tập cha của $X_i$ trong DAG ([Wikipedia][1]).

### 2.2 Suy diễn xác suất (Inference)

Khi có quan sát (evidence) trên một số biến, BN cho phép tính toán phân phối hậu nghiệm (posterior) của các biến khác. Các thuật toán chính:

* **Exact inference**: biến tiệm biến (variable elimination), hội tụ cây clique (clique tree propagation) ([Wikipedia][1]).
* **Approximate inference**: MCMC (Gibbs sampling), loopy belief propagation, importance sampling… ([Engati][2]).

## 3. Chứng minh toán học

### 3.1 Từ quy tắc chuỗi

Quy tắc chuỗi (chain rule) cho phân phối chung:

$$
p(X_1,\dots,X_n) 
= \prod_{i=1}^n p(X_i \mid X_{1:i-1}).
$$

### 3.2 Áp dụng tính độc lập có điều kiện

Giả sử trong DAG, mỗi $X_i$ chỉ phụ thuộc vào $\mathrm{Pa}(X_i)$ và không phụ thuộc vào các biến không thuộc làm con của nó (non-descendants) khi biết giá trị của cha, ta có:

$$
p(X_i \mid X_{1:i-1}) = p(X_i \mid \mathrm{Pa}(X_i)).
$$

Do đó thu được công thức phân tách:

$$
p(X_1,\dots,X_n)=\prod_{i=1}^n p(X_i \mid \mathrm{Pa}(X_i)).  
$$

Đây chính là định nghĩa **factorization** của Bayesian Network ([Wikipedia][1]).

## 4. Ví dụ lập trình với pgmpy

Dưới đây là ví dụ Python sử dụng **pgmpy** để định nghĩa một mạng Bayes đơn giản và sinh mẫu dữ liệu từ nó.

```python
from pgmpy.models import DiscreteBayesianNetwork
from pgmpy.factors.discrete import TabularCPD
from pgmpy.sampling import BayesianModelSampling

# 1. Định nghĩa cấu trúc DAG
model = DiscreteBayesianNetwork([
    ('Diff', 'Grade'),
    ('Intel', 'Grade')
])

# 2. Định nghĩa các CPD
cpd_diff = TabularCPD(variable='Diff', variable_card=2,
                      values=[[0.6], [0.4]])
cpd_intel = TabularCPD(variable='Intel', variable_card=2,
                       values=[[0.7], [0.3]])
cpd_grade = TabularCPD(variable='Grade', variable_card=3,
                       values=[
                           [0.3, 0.05, 0.9, 0.5],
                           [0.4, 0.25, 0.08, 0.3],
                           [0.3, 0.7, 0.02, 0.2]
                       ],
                       evidence=['Intel', 'Diff'],
                       evidence_card=[2, 2])

# 3. Thêm CPDs vào mô hình
model.add_cpds(cpd_diff, cpd_intel, cpd_grade)

# 4. Sinh mẫu dữ liệu
sampler = BayesianModelSampling(model)
samples = sampler.forward_sample(size=1000, seed=42)
print(samples.head())
```

Trong ví dụ trên:

* `DiscreteBayesianNetwork` khởi tạo mô hình với các cạnh (`turn1search1`).
* `TabularCPD` định nghĩa phân phối xác suất có điều kiện.
* Phương thức `forward_sample` sinh mẫu độc lập từ phân phối chung của mạng Bayes ([pgmpy][4], [pgmpy][5]).

Bạn có thể mở rộng ví dụ này để:

* Thêm biến quan sát (evidence) và sử dụng `likelihood_weighted_sample` hoặc `rejection_sample`.
* Khảo sát phân phối biên (marginal) và phân phối hậu nghiệm.
* Học cấu trúc và tham số từ dữ liệu thực với các estimator trong pgmpy ([pgmpy][6]).

---

**Tài liệu tham khảo chính**

* Wikipedia: Bayesian network ([Wikipedia][1])
* GeeksforGeeks: Basic Understanding of Bayesian Belief Networks ([GeeksforGeeks][3])
* Engati Glossary: Bayesian networks ([Engati][2])
* pgmpy Documentation: Bayesian Model Sampling ([pgmpy][4])
* pgmpy Documentation: Simulating Data From Bayesian Networks ([pgmpy][5])

[1]: https://en.wikipedia.org/wiki/Bayesian_network?utm_source=chatgpt.com "Bayesian network"
[2]: https://www.engati.com/glossary/bayesian-networks?utm_source=chatgpt.com "Bayesian networks - Engati"
[3]: https://www.geeksforgeeks.org/basic-understanding-of-bayesian-belief-networks/?utm_source=chatgpt.com "Basic Understanding of Bayesian Belief Networks | GeeksforGeeks"
[4]: https://pgmpy.org/approx_infer/bn_sampling.html?utm_source=chatgpt.com "Bayesian Model Sampling — pgmpy 1.0.0 documentation"
[5]: https://pgmpy.org/examples/Simulating%20Data.html?utm_source=chatgpt.com "Simulating Data From Bayesian Networks - pgmpy"
[6]: https://pgmpy.org/detailed_notebooks/10.%20Learning%20Bayesian%20Networks%20from%20Data.html?utm_source=chatgpt.com "Learning Bayesian Networks from Data — 1.0.0 | pgmpy docs"
