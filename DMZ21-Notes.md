$$
\begin{align}
a_1 &= g_p^{s_r} \\
a_2 &= h^{s_r}f^{s_m} \\
z_r &= s_r+er \\
z_r' &= s_r+e'r \\
\tilde{z}_r &= (e-e')r \\
\tilde{z}_m &= (e-e')x_1 \\
c_1^\tilde{e} &= g_p^{(e-e')r} \\
c_2^\tilde{e} &= (h^r f^{x_1})^\tilde{e}
               =h^{(e-e')^r}\cdot f^{(e-e'){x_1}} \\
c_1' &= g_p^{\tilde{e}r} \\
c_2' &= h^{\tilde{e}r}f^{\tilde{e}m} \\
\frac{c_2'}{(c_1')^d} &= f^{\tilde{e}m}
\end{align}
$$

💡 $c_1', c_2'$ 都可以表示成 $g$ 的幂; 前文有说 $g$ 是 $G$ 的生成元. 因此, 表达式 $c_2'/c_1'$ 看起来是除法, 实际上是幂的减法.

- **Simulator**: Used to show the **zero-knowledge property**, ensuring the verifier learns nothing beyond the validity of the statement.
- **Extractor**: Used to show the **soundness property**, ensuring the prover cannot convince the verifier of a false statement.



密码学中的「验」大多利用了**同构性**.

验$z_m$的原理.
$$
\begin{align}
z_mG &= (s_m+em)G \\
&=s_mG+emG \\
&=A+eQ
\end{align}
$$
验$z_r$的原理.
$$
\begin{align}
g_p^{z_r}&=\mathrm{pow}(g_p,s_r+er) \\
&=\mathrm{pow}(g_p,s_r)\cdot\mathrm{pow}(g_p,er) \\
&=a_1\cdot (g_p^r)^e \\
&=a_1\cdot c_1^e
\end{align}
$$

$$
\begin{align}
h^{z_r}f^{z_m}
&=\mathrm{pow}(h,s_r+er)\cdot \mathrm{pow}(f,s_m+em) \\
&=h^{s_r}h^{er}f^{s_m}f^{em} \\
&=h^{s_r}f^{s_m}h^{er}f^{em} \\
&=h^{s_r}f^{s_m}(h^rf^m)^e \\
&=a_2\cdot c_2^e
\end{align}
$$

## SigmaProm2协议 注解

首先明确一个问题, 什么叫「equality of plaintexts」? 这个问题来自于逻辑而不是内容: 明文只有一个, 也就是$m$, 它何来相等一说? 通过询问gpt和google, 我相信作者想说的是「不同算法的密文来自相同的明文」. 这实际上是明文的equivalence或consistency. 

明确作者的确切意图之后, 就得到一个技术问题. ==给定两个不同算法的密文, 如果没有密钥, 如何判断他俩对应相同的明文?==

### 知识铺垫

$C_2$是$m$的EC ElGamal加密, $c_2$是$m$的CL ElGamal加密.

文章并没有说ElGamal加密的一般形式. 我在维基上查了一下, 整理出一般形式如下:
$$
\begin{align}
\mathtt{Alice::~~}& x:=\mathrm{Rand}(G);~~ y=g^x \\
\mathtt{Bob::~~}& r:=\mathrm{Uni}(\mathrm{ord}(G));~~ c_1=g^r;~~ c_2=m\cdot y^r \\
\mathtt{Alice::~~}& m=c_2\cdot(c_1^x)^{-1}
\end{align}
$$
对于EC ElGamal来说, 通常表示成数乘形式, 并假设加密的不是$m$, 而是$m$的可逆编码$F(m)$. 虽然我很好奇如何把数$m$ ==可逆地== 映射到点$F(m)$, 但是暂且放一放, 假设存在这样的方法. 如此, EC ElGamal具有如下一般形式:
$$
\begin{align}
\mathtt{Alice::~~}& x:=\mathrm{Uni}(n);~~ H=xG \\
\mathtt{Bob::~~}& r:=\mathrm{Uni}(n);~~ C_1=rG;~~ C_2=F(m)+rH \\
\mathtt{Alice::~~}& F(m)=C_2-xC_1 \\
\mathtt{Alice::~~}& m=F^{-1}(F(m))
\end{align}
$$
💡 注意ElGamal中的 $\cdot(c_1^x)^{-1}$ 在EC ElGamal中变成了 $-xC_1$. 一定要保持清醒: 一般循环群中的「乘法」和求逆, 在加法循环群中是加法和减法.

### 正式开始讲协议

第一步: 在prover一侧, 执行
$$
\begin{align}
s_1 &:= \mathrm{Uni}(\mathbb{Z}_p) \\
s_2 &:= \mathrm{Uni}[0,U) \\
s_m &:= \mathrm{Uni}(\mathbb{Z}_p) \\
A_1,~A_2 &:= s_1G,~s_1P+s_mG \\
a_1,~a_2 &:= g_p^{s_2},~h^{s_2}f^{s_m} \\
&\mathtt{send}(\mathcal{V},A_1,A_2,a_1,a_2).
\end{align}
$$
第二步: 在verifier一侧, 执行
$$
\begin{align}
e &:= \mathrm{Uni}(\mathbb{Z}_p)\\
&\mathtt{send}(\mathcal{P},e).
\end{align}
$$
第三步: 在prover一侧, 执行
$$
\begin{align}
z_1 &:=(s_1+er_1)~\mathrm{mod}~p \\
z_m &:=(s_m+em)~\mathrm{mod}~p \\
z_2 &:=s_2+er_2 \\
&\mathtt{send}(\mathcal{V}, z_1,z_m,z_2).
\end{align}
$$
第四步: 在verifier一侧, 验证
$$
\begin{align}
& 0 \le z_2 < U+(p-1)S \\
& z_1G=A_1+eC_1 \\
& z_1P+z_mG=A_2+eC_2 \\
& g_p^{z_2}=a_1c_1^e \\
& h^{z_2}f^{z_m}=a_2c_2^e ~.
\end{align}
$$
若这些条件都满足, 则verifier宣布接受proof.

至此, 我又产生了一个疑问: ==如果prover故意用两个$m$, 比如用$m_1$算$C_2$, 用$m_2$算$c_2$, 那么verifier仍然能验算通过, 以上协议不就失效了吗?==

动笔演算之后想通了: verifier只收到了一个$z_m$. 所以如果$C_2, c_2$来自不同的明文$m_1,m_2$, 那么verifier不论收到哪一个$m_i$所对应的$z_m$, 因为总是少一个$m_i$, 所以必然验不过.

## 顺便辨析概念

明文与密文相对. 明文不一定公开,  甚至往往是私密的. 一定要保持清醒, 不要受「明」字的误导. 

换个角度想, 如果明文公开, 那么何必加密?

# SigmaProtocol 3

前文对 $\mathcal{L}_\mathrm{affine}$ 的描述非常高冷. 实际上, 里面带「撇」的密文, 等价于对明文 $m^\prime=am+b$ 进行加密.

如此, 协议3的Common Input所提到的密文$C'$, 其对应的明文是 $m^\prime=am+b$.

## 第一步: 在Prover一侧, 计算承诺并发送给Verifier

$$
\begin{align}
s_a &:=\mathrm{Uni}(pS) \\
(s_b,s_r) &:= \mathrm{Uni}(\mathbb{Z}_p) \\
A_1 &:= s_aC_1+s_rG \\
A_2 &:= s_aC_2+s_bG+s_rP \\
a_1 &:= c_1^{s_a} \\
a_2 &:= c_2^{s_a}f^{s_b} \\
&\mathtt{send}(\mathcal{V}, A_1, A_2, c_1, c_2)
\end{align}
$$

上述公式里, $(A_1, A_2)$是对$(s_am+s_b)$的同态加密. 实际上,
$$
\begin{align}
A_1 &= s_ar_1G+s_rG \\
    &= (s_ar_1+s_r)G, \\
A_2 &= s_a(r_1P+mG)+s_bG+s_rP \\
    &= (s_am+s_b)G+(s_ar_1+s_r)P.
\end{align}
$$
类似地, $(a_1, a_2)$也是对$(s_am+s_b)$的同态加密. 实际上,
$$
\begin{align}
a_1 &= g_p^{s_ar_2},\\
a_2 &= h^{s_ar_2}f^{s_am}f^{s_b}\\
    &= h^{s_ar_2}f^{s_am+s_b}.
\end{align}
$$

## 第二步: 在Verifier一侧, 摇出随机挑战并发送给Prover

$$
\begin{align}
e &:= \mathrm{Uni}(\mathbb{Z}_p)\\
&\mathtt{send}(\mathcal{P},e).
\end{align}
$$

## 第三步: 在Prover一侧, 响应挑战

$$
\begin{align}
z_a &:= s_a+ea \\
z_b &:= s_b+eb \\
z_r &:= s_r+er \\
&\mathtt{send}(\mathcal{V},z_a,z_b,z_r)
\end{align}
$$

## 第四步: 在Verifier一侧, 验证响应

这一步检查四个等式是否成立. 每个表达式的左右两边在以不同的结合性计算 $(s_a+ea)m+(s_b+eb)$ 的ElGamal加密.

我们分析前两个等式
$$
\begin{align}
z_aC_1+z_rG &= (s_a+ea)r_1G+(s_r+er)G \\
&= ((s_a+ea)r_1+s_r+er)G ~~, \\
A_1+eC_1' &= (s_ar_1+s_r)G+e(aC_1+rG) \\
&= (s_ar_1+s_r)G+e(ar_1+r)G \\
&= ((s_a+ea)r_1+s_r+er)G ~~.
\end{align}
$$

$$
\begin{align}
z_aC_2+z_bG+z_rP
&= (s_a+ea)(r_1P+mG)+(s_b+eb)G+(s_r+er)P \\
&= \Big[(s_a+ea)m+(s_b+eb)\Big]G  \\
&\hspace{1em}+ \Big[(s_a+ea)r_1+(s_r+er)\Big]P ~~,\\

A_2+eC_2' &=
(s_am+s_b)G+(s_ar_1+s_r)P \\
&\hspace{1em}+ e(a(r_1P+mG)+bG+rP) \\
&=\Big[(s_a+ea)m+(s_b+eb)\Big]G  \\
&\hspace{1em}+ \Big[(s_a+ea)r_1+(s_r+er)\Big]P ~~.
\end{align}
$$

## Phase 1

​	参与方 $\mathcal{P}_i$ 生成 $k_i, \gamma_i$ , 与其他各参与方用 $\Sigma_\mathrm{prom}^2$ 协议证明确实生成了 $k_i$ .

## Phase 2

​	参与方 $\mathcal{P}_i$ 在CL ElGamal信道与其他各方交换如下两个表达式. 这里下标 $j,i$ 代表「从 $i$ 到 $j$ 」.
$$
\begin{align}
F_\alpha &= k_j(\gamma_i+\hat{t}_{j,i})-\beta_{j,i} \\
F_\mu &= k_j(w_i+t_{j,i})-v_{j,i}
\end{align}
$$
​	然后, 其他各参与方 $\mathcal{P}_j$ 计算如下两个表达式. 这里, 符号「$\equiv$」表示事实等价, 不代表 $\mathcal{P}_j$ 能知道任何下标为 $i$ 或 $j,i$ 的变量. 强调一下: $\mathcal{P}_j$ (理论上)到底知道什么, 只取决于 $\mathcal{P}_i$ 给他发了什么, 也就是长箭头上面的东西.
$$
\begin{align}
\alpha_{j,i} &= F_\alpha-k_j\hat{t}_{j,i} \equiv k_j\gamma_i-\beta_{j,i} \\
\mu_{j,i} &= F_\mu - k_jt_{j,i} \equiv k_jw_i-v_{j,i}
\end{align}
$$
​	最后, $\mathcal{P}_i$ 计算如下两个表达式. 回忆: 公式$\eqref 2$中的 $w_i=\lambda_ix_i$, 也就是插值后的私钥分片. 可以合理推断, $W_i=w_iG$ .
$$
\begin{align}
\delta_i&=k_i\gamma_i+\sum_j^{j\neq i}(\alpha_{i,j}+\beta_{j,i}) \\
&\equiv k_i\sum_j\gamma_j ~-~ \sum_j^{j\neq i}\beta_{i,j} ~+~ \sum_j^{j\neq i}\beta_{j,i} \\
&\equiv k_i\gamma ~-~ \sum_j^{j\neq i}\beta_{i,j} ~+~ \sum_j^{j\neq i}\beta_{j,i}
\end{align}\tag{1}\label{1}
$$

$$
\begin{align}
\sigma_i&=k_iw_i+\sum_j^{j\neq i}(\mu_{i,j}+v_{j,i}) \\
&\equiv k_i\sum_jw_j ~-~ \sum_j^{j\neq i}v_{i,j} ~+~ \sum_j^{j\neq i}v_{j,i} \\
&\equiv k_ix ~-~ \sum_j^{j\neq i}v_{i,j} ~+~ \sum_j^{j\neq i}v_{j,i}
\end{align} \tag{2}\label{2}
$$

## Phase 3

​	计算 $\delta=\sum_i\delta_i=k\gamma$ . 这里 $k=\sum_i k_i, \gamma=\sum_i \gamma_i$ .

​	提示: 在求和过程中, 公式$\eqref 1$中的正负 $\beta_{i,j}$ 被消掉了.

## Phase 4

​	利用 $R=\delta^{-1}(\sum_i \Gamma_i)$ 得到签名字段 $r$ . 这里 $\Gamma_i\equiv \gamma_iG$ .

## Phase 5

​	聚合签名: $s_i=mk_i+r\sigma_i, s=\sum_i s_i$ . 

​	公式推导
$$
\begin{align}
&\hspace{1em}\sum_j U_j \\
&= \sum_j\rho_j\sum_i\big((mk_i+r\sigma_i)R+l_iG\big) \\
&\equiv \sum_j\rho_j\sum_i\big( (mk_i+r\sigma_i)k^{-1}+l_i\big)G \\
\mathrm{by~\eqref{2}}& \equiv \sum_j\rho_j\Big(mG+rQ+\sum_i V_i\Big) \\
&=\sum_j\rho_j\sum_il_iG ~~=\sum_il_iA
\end{align}
$$

