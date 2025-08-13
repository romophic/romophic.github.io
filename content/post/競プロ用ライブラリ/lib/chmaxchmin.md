+++
title = 'chmax/chmin'
date = 2024-07-29T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 使い方

`chmax(a,b)`で`a=max(a,b)`の更新をする. 更新があった場合はtrueを返す. `chmin`も同様:

## 実装

```cpp
template <class T>
bool chmax(T &a, const T &b) { return a < b ? a = b, 1 : 0; }
template <class T>
bool chmin(T &a, const T &b) { return a > b ? a = b, 1 : 0; }
```

## Depended on

- **[WarshallFloyd]({{< ref "post/競プロ用ライブラリ/lib/WarshallFloyd" >}})**
