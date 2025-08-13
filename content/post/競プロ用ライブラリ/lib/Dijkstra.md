+++
title = 'Dijkstra'
date = 2024-07-30T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

指定した頂点から他全てへの頂点への最短距離を求める. 負の辺が無いことを前提とする.

## 計算量

$ O(|E|\log|V|) $

## Depends

- **[DirectedGraph]({{< ref "post/競プロ用ライブラリ/lib/DirectedGraph" >}})**

## 使い方

### 宣言

```cpp
auto res = dijkstra(g,s);
```

`res[i]`で頂点sから頂点iの最短距離を得る.

## 実装

```cpp
vector<int> dijkstra(DirectedGraph &_g,int s) {
  vector<int> d(_g.n, INF);
  priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> que;
  d[s] = 0;
  que.push(make_pair(0, s));
  while (!que.empty()) {
    pair<int, int> p = que.top();
    que.pop();
    int v = p.second;
    if (d[v] < p.first)
      continue;
    for (auto e : _g.g[v]) {
      if (d[e.to] > d[v] + e.cost) {
        d[e.to] = d[v] + e.cost;
        que.push(make_pair(d[e.to], e.to));
      }
    }
  }
  return d;
}
```
