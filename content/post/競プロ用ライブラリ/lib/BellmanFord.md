+++
title = 'BellmanFord'
date = 2024-07-30T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

指定した始点から終点への最短距離を求める. 負の辺でもOK. 負の閉路を検出可能.

## 計算量

$ O(|V||E|) $

## Depends

- **[DirectedGraph]({{< ref "post/競プロ用ライブラリ/lib/DirectedGraph" >}})**

## 使い方

### 宣言

```cpp
auto res = bellmanford(g, s, e);
```

`res.path`でsからeへの最短パスを得る.  
`res.distances`でｓから各頂点への最短距離を得る. 経路が存在しなければINF.  
`res.hascycle`でgに負の閉路があるかを得る.

## 実装

```cpp
struct bellmanford_return {
  vector<int> path, distances;
  bool hascycle;
};
bellmanford_return bellmanford(DirectedGraph &_g,int s, int e) {
  vector<int> cnt(_g.g.size()), dist(_g.g.size(), INF), path, p(_g.g.size(), -1);
  vector<bool> inque(_g.g.size());
  queue<int> q;
  dist[s] = 0;
  q.push(s);
  inque[s] = true;
  while (!q.empty()) {
    const int from = q.front();
    q.pop();
    inque[from] = false;
    for (const auto &edge : g[from]) {
      const int d = (dist[from] + edge.cost);
      if (d < dist[edge.to]) {
        dist[edge.to] = d;
        p[edge.to] = from;
        if (!inque[edge.to]) {
          q.push(edge.to);
          inque[edge.to] = true;
          ++cnt[edge.to];
          if ((int)g.size() < cnt[edge.to])
            return {vector<int>(), vector<int>(), true};
        }
      }
    }
  }
  if (dist[e] != INF) {
    for (int i = e; i != -1; i = p[i])
      path.push_back(i);
    reverse(path.begin(), path.end());
  }
  return {path, dist, false};
}
```
