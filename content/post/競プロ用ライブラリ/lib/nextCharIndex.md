+++
title = '文字列のith以降で文字cが出現する最小のindex'
date = 2024-07-30T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

文字列の`i`th以降で文字cが出現する最小のindexを返す. 存在しなければ文字列長を返す.

## 計算量

$ O(n) $

## 使い方

```cpp
auto res = nextCharIndex(s);
```

`s`は`std::string`, `res[i][j]`で`i`th以降(`i`thも含む)で文字`c`が出現するindexを得る.

## 実装

```cpp
vector<vector<int>> nextCharIndex(string &_s) {
  vector m(_s.size() + 1, vector<int>(26));
  for (int i = 0; i < 26; i++)
    m[_s.size()][i] = _s.size();
  for (int i = _s.size() - 1; i >= 0; i--)
    for (int j = 0; j < 26; j++)
      if (_s[i] - 'a' == j)
        m[i][j] = i;
      else
        m[i][j] = m[i + 1][j];
  return m;
}
```

### Verify👍
<https://atcoder.jp/contests/typical90/submissions/57632650>
