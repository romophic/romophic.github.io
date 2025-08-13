+++
title = 'UnionFind'
date = 2024-07-29T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

要素がどの集合に属しているかを判定し,部分集合の濃度や部分集合の集合を得る.

## 計算量

$ O(\alpha(n)) $, $\alpha$はAckermann関数の逆関数

## 使い方

### 宣言

```cpp
UnionFind uf(要素数);
```

### クエリ

#### マージ

```cpp
uf.merge(a,b);
```

aが属する集合と,bが属する集合をマージする

#### 同一の集合か判定

```cpp
uf.isSame(a,b);
```

a,bが同一の集合に属しているか判定する

#### 集合サイズ

```cpp
uf.size(a);
```

aが属する集合の濃度を返す

#### 部分集合の集合

```cpp
uf.groups();
```

でvector{部分集合0, 部分集合1, ...}を得る.

## 実装

```cpp
class UnionFind {
public:
  int n;
  vector<int> p;
  UnionFind(int _n) : n(_n), p(_n, -1) {}
  bool merge(int a, int b) {
    int x = root(a), y = root(b);
    if (x == y)
      return false;
    if (-p[x] < -p[y])
      swap(x, y);
    p[x] += p[y], p[y] = x;
    return true;
  }
  bool isSame(int a, int b) {
    return root(a) == root(b);
  }
  int root(int a) {
    if (p[a] < 0)
      return a;
    return p[a] = root(p[a]);
  }
  int size(int a) {
    return -p[root(a)];
  }
  vector<vector<int>> groups() {
    vector<int> buf(n), size(n);
    for (int i = 0; i < n; i++) {
      buf[i] = root(i);
      size[buf[i]]++;
    }
    vector<vector<int>> res(n);
    for (int i = 0; i < n; i++)
      res[i].reserve(size[i]);
    for (int i = 0; i < n; i++)
      res[buf[i]].push_back(i);
    res.erase(remove_if(res.begin(), res.end(), [&](const vector<int> &v) { return v.empty(); }), res.end());
    return res;
  }
};
```

## Verify

//TODO
