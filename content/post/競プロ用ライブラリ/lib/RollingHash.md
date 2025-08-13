+++
title = 'RollingHash'
date = 2024-07-30T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

文字列が一致しているかの判定を定数時間で行う. ロリハ.

## 計算量

構築: $ O(n) $  
クエリ: $ O(1) $

## 使い方

### 構築

```cpp
RollingHash rh(s);
```

### ハッシュ

```cpp
rh.get(l,r)
```

$[l,r)$のハッシュを得る.

## 実装(WIP)

```cpp
struct RollingHash {
  vector<uint> hashed, power;
  const uint mod = 0x1fffffffffffffff, base = chrono::duration_cast<chrono::microseconds>(chrono::system_clock::now().time_since_epoch()).count() % mod;
  static constexpr uint mask(int a) { return (1ULL << a) - 1; }
  inline uint mul(uint a, uint b) const {
    __uint128_t ans = __uint128_t(a) * b;
    ans = (ans >> 61) + (ans & mod);
    if (ans >= mod)
      ans -= mod;
    return ans;
  }
  RollingHash(const string &s) {
    int n = s.size();
    hashed.assign(n + 1, 0);
    power.assign(n + 1, 0);
    power[0] = 1;
    for (int i = 0; i < n; i++) {
      power[i + 1] = mul(power[i], base);
      hashed[i + 1] = mul(hashed[i], base) + s[i];
      if (hashed[i + 1] >= mod)
        hashed[i + 1] -= mod;
    }
  }
  uint get(int l, int r) const {
    uint ret = hashed[r] + mod - mul(hashed[l], power[r - l]);
    if (ret >= mod)
      ret -= mod;
    return ret;
  }
  uint connect(uint h1, uint h2, int h2len) const {
    uint ret = mul(h1, power[h2len]) + h2;
    if (ret >= mod)
      ret -= mod;
    return ret;
  }
  void connect(const string &s) {
    int n = hashed.size() - 1, m = s.size();
    hashed.resize(n + m + 1);
    power.resize(n + m + 1);
    for (int i = n; i < n + m; i++) {
      power[i + 1] = mul(power[i], base);
      hashed[i + 1] = mul(hashed[i], base) + s[i - n];
      if (hashed[i + 1] >= mod)
        hashed[i + 1] -= mod;
    }
  }
  int LCP(const RollingHash &b, int l1, int r1, int l2, int r2) {
    int len = min(r1 - l1, r2 - l2);
    int low = -1, high = len + 1;
    while (high - low > 1) {
      int mid = (low + high) / 2;
      if (get(l1, l1 + mid) == b.get(l2, l2 + mid))
        low = mid;
      else
        high = mid;
    }
    return low;
  }
};

```

### Verify

//TODO
