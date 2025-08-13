+++
title = '累積和(1D,2D,3D)'
date = 2024-07-29T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

累積和を取り, 連続部分, 矩形, 長方形状の和を$O(1)$で求める.

## 計算量

構築: $O(n)$  
クエリ: $O(1)$

### 初期化

```cpp
Cumulate1D c1(vector);
Cumulate2D c2(matrix);
Cumulate3D c3(tensor);
```

`vector`はvector, `matrix`はvector<vector>, `tensor`はvector<vector<vector>>.

### クエリ

```cpp
c1.query(x1,x2);
c2.query(y1,x1,y2,x2);
c3.query(z1,y1,x1,z2,y2,x2);
```

c1であれば区間$[x1,x2)$の和を返す.

## 実装

```cpp
template <class T>
class Cumulate1D {
  vector<T> sum;
public:
  Cumulate1D(const vector<T> &_g) : sum(_g.size() + 1) {
    for (int i = 0; i < _g.size(); i++)
      sum[i + 1] = sum[i] + _g[i];
  }
  T query(int s, int e) { return sum[e] - sum[s]; };
};
template <class T>
class Cumulate2D {
  vector<vector<T>> sum;
public:
  Cumulate2D(const vector<vector<T>> &_g) : sum(_g.size() + 1, vector<T>(_g[0].size() + 1)) {
    for (int y = 0; y < _g.size(); y++)
      for (int x = 0; x < _g[0].size(); x++)
        sum[y + 1][x + 1] = sum[y][x + 1] + sum[y + 1][x] - sum[y][x] + _g[y][x];
  }
  T query(int y1, int x1, int y2, int x2) { return sum[y2][x2] - sum[y1][x2] - sum[y2][x1] + sum[y1][x1]; }
};
template <class T>
class Cumulate3D {
  vector<vector<vector<T>>> sum;
public:
  Cumulate3D(const vector<vector<vector<T>>> &_g) : sum(_g.size() + 1, vector<vector<T>>(_g[0].size() + 1, vector<T>(_g[0][0].size() + 1))) {
    for (int z = 0; z < _g.size(); z++)
      for (int y = 0; y < _g[0].size(); y++)
        for (int x = 0; x < _g[0][0].size(); x++)
          sum[z + 1][y + 1][x + 1] = _g[z][y][x] + sum[z + 1][y + 1][x] + sum[z + 1][y][x + 1] + sum[z][y + 1][x + 1] - sum[z + 1][y][x] - sum[z][y + 1][x] - sum[z][y][x + 1] + sum[z][y][x];
  }
  T query(int z1, int y1, int x1, int z2, int y2, int x2) { return sum[z2][y2][x2] - sum[z2][y2][x1] - sum[z2][y1][x2] - sum[z1][y2][x2] + sum[z2][y1][x1] + sum[z1][y2][x1] + sum[z1][y1][x2] - sum[z1][y1][x1]; }
};
```
