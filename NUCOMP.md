[Cohen1993, Lemma 5.4.5] Let $$I_1=a_1\Z+\frac{-b_1+\sqrt{\Delta}}{2}\Z$$ be an ideal of $$\mathcal{O}_\Delta$$, and let $$I_2$$ be a similar ideal. Set $$s=(b_1+b_2)/2$$, $$n=(b_1-b_2)/2$$, $$d=\mathrm{gcd}(a_1, a_2, s)$$, and let $$u, v, w$$ be integers such that $$ua_1+va_2+ws=d$$. Then we have
$$
I_1\cdot I_2=d\left(A\Z+\frac{-B+\sqrt{\Delta}}{2}\right),
$$
where
$$
A=d_0\frac{a_1a_2}{d^2},\;
B=b_2+\frac{2a_2}{d}\left(vn-wc_2\right).
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

[DMZ21Github, `fn GmpClassGroup::inner_multiply`]

第一个线性同余方程, 推导 $$\mu$$ 的解析式的过程如下.
$$
\begin{align}
\mu&=\frac{By_0}{\gcd(A,M)} \bmod M
\qquad\textrm{s.t.}\;
y_0A+y_1M=\gcd(A,M); \\

&=\frac{y_0(hu+sc_1)}{\gcd(tu, st)}  \bmod{st}
\qquad\textrm{s.t.}\;
y_0tu+y_1st=\gcd(tu,st); \\

&=\frac{y_0(hu+sc_1)}{t\gcd(u, s)} \bmod{st}
\qquad\textrm{s.t.}\;
y_0u+y_1s=\gcd(u,s); \\

&=\frac{y_0\left(\frac{hg}{w}+\frac{a_1c_1}{w}\right)}
{t\gcd\left(\frac{g}{w}, \frac{a_1}{w}\right)} \bmod{\frac{a_1a_2}{w^2}}
\qquad\textrm{s.t.}\;
y_0\frac{g}{w}+y_1\frac{a_1}{w}=\gcd\left(\frac{g}{w}, \frac{a_1}{w}\right);\\

&=\frac{y_0(hg+a_1c_1)}{t\gcd(a_1, g)}  \bmod{\frac{a_1a_2}{w^2}}
\qquad\textrm{s.t.}\;
y_0g+y_1a_1=\gcd\left(a_1, g\right).
\end{align}
$$
注意到 $$hg+a_1c_1=(b_2^2-\Delta)/4$$, 我们有
$$
\mu=\frac{y_0a_2c_2}{t\gcd(a_1,g)} \bmod{\frac{a_1a_2}{w^2}}
\qquad\textrm{s.t.}\;
y_0g+y_1a_1=\gcd\left(a_1, g\right).
$$
后面会用到 $$t\mu$$, 推导如下.
$$
\begin{align}
\mu&=\frac{y_0a_2c_2}{t\gcd(a_1,g)} +x_0\frac{a_1a_2}{w^2}, \\
t\mu &= \frac{y_0a_2c_2}{\gcd(a_1,g)}+x_0\frac{a_1}{w}, \\
&=
\end{align}
$$
此外, 根据线性方程有解的条件, 我们有 $$\gcd(a_1,g)\mid a_2c_2$$. (TODO: 为什么要让这样的方程有解?)

推导 $$v$$ 的解析式的过程如下.
$$
\begin{align}
v &= \frac{M}{\gcd(A,M)} = \frac{st}{\gcd(tu,st)}=\frac{s}{\gcd(u,s)} \\
&= \frac{\frac{a_1}{w}}{\gcd\left(\frac{g}{w}, \frac{a_1}{w}\right)} \\
&= \frac{a_1}{\gcd(a_1,g)}.
\end{align}
$$
第二个线性同余方程, 推导 $$\lambda$$ 的解析式的过程如下.
$$
\begin{align}
\lambda&=\frac{Bz_0}{\gcd(A,M)} 
\qquad\textrm{s.t.}\;
z_0A+z_1M=\gcd(A,M); \\

&=\frac{z_0(h-t\mu)}{\gcd(tv,s)}
\qquad\textrm{s.t.}\;
z_0tv+z_1s=\gcd(tv,s); \\
\end{align}
$$
我们首先化简 $$\gcd(tv, s)$$, 看看它到底是个什么玩意. 化简过程中, 注意使 gcd 的参数始终为整数.
$$
\begin{align}
&\gcd(tv,s) \\
&=\gcd\left( \frac{a_1a_2}{w\gcd(a_1,g)}, \frac{a_1}{w}\right) \\
&=\frac{1}{w}\gcd\left( \frac{a_1a_2}{\gcd(a_1,g)}, a_1\right) \\
&=\frac{1}{w\gcd(a_1,g)}\gcd\left( a_1a_2, a_1\gcd(a_1,g)\right) \\
&=\frac{a_1}{w\gcd(a_1,g)}\gcd\left( a_2, \gcd(a_1,g)\right) \\
&=\frac{a_1}{w\gcd(a_1,g)}=v.
\end{align}
$$
化简过程中, 应始终保持每一步中的gcd的参数都是整数. 反例
$$
\gcd\left(\frac{12}{2}\frac{15}{3}, \frac{12}{3}\right)\neq
\gcd\left(\frac{15}{2}, 1\right).
$$
左式本来等于2, 如果按照上述化简方式, 就会错误地化出参数1, 进而误以为gcd结果为1. 当gcd的参数为符号表达式时, 这个错误会更隐蔽.

我们化简 $$\lambda$$ 中的 such that 部分. 过程如下:
$$
\begin{align}
& z_0tv+z_1s=\gcd(tv,s)=v \\
& \Leftrightarrow z_0t+z_1s/v=1 \\
& \Leftrightarrow z_0\frac{a_2}{w} + z_1\frac{\gcd(a_1,g)}{w}=1 \\
& \Leftrightarrow z_0a_2 + z_1\gcd(a_1,g)=w \\
& \Leftrightarrow z_0a_2 + z_1(y_0g+y_1a_1)=w \\
& \Leftrightarrow z_1y_1a_1+z_0a_2+z_1y_0g = w =\gcd(a_1,a_2,g).
\end{align}
$$
如此, $$\lambda$$ 的such that部分就是在约束 $$a_1, a_2, g$$ 的系数, 使系数满足拓展欧几里得算法.
