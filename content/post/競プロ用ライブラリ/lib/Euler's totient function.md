+++
title = "Euler's totient function"
date = 2024-07-29T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

オイラーのトーシェント関数. $ n \in \mathbb{N} $に対して, $n$と互いに素である$1$以上$n$以下の自然数の個数$φ(n)$を与える.  
nの素因数分解が
$$
  n = \prod_{k=1}^{d}p_k^{e_k}
$$
と表されるとき,
$$
  \phi (n) = \prod_{k=1}^{d}\left(p_k^{e_k} - p_k^{e_k-1}\right) = n\prod_{k=1}^{d}\left(1-\frac{1}{p_k}\right)
$$
と変形できることを利用して計算する。

## 計算量

$ O(\sqrt{n}) $

## 使い方

```cpp
int res = euler_phi(n);
```

## 実装

```cpp
int euler_phi(int n) {
  int ret = n;
  for (int i = 2; i * i <= n; i++) {
    if (n % i == 0) {
      ret -= ret / i;
      do
        n /= i;
      while (n % i == 0);
    }
  }
  return n > 1 ? ret - ret / n : ret;
}
```
