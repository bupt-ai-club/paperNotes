## OBS

将剪枝转换为最优化问题。

已知等式：
$$
Y=XW \tag{1}
$$
其中，$X$为输入，$Y$为输出，$W$为权重。经过变换可知：
$$
W=X^{-1}Y=\left(X^T X\right)^{-1} X^T Y=\left(X^T X\right)^{-1} X^T X W  \tag{2}
$$

泰勒定理描述了一个可微函数，如果函数足够光滑的话，在已知函数在某一点的各阶导数值的情况之下，泰勒公式可以用这些导数值做系数构建一个多项式来近似函数在这一点的邻域中的值，这个多项式称为泰勒多项式，一元函数在$x_k$处的泰勒展开式如下：

$$
f(x)=f(x_k)+f^{\prime}(x_k)(x-x_k)+\frac{f^{\prime \prime}(x_k)}{2 !}(x-x_k)^2+\frac{f^{\prime \prime \prime}(x_k)}{3 !}(x-x_k)^3+\ldots \tag{3}
$$

二元函数在点 $(x_k,y_k)$ 处的泰勒展开式为：
$$
\begin{gathered}
f(x, y)=f\left(x_k, y_k\right)+\left(x-x_k\right) f_x^{\prime}\left(x_k, y_k\right)+\left(y-y_k\right) f_y^{\prime}\left(x_k, y_k\right) \\
+\frac{1}{2 !}\left(x-x_k\right)^2 f_{x x}^{\prime \prime}\left(x_k, y_k\right)+\frac{1}{2 !}\left(x-x_k\right)\left(y-y_k\right) f_{x y}^{\prime \prime}\left(x_k, y_k\right) \\
+\frac{1}{2 !}\left(x-x_k\right)\left(y-y_k\right) f_{y x}^{\prime \prime}\left(x_k, y_k\right)+\frac{1}{2 !}\left(y-y_k\right)^2 f_{y y}^{\prime \prime}\left(x_k, y_k\right) +\ldots 
\end{gathered} \tag{4}
$$

多元函数(n)在点 $x_k$ 处的泰勒展开式为：

$$
\begin{gathered}
f(x, y)=f\left(x_k, y_k\right)+\left(x-x_k\right) f_x^{\prime}\left(x_k, y_k\right)+\left(y-y_k\right) f_y^{\prime}\left(x_k, y_k\right) \\
+\frac{1}{2 !}\left(x-x_k\right)^2 f_{x x}^{\prime \prime}\left(x_k, y_k\right)+\frac{1}{2 !}\left(x-x_k\right)\left(y-y_k\right) f_{x y}^{\prime \prime}\left(x_k, y_k\right) \\
+\frac{1}{2 !}\left(x-x_k\right)\left(y-y_k\right) f_{y x}^{\prime \prime}\left(x_k, y_k\right)+\frac{1}{2 !}\left(y-y_k\right)^2 f_{y y}^{\prime \prime}\left(x_k, y_k\right) +\ldots
\end{gathered} \tag{5}
$$

推广到矩阵形式，可表示为：

$$
f(X)=f\left(X_k\right)+ \nabla f\left(X_k\right)\left(X-X_k\right)^T+\frac{1}{2 !}\left(X-X_k\right)^T H\left(X_k\right)\left(X-X_k\right)+o^n \tag{6}
$$
其中，$x^T=[x^1, x^2, x^3 ... x^n]$,$H$矩阵为黑塞矩阵,是一个多元函数的二阶偏导数构成的方阵，描述了函数的局部曲率。黑塞矩阵常用于牛顿法解决优化问题，利用黑塞矩阵可判定多元函数的极值问题。

$$
H\left(\mathbf{x}_k\right)=\left[\begin{array}{cccc}
\frac{\partial^2 f\left(x_k\right)}{\partial x_1^2} & \frac{\partial^2 f\left(x_k\right)}{\partial x_1 \partial x_2} & \cdots & \frac{\partial^2 f\left(x_k\right)}{\partial x_1 \partial x_n} \\
\frac{\partial^2 f\left(x_k\right)}{\partial x_2 \partial x_1} & \frac{\partial^2 f\left(x_k\right)}{\partial x_2^2} & \cdots & \frac{\partial^2 f\left(x_k\right)}{\partial x_2 \partial x_n} \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial^2 f\left(x_k\right)}{\partial x_n \partial x_1} & \frac{\partial^2 f\left(x_k\right)}{\partial x_n \partial x_2} & \cdots & \frac{\partial^2 f\left(x_k\right)}{\partial x_n^2}
\end{array}\right] 
$$

将权重$w$和极值$w^*$代入式中可得：

$$
{E(w)}=E\left(w^*\right)+E^{\prime}\left(w^*\right)\left(w-w^*\right)+\frac{1}{2 !}\left(w-w^*\right)^T\cdot \mathbf{H}\cdot \left(w-w^*\right)+o^n \tag{7}
$$

其中，$\mathbf{H}=\partial^2 E / \partial \mathbf{w}^2$,进一步，目标函数$\delta E$可表示为：

$$
\delta E=E(w)-E\left(w^*\right)=E^{\prime}\left(w^*\right)\left(w-w^*\right)+\frac{1}{2 !}\left(w-w^*\right)^T\cdot \mathbf{H}\cdot \left(w-w^*\right)+o^n \tag{8}
$$


关于权重误差的泰勒展开式：
$$
\delta E=\left(\frac{\partial E}{\partial \mathbf{w}}\right)^T \cdot \delta \mathbf{w}+\frac{1}{2} \delta \mathbf{w}^T \cdot \mathbf{H} \cdot \delta \mathbf{w}+o^n \tag{9}
$$

训练到局部误差最小的网络，第一项(线性)项消失，第三项和所有高阶项复杂度太高，所以这里只看第二项。

剪枝的目标是将权重$w$的一个元素（假设为$q$）设置为0，所以引入一个约束条件，如下式所示：
$$
 \delta \mathbf{w}+w_q=0 \tag{10}
$$
写成向量化的形式，如下式所示：
$$
\mathbf{e}_q^T \cdot \delta \mathbf{w}+w_q=0 \tag{11}
$$
其中 $\mathbf{e}_q^T$是单位向量。第$q$号元素是1，其他位置是0，而$w_q$是一个数值，即第$q$号元素的当前值。
目标转化为求解如下方程：
$$
\min _q\left\{\min _{\delta \mathbf{W}}\left(\frac{1}{2} \delta \mathbf{w}^T \cdot \mathbf{H} \cdot \delta \mathbf{w}\right) \mid \mathbf{e}_q^T \cdot \delta \mathbf{w}+u_q=0\right\} \tag{12}
$$

这是一个有约束的凸优化问题,为求解式12，利用拉格朗日乘数法组合式10和式11，表示如下：
$$
L=\frac{1}{2} \delta \mathbf{w}^T \cdot \mathbf{H} \cdot \delta \mathbf{w}+\lambda\left(\mathbf{e}_q^T \cdot \delta \mathbf{w}+w_q\right) \tag{13}
$$

对上式的$\delta \mathbf{w}$和$\lambda$分别求导，令导数为0，可得：

$$
\left\{\begin{array}{l}
\frac{1}{2}\left(\mathbf{H}+\mathbf{H}^T\right) \delta \mathbf{w}+\lambda \mathbf{e}_q=0 \\
\mathbf{e}_q^T \delta \mathbf{w}+w_q=0
\end{array}\right. \tag{14}
$$

对式14的第一个公式有疑问的可参考[向量，标量对向量求导数](https://blog.csdn.net/xidianliutingting/article/details/51673207)

联合求解可以得到：
$$
\delta \mathbf{w}=-\lambda \mathbf{H}^{-1} \mathbf{e}_q \tag{15}
$$

代入式14中第二个公式可以得到：

$$
\lambda=\frac{\mathbf{w}_q}{\left(\mathbf{H}^{-1}\right)_{q q}} \tag{16}
$$

代入式14中第一个公式可以得到：

$$
\delta w=-\frac{\mathbf{w}_q}{\left(\mathbf{H}^{-1}\right)_{q q}} \mathbf{H}^{-1} \mathbf{e}_q \tag{17}
$$

代入式9中可以得到：

$$
\delta E=\frac{w_q^2}{2\left(H^{-1}\right)_{q q}} \tag{18}
$$

上面两个公式17和18的意义在于：只需要找到一个权重$q$,使得误差最小，就可以自动调整其他权重。优势在于除了删除权重之外，它还计算和改变其他权重，而不需要梯度下降或其他增量训练。

假设一个非线性的神经网络满足以下公式：

$$
\mathbf{o}=\mathbf{F}(\mathbf{w}, in ) \tag{19}
$$

其中，$\mathbf{w}$是n维向量，代表神经网络的权重或其他参数，$in$表示输入向量，$o$代表输出向量。

均方误差$E$可表示为：

$$
E=\frac{1}{2 P} \sum_{k=1}^P\left(\mathbf{t}^{[k]}-\mathbf{o}^{[k]}\right)^T\left(\mathbf{t}^{[k]}-\mathbf{o}^{[k]}\right)  \tag{20}
$$

其中，$\mathbf{t}^{[k]}$表示期望输出结果。

关于$w$的一阶导数可表示为：

$$
\frac{\partial E}{\partial \mathbf{w}}=-\frac{1}{P} \sum_{k=1}^P \frac{\partial \mathbf{F}\left(\mathbf{w}, \mathbf{i n}^{[k]}\right)}{\partial \mathbf{w}}\left(\mathbf{t}^{[k]}-\mathbf{o}^{[k]}\right) \tag{21}
$$

关于$w$的二阶导数可表示为：

$$
\begin{array}{r}
\mathbf{H} \equiv \frac{1}{P} \sum_{k=1}^P\left[\frac{\partial \mathbf{F}\left(\mathbf{w}, \mathbf{i n}^{[k]}\right)}{\partial \mathbf{w}} \cdot \frac{\partial \mathbf{F}\left(\mathbf{w}, \mathbf{i n}^{[k]}\right)^T}{\partial \mathbf{w}}-\right. 
\left.\frac{\partial^2 \mathbf{F}\left(\mathbf{w}, \mathbf{i n}^{[k]}\right)}{\partial \mathbf{w}^2} \cdot\left(\mathbf{t}^{[k]}-\mathbf{o}^{[k]}\right)\right]
\end{array} \tag{22}
$$

当存在局部最小值时，$\mathbf{t}^{[k]}$接近$\mathbf{o}^{[k]}$，$\mathbf{t}^{[k]}-\mathbf{o}^{[k]}$该项可忽略，上式可表示为：

$$
\mathbf{H}=\frac{1}{P} \sum_{k=1}^P \frac{\partial \mathbf{F}\left(\mathbf{w}, \mathbf{i n}^{[k]}\right)}{\partial \mathbf{w}} \cdot \frac{\partial \mathbf{F}\left(\mathbf{w}, \mathbf{i n}^{[k]}\right)^T}{\partial \mathbf{w}} \tag{23}
$$

Case1：如果网络只有一个输出，n维的向量$\mathbf{X}^{[k]}$定义为：
$$
\mathbf{X}^{[k]} \equiv \frac{\partial \mathbf{F}\left(\mathbf{w}, \mathbf{i n}^{[k]}\right)}{\partial \mathbf{w}} \tag{23}
$$

所以式22可表示为：
$$
\mathbf{H}=\frac{1}{P} \sum_{k=1}^P \mathbf{X}^{[k]} \cdot \mathbf{X}^{[k] T} \tag{24}
$$

Case2：如果网络只有多个输出，$n * n_0$的向量$\mathbf{X}^{[k]}$定义为：

$$
\begin{aligned}
\mathbf{X}^{[k]} \equiv \frac{\partial \mathbf{F}\left(\mathbf{w}, \mathbf{i n}^{[k]}\right)}{\partial \mathbf{w}} & =\frac{\partial \mathbf{F}_1\left(\mathbf{w}, \mathbf{i n}^{[k]}\right)}{\partial \mathbf{w}}, \cdots, \frac{\partial \mathbf{F}_{n_0}\left(\mathbf{w} \cdot \mathbf{i n}^{[k]}\right)}{\partial \mathbf{w}} \\
& =\left(\mathbf{X}_1^{[k]}, \cdots, \mathbf{X}_{n_o}^{[k]}\right)
\end{aligned} \tag{25}
$$

式22可表示为：
$$
\mathbf{H}=\frac{1}{P} \sum_{k=1}^P \sum_{l=1}^{n_o} \mathbf{X}_l^{[k]} \cdot \mathbf{X}_l^{[k] T} \tag{26}
$$

由式24和式26可知，H是与梯度变量$X$相关的样本协方差矩阵。

由式24可得：完整的$\mathbf{H}$可由前一项推出来：

$$
\mathbf{H}_{m+1}=\mathbf{H}_m+\frac{1}{P} \mathbf{X}^{[m+1]} \cdot \mathbf{X}^{[m+1] T} \tag{27}
$$

但我们的目的是需要得到$\mathbf{H}$的逆。标准的求逆公式可表示如下：

$$
\begin{aligned}
& (\mathbf{A}+\mathbf{B} \cdot \mathbf{C} \cdot \mathbf{D})^{-1}= \\
& \quad \mathbf{A}^{-1}-\mathbf{A}^{-1} \cdot \mathbf{B} \cdot\left(\mathbf{C}^{-1}+\mathbf{D} \cdot \mathbf{A}^{-1} \cdot \mathbf{B}\right)^{-1} \cdot \mathbf{D} \cdot \mathbf{A}^{-1}
\end{aligned} \tag{28}
$$

将式27带入可得：

$$
\mathbf{H}_{m+1}^{-1}=\mathbf{H}_m^{-1}-\frac{\mathbf{H}_m^{-1} \cdot \mathbf{X}^{[m+1]} \cdot \mathbf{X}^{[m+1] T} \cdot \mathbf{H}_m^{-1}}{P+\mathbf{X}^{[m+1] T} \cdot \mathbf{H}_m^{-1} \cdot \mathbf{X}^{[m+1]}} \tag{29}
$$
推广到多个输出，可表示为：
$$
\begin{array}{r}
\mathbf{H}_{m l+1}=\mathbf{H}_{m l}+\frac{1}{P} \mathbf{X}_{l+1}^{[m]} \cdot \mathbf{X}_{l+1}^{[m] T} \\
\mathbf{H}_{m+1 l}=\mathbf{H}_{m n_o}+\frac{1}{P} \mathbf{X}_l^{[m+1]} \cdot \mathbf{X}_l^{[m+1] T}
\end{array} \tag{30}
$$

