# Thống kê và Phân tích Dữ liệu

## 1. **Xác suất cơ bản**
   - **Tổ hợp**:
     - **Ý nghĩa**: Cách chọn các đối tượng từ một tập hợp mà không quan tâm đến thứ tự.
     - **Công thức**: \( C(n, k) = \\frac{n!}{k!(n-k)!} \)
     - **Ứng dụng**: Tính số cách chọn nhóm từ một nhóm lớn.
   
   - **Chỉnh hợp**:
     - **Ý nghĩa**: Cách chọn các đối tượng từ một tập hợp mà quan tâm đến thứ tự.
     - **Công thức**: \( A(n, k) = \frac{n!}{(n-k)!} \)
     - **Ứng dụng**: Sắp xếp, xếp hạng.
   
   - **Hoán vị**:
     - **Ý nghĩa**: Sắp xếp các đối tượng theo một thứ tự cụ thể.
     - **Công thức**: \( P(n) = n! \)
   
   - **Xác suất**:
     - **Ý nghĩa**: Khả năng xảy ra của một sự kiện.
     - **Công thức**: \( P(A) = \frac{Số kết quả thuận lợi}{Tổng số kết quả có thể xảy ra} \)
     - **Ứng dụng**: Dự đoán kết quả của các sự kiện ngẫu nhiên.

---

## 2. **Thống kê**
   - **Thống kê mô tả**:
     - **Chỉ số Trung bình**: \( \mu = \frac{\sum X}{N} \)
     - **Độ lệch chuẩn**: \( \sigma = \sqrt{\frac{\sum (X - \mu)^2}{N}} \)
     - **Phân phối chuẩn**:
       - Ý nghĩa: Mô tả sự phân phối của dữ liệu, với đặc trưng là đối xứng xung quanh giá trị trung bình.
     - **Sự phân phối t**:
       - Sử dụng khi mẫu có kích thước nhỏ và không biết phương sai tổng thể.

   - **Công cụ và thư viện**:
     - **Python**: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy.stats`
     - **R**: `ggplot2`, `dplyr`, `stats`

---

## 3. **Phân tích Dữ liệu bằng Biểu đồ**
   - **Biểu đồ Phân phối**:
     - **Loại**: Histogram, Kernel Density Plot.
     - **Ý nghĩa**: Mô tả phân phối của dữ liệu, giúp nhận diện sự phân tán và mật độ dữ liệu.
     - **Lưu ý**: 
       - Sử dụng **Histogram** để xác định độ rộng của các nhóm dữ liệu (bins).
       - **Kernel Density Plot** giúp xem hình dạng phân phối mượt mà hơn so với Histogram.
     - **Hàm**: `seaborn.histplot()`, `seaborn.kdeplot()`
   
   - **Biểu đồ Tương quan**:
     - **Loại**: Scatter plot.
     - **Ý nghĩa**: Mô tả mối quan hệ giữa hai biến, có thể tìm thấy các mối quan hệ tuyến tính hoặc phi tuyến tính.
     - **Lưu ý**: 
       - Nếu các điểm dữ liệu xếp thành một đường thẳng hoặc gần thẳng, có thể có mối quan hệ tuyến tính.
       - Phân tích chặt chẽ các điểm ngoại lệ có thể có ảnh hưởng lớn đến kết quả.
     - **Hàm**: `seaborn.scatterplot()`
   
   - **Biểu đồ Boxplot**:
     - **Ý nghĩa**: Mô tả sự phân tán, phát hiện ngoại lệ (outlier), giúp hiểu rõ hơn về tứ phân vị (Q1, Median-Q2, Q3) thông qua phần thân (box), các râu (whiskers) và khoảng cách giữa các phân vị.
     - **Lưu ý**: 
       - Boxplot giúp phát hiện các điểm ngoại lệ dễ dàng.
       - Cần chú ý đến các phần tử có giá trị cực trị ngoài giới hạn của whiskers.
     - **Hàm**: `seaborn.boxplot()`
   
   - **Biểu đồ Bar Chart**:
     - **Ý nghĩa**: So sánh giá trị giữa các nhóm, thường sử dụng khi dữ liệu có dạng phân loại (categorical).
     - **Lưu ý**: 
       - Đảm bảo rằng các nhóm được phân loại rõ ràng, tránh các thông tin gây hiểu nhầm.
       - Biểu đồ dạng này dễ hiểu và thường dùng trong báo cáo thống kê.
     - **Hàm**: `matplotlib.pyplot.bar()`
   
   - **Biểu đồ Line (Đường)**:
     - **Ý nghĩa**: Dùng để mô tả xu hướng dữ liệu theo thời gian (time series) hoặc một biến liên tục.
     - **Lưu ý**: 
       - Đặc biệt hữu ích trong phân tích chuỗi thời gian để xem xét xu hướng và biến động.
       - Cần chú ý đến việc chọn đúng khoảng thời gian để vẽ biểu đồ.
     - **Hàm**: `matplotlib.pyplot.plot()`, `seaborn.lineplot()`
   
   - **Biểu đồ Pie (Bánh)**:
     - **Ý nghĩa**: Dùng để biểu thị tỷ lệ phần trăm của các phần tử trong tổng thể, đặc biệt khi cần thể hiện phân bổ các phần trong một nhóm.
     - **Lưu ý**:
       - Thích hợp cho dữ liệu có ít phần tử phân chia rõ ràng, tránh sử dụng Pie cho nhiều phần tử quá nhỏ.
       - Lưu ý các phần tử có tỷ lệ gần bằng nhau có thể gây khó khăn trong việc phân biệt.
     - **Hàm**: `matplotlib.pyplot.pie()`

---

## 4. **Phân tích Dữ liệu**
   
### 4.1 **Lựa chọn kiểm định phù hợp**
   - **Nếu dữ liệu là Độc lập**:
     - **T-test độc lập**:
       - **Cách đặt \(H_0\)**: \( H_0 \): Không có sự khác biệt trung bình giữa hai nhóm.
       - **Cách biện luận**: Nếu \( p\text{-value} < \alpha \), bác bỏ \( H_0 \); nếu \( p\text{-value} \geq \alpha \), không bác bỏ \( H_0 \).
       - **Ứng dụng**: So sánh trung bình giữa hai nhóm độc lập.
     - **One-way ANOVA**:
       - **Cách đặt \(H_0\)**: \( H_0 \): Không có sự khác biệt giữa các nhóm.
       - **Cách biện luận**: Tương tự T-test độc lập nhưng áp dụng cho nhiều nhóm.
     - **Kiểm định Chi bình phương**:
       - **Cách đặt \(H_0\)**: Không có mối liên hệ giữa các biến.
   
   - **Nếu dữ liệu là Phụ thuộc**:
     - **T-test cặp**:
       - **Cách đặt \(H_0\)**: Không có sự khác biệt trung bình giữa hai điều kiện.
     - **Paired Sample Wilcoxon Test**:
       - Phi tham số, thay thế cho T-test khi dữ liệu không tuân theo phân phối chuẩn.
   
   - **Nếu dữ liệu là một tổng thể**:
     - **Kiểm định trung bình một tổng thể**:
       - **Cách đặt \(H_0\)**: Trung bình mẫu bằng với giá trị kỳ vọng (\( \mu = \mu_0 \)).
     - **Chi bình phương**:
       - **Cách đặt \(H_0\)**: Không có mối liên hệ giữa các biến danh mục.
   
   - **Dữ liệu danh mục**:
     - **McNemar Test**:
       - Kiểm tra sự khác biệt giữa hai điều kiện đối với dữ liệu danh mục phụ thuộc.
   - **Nếu chưa rõ dữ liệu Độc lập hay Phụ thuộc**:
     - **Kiểm định bổ sung để xác định loại dữ liệu**:
       - **Kiểm định Levene**:
         - **Mục đích**: Kiểm tra tính đồng nhất phương sai giữa các nhóm dữ liệu.
          - **Ứng dụng**:
            - Nếu phương sai đồng nhất, dữ liệu có khả năng là độc lập.
            - Nếu phương sai không đồng nhất, có khả năng dữ liệu là phụ thuộc hoặc không đồng nhất phương sai.
          - **Cách đặt \(H_0\)**:
            - \( H_0 \): Các nhóm có phương sai bằng nhau (phương sai đồng nhất).
            - \( H_1 \): Các nhóm có phương sai không bằng nhau (phương sai không đồng nhất).
          - **Cách biện luận**:
            - Nếu \( p\text{-value} \geq \alpha \): Không bác bỏ \( H_0 \), phương sai đồng nhất → dữ liệu có thể là độc lập.
            - Nếu \( p\text{-value} < \alpha \): Bác bỏ \( H_0 \), phương sai không đồng nhất → dữ liệu có khả năng là phụ thuộc.

        - **Kiểm định McNemar (cho dữ liệu danh mục)**:
          - **Mục đích**: Kiểm tra sự khác biệt trong các giá trị cặp của dữ liệu danh mục.
          - **Ứng dụng**:
            - Nếu dữ liệu ghép cặp (phụ thuộc), kiểm định McNemar sẽ có ý nghĩa.
            - Nếu dữ liệu không ghép cặp, kiểm định không có ý nghĩa hoặc không phù hợp.
          - **Cách đặt \(H_0\)**:
            - \( H_0 \): Không có sự khác biệt giữa hai nhóm dữ liệu danh mục.
            - \( H_1 \): Có sự khác biệt giữa hai nhóm dữ liệu danh mục.
          - **Cách biện luận**:
            - Nếu \( p\text{-value} \geq \alpha \): Không bác bỏ \( H_0 \), dữ liệu có thể là độc lập.
            - Nếu \( p\text{-value} < \alpha \): Bác bỏ \( H_0 \), dữ liệu có thể là phụ thuộc.

        - **Kiểm định Chi bình phương (cho dữ liệu danh mục)**
          - **Mục đích**: Kiểm tra sự độc lập giữa hai biến danh mục.
          - **Ứng dụng**:
            - Nếu \( H_0 \): Hai biến độc lập, dữ liệu không phụ thuộc.
            - Nếu bác bỏ \( H_0 \): Hai biến có mối quan hệ, dữ liệu có khả năng phụ thuộc.
          - **Cách đặt \( H_0 \)**:
            - \( H_0 \): Hai biến là độc lập (không có mối quan hệ).
            - \( H_1 \): Hai biến không độc lập (có mối quan hệ).
          - **Cách biện luận**:
            - Nếu \( p\text{-value} \geq \alpha \): Không bác bỏ \( H_0 \), hai biến là độc lập.
            - Nếu \( p\text{-value} < \alpha \): Bác bỏ \( H_0 \), hai biến có mối quan hệ (phụ thuộc).
          - **Lưu ý**:
            - Sử dụng bảng tần suất và kiểm tra điều kiện tần suất kỳ vọng \(\geq 5\).

        - **Phân tích trực quan**
          - **Mục đích**: Quan sát mối quan hệ hoặc sự tương đồng giữa các nhóm dữ liệu.
          - **Cách thực hiện**:
            - **Scatter plot**:
              - Nếu các điểm không có sự liên hệ rõ ràng, dữ liệu có thể độc lập.
              - Nếu các điểm có xu hướng liên kết chặt chẽ, dữ liệu có khả năng phụ thuộc.
            - **Boxplot**:
              - Nếu hai nhóm có phân phối tương tự, dữ liệu có thể độc lập.
              - Nếu phân phối giữa hai nhóm có mối quan hệ mạnh, dữ liệu có khả năng phụ thuộc.
          - **Cách biện luận**:
            - Phân tích trực quan không cung cấp kiểm định xác suất, nhưng có thể định hướng lựa chọn các kiểm định tiếp theo dựa trên quan sát.

---

### **Lưu ý khi đặt \( H_0 \):**
- Trong mọi kiểm định:
  - \( H_0 \) thường giả định **không có mối khác biệt hoặc không có mối liên quan**.
  - \( H_1 \) là giả thuyết thay thế cho \( H_0 \), thường khẳng định có sự khác biệt hoặc mối liên quan.
- Lựa chọn mức ý nghĩa \(\alpha\) phổ biến (0.05) để đưa ra kết luận thống kê.

---

### 4.2. **Các phương pháp phân tích**

#### 4.2.1 Hồi quy tuyến tính
- **Mục đích**: Dự đoán giá trị của biến phụ thuộc dựa trên biến độc lập.
- **Công thức**: \( Y = \beta_0 + \beta_1 X \)
- **Ứng dụng**: Dự đoán doanh thu từ chi phí quảng cáo, học lực từ số giờ học.
- **Hàm**:
  - **Python**: `statsmodels.OLS()` hoặc `scikit-learn.linear_model.LinearRegression()`
  - **R**: `lm()`
- **Kiểm định**:
  - **H0**: Không có sự ảnh hưởng của biến độc lập đến biến phụ thuộc (\( \beta_1 = 0 \)).
  - **Cách nhận xét**: Nếu p-value < 0.05, bác bỏ H0, tức là có sự ảnh hưởng có ý nghĩa thống kê giữa biến độc lập và biến phụ thuộc.

#### 4.2.2 Hồi quy tuyến tính bội (Multiple Linear Regression)
- **Mục đích**: Dự đoán giá trị của biến phụ thuộc dựa trên nhiều biến độc lập.
- **Công thức**: \( Y = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \dots + \beta_n X_n \)
- **Ứng dụng**: Dự đoán doanh thu từ nhiều yếu tố như chi phí quảng cáo, số lượng khách hàng, và các yếu tố khác.
- **Hàm**:
  - **Python**: `statsmodels.OLS()`
  - **R**: `lm()`
- **Kiểm định**:
  - **H0**: Không có sự ảnh hưởng của các biến độc lập đến biến phụ thuộc (tất cả các \( \beta_i = 0 \)).
  - **Cách nhận xét**: Nếu p-value của bất kỳ hệ số \( \beta_i \) nào nhỏ hơn 0.05, bác bỏ H0 cho biến đó và kết luận rằng biến độc lập có ảnh hưởng đáng kể đến biến phụ thuộc.

#### 4.2.3 Hồi quy logistic
- **Mục đích**: Dự đoán xác suất của một sự kiện nhị phân (0 hoặc 1).
- **Công thức**: \( \text{logit}(p) = \beta_0 + \beta_1 X_1 + \dots + \beta_n X_n \)
- **Ứng dụng**: Dự đoán xác suất một người có mắc bệnh hay không, xác suất khách hàng sẽ mua sản phẩm.
- **Hàm**:
  - **Python**: `statsmodels.Logit()` hoặc `sklearn.linear_model.LogisticRegression()`
  - **R**: `glm(family = binomial())`
- **Kiểm định**:
  - **H0**: Không có sự ảnh hưởng của các biến độc lập đến xác suất của sự kiện (tất cả các \( \beta_i = 0 \)).
  - **Cách nhận xét**: Nếu p-value của bất kỳ hệ số \( \beta_i \) nào nhỏ hơn 0.05, bác bỏ H0 cho biến đó và kết luận rằng biến độc lập có ảnh hưởng đáng kể đến xác suất của sự kiện.

#### 4.2.4 Phân tích thành phần chính (PCA)
- **Mục đích**: Giảm chiều dữ liệu, tìm các thành phần chính.
- **Ứng dụng**: Xử lý dữ liệu lớn, giảm số lượng biến trong phân tích.
- **Hàm**:
  - **Python**: `sklearn.decomposition.PCA()`
  - **R**: `prcomp()`
- **Kiểm định**: PCA chủ yếu dùng để giảm chiều dữ liệu, không có kiểm định giả thuyết truyền thống như các kiểm định thống kê khác.


#### 4.2.5 **Kiểm định giả thuyết**

##### 4.2.5.1 **Kiểm định t-test**
- **Ứng dụng**: Kiểm tra sự khác biệt về trung bình giữa hai nhóm.
- **Phân loại**:
  - **Independent t-test (t-test độc lập)**: So sánh trung bình của hai nhóm độc lập.
  - **Paired t-test (t-test ghép cặp)**: So sánh trung bình của hai bộ dữ liệu phụ thuộc.
- **Hàm**:
  - **Python**: 
    - `scipy.stats.ttest_ind()` (t-test độc lập).
    - `scipy.stats.ttest_rel()` (t-test ghép cặp).
  - **R**: `t.test()`.
- **Kiểm định**:
  - **H0**: Trung bình của hai nhóm không có sự khác biệt.
  - **H1**: Trung bình của hai nhóm có sự khác biệt.
- **Nhận xét**:
  - Nếu p-value < 0.05, bác bỏ \( H0 \), kết luận rằng có sự khác biệt có ý nghĩa thống kê giữa hai nhóm.

##### 4.2.5.2 **Kiểm định ANOVA (Phân tích phương sai)**
- **Ứng dụng**: So sánh trung bình của nhiều nhóm (hơn 2 nhóm).
- **Phân loại**:
  - **One-way ANOVA**: Kiểm tra sự khác biệt trung bình giữa các nhóm độc lập.
  - **Two-way ANOVA**: Xem xét ảnh hưởng của hai biến độc lập đến biến phụ thuộc.
- **Hàm**:
  - **Python**: 
    - `scipy.stats.f_oneway()` (One-way ANOVA).
    - `statsmodels.formula.api.ols()` và `statsmodels.stats.anova.anova_lm()` (Two-way ANOVA).
  - **R**: `aov()`.
- **Kiểm định**:
  - **H0**: Trung bình của các nhóm là như nhau.
  - **H1**: Có ít nhất một nhóm khác biệt.
- **Nhận xét**:
  - Nếu p-value < 0.05, bác bỏ \( H0 \), kết luận rằng có sự khác biệt giữa các nhóm.

##### 4.2.5.3 **Kiểm định Chi bình phương (Chi-square Test)**
- **Ứng dụng**: Kiểm tra sự liên quan giữa hai biến phân loại.
- **Phân loại**:
  - **Chi-square test for independence**: Kiểm tra mối quan hệ giữa hai biến phân loại.
  - **Chi-square goodness-of-fit test**: Kiểm tra xem phân phối của một biến có khớp với phân phối kỳ vọng không.
- **Hàm**:
  - **Python**: 
    - `scipy.stats.chisquare()` (Goodness-of-fit).
    - `scipy.stats.chi2_contingency()` (Independence).
  - **R**: `chisq.test()`.
- **Kiểm định**:
  - **H0**: Hai biến là độc lập hoặc phân phối khớp với kỳ vọng.
  - **H1**: Hai biến có mối liên hệ hoặc phân phối không khớp với kỳ vọng.
- **Nhận xét**:
  - Nếu p-value < 0.05, bác bỏ \( H0 \), kết luận rằng hai biến có mối quan hệ hoặc phân phối không khớp.

##### 4.2.5.4 **Kiểm định ANCOVA (Analysis of Covariance)**
- **Ứng dụng**: Kết hợp giữa ANOVA và hồi quy tuyến tính để kiểm tra sự khác biệt giữa các nhóm, đồng thời kiểm soát ảnh hưởng của các biến đồng biến (covariates).
- **Hàm**:
  - **Python**: 
    - `statsmodels.formula.api.ols()` để xây dựng mô hình.
    - `statsmodels.stats.anova.anova_lm()` để thực hiện kiểm định.
  - **R**: `aov()` hoặc `lm()` để thực hiện phân tích.
- **Kiểm định**:
  - **H0**: Không có sự khác biệt giữa các nhóm sau khi kiểm soát covariates.
  - **H1**: Có sự khác biệt giữa các nhóm sau khi kiểm soát covariates.
- **Nhận xét**:
  - Nếu p-value < 0.05, bác bỏ \( H0 \), kết luận rằng có sự khác biệt giữa các nhóm sau khi kiểm soát covariates.
- **Lưu ý**:
  - Covariates cần có quan hệ tuyến tính với biến phụ thuộc.
  - Cần kiểm tra giả định về phương sai đồng nhất và tuyến tính trước khi thực hiện kiểm định.

#### 4.2.6 **Phân tích phân phối**
   - **Ứng dụng**: Kiểm tra phân phối của một biến (chuẩn, Poisson, v.v.).
   - **Mô hình**: Kiểm tra phân phối phù hợp với dữ liệu.
   - **Hàm**:
     - **Python**: `scipy.stats.normaltest()`, `stats.shapiro()`
     - **R**: `shapiro.test()`
   - **Kiểm định**:
     - Kiểm định giả thuyết cho phân phối của dữ liệu.
   - **Lưu ý**: Cần kiểm tra tính chất phân phối của dữ liệu trước khi áp dụng các mô hình thống kê.

#### 4.2.7 Phân tích tương quan
- **Mục đích**: Đánh giá mối quan hệ giữa hai hoặc nhiều biến số.
- **Ý nghĩa**: Kiểm tra sự liên kết giữa các biến. Mối quan hệ có thể là **tuyến tính** hoặc **phi tuyến tính**.
- **Hàm**:
  - **Python**: 
    - **Pearson**: `scipy.stats.pearsonr()`
    - **Spearman**: `scipy.stats.spearmanr()`
    - **Kendall**: `scipy.stats.kendalltau()`
  - **R**:
    - **Pearson**: `cor()`
    - **Spearman**: `cor(method = "spearman")`
    - **Kendall**: `cor(method = "kendall")`
- **Kiểm định**:
  - **H0**: Không có mối tương quan giữa các biến (\( \rho = 0 \)).
  - **Cách nhận xét**: Nếu p-value < 0.05, bác bỏ H0, tức là có mối tương quan có ý nghĩa thống kê giữa các biến.

#### 4.2.8 Phân tích dữ liệu chuỗi thời gian
- **Mục đích**: Dự báo giá trị trong tương lai dựa trên dữ liệu thời gian trước đó.
- **Các mô hình phổ biến**:
  - **ARIMA** (Autoregressive Integrated Moving Average).
  - **SARIMA** (Seasonal ARIMA): Phù hợp cho dữ liệu có mùa vụ.
  - **Prophet**: Phù hợp với dữ liệu có xu hướng và yếu tố mùa vụ.
- **Hàm**:
  - **Python**:
    - ARIMA: `statsmodels.tsa.ARIMA()`
    - Prophet: `fbprophet.Prophet()`
  - **R**:
    - ARIMA: `auto.arima()`
    - Prophet: `prophet()`
- **Lưu ý**:
  - **Kiểm tra tính ổn định**: Sử dụng ADF Test hoặc KPSS Test để đảm bảo chuỗi thời gian ổn định.
  - **Đánh giá mô hình**: Sử dụng MAE, RMSE, hoặc MAPE để kiểm tra độ chính xác.
  - **Nhận xét**: Dự báo được đánh giá dựa trên sự khớp giữa giá trị dự đoán và giá trị thực tế, cũng như đồ thị trực quan.

---
## 5. **Tổng kết và Lưu ý**
   - **Lựa chọn kiểm định phù hợp**:
     - Xác định loại dữ liệu (độc lập, phụ thuộc, tổng thể) để chọn kiểm định.
   - **Công cụ và thư viện**:
     - Sử dụng các thư viện phổ biến như `scipy`, `statsmodels`, `seaborn`, `matplotlib` để thực hiện các phân tích thống kê và vẽ biểu đồ.