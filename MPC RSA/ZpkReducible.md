定理. 首一多项式 $$f(x)\in \Z[x]$$ 在 $$\Z_p$$ 中可约, 当且仅当其在 $$\Z_{p^k}$$ 中可约. 这里 $$p$$ 是质数.

证明: ($$\Leftarrow$$) 设 $$f(x)\equiv g(x)h(x) \pmod {p^k}$$, 其中 $$\deg g, \deg h \ge 1$$ 且 $$\deg f = \deg g + \deg h$$. 将该式模 $$p$$ 得
$$
f(x)\equiv \bar{g}(x) \bar{h}(x) \pmod p.
$$
($$\Rightarrow$$) 设 $$f(x)\equiv g(x)h(x) \pmod p$$. 设 $$g(x)$$ 度数为 $$n$$, $$h(x)$$ 度数为 $$m$$. 我们关注 $$f,g,h$$ 的系数. 设
$$
\boldsymbol{r}=\left[a_0,\cdots,a_{n-1},b_0,\cdots,b_{m-1}\right].
$$
设函数 $$\phi(\boldsymbol{r}): \Z^{n+m}\to\Z^{n+m}$$ 为如下多项式的系数向量. 注意 $$f,g,h$$ 都是首一多项式, 因此如下多项式第 $$m+n$$ 次项的系数为 0.
$$
\left(x^n+\sum_{i=0}^{n-1} a_ix^i\right)\left(x^m+\sum_{j=0}^{m-1} b_jx^j\right)-f(x).
$$
则 $$f(x)\equiv g(x)h(x) \pmod p$$ 可以表示为 $$\phi(\boldsymbol{gh})\equiv 0\pmod p$$. 这里向量 $$\boldsymbol{g}$$ 是多项式 $$g$$ 的系数向量, 向量 $$\boldsymbol{h}$$ 同理; 向量 $$\boldsymbol{gh}$$ 是两个向量的拼接.

$$f(x)\equiv g(x)h(x) \pmod p$$ 是一种分解, 因此 $$\gcd{(g(x), h(x))}=1$$, 这意味着 Jacobian 矩阵 $$\mathbf{J}_\phi(\boldsymbol{gh})$$ 是模 $$p$$ 可逆的. 因此可以递归地应用 "多元 Hensel 定理", 将 $$\phi(\boldsymbol{gh})\equiv 0\pmod p$$ 更新为 $$\phi(\boldsymbol{\hat{g}\hat{h}})\equiv 0\pmod{p^k}$$. 🟩

