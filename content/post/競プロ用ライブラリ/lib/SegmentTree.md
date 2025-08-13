+++
title = 'SegmentTree'
date = 2024-07-29T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

**交換則**と**結合則**を満たし、**単位元**を持つ演算と配列に対して、連続する部分範囲に対する演算結果を高速に計算する.  
例:
実数の加法はAbel群であるから上記の性質を満たす. 具体的には:

- 交換則: $ a + b = b + a $
- 結合則: $ (a+b)+c = a+(b+c) $
- 単位元の存在: $ a + 0 = a $

を満たすから, これはセグ木に乗せられ, 連続する部分範囲の和を高速に求めることができる.  
類似データ構造: [LazySegmentTree]({{< ref "post/競プロ用ライブラリ/lib/LazySegmentTree" >}})

## 計算量

初期化: $O(n)$  
クエリ: $\log(n)$

## 使い方

### 宣言

```cpp
SegmentTree<class> seg(配列長, 二項演算するlambda, 単位元);
```

### 構築

```cpp
seg.set(i,x);
```

でi番目にxを代入できる.  
配列を構築後

```cpp
seg.build();
```

でセグ木を構築する.

### 更新

構築後,

```cpp
seg.update(i,x)
```

でi番目にxを代入と構築ができる.

### クエリ

```cpp
seg.query(a,b)
```

で半開区間$ \left[ a,b \right) $に演算を適応した値が得られる.

## 実装

```cpp
template <class T>
class SegmentTree {
public:
  int n;
  vector<T> s;
  const function<T(T, T)> f;
  const T m;
  SegmentTree(int _n, const function<T(T, T)> &_f, const T &_m) : f(_f), m(_m) {
    n = 1;
    while (n < _n)
      n <<= 1;
    s.assign(2 * n, _m);
  }
  void set(int k, const T &x) {
    s[k + n] = x;
  }
  void build() {
    for (int k = n - 1; k > 0; k--)
      s[k] = f(s[2 * k + 0], s[2 * k + 1]);
  }
  void update(int k, const T &x) {
    k += n;
    s[k] = x;
    while (k >>= 1)
      s[k] = f(s[2 * k + 0], s[2 * k + 1]);
  }
  T query(int a, int b) {
    T L = m, R = m;
    for (a += n, b += n; a < b; a >>= 1, b >>= 1) {
      if (a & 1)
        L = f(L, s[a++]);
      if (b & 1)
        R = f(s[--b], R);
    }
    return f(L, R);
  }
  T operator[](const int &k) const {
    return s[k + n];
  }
};
```

## Verify

//TODO

## 例

連続区間の和を高速に求めたいとして:

```cpp
SegmentTree<int> seg(n, [](int a, int b){ return a+b; }, 0);

// ~構築~
```

の様にlambdaをおけばよい.
