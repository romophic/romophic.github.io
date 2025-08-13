+++
title = 'Kruskal'
date = 2024-07-30T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

最小全域木を求める.

## 計算量

$ O(|E|\log|E|) $

## Depends

- **[UndirectedGraph]({{< ref "post/競プロ用ライブラリ/lib/UndirectedGraph" >}})**
- **[UnionFind]({{< ref "post/競プロ用ライブラリ/lib/UnionFind" >}})**

## 使い方

### 宣言

```cpp
auto res = kruskal(g);
```

`res`に最小全域木の[UndirectedGraph]({{< ref "post/競プロ用ライブラリ/lib/UndirectedGraph" >}})を得る.

## 実装

```cpp
UndirectedGraph kruskal(UndirectedGraph &_g) {
  UnionFind uf(_g.n);
  UndirectedGraph res(_g.n);
  sort(_g.g.begin(), _g.g.end(), [](auto &l, auto &r) { return l.cost < r.cost; });
  for (auto &[u, v, cost] : _g.g) {
    if (uf.merge(u, v)) {
      res.add(u,v,cost);
    }
  }
  return res;
}
```
