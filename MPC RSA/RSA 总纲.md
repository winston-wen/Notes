## 密钥生成

找到不同的质数 $$p, q$$, 令 $$n=pq$$, $$\lambda=\lambda(n)$$. 令 $$\lambda=\varphi(n)$$ 也是可以的.

随机选择 $$d\in\Z_\lambda^*$$, 计算 $$e\equiv d^{-1} \pmod \lambda$$.

公钥为 $$n, e$$. 私钥为 $$\lambda, d$$. 注意 $$\lambda$$ 保密等价于 $$p, q$$ 保密.

### 💡知识回顾

(1) 欧拉函数 $$\varphi(n)$$ 是群 $$\Z_n^*$$ 的阶. 而 Carmichael 函数 $$\lambda(n)$$ 是群 $$\Z_n^*$$ 的所有元素的阶的最小公倍数.

(2) 澄清一个想当然的误解. 群的阶不必然是元素阶的最大值. 这种情况只在群为循环群时成立. 反例: $$\Z_8^*$$, $$\Z_{15}^*$$, 等等.

(3) 回顾. 群是循环群, 当且仅当存在群元素能生成整个群. [« 模 $$n$$ 原根定理 »](https://en.wikipedia.org/wiki/Primitive_root_modulo_n) 告诉我们, $$\Z_n^*$$ 是循环群, 当且仅当 $$n=1,2,4$$ 或 $$n=p^k$$ 或 $$n=2p^k$$. 其中 $$p$$ 为奇质数, $$k$$ 为正整数.



## 加密和签名

加密: $$c=m^{e} \bmod n$$. 使用公钥 $$e$$.

解密: $$m=c^d \bmod n$$. 使用私钥 $$d$$.

解密推导: 将 $$de\equiv 1\pmod \lambda$$ 表示为 $$de = 1+k\lambda$$. 如此,
$$
c^d=m^{de}=m^{1+k\lambda}=(m^\lambda)^k\cdot m\equiv m \pmod n .
$$
签名: $$s=m^d \bmod n$$. 使用私钥 $$d$$. 消息 $$m\in \Z_n$$ 是公开的.

验签: $$m'=s^e \bmod n$$. 使用公钥 $$e$$. 若 $$m'\equiv m \pmod n$$, 则验签通过.

注: 理论上要求 $$m\in\Z_n^*$$. 但 $$\gcd{(m,n)}\ne 1$$ 的概率可以忽略.



## 转化为MPC的两大要点

(1) 生成 $$\lambda$$ 分片.

(2) 在 $$\lambda$$ 以分片形式存在的条件下, 生成 $$d$$ 分片, 使得 $$de\equiv 1\pmod \lambda$$.