# Z-Score
在进行数据预处理时，我们常用Z-Score进行数据标准化（Standerlization），可以使得数据的`均值`为 0，`标准差`为 1，下面将对这一特性进行证明
## Z-Score公式
假设我们有原始数据集$X = \lbrace X_1,X_2, \cdots , X_n \rbrace$，
则样本均值为：
$$
\overline{X} = \frac{1}{n} \sum_{i = 1}^{n}X_i
$$
样本方差$s_X^2$为（使用 n−1 作为分母，即贝塞尔校正，这也是 Pandas `std()` 的默认行为）：
$$
s_X^2 =  \frac{1}{n-1} \sum_{i = 1}^{n}(X_i - \overline{X})^2
$$
Z-Score描述了这样一种从原来的$X = \lbrace X_1,X_2, \cdots , X_n \rbrace$数据集到新的数据集$Z=\lbrace Z_1,Z_2, \cdots , Z_n \rbrace$的变换：
$$
Z_i = \frac{X_i - \overline{X}}{s_X}
$$
我们需要证明的就是：
$$
\overline{Z} = 0 , s_Z = 1
$$
## 证明
根据均值公式：
$$
\begin{align*}
\overline{Z} 
& = \frac{1}{n} \sum_{i = 1}^{n}Z_i \\
& = \frac{1}{n} \sum_{i = 1}^{n}\frac{X_i - \overline{X}}{s_X} \\
& = \frac{1}{n \cdot s_X} \sum_{i = 1}^{n}(X_i - \overline{X}) \\
& = \frac{1}{n \cdot s_X} (\sum_{i = 1}^{n}X_i - \sum_{i = 1}^{n}\overline{X}) \\
& = \frac{1}{n \cdot s_X} \cdot 0 \\
& = 0
\end{align*}
$$
$\overline{Z} = 0$证明完毕  
证明标准差为`1`即证明方差为`1`根据方差公式：
$$
\begin{align*}
s_Z^2
& = \frac{1}{n-1} \sum_{i = 1}^{n}(Z_i - \overline{Z})^2 \\
& = \frac{1}{n-1} \sum_{i = 1}^{n}(Z_i - 0)^2 \\
& = \frac{1}{n-1} \sum_{i = 1}^{n}Z_i^2 \\
& = \frac{1}{n-1} 
    \sum_{i = 1}^{n}(\frac{X_i - \overline{X}}{s_X})^2 \\
& = \frac{1}{(n-1) \cdot (s_X)^2} 
    \sum_{i = 1}^{n}(X_i - \overline{X})^2 \\
& = \frac{1}{s_X^2} \cdot \frac{1}{(n-1)}
    \sum_{i = 1}^{n}(X_i - \overline{X})^2 \\
& = \frac{1}{s_X^2} \cdot s_X^2 \\
& = 1
\end{align*}
$$
因此，$s_Z^2 = 1$ 证明完毕
## 实现
在python中，实现Z-Score非常简单，下面用一个简单的匿名函数实现：
```python
lambda x : (x - x.mean()) / (x.std())
```
