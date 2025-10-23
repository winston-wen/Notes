## linux `getrandom(2)`

(0) 入口

```c
getrandom
https://elixir.bootlin.com/linux/v6.17.4/source/tools/include/nolibc/sys/random.h#L29

NR_getrandom
https://elixir.bootlin.com/linux/v6.17.4/source/arch/x86/include/asm/vdso/getrandom.h#L24
https://elixir.bootlin.com/linux/v6.17.4/source/include/uapi/asm-generic/unistd.h#L674

sys_getrandom
https://elixir.bootlin.com/linux/v6.17.4/source/drivers/char/random.c#L1390
```

(1) 如果 Crypto RNG 没准备好, 那就等它准备好

```c
在 sys_getrandom 中的如下位置
https://elixir.bootlin.com/linux/v6.17.4/source/drivers/char/random.c#L1390

wait_for_random_bytes
https://elixir.bootlin.com/linux/v6.17.4/source/drivers/char/random.c#L137

try_to_generate_entropy
https://elixir.bootlin.com/linux/v6.17.4/source/drivers/char/random.c#L1292
```

TODO: `try_to_generate_entropy` 收集了哪些熵源?

(2) 在内核空间创建用户内存的迭代器.

```c
// https://elixir.bootlin.com/linux/v6.17.4/source/drivers/char/random.c#L1413
// &iter 才是真正的 "返回值".
ret = import_ubuf(ITER_DEST, ubuf, len, &iter);
```

(3) 从 Crypto RNG 拷贝内存.

```c
// https://elixir.bootlin.com/linux/v6.17.4/source/drivers/char/random.c#L1416
return get_random_bytes_user(&iter);

// 在此接触熵源, 生成 Crypto RNG 状态机, 后者维护一个随机字节数组.
// https://elixir.bootlin.com/linux/v6.17.4/source/drivers/char/random.c#L456
crng_make_state(&chacha_state, (u8 *)&chacha_state.x[4], CHACHA_KEY_SIZE);

// 如果目标数组较短, 则执行.
// 注意套路: iter 才是真正的返回值.
ret = copy_to_iter(&chacha_state.x[4], CHACHA_KEY_SIZE, iter);

// 在此对状态机中的字节数组进行混淆.
// https://elixir.bootlin.com/linux/v6.17.4/source/drivers/char/random.c#L469
chacha20_block(&chacha_state, block);

// 如果目标数组较长, 则执行.
copied = copy_to_iter(block, sizeof(block), iter);
```

(4)  在 `crng_make_state` 中接触熵源.

```c
// https://elixir.bootlin.com/linux/v6.17.4/source/drivers/char/random.c#L673
static void extract_entropy(void *buf, size_t len) {
    // ...
    // 熵源 1 : RDSEED 指令
    longs = arch_get_random_seed_longs(&block.rdseed[i], ARRAY_SIZE(block.rdseed) - i);
    // ...
    // 熵源 2 : RDRAND 指令
    longs = arch_get_random_longs(&block.rdseed[i], ARRAY_SIZE(block.rdseed) - i);
    // ...
    // 熵源 3 : 基于 CPU 时钟的熵源
    block.rdseed[i++] = random_get_entropy();
    // ...
    // 熵源 4 : 历史熵
    blake2s_final(&input_pool.hash, seed);
}
```

(4.1) RDSEED

```c
// 网页跳转顺序:
// https://elixir.bootlin.com/linux/v6.17.4/source/arch/x86/include/asm/archrandom.h#L53
// https://elixir.bootlin.com/linux/v6.17.4/source/arch/x86/include/asm/archrandom.h#L34

static inline bool __must_check rdseed_long(unsigned long *v)
{
	bool ok;
	asm volatile("rdseed %[out]"
		     CC_SET(c)
		     : CC_OUT(c) (ok), [out] "=r" (*v));
	return ok;
}
```

(4.2) RDRAND

```c
// 类似地,

static inline bool __must_check rdrand_long(unsigned long *v)
{
	bool ok;
	unsigned int retry = RDRAND_RETRY_LOOPS;
	do {
		asm volatile("rdrand %[out]"
			     CC_SET(c)
			     : CC_OUT(c) (ok), [out] "=r" (*v));
		if (ok)
			return true;
	} while (--retry);
	return false;
}
```



## golang `crypto/rand`

`crypto/rand : rand.go`

* On Linux, FreeBSD, Dragonfly, and Solaris, Reader uses `getrandom(2)`.
* On Windows, Reader uses the `ProcessPrng` API.
* On legacy Linux (< 3.17), Reader opens `/dev/urandom` on first use.
* On macOS, iOS, and OpenBSD Reader, uses `arc4random_buf(3)`.
* On js/wasm, Reader uses the Web Crypto API.
* On wasip1/wasm, Reader uses `random_get`.
* On NetBSD, Reader uses the `kern.arandom` sysctl.

In FIPS 140-3 mode, the output passes through an « SP 800-90A Rev. 1 Deterministic Random Bit Generator (DRBG) ».

`rand.Read([]byte)` 内部有两个分支:

```
crypto/internal/fips140/drbg.Read([]byte)
后文简称为 drbg.Read

crypto/internal/sysrand.Read([]byte)
后文简称为 sysrand.Read
```

`sysrand.Read` 关键调用堆栈:

```
sysrand.read(buf)
internal/syscall/unix.GetRandom(buf, flag)
sysrand.urandomRead(buf)
```

`drbg.Read` 关键调用堆栈:

```
sysrand.Read(aad[:16])
drbg.Generate(buf[:size], aad)
crypto.internal.entropy.Depleted(LOAD func (seed *[48]byte))
sysrand.Read(entropy)
drbg.Reseed(entropy, aad)
```