# Complex Analysis

## CH 1: Preliminaries to Complex Analysis

### Complex numbers and the complex plane

#### Complex Numbers

Omitted.

#### Convergence

**Def.** A sequence $\{z_k\}$ of complex numbers converges to $w\in\C$ if
$$
\lim_{n\to \infty}|z_n - w| = 0
$$
A sequence converges iff both its real & imaginary parts converge at the given point.

**Theorem 1.1**: $\C$ is complete, i.e. all Cauchy sequences converges.

#### Sets in the complex plane

**Def.**

- $D_r(z_0)$, the open disc of radius $r$ centered at $z_0$. $\overline{D}_r(z_0)$ for closed ones.
- $\mathbb D$, the unit disc $\{z:|z|<1\}$.

**Def.**

- $z_0$ is an interior point of $\Omega$ if $D_r(z_0)\subset \Omega$ for some $r>0$. Interior of $\Omega$ is the set of all such $z_0$'s.
- $\Omega$ is open if $\operatorname{int}\Omega\supset\Omega$, closed if $\C-\Omega$ is open.
- $z$ is a limit point of $\Omega$ if $\exist\{z_1, z_2, \dots\}\subset \Omega$ s.t. $z_k\ne z$ but $z_k\to z$
- Closure $\overline{\Omega} = \Omega \cup \operatorname{limitpoints}\Omega$
- Boundary $\partial \Omega = \overline{\Omega} - \operatorname{int}\Omega$
- $\Omega$ is bounded if $\exists M>0\forall z\in\Omega(|z|<M)$
- $\Omega$ is compact if it is both closed and bounded.
- $\operatorname{diam}(\Omega) = \sup_{z,w\in \Omega}|z - w|$

**Theorem 1.2**: $\Omega\subset \C$ is compact iff every sequence has a subsequence converging to a $z\in \Omega$.

**Theorem 1.3**: $\Omega$ is compact iff every open covering of it has a finite subcovering.

**Proposition 1.4**: If $\C\supset\Omega_1\supset\Omega_2\supset\cdots$ is compact, and $\operatorname{diam}\Omega_n\to 0$ then $\exist$ unique $w\in C$ s.t. $w\in \forall \Omega_n$

**Def.**

- Open $\Omega\subset \C$ is connected if $\neg\exists$ disjoint open partitions of it. Call $\Omega$ a region.
- Closed $F\in \C$ is connected if $\neg\exists$ disjoint closes partitions of it.

### Functions on complex plane

#### Continuous functions

**Def.**: As the one for real functions

**Theorem 2.1**: A continuous function is bounded and attains a maximum & minimum on compact sets.

#### Holomorphic functions

**Def.**: $f$ is holomorphic at point $z_0$ if $\lim_{h\to 0}\frac{f(z_0+h) - f(z_0)}{h} \exists$, and denote this limit with $f'(z_0)$, the derivative of $f$ at $z_0$.

**Def. **: $f$ is holomorphic on $\Omega$ if it is at all $z\in\Omega$, entire if it is on $\C$.

> Alt. name: regular, complex differentiable

**Proposition 2.2**: Arithmetic rules on derivative of holomorphic functions applies as if the function is real.

#### Complex-valued functions as mappings

**Def.**: $F:\R^2\to\R^2$ is differentiable at $P_0=(x_0, y_0)$ if there is a linear map $J\in\mathcal L(\R^2)$ s.t.
$$
\frac{|F(P_0+H) - F(P_0) - J(H)|}{|H|}\to 0 \text{ as }|H|\to 0
$$
**Cauchy-Riemann equations**: For holomorphic $z = x+yi$ and $f(z) = u(x,y) + iv(x,y)$: 
$$
\begin{matrix}
\displaystyle{\frac{\partial u}{\partial x} = \frac{\partial v}{\partial y}} & 
\text{and} &
\displaystyle{\frac{\partial u}{\partial y} = -\frac{\partial v}{\partial x}}
\end{matrix}
$$

> This means the Jacobian matrix of $F(x,y)\mapsto (u,v)$ must be of form:
> $$
> \begin{pmatrix}
> \large * & -\triangle \\
> \triangle & \large *
> \end{pmatrix}
> $$

**Def.**: 
$$
\begin{matrix}
\displaystyle{\frac{\partial}{\partial z} = \frac{1}2\left(\frac{\partial}{\partial x}+\frac1i \frac{\partial}{\partial y}\right)} & 
\text{and} &
\displaystyle{\frac{\partial}{\partial \overline{z}} = \frac{1}2\left(\frac{\partial}{\partial x}-\frac1i \frac{\partial}{\partial y}\right)}
\end{matrix}
$$
**Proposition 2.3**: If $f$ is holomorphic at $z_0$, then
$$
\begin{matrix}
\displaystyle{\frac{\partial f}{\partial \overline{z}}(z_0) = 0} & 
\text{and} &
\displaystyle{\displaystyle{\frac{\partial f}{\partial z}(z_0)} = f'(z_0) = 2\frac{\partial u}{\partial z}(z_0)}
\end{matrix}
$$
Also if we write $F(x, y) = f(z)$, then $F$ is differentiable, and 
$$
\det J_F(x_0, y_0) = |f'(z_0)|^2
$$
**Theorem 2.4**: Both $\Re f$ and $\Im f$ is continuously differentiable on $\Omega$ and satisfy the Cauchy-Riemann equations, then f is holomorphic on $\Omega$ and $f'(z) = \frac{\partial f}{\partial z}$.

#### Power series

**Theorem 2.5**: Given $\sum_{n =0} ^\infty a_n z^n$, there is $0\le R\le \infty$ s.t.

- If $|z|<R$, the series converges.
- If $|z| > R$, the series diverges.

And $R$ is given by the Hadamard's formula
$$
\frac 1R = \limsup |a_n|^{1/n}
$$
**Def.**: 

- $R$ is the radius of convergence
- $\{z:z< R\}$ is the disk of convergence

**Theorem 2.6**: $f(z) = \sum a_n z^n$ defines a holomorphic function in its disk of convergence. The derivative of $f$, $f'$,  can be obtained with termwise differentiation, and has the same radius of convergence as $f$.

Sketch of proof: The proof of invariant radius is simple for that $n^{1/n}\to 1$, for the former, split the series at the $N$th term.

**Corollary 2.7**: A power series is infinitely differentiable within its disk of convergence.

**Def.**: $f$ is analytic at $z_0$ if it has a power series expansion converging to it in a neighborhood of $z_0$.

> Theorem 2.8 implies that analytic functions are holomorphic. The converse also holds, as to prove in the following chapter, leading to an equivalence between these two concept.