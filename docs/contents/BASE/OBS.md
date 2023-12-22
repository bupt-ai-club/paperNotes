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

我们首先要找一个  使得(7)式最小，找到该权重以后，再依据式子(6)调整其他权重。如此，便能使得损失(7)最小。