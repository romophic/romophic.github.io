+++
title = 'getGraphDiameter(木の直径を求める)'
date = 2024-07-30T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

木の直径を求める.

## 計算量

$ O(n) $

## Depends

- **[getFarthestVertex(最遠頂点を求める)]({{< ref "post/競プロ用ライブラリ/lib/getFarthestVertex" >}})**

## 使い方

### 宣言

```cpp
auto res = getGraphDiameter(g,s);
```

`res.cost`で直径を得る. `res.u`, `res.v`で直径を結ぶ頂点を得る.

## 実装

```cpp
struct getGraphDiameter_return {
  int u, v, cost;
};
getGraphDiameter_return getGraphDiameter(DirectedGraph &_g) {
  auto u = getFarthestVertex(_g, 0);
  auto v = getFarthestVertex(_g, u.v);
  return {u.v, v.v, v.cost};
}
```

### Verify👍
<https://atcoder.jp/contests/typical90/submissions/57586680>
