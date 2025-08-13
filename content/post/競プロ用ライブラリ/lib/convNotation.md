+++
title = '進数変換'
date = 2024-07-29T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

n進数からm進数に変換

## 使い方

```cpp
string res = convNotation(str,n,m);
```

## 実装

```cpp
string convNotation(const string &s, int from, int to) {
  int n = stoll(s, nullptr, from);
  if (n == 0)
    return "0";
  string result;
  while (n) {
    result += n % to < 10 ? '0' + n % to : 'A' + n % to - 10;
    n /= to;
  }
  if (s[0] == '-')
    result += '-';
  reverse(result.begin(), result.end());
  return result;
}
```
