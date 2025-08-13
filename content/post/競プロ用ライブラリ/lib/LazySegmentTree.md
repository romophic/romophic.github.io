+++
title = 'LazySegmentTree'
date = 2024-07-29T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

[SegmentTree]({{< ref "post/競プロ用ライブラリ/lib/SegmentTree" >}})の一点更新を区間更新として$O(\log n)$で行う.

## 計算量

初期化: $O(n)$  
クエリ: $\log(n)$

## 使い方

### 宣言

```cpp
LazySegmentTree<class> lseg(配列長, 二項演算するlambda, 単位元);
```

### 構築&更新

```cpp
lseg.update(a, b, x);
```

で$ [a,b) $をxで更新する.

### クエリ

```cpp
lseg.query(a,b)
```

で半開区間$ \left[ a,b \right) $に演算を適応した値が得られる.

## 実装

例として区間和を求める場合、`update(a,b,x)`の動作を

- 区間更新: $ \text{seg}_i \rightarrow x$
- 区間加算: $ \text{seg}_i \rightarrow \text{seg}_i + x $

にするかで実装が異なる

### 区間更新型ver

```cpp
template <class T>
struct LazySegmentTree {
  int n;
  vector<T> s, lazy;
  const function<T(T, T)> f;
  const T m;
  LazySegmentTree(int _n, const function<T(T, T)> &_f, const T &_m) : s(_n * 4, m), lazy(_n * 4, m), f(_f), m(_m) {
    n = 1;
    while (n < _n)
      n *= 2;
    s.assign(n * 2, m);
    lazy.assign(n * 2, m);
  }
  void eval(int k) {
    if (lazy[k] == m)
      return;
    if (k < n - 1) {
      lazy[k * 2 + 1] = lazy[k];
      lazy[k * 2 + 2] = lazy[k];
    }
    s[k] = lazy[k];
    lazy[k] = m;
  }
  void update(int a, int b, T x, int k, int l, int r) {
    eval(k);
    if (a <= l and r <= b) {
      lazy[k] = x;
      eval(k);
    } else if (a < r and l < b) {
      update(a, b, x, k * 2 + 1, l, (l + r) / 2);
      update(a, b, x, k * 2 + 2, (l + r) / 2, r);
      s[k] = f(s[k * 2 + 1], s[k * 2 + 2]);
    }
  }
  void update(int a, int b, T x) { update(a, b, x, 0, 0, n); }
  T query_sub(int a, int b, int k, int l, int r) {
    eval(k);
    if (r <= a or b <= l) {
      return m;
    } else if (a <= l and r <= b) {
      return s[k];
    } else {
      T vl = query_sub(a, b, k * 2 + 1, l, (l + r) / 2);
      T vr = query_sub(a, b, k * 2 + 2, (l + r) / 2, r);
      return f(vl, vr);
    }
  }
  T query(int a, int b) { return query_sub(a, b, 0, 0, n); }
};
```

### 区間加算型ver

```cpp
template <class T>
struct LazySegmentTree {
  int n;
  vector<T> s, lazy;
  const function<T(T, T)> f;
  const T m;
  LazySegmentTree(int _n, const function<T(T, T)> &_f, const T &_m) : s(_n * 4, m), lazy(_n * 4, 0), f(_f), m(_m) {
    n = 1;
    while (n < _n)
      n *= 2;
    s.assign(n * 2, m);
    lazy.assign(n * 2, 0);
  }
  void eval(int k, int l, int r) {
    if (lazy[k] != 0) {
      s[k] += lazy[k] * (r - l);
      if (k < n - 1) {
        lazy[k * 2 + 1] += lazy[k];
        lazy[k * 2 + 2] += lazy[k];
      }
      lazy[k] = 0;
    }
  }
  void update(int a, int b, T x, int k, int l, int r) {
    eval(k, l, r);
    if (a <= l and r <= b) {
      lazy[k] += x;
      eval(k, l, r);
    } else if (a < r and l < b) {
      update(a, b, x, k * 2 + 1, l, (l + r) / 2);
      update(a, b, x, k * 2 + 2, (l + r) / 2, r);
      s[k] = f(s[k * 2 + 1], s[k * 2 + 2]);
    }
  }
  void update(int a, int b, T x) {
    update(a, b, x, 0, 0, n);
  }
  T query_sub(int a, int b, int k, int l, int r) {
    eval(k, l, r);
    if (r <= a or b <= l) {
      return m;
    } else if (a <= l and r <= b) {
      return s[k];
    } else {
      T vl = query_sub(a, b, k * 2 + 1, l, (l + r) / 2);
      T vr = query_sub(a, b, k * 2 + 2, (l + r) / 2, r);
      return f(vl, vr);
    }
  }
  T query(int a, int b) {
    return query_sub(a, b, 0, 0, n);
  }
};
```

## Verify

//TODO

## 例

連続区間の和を高速に求めたいとして:

```cpp
LazySegmentTree<int> lseg(n, [](int a, int b){ return a+b; }, 0);

// ~構築~
```

の様にlambdaをおけばよい.
