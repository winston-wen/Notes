## Part 1. Order of a quadratic field

An integer $d$ is ==square-free== iff the prime factorization has exactly one factor for each prime. Formally, $d=p_1p_2\cdots p_k$ where the $p_i$s are distinct primes.

An ==algebraic number== is a (complex) root of a non-zero polynomial (over one-variable, of finite degree) with integer (or equivalently, rational) coefficients.

* The root can be real or complex.
* The coefficients are rational numbers.
* The coefficients become integers after multiplying the least common multiple of denominators. 通分.

An ==algebraic integer== is a (complex) root of a polynomial with integer coefficients, and the leading coefficient is 1.

The ==minimal polynomial of an algebraic number== $a$ is the unique, monic, irreducible (over the rationals) polynomial of smallest degree $p(x)$ with rational coefficients such that $p(a)=0$.

* $p(x)\in\mathbb{Q}(x)$, with 1 as the leading coefficient.

By construction, the ==minimal polynomial of $a+b\sqrt{d}$== is
$$
\begin{align}
p(x)&=(x-(a+b\sqrt{d}))(x-(a-b\sqrt{d})) \\
&=x^2-2ax+a^2-b^2d
\end{align}
$$
A ==quadratic **field**== $F$ is a field extension of $\mathbb{Q}$ of dimension/rank 2 as a vector space over $\mathbb{Q}$. That is,
$$
F = \mathbb{Q}(\sqrt{d})=\left\{a+b\sqrt{d}: \forall a,b\in\mathbb{Q}\right\} ~~.
$$
To construct "meaningful" (nontrivial, and unique up to simplest square root) extensions over $\mathbb{Q}$, we ==usually require that $d$ is square-free==. Counter-examples:

* trivial: $\mathbb{Q}(\sqrt 4)=\mathbb{Q}$
* duplicate: $\mathbb{Q}(\sqrt{108})=\mathbb{Q}(\sqrt{3})$

==The algebraic integers of $F= \mathbb{Q}(\sqrt{d})$== is the totality of elements of the form $a+b\sqrt{d}$ s.t. $p(x)$ has integral coefficients.

Let $\mathcal{O}_F$ be the set of all algebraic integers of $F$, then
$$
\mathcal{O}_F = \begin{cases}
\mathbb{Z}\left[\dfrac{1+\sqrt{d}}{2}\right] & d\equiv 1~(\mathrm{mod}~4) \\
\mathbb{Z}\left[\sqrt{d}\right] & d\equiv 2,3~(\mathrm{mod}~4) ~~.
\end{cases}
$$
Note that the case $d\equiv 0~(\mathrm{mod}~4)$ is impossible, since $d$ is square-free.

**Question:** Why $\mathbb{Z}\left[\sqrt{d}\right]$ cannot exhaust $\mathcal{O}_F$ for any $d$ ?

**Explanation:**

To make $a+b\sqrt{d}~~(a,b\in \mathbb{Q})$ an algebraic integer, we need to make both $2a$ and $a^2-db^2$ as integers. Note that $a, b$ are rational numbers. Thus we need to discuss the possible patterns of $a, b$. Let $h,j,m,n,p,q$ be integers.

(Case 1) If $a=h$, then either $b=p/q$ or $b=p$.

(Case 1.1) If $b=p/q$, then $db^2=d\frac{p^2}{q^2}$, where $\gcd(p,q)=1$. As $db^2$ is integer, we have $q^2\mid d$, which contradicts with $d$ being square-free.

(Case 1.2) If $b=p$, then $a^2-db^2$ is integer for any $d$.

(Case 2) If $a=h+\frac{1}{2}$. Let $b=p/q$ where $\gcd(p,q)=1$, then $a^2-db^2=h^2+h+\frac{1}{4}-\frac{dr^2}{s^2}$.

(Case 2.1) If $s=1$, then it contradicts with $\frac{1}{4}-\frac{dr^2}{s^2}$ being integer.

(Case 2.2) If $s=2$. Let $r=2j+1$, then $\frac{1}{4}-\frac{dr^2}{s^2}=\frac{1}{4}-\frac{d(4j^2+4j+1)}{4}$. The only possible $d$ is $d\equiv 1~(\mathrm{mod}~4)$.

(Case 2.3) For any other $s$, assume $s=p_1^{r_1}p_2^{r_2}\cdots p_S^{r_S}$ and $d=q_1q_2\cdots q_D$. If there exist some $q$-s that are identical to some $p$-s, then in the denominator of the simplified $\frac{d}{s^2}$, these identical prime factors are raised to powers of odd numbers. Thus the denominator cannot be 4, which contradicts with $\frac{1}{4}-\frac{dr^2}{s^2}$ being integer.

From the above discussion, we have

* If $d\equiv 1~(\mathrm{mod}~4)$, then $(a, b)$ can be ==pairs of either integers or half-integers==. Such $a+b\sqrt{d}$ can be expressed by a $\mathbb{Z}$-module of basis $\left\{1, \frac{1+\sqrt{d}}{2} \right\}$.
* Otherwise, $a, b$ can be integers. Such $a+b\sqrt{d}$ can be expressed by a $\mathbb{Z}$-module of basis $\left\{1, \sqrt{d} \right\}$.

$\mathcal{O}_F$ is a subring of $F$, which is called the ==maximal order== of $F$. Any subring $\mathcal{O}$ of $\mathcal{O}_F$ containing 1 and being a free $\mathbb{Z}$-module of rank 2 is called an ==order== of $F$.

## Part 2. Class group of a quadratic field

An ==ideal== is an additive subgroup $\mathfrak{I}$ (Fraktur font of "I") of a ring $\mathcal{R}$ satisfying the "multiplicative trap" property, that is, 
$$
xy\in \mathfrak{I}~\mathrm{and}~yx\in \mathfrak{I}~~\forall x\in\mathcal{R},y\in\mathfrak{I}~.
$$

> Key words: additive subgroup, multiplicative trap.

The addition of two ideals $\mathfrak{a},\mathfrak{b}$ is defined by
$$
\mathfrak{a}+\mathfrak{b} = 
\left\{
a+b
~|~
a\in\mathfrak{a},b\in \mathfrak{b}
\right\} ~.
$$
The multiplication of two ideals is defined by
$$
\mathfrak{a}\mathfrak{b} = 
\left\{
\sum_{i=1}^n a_i b_i
~|~
a_i\in\mathfrak{a},b_i\in \mathfrak{b},n\ge 1
\right\} ~.
$$
