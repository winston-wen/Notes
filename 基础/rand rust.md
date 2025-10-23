(1) 创建助记词.

```
anychain_kms::bip39::mnemonic
impl Mnemonic
fn new
```

(2) 获取随机缓冲区.

```
anychain_kms::bip39::crypto
fn get_random_bytes
```

(3) 填充随机缓冲区.

```
rand::rngs::thread::ThreadRng
fn fill_bytes
```

💡 3, 4 之间有若干个行数极少的, 名为 `fill_bytes` 的函数. 因为它们太琐碎, 这里就不记录了. 一路点下去, 得到如 4 所示的具体实现.

(4) 拷贝随机缓冲区.

```
rand_core::block::BlockRng
impl<R> RngCore for BlockRng<R>
fn fill_bytes
```

该函数分为 step1. 生成内核态随机缓冲区. step2. 拷贝到用户态随机缓冲区.

(5) 生成内核态随机缓冲区.

```
rand_core::block::BlockRng
impl<R> BlockRng<R>
pub fn generate_and_set
```

(6) 生成内核态随机缓冲区.

rust-analyzer跳转到如下Trait 定义:

```
rand_core::block
pub trait BlockRngCore
fn generate
```

尝试在 (5) 所在的 `reseeding.rs` 搜索 `fn generate`, 很幸运地搜索到具体实现.

```
rand::rngs::adapter::reseeding::ReseedingCore
impl<R, Rsdr> BlockRngCore for ReseedingCore<R, Rsdr>
fn generate(...) {
	if ... {
        self.reseed_and_generate(...);
	}
	self.inner.generate(...);
}
```

RNG 本质上是一个状态机, 内部维护一个内核态随机缓冲区.   RNG有两个原语:

* reseed. 用熵更新缓冲区. 该原语是定期执行的.
* generate. **用确定性的算法对缓冲区进行散列运算**, 更新缓冲区.

话说到这里, 我们必然会想到, 为什么不直接用熵, 还要对熵进行散列? 这是因为熵源生成新熵的速度可能赶不上用户代码消耗熵的速度, 需要在两次 reseed 之间插入少量确定性的 generate .

虽然 generate 是确定性的, 但是 generate 满足

* 与均匀分布无法区分.
* 两次执行是独立的, 具体来说:
  * 无法回测. 即无法用新结果预测老结果.
  * 无法预测. 即无法用老结果预测新结果.

(7) 根据上述理论, 跳转到 reseed 函数.

```
rand::rngs::adapter::reseeding::ReseedingCore
impl<R, Rsdr> ReseedingCore<R, Rsdr>
fn reseed_and_generate
```

(8) reseed 具体实现.

```rust
rand::rngs::adapter::reseeding::ReseedingCore
impl<R, Rsdr> ReseedingCore<R, Rsdr>
fn reseed(...) -> ... {
	R::from_rng(&mut self.reseeder)...;
}
```

进入 `from_rng`, 发现它调用了 `try_fill_bytes`. 如此需查看 `self.reseeder` 是什么类型.

(9) 回到 ThreadRng 结构体的定义.

```rust
rand::rngs::thread
pub struct ThreadRng {
    rng: Rc<UnsafeCell<ReseedingRng<ChaCha12Core, OsRng>>>,
}
```

如此, 8 中的 `self.reseeder` 是一个 `OsRng`.

(10) 查看结构体 OsRng 的定义和实现.

```rust
rand_core::os::OsRng
impl RngCore for OsRng
fn try_fill_bytes(...) -> ... {
    getrandom(dest)...;
}
```

至此已经很明确, 创建助记词用的是 Unix 系统调用 `getrandom`, 是安全的.



