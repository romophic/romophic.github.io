+++
title = 'インデックス変換(2D,3D)'
date = 2024-07-29T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 使い方

`ConvIndex2.conv(y,x)`で$(x,y)$を一次元のインデックスに変換する.
`ConvIndex3.conv(z,y,x)`で$(x,y,z)$を一次元のインデックスに変換する.

## 実装

```cpp
class ConvIndex2 {
  int y, x;
public:
  ConvIndex2(int _y, int _x) : y(_y), x(_x) {}
  int conv(int _y, int _x) { return _y * x + _x; }
  int prod() { return y * x; }
};
class ConvIndex3 {
  int z, y, x;
public:
  ConvIndex3(int _z, int _y, int _x) : z(_z), y(_y), x(_x) {}
  int conv(int _z, int _y, int _x) { return _z * y * x + _y * x + _x; }
  int prod() { return z * y * x; }
};
```
