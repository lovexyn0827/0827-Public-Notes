# Notes on *Statistic Inference*

## CH 1: Probability Theory

### Getting started

Sample space: Set $S$ of all possible outcomes of a particular experiment.

Event: Any collection of outcomes, that is, any subset of $S$.

Partition: Disjoint $A_1, A_2, \cdots$, s.t. $\bigcup_{i =1}^\infty A_i = S$

$\sigma-$algebra (on $S$): A set $\mathscr B \subset P(S)$ s.t.

- $\emptyset \in \mathscr B$
- $A\in \mathscr B \implies A^c \in \mathscr B$
- $A_1, A_2, \dots \in \mathscr B \implies \bigcup_{i = 1}^\infty A_i \in \mathscr B$

Probability function: $P$ with domain $\mathscr B$ s.t.

- $\forall A\in \mathscr B, P(A) \ge 0$
- $P(S) = 1$
- $A_1, A_2, \dots \text{ are pairwise disjoint } \implies P(\bigcup_{i = 1}^\infty A_i) = \sum_{i = 1}^\infty P(A_i)$

Theorem 1.2.8 - 1.2.11: If $P$ is a probability function and $A, B\in \mathscr B$, then:

- $P(\emptyset) = 0$
- $P(A) \le 1$
- $P(A^c) = 1 - P(A)$
- $P(B\cap A^c) = P(B) - P(A\cap B)$
- $P(A\cup B) = P(A) + P(B) - P(A\cap B)$
- $A\subset B\implies P(A) \le P(B)$
- $P(A) = \sum_{i  =1}^\infty P(A\cap C_i)$ for any partition $C_1, C_2, \dots$
- $P(\bigcup_{i = 1}^\infty A_i) \le \sum_{i = 1}^\infty P(A_i)$ for any sets $A_1, A_2, \dots$

Theorem 1.2.6: Let $S = \{s_1, s_2, \dots\}$ be an countable set, $\mathscr B$ be any $\sigma-$ algebra on $S$, $p_1, p_2, \dots$ be nonnegative numbers sum to 1, Define $P$ on $\mathscr B$ by 
$$
P(A) = \sum_{\{i:s_1\in A\}} p_i
$$
Then, $P$ in a probability function on $\mathscr B$.

Counting: Number of arrangements of size $r$ out of $n$ objects:

|           | With Replacement                                | Without Replacement                                      |
| --------- | ----------------------------------------------- | -------------------------------------------------------- |
| Ordered   | $\frac{n!}{(n - r)!}$                           | $n^r$                                                    |
| Unordered | $\left(\begin{matrix}n \\ r\end{matrix}\right)$ | $\left(\begin{matrix} n + r - 1 \\ r\end{matrix}\right)$ |

$k$ digits, with $m$ distinct symbols, each appearing $k_1, \dots, k_m$ times: $\frac{k!}{k_1!\cdot k_2!\cdot \cdots\cdot k_m!}$ possible ordered samples.

### Conditional Probability and Independence

Conditional probability of $A$ given $B$: $A, B$ are events, and $P(B) > 0$, denote it as 
$$
P(A|B) = \frac{P(A\cap B)}{P(B)}
$$
Bayes' Rule: Let $A_1, A_2, \dots$ be partition of $S$, and $B$ be any set, then, for each $i = 1, 2, \dots$:
$$
P(A_i|B) = \frac{P(B|A_i)P(A_i)}{\sum_{j = 1}^\infty P(B|A_j) P(A_j)}
$$
Statistically independent (two events): $P(A\cap B) = P(A)P(B)$

Events $A_1, \dots, A_n$ mutually independent iff for any $\{A_{i_1}, \dots, A_{i_k}\} \subset \{A_1, \dots, A_n\}$
$$
P\left(\bigcap_{j = 1}^k A_{i_j}\right) = \prod_{j = 1}^k P\left(A_{i_j}\right)
$$
Theorem 1.3.9: If $A, B$ are independent, then pairs $A$ and $B^c$, $A^c$ and $B$, $A^c$ and $B^c$ are also independent.

### Random Variable and Distribution

Random variable: A function $X: S\to \R$

Cumulative distribution function (cdf) of $X$: 
$$
F_X(x) = P_X(X \le x)
$$
Theorem 1.5.3: A function $F$ is a cdf iff:

- $\lim_{x\to -\infty} = 0$
- $\lim_{x\to+\infty} = 1$
- $F(x)$ is nondecreasing
- $F(x)$ is right continuous, i.e. $\lim_{x\to x_0^+} F(x) = F(x_0)$

Random variable $X$ is continuous if $F_X$ is continuous, is discrete of $F_X$ is a step function

Random variable $X, Y$ are identically distributed iff $\forall A\in \mathscr B^1, P(X\in A) = P(Y\in A)$, where $\mathscr B^1$ is the smallest $\sigma-$algebra containing all real intervals.

> Identically distributed random variables are not necessarily equal.

Theorem 1.5.10: $X, Y$ identically distributed iff $\forall x, F_X(x) = F_Y(x)$

Probability mass function (pmf) of a discrete random variable $X$: 
$$
f_X(x) = P(X = x)
$$
Probability density function (pdf) of a continuous random variable is $f_X$ s.t. 
$$
F_X(x) =\int_{-\infty}^x f_X(t)\mathrm dt
$$
A function $f_X$ is a pdf (or pmf) iff

- $\forall x, f_X(x) \ge 0$
- $\sum_x f_X(x) = 1$ (pmf) or $\int_{-\infty}^{+\infty} f_X(x)\mathrm dx = 1$ (pdf)

## CH 2: Transformations and Expectations

### Distributions of Functions of a Random Variable

Determining cdf of $Y = g(X)$:
$$
\begin{eqnarray}
	F_Y(y) &=& P(Y\le y)\\
	&=& P(g(X)\le y)\\
	&=& P(\{x\in \mathscr X:g(x)\le y\})\\
	&=& \int_{\{x\in \mathscr X:g(x)\le y\}}f_X(x)\mathrm dx
\end{eqnarray}
$$
Theorem 2.1.3: Let $Y = g(X)$, $\mathscr X = f_X^{-1}(\R^+)$, $\mathscr Y = g(\mathscr X)$, then

- If $g$ is an increasing function on $\mathscr X$, $F_Y(y) =F_X\left(g^{-1}(y)\right), \forall y\in \mathscr Y$
- If $g$ is a decreasing function on $\mathscr X$, and $X$ is continuous, $F_Y(y) = 1 - F_X\left(g^{-1}(y)\right),  \forall y\in \mathscr Y$

> Where $\mathscr X$is called the support set (abbr. support) of $X$

Theorem 2.1.5: $Y = g(X)$ and $g$ is monotonic. Define $\mathscr X, \mathscr Y$ as above. Suppose that $f_X(x)$ is continuous on $\mathscr X$ and $g^{-1}(y)$ has a continuous derivative on $\mathscr Y$, then
$$
f_Y(y) = \begin{cases}
f_X\left(g^{-1}(y)\right)\left|\frac{\mathrm d}{\mathrm dy}g^{-1}(y) \right| & y\in \mathscr Y\\
0 & \text{otherwise}
\end{cases}
$$


Theorem 2.1.8: $Y = g(X)$, $\mathscr X = f_X^{-1}(\R^+)$. Suppose there exists a partition $A_0, A_1, \dots, A_k$ of $\mathscr X$ s.t. $P(X\in A_0 = 0)$ and $f_X$ is continuous on each $A_i$. Furthermore, suppose there exists functions $g_1, \dots , g_k$ on $A_1, \dots, A_k$, respectively, satisfying:

1. $g(x) = g_i(x), \forall x\in A_i$
2. $g_i(x)$ is monotone on $A_i$
3. $g_1(A_1) = \cdots = g_n(A_n)$
4. each $g_i^{-1}$ has continuous derivative on $g_i(A_i)$

Then, 
$$
f_Y(y) = \begin{cases}
\displaystyle \sum_{i = 1}^k f_X\left(g_i^{-1}(y)\right)\left|\frac{\mathrm d}{\mathrm dy}g^{-1}(y) \right| & y\in \mathscr Y\\
0 & \text{otherwise}
\end{cases}
$$
Theorem 2.1.10: $X$ has continuous cdf, then $F_X(X) \sim \operatorname{uniform}(0, 1)$

### Expected Value

Expected value (or mean) of $g(X)$: 
$$
E\left(g(X)\right) = \begin{cases}
\displaystyle{\int_{-\infty}^{+\infty} g(x)f_X(x)\mathrm dx} & X \text { is continuous}\\
\displaystyle{\sum_{x\in \mathscr X} g(x)f_X(x) = \sum_{x \in \mathscr X} g(x)P(X = x)} & X \text{ is discrete}
\end{cases}
$$
$E(g(X))$ doesn't exist if $E|g(X)| = \infty$

Theorem 2.2.5: Let $X$ be a random variable and let $a, b, c$ be constants. Then for any function $g_1, g_2$ whose expectation exists:

- $E(ag_1(X) + bg_2(X) + C) = aEg_1(X) + bEg_2(X) + c$
- $(\forall x,g_1(x)\ge 0) \implies Eg_1(X) \ge 0$
- $(\forall x, g_1(x) \ge g_2(x)) \implies Eg_1(X) \ge Eg_2(X)$
- $(\forall X, a \le g_1(X) \le b) \implies a \le Eg_1(X) \le b$

### Moments and Moment Generating Function

For $n\in \Z$, the $n$th moment of $X$ (or $F_X(x)$) is
$$
\mu_n' = EX^n
$$
The $n$th central moment of $X$, is
$$
\mu_x = E(X - E(X))^n
$$
The variance of a random variable is its second central moment, that is 
$$
\operatorname{Var} X = E(X - EX)^2
$$
The positive square root of it is the standard deviation of $X$.

Theorem 2.3.4: For $X$ with a finite variance, following holds for any constant $a, b$:
$$
\operatorname{Var}(aX + b) = a^2 \operatorname{Var} X
$$
The moment generating function (mgf) of $X$ (or $F_X$) is 
$$
M_X(t) = E\mathrm e^{tX}
$$
Theorem 2.3.7: The $n$th moment is equal to the $n$th derivative of $M_X(t)$ evaluated at $t = 0$, that is,
$$
E X^n = M_X^{(n)}(0) = \left.\frac{\mathrm d^{n}}{\mathrm dt^n}M_X(t)\right|_{t = 0}
$$
Theorem 2.3.11 (characterizing a distribution with moments): $F_X, F_Y$ be cdfs of all of whose moments exists, then

- $X, Y$ has bounded support $\implies$ $(\forall u(F_X(u) = F_Y(u))\iff (\forall r \in \N(EX^r = EY^r))$
- $(\exist\varepsilon > 0\forall t\in(-\varepsilon, \varepsilon)(M_X(t) = M_Y(t))) \implies (\forall u (F_X(u) = F_Y(u)))$

Theorem 2.3.15: For any constant $a, b$, 
$$
M_{aX+b}(t) = \mathrm e^{bt} M_X(at)
$$

### Differentiating under an Integral Sign

Theorem 2.4.1 (Leibnitz's Rule): If $f(x, \theta)$, $a(\theta)$, $b(\theta)$ are differentiable with respect to $\theta$, then
$$
\frac{\mathrm d}{\mathrm d\theta}\int_{a(\theta)}^{b(\theta)} f(x, \theta) \mathrm dx
= f(b(\theta), \theta)\frac{\mathrm d}{\mathrm d\theta}b(\theta) - f(a(\theta), \theta)\frac{\mathrm d}{\mathrm d\theta}a(\theta)
+\int_{a(\theta)}^{b(\theta)} \frac{\partial}{\partial \theta}f(x, \theta) \mathrm dx
$$
Especially, if $a(\theta), b(\theta)$ are constants, 
$$
\frac{\mathrm d}{\mathrm d\theta}\int_a^b f(x, \theta) \mathrm dx = \int_a^b\frac{\partial}{\partial \theta}f(x, \theta) \mathrm dx
$$
(Omitting other theorems appearing in Analysis textbooks, including interchanging of infinity summation, function limit, integration, and differentiation.)

## CH 3: Common Families of Distributions

### Instances of Distributions

Discrete Distributions:

| Distribution      | pmf.                                                         | $\operatorname{E}$ | $\operatorname{Var}$                    | Models                      |
| ----------------- | ------------------------------------------------------------ | ------------------ | --------------------------------------- | --------------------------- |
| Uniform           | $1/N$                                                        | $\frac{N+1}2$      | $\frac{N^2 - 1}{12}$                    | ~                           |
| Hypergeometric    | $\frac{C_M^x C_{N-M}^{K-x}}{C_N^K}$                          | $\frac{M}{N} K$    | $\frac{M}{N}K\frac{(N-M)(N-K)}{N(N-1)}$ | ~                           |
| Binomial          | $C_n^x p^x(1-p)^{n-x}$                                       | $np$               | $np(1-p)$                               | ~                           |
| Poisson           | $\mathrm e^{\lambda}\frac{\lambda^x}{x!}$                    | $\lambda$          | $\lambda$                               | $P\propto \text{time}$      |
| Negative Binomial | $\begin{eqnarray}C_{x - 1}^{r - 1}p^r(1-p)^{x - r}\\=C_{r+y+1}^yp^r(1-p)^y\end{eqnarray}$ | $r\frac{p}{1-p}$   | $r\frac{1-p}{p^2}$                      | Trials before $r$th success |
| Geometric         | $p(1-p)^{x-1}$                                               | $\frac1p$          | $\frac{1-p}{p^2}$                       | ~                           |

> Poisson distribution is the continuous variant of binomial distribution.
>
> Let $r = 1$ in negative binomial distribution to obtain an geometric distribution.

Continuous Distributions:

| Distribution       | pdf.                                                         | $\operatorname{E}$                   | $\operatorname{Var}$                                         | Semantic Def.                                                | Args.                             |
| ------------------ | ------------------------------------------------------------ | ------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | --------------------------------- |
| Uniform            | $\begin{cases}\frac{1}{a-b} & x\in[a, b]\\ 0 & \text{Otherwise}\end{cases}$ | $\frac{a+b}2$                        | $\frac{(b-1)^2}{12}$                                         | ~                                                            | $a, b$                            |
| Gamma              | $\frac{1}{\Gamma(\alpha)\beta^\alpha}x^{\alpha - 1}\mathrm e^{-\frac{x}{\beta}}$ where $x>0$ | $\alpha\beta$                        | $\alpha\beta^2$                                              | $f_T = \frac{t^{\alpha - 1}\mathrm e^{-t}}{\Gamma(\alpha)}$ and $X = \beta T$ | $\alpha,\beta\in\R^+$             |
| Normal             | $\frac{1}{\sqrt{2\pi}\sigma}\exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)$ | $\mu$                                | $\sigma^2$                                                   | ~                                                            | $\mu\in \R, \sigma^2(\sigma > 0)$ |
| Beta               | $\frac{1}{B(\alpha, \beta)}x^{\alpha - 1}(1-x)^{\beta - 1}$ where $0<x<1$ | $\frac{\alpha}{\alpha + \beta}$      | $\frac{\alpha\beta}{(\alpha + \beta)^2(\alpha + \beta + 1)}$ | $B(\alpha,\beta)=\frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha + \beta)}$ | $\alpha, \beta\in\R^+$            |
| Lognormal          | $\frac{1}{\sqrt{2\pi}\sigma x}\exp\left(-\frac{(\ln x-\mu)^2}{2\sigma^2}\right)$ where $x > 0$ | $\mathrm e^{\mu + \frac{\sigma^2}2}$ | $\mathrm e^{2\mu + 2\sigma^2}-\mathrm e^{2\mu+\sigma^2}$     | $\ln X\sim \operatorname{n}(\mu,\sigma^2)$                   | $\mu\in \R, \sigma^2(\sigma > 0)$ |
| $\chi^2$           | $\frac{1}{\Gamma\left(\frac p2\right)2^{\frac p2}} x^{\frac p2 - 1}\mathrm e^{-\frac p2}$ where $x>0$ |                                      |                                                              |                                                              | $p$                               |
| Exponential        | $\frac1\beta e^{-\frac x\beta}$ where $x>0$                  |                                      |                                                              |                                                              | $\beta$                           |
| Double Exponential | $\frac{1}{2\sigma}\mathrm e^{-\frac{|x-\mu|}{\sigma}}$       | $\mu$                                | $2 \sigma^2$                                                 | ~                                                            | $\mu, \sigma(\sigma > 0)$         |
| Cauchy             | $\frac1\pi \frac{1}{1+(x-\theta)^2}$                         | $\neg\exists$                        | $\neg\exists$                                                | $\operatorname{n}(0,1)/\operatorname{n}(0,1)$                | $\theta\in\R$                     |

> The $\chi^2$ ($\alpha = \frac p2, \beta = 2$) and exponential distribution ($\alpha = 1$) is special cases of Gamma distribution.

### Exponential Families

**Def.**: Exponential family is a family of pdfs or pmfs that can be expressed as
$$
f(x|\theta) = h(x)c(\theta)\exp\left(\sum_{i = 1}^k w_i(\theta)t_i(x)\right)
$$
Where $h(x) \ge 0$ and $t_i(x)$ are real-valued functions of $x$; $c(\theta)\ge 0$ and $w_i(\theta)$ are real-valued functions of $\theta$, and $\theta$ may be either scalars or vectors.

**Def.**: The indicator function of set $A$, is
$$
I_A(x) = I(x\in A) = \begin{cases}
1 & x\in A\\
0 & x\notin A
\end{cases}
$$
**Def.**: A curved exponential family is an exponential family with dimension $d$ of vector $\theta$ ls smaller than $k$ (number of terms of the summation); or called full exponential family if $d = k$.

Alternative form of pdf & pmfs in exponential families:
$$
f(x|\eta) = h(x)c^*(\eta)\exp\left(\sum_{i = 1}^k \eta_i t_i(x)\right)
$$
Where $\mathscr H=\left\{\eta = (\eta_1, \dots, \eta_k):\int_{\R} h(x)\exp\left(\sum_{i = 1}^k \eta_i t_i(x)\right)\mathrm dx<\infty\right\}$ is the natural parameter space.

This gives a simplified version of Theorem 3.4.2 (whose original from is to ugly to type down):
$$
\begin{eqnarray}
E(t_j(X)) &= -\frac{\partial}{\partial\eta_j}\log c^*(\eta)\\

\operatorname{Var}(t_j(X)) &= -\frac{\partial^2}{\partial\eta_j^2}\log c^*(\eta)
\end{eqnarray}
$$

### Location and Scale Families

**Theorem 3.5.6**: Let $f$ be any pdf, $\mu\in\R$ and $\sigma \in\R^+$, then $X$ is a random variable with pdf $\frac1\sigma f\left(\frac{x-\mu}{\sigma}\right)$ iff $Z$ has pdf $f$ and $X = \sigma Z + \mu$

### Inequalities and Identities

**Theorem 3.6.1 Chebychev's Inequality **: Let $X$ be a random variable, $g$ be a nonnegative function, for any $r>0$,
$$
P(g(X)\ge r) \le \frac{Eg(X)}{r}
$$
Proof: 
$$
\begin{eqnarray}
Eg(X) &=& \int_{-\infty}^{+\infty} g(x)f_X(x)\mathrm dx\\
 &\ge& \int_{\{x:g(x)\ge r\}} g(x)f_X(x)\mathrm dx\\
 &\ge& \int_{\{x:g(x)\ge r\}} rf_X(x)\mathrm dx\\
 &=& rP(g(X)\ge r)
\end{eqnarray}
$$
**Variant**: Let $\mu = EX$, $\sigma^2 = \operatorname{Var}X$, $g(x) = \frac{(x - \mu)^2}{\sigma^2}$, $r = t^2$, applying the inequality,
$$
P\left(\left(\frac{X-\mu}{\sigma}\right)^2\ge t^2\right)\le\frac1{r^2}
$$
**Theorems omitted~**