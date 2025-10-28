Hensel 引理. 设多项式 $$f(x)\in\Z[x]$$ 在模质数幂的意义上有根 $$a$$, 即满足
$$
f(a)\equiv 0 \pmod{p^k}; \label{pre}\tag{pre}
$$
并且有 $$f'(a)\neq 0 \pmod p$$, 则存在唯一整数 $$t\bmod p$$ 使得
$$
f(a+tp^k)\equiv 0 \pmod{p^{k+1}}.\tag{lift}\label{lift}
$$
证明:

对 $$f(a+tp^k)$$ 实施 $$n$$ 阶泰勒展开, 得到
$$
\begin{align}
&\hphantom{{}={}}
f\left(a+tp^k\right) \\
&=
f\left(a\right)
+ f'\left(a\right)tp^k
+ \frac{f''\left(a\right)}{2!}(tp^k)^2
+ \cdots
+ \frac{f^{(n)}\left(a\right)}{n!}(tp^k)^n.
\end{align} \tag{taylor}\label{taylor}
$$
易证泰勒展开的各系数都是整数, 并且从第 2 阶开始, 都能被 $$p^{k+1}$$ 整除. 因此可以合法地结合 $$\eqref{lift}$$ 和 $$\eqref{taylor}$$ 两式, 得到
$$
\begin{align}
f(a) + tp^kf'(a) &\equiv 0 \pmod{p^{k+1}} \\
\frac{f(a)}{p^k} + tf'(a) &\equiv 0 \pmod  p\\
-\left(
\frac{f(a)}{p^k}\cdot\frac{1}{f'(a)}
\right) &\equiv t  \pmod p.
\end{align} \tag{res}\label{res}
$$
注意: 式 $$\eqref{res}$$ 中 $$f(a)/p^k$$ 是整数除法, 这是由前提条件 $$\eqref{pre}$$ 给出的. 而 $$1/f'(a)$$ 是模 $$p$$ 逆, 这是由 $$\eqref{res}$$ 所示的运算过程给出的. 🟩

----

例子: 找到 $$x^3-2x\equiv 1\pmod{125}$$ 的一个解.

解: 令 $$f(x)=x^3-2x-1$$. 试出 $$f(x)\equiv 0\pmod{5}$$ 有解 $$3, 4$$.

计算 $$f$$ 的一阶导数, $$f'(x)=3x^2-2$$.

因为 $$f'(3)\equiv 0 \pmod 5$$, 所以 3 不能继续迭代.

因为 $$f'(4)\equiv 1\not\equiv0 \pmod 5$$, 所以 4 可以继续迭代. 进而模 25 的解为
$$
\begin{align}
&\phantom{{}={}}4-f(4)\left[f'(4)\right]^{-1}_{(\mathrm{mod}5)} &\pmod{25}\\
&=4-55\times 1 & \pmod{25} \\
&=24. & \pmod{25}
\end{align}
$$
进而模 125 的解为
$$
\begin{align}
&\phantom{{}={}}24-f(4)\left[f'(24)\right]^{-1}_{(\mathrm{mod}5)} &\pmod{125}\\
&=4-13775\times 1 & \pmod{125} \\
&=124. & \pmod{125}
\end{align}
$$
最终, $$x=124$$ 是 $$x^3-2x\equiv 1\pmod{125}$$ 的一个解.

-----

Hensel 引理, 多变量版本. 若有 $$f(\boldsymbol{a})\equiv\boldsymbol{0}\pmod{p^k}$$, 并且 Jacobian 矩阵 $$J_f(\boldsymbol{a})$$ 在模 $$p$$ 下可逆; 则存在唯一的向量 $$\boldsymbol{t} \bmod p$$, 使得 $$f(\boldsymbol{a}+p^k \boldsymbol{t})\equiv \boldsymbol{0}\pmod {p^{k+1}}$$.

