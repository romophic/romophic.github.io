+++
title = "Mo's Algorithm"
date = 2024-07-30T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

オフラインクエリかつクエリ区間の伸縮が簡単に出来る時高速に処理する.

## 計算量

$ O(Q\sqrt{N}) $

## 使い方(WIP)

## 実装(WIP)

```cpp
struct Mo { int width; vector<int> left, right, order; vector<bool> v; Mo(int N, int Q) : width((int)sqrt(N)), order(Q), v(N) {
    iota(begin(order), end(order), 0);
  }
  void add(int l, int r) {
    left.emplace_back(l);
    right.emplace_back(r);
  }
  void run(const auto &add, const auto &del, const auto &rem) {
    assert(left.size() == order.size());
    sort(begin(order), end(order), [&](int a, int b) {
      int ablock = left[a] / width, bblock = left[b] / width;
      if (ablock != bblock)
        return ablock < bblock;
      if (ablock & 1)
        return right[a] < right[b];
      return right[a] > right[b];
    });
    int nl = 0, nr = 0;
    auto push = [&](int idx) {
      v[idx].flip();
      if (v[idx])
        add(idx);
      else
        del(idx);
    };
    for (auto idx : order) {
      while (nl > left[idx])
        push(--nl);
      while (nr < right[idx])
        push(nr++);
      while (nl < left[idx])
        push(nl++);
      while (nr > right[idx])
        push(--nr);
      rem(idx);
    }
  }
};
```

### Verify

//TODO
