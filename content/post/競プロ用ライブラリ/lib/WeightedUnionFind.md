+++
title = 'WeightedUnionFind'
date = 2024-07-29T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++

## 用途

UnionFindに重みを持たせて要素間の距離も管理できるようにしたもの.

## 計算量

$ O(\alpha(n)) $, $\alpha$はAckermann関数の逆関数

## 使い方

### 宣言

```cpp
WeightedUnionFind<距離を表すclass> wuf(要素数);
```

### クエリ

#### マージ

```cpp
uf.merge(a,b,w);
```

aが属する集合と,bが属する集合をbの重み-aの重み = w、つまりaよりbの方がw重みがあるようにマージする.

#### 同一の集合か判定

```
wuf.isSame(a,b);
```

a,bが同一の集合に属しているか判定する

#### 集合サイズ

```cpp
wuf.size(a);
```

aが属する集合の濃度を返す

#### 重みの差

```cpp
wuf.diff(a,b);
```

でbの重み-aの重みを得る.

## 実装

```cpp
template <class T>
class WeightedUnionFind {
public:
  WeightedUnionFind(int n) : parents(n, -1), weights(n, 0) {}
  int find(int i) {
    if (parents[i] < 0)
      return i;
    weights[i] += weights[parents[i]];
    return parents[i] = find(parents[i]);
  }
  void merge(int a, int b, T w) {
    w += weight(a) - weight(b);
    a = find(a), b = find(b);
    if (a != b) {
      if (-parents[a] < -parents[b]) {
        swap(a, b);
        w = -w;
      }
      parents[a] += parents[b];
      parents[b] = a;
      weights[b] = w;
    }
  }
  T diff(int a, int b) {
    return weight(b) - weight(a);
  }
  bool connected(int a, int b) {
    return find(a) == find(b);
  }
  int size(int i) {
    return -parents[find(i)];
  }
private:
  vector<int> parents;
  vector<T> weights;
  T weight(int i) {
    find(i);
    return weights[i];
  }
};
```

## Verify

//TODO
