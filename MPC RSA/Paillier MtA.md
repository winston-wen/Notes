## Paillier Keygen

定义. Carmichael 函数. 对任意 $$a\in \Z_n^*$$, 满足 $$a^{\lambda{(n)}}\equiv 1\pmod n$$ .

Step 1 : 随机选择大质数 $$p, q$$, 满足 $$pq$$ 与 $$(p-1)(q-1)$$ 互质. 计算 $$n=pq$$, $$\lambda=\lambda(n)=\mathrm{lcm}{(p-1, q-1)}$$.

Step 2 : 随机选择 $$g\in\Z_n^*$$. 由 $$g^\lambda\equiv 1\pmod n$$, 可知存在 $$\lambda_0\in \Z_n$$, 使得 $$g^\lambda\equiv 1+\lambda_0 n \pmod{n^2}$$ (提示: 二项式定理). 检查确保 $$\lambda_0\in\Z_n^*$$.

💡1 : $$\left<g\right>$$ 的阶为 $$\lambda$$. 这意味着同态运算如果累积到 $$\lambda$$, 则会被截断.

💡2 : 为了计算方便, 我们通常选择 $$g=n+1$$. 此时 $$\lambda_0=\lambda$$.

💡3 : 如果 $$\lambda_0\not\in\Z_n^*$$, 那么明文空间将大为缩小.

至此, 得到公钥 $$(n, g)$$, 私钥 $$(p, q)$$.



## Paillier Enc/Decryption

设明文 $$m\in \Z_n$$. 随机选择 $$r\in \Z_n^*$$. 定义密文 $$c$$ 为
$$
c\equiv g^m\cdot r^n\pmod{n^2}.
$$
解密公式为
$$
m\equiv\left\lfloor
\frac{\left(c^\lambda\bmod n^2\right)-1}{n}
\right\rfloor \cdot \lambda_0^{-1}  \pmod{n}.
$$
解密推导:
$$
\begin{align}
c^\lambda &\equiv g^{\lambda m}\cdot r^{\lambda n} \pmod{n^2} \\
&\equiv (1+\lambda_0n)^m \cdot (1+un)^n \pmod{n^2} \\
&\textrm{apply binomial theorem:} \\
&\equiv (1+m\lambda_0n)\cdot(1+nun) \pmod{n^2} \\
&\equiv 1+m\lambda_0n \pmod{n^2}.
\end{align}
$$



## Paillier Homomorphism

设明文 $$m_1, m_2\in \Z_n$$, 临时密钥 $$r_1, r_2 \in \Z_n^*$$. 设函数 $$C(m;r)=g^{m}\cdot r^n \bmod{n^2}$$. 设 $$c_i=C(m_i;~r_i)$$.

(1) $$c_1c_2=C(m_1+m_2;~r_1r_2)$$.

(2) $$c_1g^{m_2}=C(m_1+m_2;~r_1)$$.

(3) $$c_1^{m_2}=C(m_1m_2;~r_1^{m_2})$$.



## Paillier MtA

$$m$$ 个参与方编号为 1 到 $$m$$. 第 $$i$$ 参与方的流程如下.

Step 1 : 生成 Paillier 私钥. 生成随机 $$p_i, q_i$$. 计算 Paillier 密文 $$[p_i]$$. 对每个 $$j\neq i$$, 生成随机 $$b_{i,j}$$. 交换 $$[p_i]$$ 和 Paillier 公钥.

Step 2 : 构造等式关系 $$\eqref{mta}$$. 这实际上是计算 $$\eqref{aij}$$. 交换 $$[a_{i,j}]$$.
$$
[a_{i,j}+b_{i,j}]=[p_j\cdot q_i].
\label{mta}\tag{mta}
$$

$$
[a_{i,j}]:=[p_j]\otimes q_i ~\ominus~b_{i,j}.
\tag{aij}\label{aij}
$$

Step 3 : 解密 $$[a_{j,i}]$$. 计算 $$\eqref{ni}$$. 交换 $$n_i$$.
$$
n_i:=p_iq_i+\sum_{j\ne i}(a_{j,i}+b_{i,j}).
\label{ni}\tag{ni}
$$
Step 4 : 计算 $$n:=\sum_k n_k$$. 各方得到相同的 $$n$$.

