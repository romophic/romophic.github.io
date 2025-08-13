+++
title = 'DirectedGraph'
date = 2024-07-30T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

重み付き有向グラフを扱う.

## 使い方

### 宣言

```cpp
DirectedGraph g(n);
```

### 重み付き有向パスの追加

```cpp
g.add(パス始点, パス終点, 重み);
```

## 実装

```cpp
class DirectedGraph {
public:
  struct Edge {
    int to, cost;
  };
  const int n;
  vector<vector<Edge>> g;
  DirectedGraph(int _n) : n(_n), g(_n) {}
  void add(int s, int t, int cost) {
    g[s].push_back({t, cost});
  }
};
```

## Depended on

- **[WarshallFloyd]({{< ref "post/競プロ用ライブラリ/lib/WarshallFloyd" >}})**
- **[Dijkstra]({{< ref "post/競プロ用ライブラリ/lib/Dijkstra" >}})**
- **[BellmanFord]({{< ref "post/競プロ用ライブラリ/lib/BellmanFord" >}})**
- **[TopologicalSort]({{< ref "post/競プロ用ライブラリ/lib/TopologicalSort" >}})**
- **[getFarthestVertex(最遠頂点を求める)]({{< ref "post/競プロ用ライブラリ/lib/getFarthestVertex" >}})**
