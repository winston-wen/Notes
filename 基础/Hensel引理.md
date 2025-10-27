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
⚠️式 $$\eqref{res}$$ 中 $$f(a)/p^k$$ 是整数除法, 这是由前提条件 $$\eqref{pre}$$ 给出的. 而 $$1/f'(a)$$ 是模逆, 这是由 $$\eqref{res}$$ 所示的运算过程给出的.