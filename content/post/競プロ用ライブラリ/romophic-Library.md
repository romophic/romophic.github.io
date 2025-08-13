+++
title = 'romophic-Library'
date = 2024-07-30T22:01:37+09:00
description = "Library for Competitive Programming"
categories = [
  "c++",
  "competitive programming",
  "heuristic"
]
aliases = [
  "競プロライブラリ",
  "競プロ用ライブラリ"
]
+++
元々は[github.com/romophic/Compro](https://github.com/romophic/Compro)にまとめていたライブラリを適当にまとめたものです. 盆栽を勧められたので始めました.  
前提テンプレート:

```cpp
#pragma GCC optimize("Ofast")
#include <bits/stdc++.h>
#define int long long
#define double long double
#define uint unsigned long long
#define int128 __int128
#define uint128 unsigned __int128
using namespace std;
constexpr int INF = 1LL << 60;
template <class T>
bool chmax(T &a, const T &b) { return a < b ? a = b, 1 : 0; }
template <class T>
bool chmin(T &a, const T &b) { return a > b ? a = b, 1 : 0; }
```

## アルゴリズム

### グラフ

- **[DirectedGraph]({{< ref "post/競プロ用ライブラリ/lib/DirectedGraph" >}})**
  - **[WarshallFloyd]({{< ref "post/競プロ用ライブラリ/lib/WarshallFloyd" >}})**
  - **[Dijkstra]({{< ref "post/競プロ用ライブラリ/lib/Dijkstra" >}})**
  - **[BellmanFord]({{< ref "post/競プロ用ライブラリ/lib/BellmanFord" >}})**
  - **[TopologicalSort]({{< ref "post/競プロ用ライブラリ/lib/TopologicalSort" >}})**
  - **[getFarthestVertex(最遠頂点を求める)]({{< ref "post/競プロ用ライブラリ/lib/getFarthestVertex" >}})**
  - **[getGraphDiameter(木の頂点を求める)]({{< ref "post/競プロ用ライブラリ/lib/getGraphDiameter" >}})**
- **[UndirectedGraph]({{< ref "post/競プロ用ライブラリ/lib/UndirectedGraph" >}})**
  - **[Kruskal]({{< ref "post/競プロ用ライブラリ/lib/Kruskal" >}})**
- **[強連結成分分解(SCC)]({{< ref "post/競プロ用ライブラリ/lib/SCC" >}})**

### データ構造

- **[UnionFind]({{< ref "post/競プロ用ライブラリ/lib/UnionFind" >}})**
- **[WeightedUnionFind]({{< ref "post/競プロ用ライブラリ/lib/WeightedUnionFind" >}})**
- **[SegmentTree]({{< ref "post/競プロ用ライブラリ/lib/SegmentTree" >}})**
- **[LazySegmentTree]({{< ref "post/競プロ用ライブラリ/lib/LazySegmentTree" >}})**

### 数学

- **[素因数分解]({{< ref "post/競プロ用ライブラリ/lib/素因数分解" >}})**
- **[約数列挙]({{< ref "post/競プロ用ライブラリ/lib/約数列挙" >}})**
- **[繰り返し二乗法]({{< ref "post/競プロ用ライブラリ/lib/繰り返し二乗法" >}})**
- **[ModInt]({{< ref "post/競プロ用ライブラリ/lib/ModInt" >}})**
- **[進数変換]({{< ref "post/競プロ用ライブラリ/lib/convNotation" >}})**
- **[Euler's totient function]({{< ref "post/競プロ用ライブラリ/lib/Euler's totient function" >}})**
- **[多倍長整数]({{< ref "post/競プロ用ライブラリ/lib/BigInt" >}})**

### 文字列

- **[文字列のith以降で文字cが出現する最小のindex]({{< ref "post/競プロ用ライブラリ/lib/nextCharIndex" >}})**
- **[RollingHash]({{< ref "post/競プロ用ライブラリ/lib/RollingHash" >}})**
- **[SuffixArray]({{< ref "post/競プロ用ライブラリ/lib/SuffixArray" >}})**

### その他

- **[二分探索]({{< ref "post/競プロ用ライブラリ/lib/二分探索" >}})**
- **[chmax/chmin]({{< ref "post/競プロ用ライブラリ/lib/chmaxchmin" >}})**
- **[STLデータ構造にそのままcin/coutするやつ]({{< ref "post/STLデータ構造をistream,ostream-compatibleにする" >}})**
- **[入出力高速化]({{< ref "post/競プロ用ライブラリ/lib/入出力高速化" >}})**
- **[Mo's Algorithm]({{< ref "post/競プロ用ライブラリ/lib/Mo" >}})**
- **[累積和(1D,2D,3D)]({{< ref "post/競プロ用ライブラリ/lib/Cumulate" >}})**
- **[インデックス変換(1D,2D,3D)]({{< ref "post/競プロ用ライブラリ/lib/ConvIndex" >}})**

## ヒューリスティック

- **[SimulatedAnnealing]({{< ref "post/競プロ用ライブラリ/lib/SimulatedAnnealing" >}})**

## お世話になったライブラリ

自由に使って良いとあるところからのみ参考にさせて頂いて実装しました.  &emsp;$ \mathit{thank\ you...} $

- <https://ei1333.github.io/luzhiled>
- <https://github.com/tatyam-prime/kyopro_library>
