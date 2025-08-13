+++
title = 'UndirectedGraph'
date = 2024-07-30T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

重み付き無向グラフを扱う.

## 使い方

### 宣言

```cpp
UndirectedGraph g(n);
```

### 重み付き無向パスの追加

```cpp
g.add(頂点, 頂点, 重み);
```

## 実装

```cpp
class UndirectedGraph{
public:
  struct Edge {
    int u,v,cost;
  };
  const int n;
  vector<Edge> g;
  UndirectedGraph(int _n):n(_n){}
  void add(int u,int v,int cost){
    g.push_back({u,v,cost});
  }
};
```

## Depended on

- **[Kruskal]({{< ref "post/競プロ用ライブラリ/lib/Kruskal" >}})**
