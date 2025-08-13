+++
title = 'TopologicalSort'
date = 2024-07-30T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

有向非巡回グラフ(DAG)の頂点を線形順序に並べる.

## 計算量

$ O(V + E) $

## Depends

- **[DirectedGraph]({{< ref "post/競プロ用ライブラリ/lib/DirectedGraph" >}})**

## 使い方

### 宣言

```cpp
auto res = topologicalSord(g);
```

`res`で線形順序に並べられた頂点を得る.

## 実装

```cpp
vector<int> topologicalSort(DirectedGraph &_g) {
  vector<int> d, ind(_g.n);
  for (int i = 0; i < _g.n; i++)
    for (auto e : _g.g[i])
      ind[e.to]++;
  queue<int> que;
  for (int i = 0; i < _g.n; i++)
    if (ind[i] == 0)
      que.push(i);
  while (!que.empty()) {
    int now = que.front();
    d.push_back(now);
    que.pop();
    for (auto e : _g.g[now]) {
      ind[e.to]--;
      if (ind[e.to] == 0)
        que.push(e.to);
    }
  }
  return d;
}
```
