# Mathematical Analysis Notes

## Elementary inequalities

Bernoulli不等式：$h>-1$、$n\in\N$
$$
(1+h)^n\ge 1+nh
$$


## Limits of real sequences

$$
\lim_{n\to\infty}x_n=x:\forall\varepsilon\exist N(N\in\N\land(n>N\rightarrow|x_n-x|<\varepsilon))
$$

### Properties of converging sequences

- Uniqueness
- Convergence implies boundedness
- Sign-preserving
- Compatibilities with arithmetic operations
- Subsequences converges at the same limit

善用夹逼；单调有界收敛审敛

证明$\{\sin x\}$发散：构造位于不同符号范围的子列；或差分、积化和差反证之

### Monotonic sequences

- Mono. & Bounded ==> Conv.
- Mono. & Bounded ==> Signed Inf.

### Cauchy Proposition

Cauchy命题：$x_n\to l\implies \overline{x_n}=\frac1n \sum{x_k}\to l$

Proof：在“$N_1$”切分，……

对符号确定的无穷大亦成立。

### Stolz's Theorem

0/0型：$a_n\to0$、$b_n\to0$，$a_n$严格递减，则
$$
\frac{b_{n+1}-b_n}{a_{n+1}-a_n}\to l\implies \frac{b_n}{a_n}\to l
$$

> $a_n$严格单调避免差分为0

$*/\infty$型：$a_n$为严格递增的无穷大量，则
$$
\frac{b_{n+1}-b_n}{a_{n+1}-a_n}\to l\implies \frac{b_n}{a_n}\to l
$$
两者可处理递推数列：$a_{n+1}=a_n+1/a_n$、$x_{n+1}=\sin x_n$、etc.

### $e$ & $\gamma$

证$e=\sum\frac1{k!}$：二项式展开定义式，一端比较，另一端截项，夹逼之
$$
1/(n+1)!<e-\sum(1/n!)<1/(n!n)
$$

$$
e-\left(1-1/n\right)^n\sim e/(2n)
$$

$$
\gamma\overset{\mathrm{def}}= \sum1/n-\ln n
$$

$$
\sum 1/n\sim \ln n+1/(2n)+\gamma
$$

### Sequences generated with iterations

第一律：迭代数列极限必为不动点
$$
x_{n+1}=f(x_n)\land x_n\to\eta\implies f(\eta)=\eta
$$
第二律：$x_{n+1}=f(x_n)$，且$f$在$\{x_k\}$所在区间$I$单调，则两者必有其一：

- $f$单增，$\{x_n\}$单调
- $f$单减，$\{x_n\}$奇偶项分别有相反的单调性

证明：对单增，用2023.5.15的办法比较；对单减，$f(f(x))$单增

命题2.6.3：$a$为$f$不动点，$f$在$a$处连续，在邻域$U=(a-r,a+r)$严格单增，在$(a-r,a)$上$f>x$，在$(a,a+r)$上$f<x$，且$x_0\in U$，则$f^n(x_0)\in U$，$f^n(x_0)\to a$

证：归纳有界，单调收敛，不动点为极限

压缩映射原理：$f([a,b])\subset[a,b]$，且存在压缩常数$0<k<1$，对$[a,b]$上任意$x$、$y$，$|f(x)-f(y)|\le k|x-y|$，则：

- $f$在$[a,b]$有唯一不动点$\eta$
- $a_{n+1}=f(a_n)\implies a\to\eta$
- 存在误差估计……（trivial）

可与Lagrange中值定理结合使用

### 上下极限

$\limsup$&$\liminf$

## Fundamental theorems of real numbers

### 确界存在

有上界必有最小上界（上确界）；有下界必有最大下界（下确界）；约定无界集的上下确界

### 闭区间套

闭区间套：$\{I_n\}$，其中每个$I_n$是闭区间，且$I_1\supset \cdots\supset I_n\supset\cdots$

闭区间套定理：$\bigcap_{i=1}^{\infty} I_n\ne\emptyset$；若$|I_n|\to 0$，$\bigcap_{i=1}^{\infty} I_n=\{x\}$

数列形式略。

对开区间不成立。

可证$|\R|>\aleph_0$

### 凝聚定理

有界数列必有收敛子列。

### Cauchy收敛准则

$$
\forall\varepsilon\exist N\forall m\forall n(N\in\N\land(m>N\land n>N\to |a_n-a_m|<\varepsilon))\Longleftrightarrow a_n ~\mathrm{converge}
$$

即：收敛数列与基本数列等价

### 覆盖定理

闭区间的任一开覆盖必有有限子覆盖。

加强形式：对闭区间$I$的开覆盖，存在$\delta >0$，对区间中任意$|x_1-x_2|<\delta$，开覆盖中有开区间$O$覆盖两数

## Limit Of Functions

### Definition

$$
\forall\varepsilon\exist\delta
$$

### Properties

- Uniqueness
- Local boundedness
- Local sign-preserving
- Arithmetics

Heine归结原理：
$$
f(x)\to A(x\to a)\Longleftrightarrow \forall\{a_n\}((a_n\to a)\to (f(a_n)\to A))
$$
Cauchy收敛准则：
$$
\forall \varepsilon>0\exist\delta\forall x_1,x_2\in O_{\delta}(a)-\{a\}(|f(x_1)-f(x_2)|<\varepsilon)
$$

### Two important limits

### ~

- $f=o(g)$：$f/g\to0$
- $f=O(g)$：$f/g$在去心邻域有界
- $f\sim g$：$f/g\to1$
- $f/(x-a)^{\alpha}=l>0$：$f$为$\alpha$阶无穷小
- 极限过程（$(x\to 1)$等）不可省略

等价量代换：注意仅限乘法

## Continuity

间断点：

- 存在两单侧极限为第一类；否则第二类。跳跃、可去、震荡、无界？

有界闭区间上的连续函数：

- 有界
- 有最值
- 一致连续

一致连续：定义略

开区间上的函数，在端点处存在有限极限亦一致连续。

满足Lipschitz条件（割线斜率有界）必一致收敛

单调函数间断点必然可数

## Derivatives

### Definitions

左右导数。

无穷小增量公式：$\Delta y=f'(x_0)\Delta x+o(\Delta x)~(\Delta x\to 0)$

反函数求导公式：$f=\varphi^{-1}$，$f'(x_0)=1/\varphi'(y_0)$

（一点处）可导一定连续，连续不一定可导

### High-order derivatives

Leibniz公式：
$$
(uv)^{n}=\sum_{k=0}^n C_n^ku^{(k)}v^{(n-k)}
$$
例题：$\arcsin^{(n)}(0)$

> 简单求导、整理易得：$(1-x^2)y''-xy'=0$
>
> 出现低次多项式因子，Leibniz展开，整理，代入$x=0$得递推公式
> $$
> y^{(n+2)}(0)=n^2 y^{(n)}(0)
> $$
> 从而易解。

从$e^{-1/x^2}$可将两常值函数延拓为无限可微函数。

### 隐函数求导

求$\frac{\mathrm d}{\mathrm dx}F(x,y(x))$，即可能求出$y'(x)$

### 参数方程求导

$$
\begin{cases}
x=x(t)\\
y=y(t)
\end{cases}\land x(t),y(t)可导\land x'(t)\ne0
\implies
y'(x)=\frac{y'(t)}{x'(t)}
$$

a.k.a
$$
y'_x=y'_tt'_x=y'_t/x'_t
$$

### 一阶微分形式不变性

## Theorems on derivatives

### Fermat's Lemma

Fermat定理：极值点处导数若存在，必为0

> 极值不要求严格大于/小于

### Rolle's Mean Value Theoem

$f$在$[a,b]$连续，在$(a,b)$可微，且$f(a)=f(b)$，则在$(a,b)$存在驻点

### Lagrange's Mean Value Theorem

（条件同）

### Cauchy's Mean Value Theorem

原条件 + $g(b)-g(a)\ne 0$ + $(f')^2+(g')^2\ne0$

### 

邻域上存在的导函数在对应点有极限，该导函数即在此处连续

### Taylor's Theorem

形式懒得敲

| Name     | $R_n(x)$                                                     | Requirement                   |
| -------- | ------------------------------------------------------------ | ----------------------------- |
| Peano    | $o((x-x_o)^n)$                                               | $f^{(n)}(x_0)\exists$         |
| Lagrange | $\frac{f^{(n+1)}(\xi)}{(n+1)!}(x-x_0)^{(n+1)}$               | $f^{(n+1)}\exist~@~O_r(x_0)$  |
| Cauchy   | $\frac{f^{(n+1)}(\eta)}{n!}(x-\eta)^n(x-x_0)$                | ibid.                         |
| Integral | $\frac1{n!}\displaystyle\int_{x_0}^x f^{(n+1)}(t)(x-t)^n\mathrm dt$ | $f\in C^{(n+1)}(x_0-r,x_0+r)$ |



### Examples



## Applications of derivatives

## Indefinite Integrals

## Definite Integrals

## Application of definite integrals

Wallis Formula:
$$
\frac{(2n)!!}{(2n-1)!!}\sim\sqrt{\pi n}
$$
 Stirling Formula:
$$
n!\sim \sqrt{2\pi n}\left(\frac ne\right)^n
$$


## Generalized integrals

## Real series

### With positive terms

Cauchy

#### Determination of convergence

比较判别法：～

| Name        | Definition                                                   | Converge | Diverge   |
| ----------- | ------------------------------------------------------------ | -------- | --------- |
| Cauchy Root | $\limsup_{n\to\infty} ~^n\sqrt{a_n}=c$                       | $c<1$    | $c>1$     |
| d'Alembert  | $\lim_{n\to\infty} \frac{a_{n+1}}{a_n}=d$                    | $d<1$    | $d>1$     |
| Raabe       | $\lim_{n\to\infty}n\left(\frac{a_n}{a_n+1}-1\right)=r$       | $r>1$    | $r<1$     |
| Bertrand    | $\lim_{n\to\infty}\ln n\left(n\left(\frac{a_n}{a_{n+1}}-1\right)-1\right)=b$ | $b>1$    | $b<1$     |
| Gauss       | $\frac{a_n}{a_{n+1}}=1+\frac{\mu}{n}+O\left(\frac{1}{n^{1+\varepsilon}}\right)$ | $\mu>1$  | $\mu\le1$ |

Cauchy积分判别法：$f$在$[1,+\infty)$上单调减少，则级数$\sum f(n)$与积分$\int_1^{+\infty}f(x)$同敛散

Cauchy凝聚判别法：$\sum a_n$与$\sum 2^n a_{2^b}$同敛散

### General Real Series

#### Convergence

Leibniz判别法：$a_n$单调收敛于0，$\sum_{n=1}^{\infty}(-1)^{n-1}a_n$收敛

Dieichlet判别法：$\{a_n\}$部分和数列有界，$\{b_n\}$单调收敛于0，则$\sum a_nb_n$收敛

Abel判别法：$\sum a_n$收敛，$\{b_n\}$单调有界，$\sum a_nb_n$收敛

#### Properties

Riemann重排定理：～

Cauchy乘积：$\sum_{n=1}^\infty \sum_{i+j=n+1}a_ib_j$

Mertens定理：$\sum a_n\to A$、$\sum b_n\to B$，且两者任一绝对收敛，则其柯西乘积收敛于$A\cdot B$

### Infinite Products

注意发散到0也是发散。

Viete公式：$\frac2\pi=\prod_{n=1}^\infty \cos\frac{\pi}{2^{n+1}}$

Alt. Form for Wallis Formula：～

正弦函数的无穷乘积形式：
$$
\sin x=x\prod_{n=1}^\infty\left(1-\frac{x^2}{n^2\pi^2}\right)
$$

> 乍看平凡，实则很有趣一公式

### Quizes

## Series of functions



### Taylor series

收敛半径
$$
R=\frac{1}{\displaystyle\limsup_{n\to\infty}~^n\sqrt{|a_n|}}=\lim_{n\to\infty} \frac{|a_n|}{|a_{n+1}|}
$$


## Fourier Series

## Applications of Series

## Point Sets In High-Dimensional Spaces

## Limit & Continuity of Multi-variable Functions

## Partial Derivatives

### Chaining Rule

$$
\begin{pmatrix}
\frac{\partial z}{\partial x_1}&\cdots&\frac{\partial z}{\partial x_n}
\end{pmatrix}
=\begin{pmatrix}
\frac{\partial f}{\partial u_1}&\cdots&\frac{\partial f}{\partial u_m}
\end{pmatrix}
\begin{pmatrix}
\frac{\partial u_1}{\partial x_1}&\cdots&\frac{\partial u_1}{\partial x_n}\\
\vdots&&\vdots\\
\frac{\partial u_m}{\partial x_1}&\cdots&\frac{\partial u_m}{\partial x_n}
\end{pmatrix}
$$



## Implied Functions And Their Partial Derivatives

### One Equations

若

- $(x_0,y_0)$邻近的矩形区域$D$上$F(x,y)$存在连续偏导数
- $F(x_0,y_0)=0$
- $F_y(x_0,y_0)\ne0$

则有

- $F(x,y)=0$唯一确定$y=f(x)$

- $f(x)$在$x_0$邻近连续

- $$
  f'(x)=-\frac{F_x(x,y)}{F_y(x,y)}
  $$

- 

### 隐函数组

若

- $F(x,y,u,v)$和$G(x,y,u,v)$在$p_0(x_0,y_0,u_0,v_0)$的一个邻域内有连续偏导
- $F(p_0)=G(p_0)=0$
- $J(p_0)=\frac{\partial(F,G)}{\partial(u,v)}|_{p_0}=\begin{vmatrix}F_u&F_v\\G_u&G_v\end{vmatrix}\ne0$

则

- $p_0$的一个邻域内$F=G=0$唯一确定一对函数$u=u(x,y)$，$v=v(x,y)$

- $$
  \begin{matrix}
  \frac{\partial u}{\partial x}=-J^{-1}\frac{\partial(F,G)}{\partial(x,v)}&\frac{\partial u}{\partial y}=-J^{-1}\frac{\partial(F,G)}{\partial(y,v)}\\
  \frac{\partial v}{\partial x}=-J^{-1}\frac{\partial(F,G)}{\partial(u,x)}&\frac{\partial v}{\partial y}=-J^{-1}\frac{\partial(F,G)}{\partial(u,y)}
  \end{matrix}
  $$

  

## Applications of Partial Derivatives

### Geometric Applications

#### 切平面（由一般方程）

对曲面$F(x,y,z)=0$，可给出法向量
$$
\boldsymbol n=\left(F_x,F_y,F_z\right)
$$


#### 切平面（由参数方程）

若曲面由参数方程
$$
(x,y,z)=(x(u,v),y(u,v),z(u,v))
$$
确定，则其法向量为
$$
\boldsymbol n=\left(
\frac{\partial(y,z)}{\partial(u,v)},\frac{\partial(x,z)}{\partial(u,v)},\frac{\partial(x,y)}{\partial(u,v)}
\right)
$$

#### 切向量与法平面

> 参数方程太简单不再给出

若直线由两曲线相交而成：
$$
F(x,y,z)=G(x,y,z)=0
$$
而且$F$、$G$有连续的偏导数，则可给出直线在$p_0$处的切向量
$$
\boldsymbol\tau=\left(\frac{\partial(F,G)}{\partial(y,z)},\frac{\partial(F,G)}{\partial(x,z)},\frac{\partial(F,G)}{\partial(x,y)}\right)=(\tau_x,\tau_y,\tau_z)
$$
从而不难给出切线与法平面方程
$$
\frac{x-x_0}{\tau_x}=\frac{y-y_0}{\tau_y}=\frac{z-z_0}{\tau_z}
$$

$$
\tau_x(x-x0)+\tau_y(y-y_0)+\tau_z(z-z_0)=0
$$

#### 

## 重积分

## Integrals With Parameters

Leibniz Rule:
$$
\varphi'(t)=f(\beta(t),t)\beta'(t)-f(\alpha(t),t)\alpha'(t)+\int_{\alpha(t)}^{\beta(t)}f_t(x,t)\mathrm dt
$$


## Integrals Along Curves

Green公式：$D$为有界闭区域，$\partial D$为$D$的一个正向分段光滑边界，$P$、$Q$有连续偏导数，则
$$
\iint_D\left(\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y}\right)\mathrm dx\mathrm dy
=\oint_{\partial D}P\mathrm dx+Q\mathrm dy
$$
即
$$
\iint\begin{vmatrix}\partial_x&\partial _y\\P & Q\end{vmatrix}\mathrm dx\mathrm dy
=\oint_{\partial D}P\mathrm dx+Q\mathrm dy
$$


## Integrals On Surfaces

Gauss公式：D为有界区域，$\partial D$为逐段光滑的外边界，$P$、$Q$、$Q$具有连续的偏导数，则有
$$
\iiint_D\left(\frac{\partial P}{\partial x}+\frac{\partial Q}{\partial y}+\frac{\partial R}{\partial z}\right)
\mathrm dx\mathrm dy\mathrm dz
={\oiint}_{\partial D}P\mathrm dy\mathrm dz+Q\mathrm dz\mathrm dx+R\mathrm dx\mathrm dy
$$
Stokes公式：$D$为$\R^3$中的光滑曲面，$\partial D$为$D$的分段光滑曲线，方向由右手定则确定，$P$、$Q$、$R$具有连续偏导数，有
$$
\oint_{\partial D}P\mathrm dx+Q\mathrm dy+R\mathrm dz
=\iint_D \begin{vmatrix} 
\mathrm dy\mathrm dz & \mathrm dz\mathrm dx&\mathrm dx\mathrm dy\\
\frac{\partial}{\partial x} & \frac{\partial}{\partial y} & \frac{\partial}{\partial z}\\
P&Q&R
\end{vmatrix}
$$


## Preliminary Field Theories



