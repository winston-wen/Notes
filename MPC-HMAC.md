## 关键词

Garbled Circuit

## 论文摘录

### [Bon20] Thresholdizing HashEdDSA: MPC to the Rescue

Our first strategy is to securely evaluate the hash function using a Garbled Circuit (GC) based approach for n parties. In particular, we use a variant of the HSS protocol [HSS17].

Our second approach is to use evaluate the hash function circuit using a secret sharing based approach over F2. In particular we adapted the method of Araki et al. [ABF+17], ... These methods are explained in Section 3, and are to be incorporated in the v1.11 release of SCALE-MAMBA [ACC+20].

We then convert these bit-sharings into an $$\mathbb{F}_q$$-sharing for the desired $$\mathcal{Q}_2$$ access structure using a modification of the daBit procedure from [RW19, AOR+19].

Thus in Section 4, we provide a variant of the method in [RST+19] which works in our situation. This variant works by only requiring a qualified subset of the parties to contribute to the computation of the so-called correction terms in the big field.

Our key MPC functionality needs to process shared values in Fq as well as evaluate binary garbled circuits using the HSS protocol, [HSS17]. We therefore adopt the Zaphod framework from [AOR+19].

## 开源实现

1. `https://github.com/getamis/alice/blob/master/crypto/bip32/README.md` 
2. `https://github.com/markkurossi/mpc` 似乎是个通用MPC电路编译器.

## 现有产品

1. `https://docs.mpcvault.com/techoverview/`



