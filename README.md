# gf256
## Fast, Portable 8-bit Galois Field Math in C

This library provides efficient implementations of bulk GF(2^^8) math operations over memory buffers,
which are common operations in application-layer Forward Error Correction.
This library is the basis for all of my fast FEC software.

Addition is done over the base field in GF(2) meaning that addition is XOR between memory buffers.

Multiplication is performed using table lookups via vector instructions.
This is somewhat slower than XOR, but fast enough to not become a major bottleneck when used sparingly.


#### API

`gf256_add` : return x + y (XOR two bytes)

`gf256_mul` : return x * y. Memory-access optimized for constant multiplicands in y.

`gf256_div` : return x / y. Memory-access optimized for constant divisors in y.

`gf256_inv` : return 1 / x

`gf256_sqr` : return x * x

`gf256_add_mem` : Performs "x[] += y[]" bulk memory XOR operation

`gf256_add2_mem` : Performs "z[] += x[] + y[]" bulk memory operation

`gf256_addset_mem` : Performs "z[] = x[] + y[]" bulk memory operation

`gf256_mul_mem` : Performs "z[] = x[] * y" bulk memory operation

`gf256_muladd_mem` : Performs "z[] += x[] * y" bulk memory operation

`gf256_div_mem` : Performs "x[] /= y" bulk memory operation

`gf256_memswap`: Swap two memory buffers in-place


#### Key Features

It's the fastest implementation available online.

* Runtime CPU feature detection enables AVX2, SSSE3 for worry-free compilation.

* ARM NEON vectorization (Work in progress...)

* The polynomial can be chosen at runtime by editing the code.

* Hand-tuned loop unrolling.
