# LADR Notes

## Vector Space

### $\R^n$ and $\C^n$

List are ordered, and infinite.

(Omitting most of trivial contents)

### Definition of Vector Spaces

Axioms defining vector spaces (and thus vectors):

- Commutativity of addition
- Associativity of addition & scalar multiplication
- Identity for addition & scalar addition exists
- Additive inverse exists
- Scalar multiplication inverse exists
- Addition is distributive on scalar multiplications

**Def.**: Let $S$ be a set, $\mathbf F^S$  denotes the set of functions from $S$ to $\mathbf F$.

**1.26**: A vector space has a unique additive identity.

**1.27**: Every vector has a unique additive inverse.

**1.30**: $\forall v\in V, 0v = 0$

**1.31**: $\forall a\in \mathbf F, a0 = 0$

**1.32**: $\forall v\in V, (-1)v = -v$

### Subspaces

**1.34 (Conditions for a subspace)**: $U\subset V$ is a subspace iff it

- has the additive identity
- closed under addition
- closed under scalar multiplication

Sketch of proof: Trivial.

**Def. 1.36**: Sum of subspaces
$$
V_1+\cdots + V_n = \{v_1+\cdots+v_n: v_k\in V_k, \forall 1\le k\le n\}
$$
The sum is direct (**1.41**) if each element in the sum has a unique way to be written as sum of vectors. Using $\oplus$ to emphasize.

**1.40 (Minimality of sum of subspaces)**: $V_1,\dots, V_m$ be subspaces of $V$, then $V_1+\cdots+V_n$ is the smallest subspace containing all of them.

Conditions for direct sums:

- **1.45 (Iff 0 has unique representation as a sum)**: $V_1+\cdots+V_n$ is direct iff
  $$
  0 = v_1+\cdots +v_n\iff v_1 = \cdots = v_n = 0
  $$

- **1.46**: For pairs, their sum is direct iff disjoint
  $$
  U\oplus W \iff U\cap W = \{0\}
  $$
  Sketch of proof: For $\implies$ part, suppose $v\in U\cap W$ and have $v=0$ as $0 = v+(-v)$ has unique representation.

  For the reverse part, suppose $0 = u + w$, and show $u = w = 0$ by $u = -w\in U\cap W$

  >  But note that pairwise disjoint does NOT imply direct sum of multiple subspaces.

- 2.43: For pairs of finite-dimensional spaces, their sum is direct iff their dimension adds up:
  $$
  U\oplus W\iff \dim(U+W) = \dim U + \dim W
  $$

## Finite-Dimensional Vector Spaces

### Span and independence

**Def. 2.4**: span of vectors
$$
\operatorname{span}(v_1, \dots, v_m) = \text{linear combinations of } v_1, \dots, v_m
$$
If $\operatorname{span}(v_1, \dots, v_m) = V$, then $v_1, \dots, v_m$ is said to span $V$. (**2.7**)

**2.6 (Minimality of span)**: The span is the smallest subspace containing all listed vectors.

Sketch of proof: Show the span is a subspace, and then show minimality by that every subspace of $V$ contains it.

**Def. 2.9**: A vector space is finite-dimensional if some (finite) list spans it. Infinite-dimensional otherwise.

**Def. 2.15**: $v_1, \dots, v_m\in V$ is linearly independent iff
$$
a_1v_1 + \cdots + a_mv_m = 0 \iff a_1 = \cdots = a_m = 0
$$
In particular, the empty list $()$ is linearly independent.

**2.19 (Linear dependence lemma)**: Suppose $v_1, \dots, v_m\in V$ is linearly dependent, then $\exist 1\le k\le m$ s.t.
$$
v_k\in \operatorname{span}(v_1,\dots,v_{k-1})
$$
Furthermore, the removal of $v_k$ from the list leaves the span unchanged.

Sketch of proof: Find the largest $k$ s.t. $a_k\ne 0$ in some representation of $0$.

**2.22**: For finite-dimensional spaces, linearly independent lists is no longer than spanning lists.

**2.25**: If a vector space is finite-dimensional, so do its subspaces.

> Both of the two propositions above are proven with $n-$step algorithms.

### Bases

**Def. 2.26**: A basis of $V$ is a linearly independent list spanning $V$.

**2.28**: List $v_1, \dots, v_n$ is a basis of $V$ iff every $v\in V$ has a unique representation as linear combination of vectors in the list.

Sketch of proof. Spanning $V$ implies the desired existence. For the uniqueness, suppose $\sum a_k v_k = \sum c_kv_k=v$, and show that each $a_k - c_k=0$ by linear independence.

**2.30**: Every spanning list contains a basis. 

Sketch of proof: Repeatedly remove $v_k$'s s.t. $v_k\in\operatorname{span}(v_1, \dots, v_{k-1})$, for $k = 1, \dots, n$, to gain linear independence while remaining to span $V$.

**2.31**: Every finite-dimensional vector spaces has a basis.

**2.32**: Every linearly independent list of $V$ can be extended to a basis of it.

Sketch of proof: Concatenate the list with a spanning list, and apply the algorithm in the proof of **2.30**.

**2.33**: Given subspace $U$ of finite-dimensional $V$, there exist another subspace $W$ s.t. $V = U\oplus W$.

Sketch of proof: Extend the basis of $U$ to a basis of $V$, and denote the span if the extension as $W$. The rest is trivial.

### Dimension

**2.34**: Every basis of a finite-dimensional vector space have the same length.

Sketch of proof: Apply **2.22** that linearly independent lists is no longer than spanning lists.

**Def. 2.35**: $\dim V = \text{the length of bases of }V$

**2.37 & 2.39**: V is finite-dimensional, and $U$ is a subspace of $V$, then $\dim U\le \dim V$. Equality holds iff $U=V$.

Sketch of proof: For the inequality, again, use 2.22. For the equality, use 2.38.

**2.38 & 2.41**: $V$ is finite-dimensional, then every linearly independent list with length $\dim V$ is a basis of it. Similar result holds for spanning lists,

Sketch of proof: Needless to extend (or reduce) to be a basis.

**2.43**: For finite-dimensional $U, V$,
$$
\dim(U + V) = \dim U + \dim V - \dim(U\cap V)
$$
In particular, $\dim(U \oplus V) = \dim U + \dim V$

> Question: Is $U\cap V$ a vector space? Try to prove it with 1.34!

Sketch of proof: Extend a basis of $U\cap V$ to basis of $U$ and $V$, and prove that the union is a basis of $U + V$.

## Linear Maps

### Vector Space of Linear Maps

**Def. 3.1 & 3.2**: A linear map from $V$ to $W$ is a function $T: V\to W$ with

- Additivity: $T(u + v) = Tu + Tv, \forall u,v\in V$
- Homogeneity: $T(\lambda v)=  \lambda Tv, \forall \lambda\in\mathbf F\forall v\in V$

Denote $\mathcal{L}(V,W)$ as the set of $T:V\to W$, and $\mathcal L(V) = \mathcal L(V, V)$

**3.4 (Linear map lemma)**: Suppose $v_1, \dots, v_n$ is a basis of $V$ and $w_1,\dots, w_n\in W$, then there exist a unique linear map $T:V\to W$ s.t.
$$
Tv_k = w_k, \forall 1\le k\le n
$$

> That is, the value on a basis uniquely characteristic a linear map.

Sketch of proof: Define $T(\sum c_kv_k) = \sum c_kw_k$ to justify the existence of $T$ as a function, and verify its linearity trivially. Reconstruct the form with additivity, homogeneity and the hypothesis and use the fact $v_1, \dots, v_n$ being a basis to show uniqueness.

**3.5, 3.6, 3.7**: Omitted

**3.8**: Linear maps has:

- Associativity: $(RS)T = R(ST)$
- Identity: $\exist I\forall T(TI = IT = T)$, note that the $I$ in $IT$ and $TI$ may differ.
- Distributive properties: $(S_1+S_2)T = S_1T + S_2T$, $S(T_1 + T_2) = ST_1 + ST_2$

**3.9**: $T(0) = 0$

**Exercise 3A 3**: Suppose $T\in\mathcal L(\mathbf F^n, \mathbf F^m)$, $\exist A_{jk}\in F$ s.t. for every $(x_1,\dots,x_n)\in \mathbf F$, 
$$
T(x_1, \dots, x_n) = \left(\sum A_{1,j}x_j, \dots, \sum A_{n,j}x_j\right)
$$
Sketch of proof: Standard basis & linear map lemma.

**Exercise 3A 4**: $Tv_1, \dots, Tv_m$ may be linearly independent only if $v_1, \dots, v_m$ does.

### Null Space and Ranges

**Def. 3.11**: $\operatorname{null} T = \{v\in V: Tv = 0\}$

**3.13**: $T\in \mathcal L(V, W)$, then $\operatorname{null} T$ is a subspace of $V$.

**Def. 3.14**: Function $T: V\to W$ is injective if $Tu = Tv \implies u = v$

**3.15**: $T\in \mathcal L(V, W)$, then $T \text{ is injective } \iff \operatorname{null} T = \{0\}$

Sketch of proof: For the $\implies$ part, suppose $v\in \operatorname{null}T$, and get $Tv = T0 = 0$ and thus $v = 0$. For the converse part, show that $T(u-v) = 0$.

**Def. 3.16**: $\operatorname{range} T = \{Tv: v\in V\}$

**3.18**: $\operatorname{range} T$ is a subspace of $W$.

**Def. 3.19**: Function $T: V\to W$ is surjective if $\operatorname{range} T = W$

**3.21 (FUNDAMENTAL THEOREM OF LINEAR MAPS)**: Suppose $V$ is finite-dimensional and $T\in \mathcal L(V, W)$, then $\operatorname{range} T$ is finite-dimensional and
$$
\dim V = \dim\operatorname{null}T + \dim\operatorname{range}T
$$
Sketch of proof: Let $u_1,\dots, u_m$ be a basis of $\operatorname{null} T$, and extend it to a basis of $V$, namely $u_1,\dots, u_m, v_1, \dots, v_n$. Then show that $Tv_1\dots,Tv_n$ is a basis of $\operatorname{range}T$, by verifying the list spans it ($Tv = \sum b_kTv_k$) and is linearly independent (Suppose $\sum c_kTv_k=0$ and show that $c_k\equiv 0$). The rest of the proof is trivial.

**3.22**: $V, W$ are finite-dimensional, and $\dim V > \dim W$, then there is no injective linear map in $\mathcal L(V, W)$.

**3.23**: $V, W$ are finite-dimensional, and $\dim V < \dim W$, then there is no surjective linear map in $\mathcal L(V, W)$.

Sketch of proof: For 3.22, $\dim \operatorname{null}T = \dim V - \dim \operatorname{range}T\ge \dim V - \dim W > 0$.

**3.26**: A homogeneous system of linear equations with more variable than equations has non-zero solutions.

**3.28**: An inhomogeneous system of linear equations with more equations than variables may have no solution for some choice of constant terms.

Sketch of proof: Use 3.22 & 3.23.

**Exercise 3B 5 & 6**: $T$ s.t. $\operatorname{range}T=\operatorname{null}T$ exists in $\mathcal L(\R^4)$ but not in $\operatorname{\R^5}$.

**Exercise 3B 21**: $\dim T^{-1}U = \dim \operatorname{null} T + \dim(U\cap \operatorname{range}T)$

**Exercise 3B 22**: $\dim \operatorname{null}ST\le \dim\operatorname{null}S + \dim \operatorname{null} T$

**Exercise 3B 26**: $\operatorname{range}S\subset \operatorname{range}T\iff \exist E\in\mathcal L(V)(S = TE)$ (Similar result holds for null spaces, as demonstrated in Q25)

**Exercise 3B 27**: $P\in \mathcal{L}(V)$, then $P^2 = P\implies V = \operatorname{null}P + \operatorname{range}P$

### Matrices

**Def. 3.29**: Definition of matrices omitted. Let $A_{j,k}$ denote the entry in the row $j$, column $k$ of $A$.

**Def. 3.31**: Suppose $T\in \mathcal{L}(V, W)$ and $v_1, \dots, v_n$ is a basis of $V$, $w_1, \dots, w_m$ a basis of $W$. The matrix of $T$ with respect to these bases is the $m-$by$-n$ matrix $\mathcal M(T)$ whose entries are defined by
$$
Tv_k = A_{1, k}w_1 + \cdots + A_{m,k}w_m
$$
Use notation $\mathcal{M}(T, v_1,\dots, v_n, w_1, \dots, w_m)$ when bases in not clear from the context.

> How do this definition make sense?
