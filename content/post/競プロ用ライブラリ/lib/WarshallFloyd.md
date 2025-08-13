+++
title = 'WarshallFloyd'
date = 2024-07-30T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

重み付き有向グラフの全頂点ペアの最短距離を求める. 負の閉路が無いことを前提とする.

## 計算量

$ O(n^3) $

## Depends

- **[DirectedGraph]({{< ref "post/競プロ用ライブラリ/lib/DirectedGraph" >}})**
- **[chmax/chmin]({{< ref "post/競プロ用ライブラリ/lib/chmaxchmin" >}})**

## 使い方

```cpp
auto res = warshallfloyd(g);
```

`res.dist[s][e]`で頂点sからeの距離, `res.next[s][e]`で頂点sからeへ最短で到達するために次に到達すべき頂点を得る.

## 実装

```cpp
struct warshallfloyd_return {
  vector<vector<int>> dist, next;
};
warshallfloyd_return warshallfloyd(DirectedGraph &_g) {
  vector<vector<int>> dist(_g.n, vector<int>(_g.n, INF)), next(_g.n, vector<int>(_g.n, INF));
  for (int i = 0; i < _g.n; i++)
    dist[i][i] = 0;
  for (int i = 0; i < _g.n; i++)
    for (int j = 0; j < _g.n; j++)
      next[i][j] = j;
  for (int i = 0; i < _g.n; i++)
    for (auto &j : _g.g[i])
      chmin(dist[i][j.to], j.cost);
  for (int k = 0; k < _g.n; k++)
    for (int i = 0; i < _g.n; i++)
      for (int j = 0; j < _g.n; j++)
        if (chmin(dist[i][j], dist[i][k] + dist[k][j]))
          next[i][j] = next[i][k];
  return {dist, next};
}
```
