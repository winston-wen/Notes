定义 Euler-phi 函数 $\varphi(n)$ 为小于 $n$ 且与 $n$ 互质的正整数的个数; 另外, $\varphi(0) = \varphi(1) = 1$. 设 $n$ 的质因数分解为
$$
n=p_1^{m_1}p_2^{m_2}\cdots p_k^{m_k}
$$
证明:
$$
\varphi(n)=n\left(1-\frac{1}{p_1}\right)\left(1-\frac{1}{p_2}\right)\cdots\left(1-\frac{1}{p_k}\right)
$$
方法1: 容斥定理. 详见: https://math.stackexchange.com/a/1734686

方法2: 

先证明当 $p, q$ 互质时, 有
$$
\varphi(pq)=\varphi(p)\varphi(q)
$$
再证明对于质数 $p$, 有
$$
\varphi(p^k)=p^k-p^{k-1}=p^k\left(1-\frac{1}{p}\right)
$$
将以上两式用于 $n$ 的质因数分解形式, 即得到待证明的式子.