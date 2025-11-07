## Paillier Keygen

定义. Carmichael 函数. 对任意 $$a\in \Z_n^*$$, 满足 $$a^{\lambda{(n)}}\equiv 1\pmod n$$ .

Step 1 : 随机选择大质数 $$p, q$$, 满足 $$pq$$ 与 $$(p-1)(q-1)$$ 互质. 计算 $$n=pq$$, $$\lambda=\lambda(n)=\mathrm{lcm}{(p-1, q-1)}$$.

Step 2 : 随机选择 $$g\in\Z_n^*$$. 由 $$g^\lambda\equiv 1\pmod n$$, 可知存在 $$\lambda_0\in \Z_n$$, 使得 $$g^\lambda\equiv 1+\lambda_0 n \pmod{n^2}$$ (提示: 二项式定理). 检查确保 $$\gcd{(\lambda_0,n)}\equiv 1\pmod n$$, 也就是 $$\lambda_0$$ 模 $$n$$ 可逆.

💡1 : 为了计算方便, 我们通常选择 $$g=n+1$$. 此时 $$\lambda_0=\lambda$$.

💡2 : 如果

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
\right\rfloor \cdot \lambda_0^{-1}  \pmod{n^2}.
$$
解密推导:
$$
\begin{align}
c^\lambda &\equiv g^{\lambda m}\cdot r^{\lambda n} \pmod{n^2} \\
&\equiv (1+\lambda_0n)^m \cdot (1+un)^n \pmod{n^2} \\
\textrm{(binomial theorem)} &\equiv (1+m\lambda_0n)\cdot(1+nun) \pmod{n^2} \\
&\equiv 1+m\lambda_0n \pmod{n^2}.
\end{align}
$$


## Paillier Homomorphism

设明文 $$m_1, m_2\in \Z_n$$, 临时密钥 $$r_1, r_2 \in \Z_n^*$$. 设函数 $$C(m;r)=g^{m}\cdot r^n \bmod{n^2}$$. 设 $$c_i=C(m_i;~r_i)$$.

(1) $$c_1c_2=C(m_1+m_2;~r_1r_2)$$.

(2) $$c_1g^{m_2}=C(m_1+m_2;~r_1)$$.

(3) $$c_1^{m_2}=C(m_1m_2;~r_1^{m_2})$$.

