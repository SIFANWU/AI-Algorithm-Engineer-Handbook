---
export_on_save:
 html: true
---
# 线性代数 Linear algebra

## 向量 vector

**1. 向量的L1范数和L2范数的区分：**
* L0范数：向量中非0元素的个数.
* L1范数：向量中各个元素绝对值之和.
* L2范数：向量中各元素的平方和再开平方根.

**2. 各中范数的优缺点对比：**
* L1范数可以进行特征选择，让部分特征系数变成0,即具有稀疏性.
* L2范数可以防止过拟合，提高模型的泛化能力.
* L1会趋向于产生少量的特征，使大部分特征系数变成0；L2会选择更多地特征，这些特征都会接近0（即 系数非常小）。
  
**概念的直观理解：**
范数是具有“长度”概念的函数。在向量空间内，为所有的向量都赋予了非零的增长度或者大小。不同的范数，所求的长度或者大小是不同的。

For Example: 二维空间中，向量（3，4）的长度是5，那么5就是这个向量的范数的值，更确切的说，是欧式范数或者L2范数的值。

> 公式理解：对于$P-$范数，如果 
>     
> ![](https://www.zhihu.com/equation?tex=x=[x_1,x_2,x_3,\cdots,x_n]^{T}\\\\)    
> 
> 那么向量x的$P-$范数就是:
>    
> ![](https://www.zhihu.com/equation?tex=||x||_p=(|x_1|^p+|x_2|^p+|x_3|^p+\cdots+|x_n|^p)^{\frac{1}{p}}\\\\) 
> 
> L1范数：
>   
> ![](https://www.zhihu.com/equation?tex=||x||_1%20=|x_1|%20+%20|x_2|%20+|x_3|%20+%20\cdots%20+|x_n|\\\\)
>  
> L2范数：
>
> ![](https://www.zhihu.com/equation?tex=||x||_2%20=(|x_1|^2%20+%20|x_2|^2%20+|x_3|^2%20+%20\cdots%20+%20|x_n|^2)^{\frac{1}{2}}\\\\)
> 
*特别的，L0范数：指向量中非零元素的个数。无穷范数：指向量中所有元素的最大绝对值。*

**深度理解：**
一般来说，监督学习可以看做优化两个目标函数：
1. 损失函数（Loss function）- 实际数值与预测数值的差距.
   * 对于Loss函数，如果是Square loss，那就是最小二乘了；如果是Hinge Loss，那就是著名的SVM了；如果是exp-Loss，那就是牛逼的 Boosting了；如果是log-Loss，那就是Logistic Regression了；不同的loss函数，具有不同的拟合特性。
2. 规则化函数 即正则项 -不仅要保证训练误差值最小，更希望模型的测试误差小，对参数矩阵W的规则化函数去约束模型，使之尽量的简单。
   * 规则化函数Ω(w)也有很多种选择，一般是模型复杂度的单调递增函数，模型越复杂，规则化值就越大。比如，规则化项可以是模型参数向量的范数。然而，不同的选择对参数w的约束不同，取得的效果也不同，但我们在论文中常见的都聚集在：零范数、一范数、二范数、迹范数、Frobenius范数和核范数等等。
3. L0范数是指向量中非0的元素的个数。如果我们用L0范数来规则化一个参数矩阵W的话，就是希望W的大部分元素都是0，即具有稀疏功能。
    * 为什么不用L0范数？
      * 个人理解：一是因为L0范数很难优化求解（NP难问题），二是L1范数是L0范数的最优凸近似，而且它比L0范数要容易优化求解。总结：L1范数和L0范数可以实现稀疏，L1因具有比L0更好的优化求解特性而被广泛应用。
     * 参数稀疏的好处：
       * 特征选择(Feature Selection)：将非主要信息特征权重置为0可以避免这些信息对测试集样本预测结果的干扰，相当于特征的自动选择或者过滤。
       * 可解释性(Interpretability)：只选出主要影响的特征，便于分析影响预测的结果的主要因素，比如 1000维参数，只有5个才是决定是否正确的特征，则只要这5个特征预测准确即可。
4. L2范数为何更受欢迎？L2范数可以避免过拟合的发生。优化L2范数的规则项||w||<sup>2</sup>，使之值最小，可以使参数矩阵||w||中每个值都很小，接近于0，但是不等于0（此处于L0范数的区别），这样使模型越简单，越简单的模型越不容易产生过拟合现象。
   * 为什么参数越小，模型越简单？
     * 个人理解：1.参数数值越小，对模型预测结果的影响就越小。只有权重系数较大的特征对模型的预测结果影响较大。2.参数值越小，实际上限制了多项式分量的影响，相当于变相减少了参数的个数，所以模型变得简单。

##### 总结：L1会趋向于产生少量的特征，而其他的特征都是0，而L2会选择更多的特征，这些特征都会接近于0。
----
## 矩阵 matrix
>
>在线性代数中，一个![](http://latex.codecogs.com/gif.latex?n*n}) 矩阵A的对角线(从左上方至右下方的对角线)上各个元素的总和被称为矩阵A的迹，一般记作![](http://latex.codecogs.com/gif.latex?tr(A)).

>数学表达：设矩阵 ![](http://latex.codecogs.com/gif.latex?A%20=(a_{i,j})_{m*n}) ,则A的迹为: ![](http://latex.codecogs.com/gif.latex?tr(A)=\sum_i%20a_{i,i}).

迹的性质有：
* 迹是所有对角线元素的和
* 迹是所有特征值的和
* A的F范数等于$AA^T$的迹的平方根：![](http://latex.codecogs.com/gif.latex?||A||_F=\sqrt{tr(AA^T)}) 
* A的迹等于$A^T$的迹：![](http://latex.codecogs.com/gif.latex?tr(A)=tr(A^T))
* 交换律：假设 ![](http://latex.codecogs.com/gif.latex?A\in{R^{m*n}},B\in{R^{n*m}}), 则有：![](http://latex.codecogs.com/gif.latex?tr(AB)=tr(BA)) 
* 结合律：![](http://latex.codecogs.com/gif.latex?tr(ABC)=tr(CAB)=tr(BCA))
  
**矩阵的运算**
> 给定两个矩阵![](http://latex.codecogs.com/gif.latex?A=(a_{i,j})\in{R^{m*n}},B=(b_{i,j})\in{R^{m*n}}),定义：  
> * 阿达马积 `Hadamard product`(又称作逐元素积)：  
> ![](http://latex.codecogs.com/gif.latex?A\circ{B}=%20\left[\begin{matrix}%20a_{1,1}b_{1,1}%20%20&%20a_{1,2}b_{1,2}%20%20&%20\cdots%20&a_{1,n}b_{1,n}%20\\\\%20a_{2,1}b_{2,1}%20%20&%20a_{2,2}b_{2,2}%20%20&%20\cdots%20&a_{2,n}b_{2,n}%20\\\\%20\vdots%20&%20\vdots%20&%20\ddots%20&%20\vdots%20\\\\%20a_{m,1}b_{m,1}%20%20&%20a_{m,2}b_{m,2}%20%20%20&%20\cdots%20&a_{m,n}b_{m,n}%20\\%20\end{matrix}%20\right])
> * 克罗内积 `Kronnecker product`:  
> ![](http://latex.codecogs.com/gif.latex?A%20\otimes%20B%20=%20\left[%20\begin{matrix}%20a_{1,1}B%20%20&%20a_{1,2}B%20%20&%20\cdots%20&a_{1,n}B%20%20\\\\%20a_{2,1}B%20%20&%20a_{2,2}B%20%20&%20\cdots%20&a_{2,n}B%20%20\\\\%20\vdots%20&%20\vdots%20&%20\ddots%20&%20\vdots%20\\\\%20a_{m,1}B%20&%20a_{m,2}B%20%20%20&%20\cdots%20&a_{m,n}B%20\\%20\end{matrix}%20\right])
>
> * 各种类型的偏导数:
>    - 标量对标量的偏导数：![](http://latex.codecogs.com/gif.latex?\frac{\partial{u}}{\partial{v}})
>    - 标量对向量(n维向量)的偏导数: 
> 
> ![](http://latex.codecogs.com/gif.latex?\frac{\partial{u}}{\partial{\vec{v}}}=(\frac{\partial{u}}{\partial{v_1}},%20\frac{\partial{u}}{\partial{v_2}},\cdots,\frac{\partial{u}}{\partial{v_n}})^T)
>    - 标量对矩阵($m*n$阶矩阵)的偏导数：
> 
> ![](http://latex.codecogs.com/gif.latex?\frac{\partial%20u}{\partial%20V}%20=%20\left[%20\begin{matrix}%20\frac{\partial%20u}{\partial%20V_{1,1}}%20%20&%20\frac{\partial%20u}{\partial%20V_{1,2}}%20&%20\cdots%20&%20\frac{\partial%20u}{\partial%20V_{1,n}}%20\\\\%20\frac{\partial%20u}{\partial%20V_{2,1}}%20%20&%20\frac{\partial%20u}{\partial%20V_{2,2}}%20&%20\cdots%20&%20\frac{\partial%20u}{\partial%20V_{2,n}}%20\\\\%20\vdots%20&%20\vdots%20&%20\ddots%20&%20\vdots%20\\\\%20\frac{\partial%20u}{\partial%20V_{m,1}}%20%20&%20\frac{\partial%20u}{\partial%20V_{m,2}}%20&%20\cdots%20&%20\frac{\partial%20u}{\partial%20V_{m,n}}%20\\%20\end{matrix}%20\right])
> 
> - 向量(m维向量)对标量的偏导数：
> 
> ![](http://latex.codecogs.com/gif.latex?\frac{\partial%20\vec{u}}{\partial%20v}=(\frac{\partial%20u_1}{\partial%20v},%20\frac{\partial%20u_2}{\partial%20v},%20\cdots,\frac{\partial%20u_n}{\partial%20v})^T)
> - 向量(m维向量)对向量(n维向量)的偏导数(雅可比矩阵，行优先)
> 
> ![](http://latex.codecogs.com/gif.latex?\frac{\partial%20\vec{u}}{\partial%20\vec{v}}%20=%20\left[%20\begin{matrix}%20\frac{\partial%20u_1}{\partial%20V_1%20}%20%20&%20\frac{\partial%20u_1}{\partial%20V_2}%20&%20\cdots%20&%20\frac{\partial%20u_1}{\partial%20V_n%20}%20\\\\%20\frac{\partial%20u_2}{\partial%20V_1%20}%20%20&%20\frac{\partial%20u_2}{\partial%20V_2}%20&%20\cdots%20&%20\frac{\partial%20u_2}{\partial%20V_n%20}%20\\\\%20\vdots%20&%20\vdots%20&%20\ddots%20&%20\vdots%20\\\\%20\frac{\partial%20u_m}{\partial%20V_1%20}%20%20&%20\frac{\partial%20u_m}{\partial%20V_2}%20&%20\cdots%20&%20\frac{\partial%20u_m}{\partial%20V_n%20}%20\\%20\end{matrix}%20\right])
>>> 如果为列优先，则为上面矩阵的转置。    
> - 矩阵($m*n$阶矩阵)对标量的偏导数
> 
> ![](http://latex.codecogs.com/gif.latex?\frac{\partial%20U}{\partial%20v}%20=%20\left[%20\begin{matrix}%20\frac{\partial%20U_{1,1}}{\partial%20v}%20%20&%20\frac{\partial%20U_{1,2}}{\partial%20v}%20&%20\cdots%20&%20\frac{\partial%20U_{1,n}}{\partial%20v%20}%20\\\\%20\frac{\partial%20U_{2,1}}{\partial%20v}%20%20&%20\frac{\partial%20U_{2,2}}{\partial%20v}%20&%20\cdots%20&%20\frac{\partial%20U_{2,n}}{\partial%20v%20}%20\\\\%20\vdots%20&%20\vdots%20&%20\ddots%20&%20\vdots%20\\\\%20\frac{\partial%20U_{m,1}}{\partial%20v}%20%20&%20\frac{\partial%20U_{m,2}}{\partial%20v}%20&%20\cdots%20&%20\frac{\partial%20U_{m,n}}{\partial%20v%20}%20\\%20\end{matrix}%20\right])



----
