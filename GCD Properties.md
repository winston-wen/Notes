(1) 交换律.
$$
\gcd(a,b)=\gcd(b,a)
$$
(2) 对称性.
$$
\gcd(a,b)=\gcd(\pm a,\pm b).
$$
(3) 周期性. 对任意整数 $$n$$, 有
$$
\gcd(a,b)=\gcd(a,b+an).
$$
💡 特别地, 如果跟交换律结合起来, 令 $$n$$ 为负数, 那么gcd的两个参数就会越来越小, 直到其中一个收敛到0. 这就是原始的欧几里得算法.

(4) 结合律.
$$
\gcd(a,b,c) = \gcd\left(a,\gcd\left(b,c\right)\right).
$$
(5) 数乘分配律. 对任意整数 $$n$$, 有
$$
n\gcd(a,b)=\gcd(na,nb).
$$
(6) 递归性.
$$
\gcd(a,bc) = \gcd\left(
\gcd\left(a,b\right),
\gcd\left(a,c\right)
\right).
$$
