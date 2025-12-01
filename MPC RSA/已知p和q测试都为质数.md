原标题: Efficient Generation of Shared RSA Keys

原作者: [Dan Boneh](dabo@bellcore.com), [Matthew Franklin](franklin@research.att.com).



## Procedure 1. Semi-primality test

Assume $$p, q$$ be positive random integers with $$p\equiv q\equiv 3\pmod 4$$. Let $$n=pq$$.

Step 1. Choose $$g\in\Z_n^*$$.

Step 2. If $$(g/n)\neq 1$$, go back to Step 1.

Step 3. Check whether
$$
g^\frac{n-p-q+1}{4}\equiv \pm 1\pmod n.
$$

---

## Lemma 2.

Roughly, Procedure 1 has low false-positive and no false-negative.

Formally, if $$n$$ is a product of two distinct primes, then the above procedure always succeeds. Otherwise, the procedure fails with probability at least $$1/2$$, over the choice of $$g$$.

### Proof:

I. Suppose $$p, q$$ are primes. Now $$\varphi(n)=n-p-q+1$$. In Step 2 we verify that $$(g|N)=1$$. This implies $$(g|p)=(g|q)$$. Also, since $$(p-1)/2$$ and $$(q-1)/2$$ are odd, we have:
$$
g^{\frac{\varphi (n)}{4}}=g^{\frac{p-1}{2}\frac{q-1}{2}}
\equiv\left(\dfrac{g}{n}\right)^{\frac{q-1}{2}}
\equiv \left(\dfrac{g}{n}\right)
\pmod p.
$$
Similarly, we have:
$$
g^{\frac{\varphi (n)}{4}}\equiv \left(\dfrac{g}{n}\right) \pmod q.
$$
Since $$(g|p)=(g|q)$$ it follows that $$g^{\frac{\varphi (n)}{4}}\equiv \pm 1 \bmod n$$. (See Note 2)

So in this case, the procedure always succeeds.

II. Suppose at least one of $$p, q$$ is not prime. Assume $$n$$ have $$m$$ distinct prime factors, that is, $$n=p_1^{d_1}p_2^{d_2} \cdots p_m^{d_m}$$, where at least one $$d_i\ge 2$$. Let $$e=(n-p-q+1)/4$$. By computation, we know that $$e$$ is odd since $$p\equiv q \equiv 3 \pmod 4$$. 

Define the following two subgroups of $$\Z_n^*$$ (See Note 1). 

$$
\begin{align}
G&=\set{g\in\Z_n^* ~:~ (g|n)=1},\\
H&=\set{g\in G ~:~ g^e\equiv 1\pmod n}.
\end{align}
$$
Now $$G$$ is the set of all possible $$g$$-s at Step 2, and $$H$$ is the set of all successful $$g$$-s at Step 3. To prove Lemma 2, we show that $$\lvert H \rvert \le \frac{1}{2}\lvert G \rvert$$ (See Note 3 for hint). Since $$H$$ is a subgroup of $$G$$, it suffices to prover proper containment of $$H$$ in $$G$$, i.e. prove the existence of $$g\in G\backslash H$$. There are 4 cases to consider.

Case 1. Suppose $$m\ge 3$$, that is, $$n$$ has at lease 3 distinct prime factors. Let $$a$$ be a quadratic non-residue modulo $$p_3$$. Define $$g\in\Z_n^*$$ to be an element satisfying the following congruence system:
$$
\begin{align}
g&\equiv 1 \pmod{p_1} \\
\land ~ g&\equiv -1  \pmod{p_2} \\
\land ~ g&\equiv \begin{cases}
1 \pmod{p_3} & \mathrm{if}~(-1|p_2)=1 \\
a \pmod{p_3} & \mathrm{if}~(-1|p_2)=-1
\end{cases}  \\
\land ~ g&\equiv 1 \pmod {p_i} \mathrm{~for~} i\ge 3.
\end{align}
$$
Note that the above congruence system is always valid, which is ensured by CRM. Observe that $$g\in G$$. Since $$e$$ is odd, $$g^e\equiv g \equiv 1 \pmod{p_1}$$, and $$g^e\equiv g \equiv -1 \pmod{p_2}$$. Consequently, $$g^e\not\equiv \pm 1 \pmod{N}$$ (See Note 2 for hint), i.e. $$g\not\in H$$.

Case 2. Suppose $$\gcd(p, q)>1$$. Then there exists an odd prime $$p_1$$ which divides $$p, q$$. Then $$p_1^2$$ divides $$n$$, which implies that $$p_1$$ divides $$\varphi(n)$$ (See Note 4 for hint).

It follows that in $$\Z_n^*$$ there exists an element $$g$$ of order $$p_1$$. Since $$p_1$$ is odd, we have $$(g|n)=(g^{p_1}|n)=(1|n)=1$$, i.e. $$g\in G$$ by definition (See Note 5 for hint). Since $$r$$ divides $$p, q$$, we know that $$r$$ does not divide $$4e=n-p-q+1$$. Consequently, $$g^{4e}\not\equiv 1\pmod n$$, which implies that $$g^e \neq \pm 1 \pmod n$$. Hence $$g\not\in H$$.

Case 3. The only way $$n=pq$$ does not fall into both above cases is: if $$p=p_1^{d_1}$$ and $$q=p_2^{d_2}$$ where $$p_1, p_2$$ are distinct odd primes,  $$d_1, d_2$$ are odd positive integers (see Note 6), and at least one of $$d_1, d_2$$ is larger than 1. By symmetry, we may assume $$d_1>1$$. Since $$\Z_p^*$$ is a cyclic group of order $$\varphi(p)=p_1^{d_1-1}(p_1-1)$$, it contains an element of order $$p_1^{d_1-1}$$. It follows that $$\Z_n^*$$ also contains an element $$g$$ of order $$p_1^{d_1-1}$$. As stated in Case 2, $$(g|n)=1$$, i.e. $$g\in G$$. If $$q\not\equiv 1 \pmod{p_1^{d_1-1}}$$, then $$4e=n-p-q+1$$ is not divisible by $$p_1^{d_1-1}$$. Consequently, $$g^{4e}\not\equiv 1\pmod n$$. Hence $$g\not\in H$$.

Case 4. We are left with the case which inherits Case 3, except that $$q\equiv 1 \pmod{p_1^{d_1-1}}$$. In this case, it may happen that $$H=G$$. For example, $$p=3^t$$ and $$q=2\cdot 3^{t-1} + 1$$ such that $$t$$ is odd and $$q$$ is prime.

TODO: Calculate the following probability: □
$$
\mathrm{Pr}=\dfrac{\#\left[
\begin{align}
p=p_1^{d_1} &\land q=p_2^{d_2} \land d_1\ge 2 \\
&\land q\equiv1\pmod{p_1^{d_1-1}}
\end{align}
\right]}{\#\left[p\equiv q\equiv 3\pmod 4\right]}. 
$$

### Notes.

#### Note 1.

The set of integers $$\set{g~:~0\le g\le n-1\land\gcd(g,n)=1}$$  forms a group under multiplication modulo $$n$$. Such set is often denoted as $$\Z_n^*$$, $$\Z_n^\times$$, $$(\Z/\Z_n)^\times$$, etc.

#### Note 2.

The following lemma states that $$g\equiv s\pmod n$$, if and only if $$g\equiv s$$ w.r.t every prime factors of $$n$$.

Lemma. Assume $$n=p_1^{d_1}p_2^{d_2} \cdots p_m^{d_m}$$ is the canonical prime factorization of integer $$n$$. For any integer $$g$$ and $$s$$, we have:
$$
g\equiv s\pmod n \iff g\equiv s \pmod{p_i^{a_i}} ~\mathrm{for~any~} i.
$$
Proof: 

(if) Assume $$g\equiv s\pmod n$$. Then there exists integer $$k$$ such that $$g=kn+s$$. Then for any $$i$$, as $$p_i^{a_i}\mid kn$$, we have $$p_i^{a_i}\mid (g-s)$$. Now we proved the "if" part.

(only if) Assume $$g\equiv s\pmod {p_i^{a_i}}$$ for any $$i$$. Then for any $$i$$, there exists integer $$k_i$$ such that $$g=kp_i^{a_i}+s$$. Then $$p_i^{a_i}\mid (g-s)$$ for any $$i$$. This implies $$\mathrm{lcm}(\dots,~p_i^{a_i},~\dots)\mid (g-s)$$. Note that the "lcm" expression is indeed $$n$$. Now we proved the "only if" part. □

#### Note 3.

By Lagrange Theorem of group order.

#### Note 4.

For prime $$p$$ and positive integer $$k$$, $$\varphi(p^k)$$ $$=p^k-p^{k-1}$$. For coprime $$p, q$$, $$\varphi(pq)=\varphi(p)\varphi(q)$$.

### Note 5.

order of $$g$$ is $$p_1$$ : $$(g^{p_1}|n)=(1|n)=1$$.

kronecker symbol : $$(g^{p_1}|n) = (g|n)^{p_1}$$.

$$p_1$$ is odd : $$(g|n)=\sqrt[p_1]{(g|n)^{p_1}}$$.

#### Note 6.

If $$p^k\equiv 3 \pmod 4$$, then $$p\equiv 3\pmod 4$$ and $$k$$ is odd.

----

## Procedure 2.

This is a patch on Procedure 1.

Step 4. Let $$K$$ be a group defined as follows (See Note 1~2). When $$n=pq$$ is a semi-prime, $$K$$ contains $$(p+1)(q+1)$$ elements. In this case, we pick arbitrary $$h\in K$$ and get $$h^{(p+1)(q+1)}=1$$.
$$
K=\left(\Z_n\left[x\right]/\left(x^2+1\right)\right)^*/\Z_n^*.
$$

When $$n$$ falls into Case 4, $$K$$ contains far more than $$(p+1)(q+1)$$ elements, which causes at least half the elements in $$K$$ do not satisfy $$h^{(p+1)(q+1)}=1$$.

### Notes.

#### Note 1. Explore $$K_0$$.

$$\Z_n[x]$$ is the polynomial ring with coefficients in $$\Z_n$$.

$$(x^2+1)$$ is an ideal of $$\Z_n[x]$$ generated by element $$x^2+1$$. By definition of "ideal", we have
$$
(x^2+1)=\set{(x^2+1)\cdot p(x)\mid p(x)\in \Z_n[x]}.
$$
In other words, the ideal $$(x^2+1)$$ is composed of all polynomials with factor $$x^2+1$$.

Let $$K_0=\Z_n[x]/(x^2+1)$$ be a quotient ring. Two polynomials $$f(x), g(x)$$ are equivalent in $$K_0$$, if and only if
$$
f(x)-g(x)\in(x^2-1).
$$
We also write:
$$
f(x)\equiv g(x)\pmod{(x^2+1)}.
$$
This notation naturally introduces Euclidean Division of polynomials:
$$
f(x)=q(x)\cdot(x^2+1)+r(x).
$$
The elements of $$K_0$$ consists of all possible $$r(x)$$-s. Here every $$r(x)$$ is not only $$r(x)$$ itself, but also a "class" or an "orbit", defined by:
$$
[r(x)]=\set{r(x)+(x^2+1)q(x)\mid q(x)\in\Z_n[x]}.
$$
⚠️ $$\Z_n$$ modulo any **monic** $$t$$-degree polynomial, e.g. $$x^2$$, $$x^2+3$$, results in : 

* a **set** of all $$t-1$$ degree polynomials in $$\Z_n[x]$$. This set has $$n^2$$ elements.
* Computation between elements changes with the divisor.

Indeed, $$K_0$$ is a commutative ring with identity, whose arithmetic is defined as :

(1) Addition: addition of coefficients, i.e.
$$
[a_1x+b_1]+[a_2x+b_2]=[(a_1+a_2)x+(b_1+b_2)].
$$
Zero: $$[0+0x]=[0]$$.

(2) Multiplication: by definition, we have
$$
\begin{align}
&[a_1x+b_1]\times [a_2x+b_2]\\
&=[(a_1x+b_1)(a_2x+b_2)\bmod(x^2+1)] \\
&=[(a_1b_2+a_2b_1)x+b_1b_2-a_1a_2].
\end{align}
$$
Hint: the second step is achieved by applying $$x^2\equiv-1$$.

Unity: $$[1+0x]=[1]$$.

#### Note 2. Structure of group $$K$$.

Assume $$n=pq$$, $$p=p_1^{d_1}$$, $$q=p_2^{d_2}$$.

By CRT we have $$\Z_{pq}\cong \Z_p\times \Z_q$$; this is available as $$\gcd(p,q)=1$$. This can be promoted to $$\Z_{pq}[x]\cong \Z_p[x]\times \Z_q[x]$$. By [this lemma](./ZpkReducible.md), $$x^2+1$$ is irreducible in $$\Z_p$$ and $$\Z_q$$. Therefore,
$$
K_0\cong
\frac{\Z_p[x]}{x^2+1}\times\frac{\Z_q[x]}{x^2+1}.
$$
It follows that
$$
K_0^*\cong
\left(\frac{\Z_p[x]}{x^2+1}\right)^*
\times
\left(\frac{\Z_q[x]}{x^2+1}\right)^*.
$$
Now we study the order of $$R=\left(\frac{\Z_{r^t}[x]}{x^2+1}\right)^*$$ where $$r\equiv 3\pmod 4$$ is prime and $$t$$ is positive integer.

An element $$[ax+b]\in R$$ is invertible, if and only if there exists $$[cx+d]\in R$$, such that:
$$
(ax+b)(cx+d)\equiv 1 \pmod{(x^2+1)}.
$$
By calculation, we have the following congruence system
$$
\begin{cases}
bc+ad \equiv 0 \pmod{r^t} \\
bd-ac \equiv 1 \pmod{r^t},
\end{cases}
$$
which is also denoted as
$$
\begin{bmatrix}b&a\\-a&b\end{bmatrix}\cdot
\begin{bmatrix}c\\d\end{bmatrix}\equiv
\begin{bmatrix}0\\1\end{bmatrix}\pmod{r^t}.
$$
Now $$\det \begin{bmatrix}b&a\\-a&b\end{bmatrix}=a^2+b^2$$. The equation has unique solution if and only if $$\gcd(\det,r^t)=1$$, which is equivalent to $$\det\equiv 0 \pmod r$$.

For any element $$ax+b\in R$$, $$a,b\in\Z_r^t$$, the element is invertible if and only if $$\gcd{(a^2+b^2,r^t)}=1$$ (See Note 2). This implies $$r\not\mid(a^2+b^2)$$. By evaluating the Legendre symbol $$(-b^2)^{(r-1)/2}$$, we see that 
$$
a^2+b^2\equiv 0\pmod r
\mathrm{~iff.~}
a\equiv b \equiv 0 \pmod r.
$$
The count of such $$(a, b)$$ is $$(r^{t-1})^2$$. Hence
$$
\left| R \right| = (r^t)^2-(r^{t-1})^2.
$$
Now we go back to our main task. It follows that
$$
\begin{align}
\left|K_0^*\right|&=
\left((p_1^{d_1})^2-(p_1^{d_1-1})^2\right)
\left((p_2^{d_2})^2-(p_2^{d_2-1})^2\right).
\end{align}
$$
On the other hand,
$$
\begin{align}
\left| Z_n^* \right|&=\varphi(n)=\varphi(p_1^{d_1})\varphi(p_2^{d_2}) \\
&=(p_1^{d_1}-p_1^{d_1-1})(p_2^{d_2}-p_2^{d_2-1}).
\end{align}
$$
Therefore,
$$
\begin{align}
\lvert K \rvert 
&= \frac{\lvert K_0^*\rvert}{\lvert\Z_n^*\rvert} \\
&= (p_1^{d_1}+p_1^{d_1-1})(p_2^{d_2}+p_2^{d_2-1}) \\
&= (p+p_1^{d_1-1})(q+p_2^{d_2-1}) \\
&\ge (p+1)(q+1)
\end{align}
$$
