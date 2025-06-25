# 1. Pairing

Intro 1: Pairing **is a primitive** behind various constructions, including deterministic threshold signatures, ZK-SNARKs, and some other simpler forms of ZK proofs.

Intro 2: Elliptic curve pairing introduces a form of **encrypted multiplication**, which greatly expands what elliptic curve based protocols can do.

**Pairing allows DDH.** Decisional Diffie Hellman (DDH) problem: assume $P=pG, Q=qG, R=rG$; if $P, Q, R$ is known, check whether or not $pq=r$. 

**Pairing doesn't allow CDH.** Computational Diffie Hellman (CDH) problem: assume $P=pG, Q=qG$; if $P, Q$ is known, compute $R$ such that $R=pqG$.

Elliptic curves allow checking linear constraints. For example,
$$
ap+bq=cr\hspace{1em}\Leftrightarrow\hspace{1em}aP+bQ=cR.
$$
**Pairing allows checking quadratic constraints.** For example,
$$
pq+r=0\hspace{1em}\Leftrightarrow\hspace{1em}e(P,Q)\cdot e(G,R)=1.
$$
**Pairing is bilinear**, which means
$$
e(P,Q+R)=e(P,Q)\cdot e(P,R)\\
e(P+Q,R)=e(P,R)\cdot e(Q,R)\\
$$
An example of a toy pairing: $e(x,y)=2^{xy}$. Not suitable for cryptography.

An example of elliptic curve pairing can be a map $C_1\times C_2 \leftarrow C_t$, where:

* $C_1$ is an elliptic of the form $y^2=x^3+b$, where $x,y\in\mathbb{F}_p$.
* $C_2$ is an elliptic of the form $y^2=x^3+b$, where $x,y\in(\mathbb{F}_p)^{12}$.
* $C_t$ is the resulting elliptic curve. Its coordinates are elements of $(\mathbb{F}_p)^{12}$.

Recall that:

*  $\mathrm{ord}(<\mathbb{F}_p,\times>)=p-1$.
*  $\mathrm{ord}(<(\mathbb{F}_p)^{12},\times>)=p^{12}-1$. TODO: Why?

**Pairing is invertible.** Notice that $e(P,Q)$ belongs to a multiplicative group, and for (almost) any element, there exists $e^{-1}(P,Q)$.

**The embedding degree** $k$: The above number 12 is chosen as the embedding degree. Every elliptic curve has a value called embedding degree; essentially, the smallest $k$ such that $p^k-1$ is the multiple of $n$, where $n$ is the curve order.

* Too small $k$ makes DL problem much easier to crack.
* Too large $k$ makes pairings infeasible to compute.

A useful pairing should not degenerate. E.g. one could just define $e(P,Q)=1$, but it's useless.

TODO: How pairing is done?

# 2. Quadratic Arithmetic Program (QAP)

```
https://medium.com/@VitalikButerin/quadratic-arithmetic-programs-from-zero-to-hero-f6d558cea649
```

**Intuition.** ZK-SNARKs cannot be applied to any computational problem directly. Rather, one has to convert the problem into a QAP form.

## 2.1. Step 1: Flattening

Convert the original code into a finite, determined sequence of statements that are of two forms:

* Assignment: `x = y` where `y` can be a variable or a number.
* Op Assignment: `x = y (op) z` where `op` can be `+, -, *, /`, and `y, z` can be variables, numbers., or finite expressions.

## 2.2. Step 2: R1CS

A rank-1 constraint system (R1CS) represents a set of constraints in the form:
$$
(\boldsymbol{a}_i\cdot \boldsymbol{w})
\cdot(\boldsymbol{b}_i\cdot \boldsymbol{w})
=(\boldsymbol{c}_i\cdot \boldsymbol{w})\qquad
\forall i\in\left\{1,\dots,m\right\}.
$$
Here, 

(1) The bold symbols are vectors, and the "dot product" between vectors is their inner product, which is the sum of element-wise product.

(2) The vector $\boldsymbol{x}$ is the assignment to symbols. It is also called the "witness". Its length is denoted as $n$.

(3) The subscript $i$ represents the $i$-th constraint. Its upper boundary $m$ is certainly the number of constraints/gates .

Example:

```
Symbols: [1, x, out, u1, y, u2]
Witness: [1, 3, 35, 9, 27, 30]
Gate1: x * x == u1
	a: [0, 1, 0, 0, 0, 0]
	b: [0, 1, 0, 0, 0, 0]
	c: [0, 0, 0, 1, 0, 0]
Gate2: u1 * x == y
	a: [0, 0, 0, 1, 0, 0]
	b: [0, 1, 0, 0, 0, 0]
	c: [0, 0, 0, 0, 1, 0]
Gate3: x + y == u2
	a: [0, 1, 0, 0, 1, 0]
	b: [1, 0, 0, 0, 0, 0]
	c: [0, 0, 0, 0, 0, 1]
Gate4: u2 + 5 == out
	a: [5, 0, 0, 0, 0, 1]
	b: [1, 0, 0, 0, 0, 0]
	c: [0, 0, 1, 0, 0, 0]
```

## 2.3. Step 3: R1CS to QAP

QAP is short for quadratic arithmetic program.

Polynomial of matrix $\boldsymbol{A}$ and the $k$-th symbol:
$$
A_k(x)=\Lambda\Big(
(x_1, a_{1,k}),~(x_2,a_{2,k}),~\dots,~(x_m,a_{m,k})\Big),
$$
where 

* $\Lambda$ is Lagrange interpolation; and,
* $m$ is the number of R1CS gates/constraints.
* $a_{i,k}$ is the $k$-th element of $\boldsymbol{a}_i$.
* $x_1,\dots,x_m$ are distinct numbers chosen at will. 

💡 Usually, we choose $t_i=i$ 💡

Similarly, we have polynomials $B_k(x)$ and $C_k(x)$ for matrices $\boldsymbol{B}$ and $\boldsymbol{C}$. There are a total of $3n$ polynomials as such.

Next, we compute polynomials $A(x)$, $B(x)$, $C(x)$ and $Z(x)$.

## 2.4. Step 4: Validation of QAP

The polynomial $A(x)$ is the sum of $A_k(x)$ weighted by $\boldsymbol{w}$. i.e.,
$$
A(x)=\sum_{k=1}^m A_k(x)w_k.
$$
Here, $w_k$ is the $k$-th element of $\boldsymbol{w}$. We compute $B(x)$ and $C(x)$ in similar way.

The R1CS constraints hold if and only if the polynomial
$$
L(x)=A(x)B(x)-C(x)
$$
have zeroes at $x\in\left\{x_1,\dots,x_m\right\}$. The reasoning is omitted here.

Subsequently, $L(x)$ must have a **factor** of
$$
Z(x)=\prod_{i=1}^m (x-x_i),
$$
which is the minimal polynomial have zeroes at $x\in\left\{x_1,\dots,x_m\right\}$.

Now, if $Z(x)$ divides $A(x)B(x)-C(x)$, the validation passes.

# 3. Walkthrough ZK-SNARK

```
https://vitalik.eth.limo/general/2017/02/01/zk_snarks.html
```

## 3.1. KEA1

KEA1 is short for Knowledge of Exponents Assumption 1. 

KEA1: for any adversary $A$ that take input $g, g^x$ and returns $h_1, h_2$ with $h_2=h_1^x$, there exists an extractor $E$ which gives the same inputs as $A$ and returns $y$ such that $h_1=g^y$.

💡 Note that the adversary $A$ has no explicit knowledge to $x$.

💡 In the context of zero-knowledge proofs, ==an extractor is a theoretical algorithm that formalizes the knowledge of a secret.== In the specific context of KEA1, if the extractor doesn't exist, the adversary could pretend to generate valid outputs without actually knowing $y$.

If we apply KEA1 on elliptic curve points, it roughly states that: 
to generate a pair of points $(U, V=U^x)$ given $(P,Q=P^x)$ and $x$ is not accessible; the only way is to compute $(yP, yQ)$ where $y$ is personally known.

 ## 3.2. Trusted Setup

Where does the concept "trusted setup" come from?

Given any specific finite set of $P_1, \dots,P_n$ that one might want to check linear combinations for, one cannot actually create the accompanying points $Q_1,\dots, Q_n$ without knowing the scale factor $x$. Otherwise, one knows the $x$, then one can create $(P, Q=P^x)$ for whatever $P$ one wants, without bothering to create a linear combination. Thus whoever created $P_1,\dots,P_n$ and $Q_1, \cdots,Q_n$ is trustworthy.

💡 Note that thanks to elliptic curve pairings, checking the **existence** of $x$ such that $Q=P^x$ does not require knowing $x$ -- instead, one can simply check
$$
e(P, V) = e(Q,U).
$$
For ZK-SNARKS, the trusted setup consists of

* $t^jG$ for $j\in{0,\dots,n-1}$.
* $k_aG, k_bG, k_cG$.

Here $t, k_a, k_b, k_c$ are kept secret and ephemeral.

⚠️ If we insist on no-interaction, then the ephemeral values should be generated by another party called the "trusted setup generated", neither by the prover nor by the verifier. 

⚠️ If we allow a few interactions, however, then the verifier is responsible for generating the ephemerals, and sending "public version" of ephemerals (and its powers) to the prover. This requires the verifier to be honest. To ensure honesty of verifier, we can (1) require Pedersen commitments of ephemerals, (2) or, generate the ephemerals by MPC.

The prover gives:
$$
\begin{align}
&\pi_a=A(t)G ,\qquad \pi'_a=k_a\pi_a \\
&\pi_b=B(t)G ,\qquad \pi'_b=k_b\pi_b \\
&\pi_c=C(t)G ,\qquad \pi'_c=k_c\pi_c \\
&\pi_h=\frac{A(t)B(t)-C(t)}{Z(t)}G.\\
\end{align}
$$
💡 Note that the prover has no access to $k_a, k_b, k_c$. Therefore, the only way for the prover to compute $\pi_a', \pi_b', \pi_c'$ is to "know" $A(t), B(t), C(t)$.

The verifier checks:
$$
\frac{e(\pi_a,\pi_b)}{e(\pi_c,G)}=e(\pi_h,Z(t)G).
$$

# 4. ZK-SNARK Applications

```
https://vitalik.eth.limo/general/2022/06/15/using_snarks.html
```

