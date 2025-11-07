## 回顾

给定随机整数 $$p,q$$ 满足 $$p\equiv q\equiv 3\pmod 4$$. 令 $$n=pq$$. 如下步骤能够随机但无偏地判断 $$p,q$$ 是否为不同的质数.

Step 1. 随机挑选 $$g\in\Z_n^*$$, 满足 $$(g|n)=1$$. 检查以下条件, 若为真则继续.
$$
g^\frac{n-p-q+1}{4}\equiv \pm 1\pmod n. \label{s1}\tag{s1}
$$
Step 2. 随机挑选一阶多项式 $$ax+b\in K$$. 群 $$K$$ 定义为:
$$
K=\left(\Z_n\left[x\right]/\left(x^2+1\right)\right)^*/\Z_n^*.
$$
也就是说, $$a,b\in\Z_n$$, $$\gcd{(a^2+b^2,n)}=1$$. 计算下式,
$$
(Ax+B)=(ax+b)^{(p+1)(q+1)}.
$$
检查以下条件, 若为真, 则 $$p,q$$ 皆为质数.
$$
A\equiv0~(\mathrm{mod}~n)\;\land\; \gcd{(b,n)}=1.
$$
## 分布式半质数测定

基于上一节所回顾的判定方法, 我们不难得到 $$m$$ 方半质数测定算法.

Round 1: 各方分别生成 $$p_i, q_i$$. 其中, $$p_1,q_1\equiv 3\pmod 4$$, 其余 $$p_i,q_i\equiv 0\pmod 4$$. 这些参与方以 Paillier MtA 算法, 计算
$$
n=\left(\sum_{i=1}^m p_i\right)\left(\sum_{j=1}^m q_j\right).
$$
Round 2: 这些参与方协商出一个 $$g\in \Z_n^*$$, 也就是 $$\gcd{(g,n)}=1$$.

Round 3: 第1方计算 $$v_1=g^{(n-p_1-q_1+1)/4}$$. 其他方计算 $$v_i=g^{(p_i+q_i)/4}$$. 各方分享 $$v_i$$.

Round 4: 各方计算 $$v=\prod{v_i}$$. 至此, 公式 $$\eqref{s1}$$ 得以重构为安全的形式. 执行上一节的判定方法, 完成分布式半质数测定.

💡 Round 3 中的分享是安全的, 因为破解的难度是整数的离散对数. 对比一下, 直接公开指数是不安全的. 如果检测通过, 各方就得到如下方程组, 进而得到 $$n$$ 的分解.
$$
\begin{align}
pq&=n, \\
(p-1)(q-1)&=\varphi(n).
\end{align}
$$
