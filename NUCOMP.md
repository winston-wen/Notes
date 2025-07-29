[Cohen1993, Lemma 5.4.5] Let $$I_1=a_1\Z+\frac{-b_1+\sqrt{\Delta}}{2}\Z$$ be an ideal of $$\mathcal{O}_\Delta$$, and let $$I_2$$ be a similar ideal. Set $$s=(b_1+b_2)/2$$, $$n=(b_1-b_2)/2$$, $$d=\mathrm{gcd}(a_1, a_2, s)$$, and let $$u, v, w$$ be integers such that $$ua_1+va_2+ws=d$$. Then we have
$$
I_1\cdot I_2=d\left(A\Z+\frac{-B+\sqrt{\Delta}}{2}\right),
$$
where
$$
A=d_0\frac{a_1a_2}{d^2},\;
B=b_2+\frac{2a_2}{d}\left(v(s-b_2)-wc_2\right).
$$
In general, $$d_0=\mathrm{gcd}(a_1, a_2, s, c_1, c_2, n)$$. If at least one of the form $$(a_1, b_1, c_1)$$ or $$(a_2, b_2, c_2)$$ is primitive, then $$d_0=1$$.

<u>Proof.</u> The ideal $$I_3=I_1\cdot I_2$$ is generated as a $$\Z$$-module by the four products of the generators of $$I_1$$ and $$I_2$$. To be more specific, the four generators of $$I_3$$ are
$$
\begin{align}
g_1&=a_1a_2,\\
g_2&=-a_1b_2/2+(a_1/2)\sqrt{\Delta},\\
g_3&=-a_2b_1/2+(a_2/2)\sqrt{\Delta},\\
g_4&=(b_1b_2+\Delta)/4-(s/2)\sqrt{\Delta}.
\end{align}\label{gen}\tag{gen}
$$
Now by Proposition 5.2.1 we know that we can write
$$
I_3=C\left(A\Z+\frac{-B+\sqrt{\Delta}}{2}\right)
$$
for some integers $$A, B$$ and $$C$$. It is clear that $$C$$ is the smallest positive coefficient of $$\sqrt{\Delta}/2$$ in $$\eqref{gen}$$. So $$C=\mathrm{gcd}(a_1,a_2,s)$$ as stated.

Now we determine the value of $$AC$$, which is the least positive integer belonging to $$I_3$$. Any element of $$I_3$$ is of the form $$x=x_1g_1+x_2g_2+x_3g_3+x_4g_4$$ for integer $$x_i$$-s. The set $$I_3\cap \Z$$ is the set of such element with $$x_2a_1+x_3a_2-x_4s=0$$.

Using [Cohen1993, Exercise 5.11], the general solution to this equation is
$$
\begin{align}
x_1 &= \lambda_4,\\
x_2 &= \lambda_3\frac{a_2}{\gcd(a_1, a_2)}-\lambda_2\frac{-s}{\gcd(a_1,s)},\\
x_3 &= \lambda_1\frac{-s}{\gcd(a_2,s)}-\lambda_3\frac{a_1}{\gcd(a_1,a_2)},\\
x_4 &= \lambda_2\frac{a_1}{\gcd(a_1,s)}-\lambda_1\frac{a_2}{\gcd(a_2,s)}.
\end{align} \tag{xs}\label{xs}
$$
for arbitrary integers $$\lambda_i$$.

(笔记1) 方程 $$u_2a_1+u_3a_2-u_4s=0$$ 的意思是 "令 $$\sqrt{\Delta}$$ 项的系数为0". 这在逻辑上是 $$I_3$$ 中的元素为整数的必要条件. 还需排除元素的有理部分为半整数的情况. 有理部分表示为
$$
R_x=(a_1a_2)x_1+(-a_1b_2/2)x_2+(-a_2b_1/2)x_3
+\left(\left(b_1b_2+\Delta\right)/4\right)x_4. \tag{cal}\label{cal}
$$
根据 $$\Delta=b^2-4ac$$ 可知 $$\Delta$$ 与 $$b$$ 奇偶性相同. 当 $$\Delta\equiv 0\pmod 4$$  时, $$b_1, b_2$$ 都是偶数, 表达式 $$\eqref{cal}$$ 的结果是整数. 还需考察 $$\Delta\equiv 1 \pmod 4$$ 的情况. (笔记1结束)

After a short calculation, we see that $$I_3\cap \Z=e\Z$$ where
$$
\begin{align}
t &=\gcd\left(
\frac{a_1a_2c_1}{\gcd(a_2,s)},
\frac{a_1a_2c_2}{\gcd(a_1,s)},
\frac{a_1a_2n}{\gcd(a_1,a_2)},
a_1a_2 \right) \\
&=\frac{a_1a_2}{\gcd(a_1, a_2, s)}
\gcd(a_1, a_2,s,c_1,c_2,n).
\end{align}
\tag{stride}\label{stride}
$$
This gives the claimed value $$A=d_0\frac{a_1a_2}{d^2}$$.

(笔记2) 这short calculation都算了什么? 首先将 $$\eqref{xs}$$ 代入 $$\eqref{cal}$$, 得到
$$
\begin{align}
R_x &=\frac{a_1a_2c_1}{\gcd(a_2,s)}\lambda_1-\frac{a_1a_2c_2}{\gcd(a_1,s)}\lambda_2+\frac{a_1a_2n}{\gcd(a_1,a_2)}\lambda_3 + a_1a_2\lambda_4.
\end{align} \tag{x.r}\label{x.r}
$$
显然, 相加的各项都是整数, 因此 $$R_x$$ 也是整数. 根据理想的定义(加法群, 乘法封闭), 两个理想的交集是这两个理想的理想. 所以交集一定是 $$t\Z$$ 的形式. 因此, 无论自由整数 $$\lambda_i$$ 取何值, $$R_x$$ 都将呈现出周期性, 周期为 $$\lambda_i$$ 的各系数的GCD. 公式$$\eqref{stride}$$ 就是这么来的. (笔记2结束)

(笔记3) 公式 $$\eqref{x.r}$$ 中, $$\lambda_i$$ 的各系数是怎么算的?

$$\lambda_4$$ 的系数是显然的, 这里略过.

$$\lambda_3$$ 的系数的来历如下.
$$
a_1a_2n=-a_2a_1b_2/2+a_1a_2b_1/2.
$$
$$\lambda_2$$ 的系数的来历如下.
$$
\begin{align}
-a_1a_2c_2
&=-a_1b_2s/2+a_1(b_1b_2+\Delta)/4 \\
&=a_1(-b_1b_2-b_2^2+b_1b_2+\Delta)/4 \\
&=a_1(-b_1b_2-b_2^2+b_1b_2+b_2^2-4a_2c_2)/4.
\end{align}
$$
类似地, $$\lambda_1$$ 的系数的来历如下.
$$
\begin{align}
a_1a_2c_1
&= a_2b_1s/2-a_2(b_1b_2+\Delta)/4 \\
&=a_2(b_1b_2+b_1^2-b_1b_2-b_1^2+4a_1c_1)/4.
\end{align}
$$
(笔记3结束)

Finally, if $$d=ua_1+va_2+ws$$, one possible value of B is clearly
$$
\begin{align}
B
&= \frac{ua_1b_2+va_2b+1+w(b_1b_2+\Delta)/2}{d} \\
&= \frac{db_2+va_2(b_1-b_2)-2a_2c_2w}{d},
\end{align}
$$
thus proving the lemma. 🟩

[Cohen1993, Algorithm 5.4.9] (NUCOMP) Given two quadratic forms $$f_1=(a_1,b_1,c_1)$$ and $$f_2=(a_2,b_2,c_2)$$, which are primitive positive definite with the same discriminant. This algorithm computes the **composite** $$f_3=(a_3, b_3, c_3)$$ of $$f_1$$ and $$f_2$$. We assume the constant $$L=\lfloor\left(D/4\right)^{1/4}\rfloor$$ is already pre-computed.

