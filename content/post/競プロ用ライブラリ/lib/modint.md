+++
title = 'ModInt'
date = 2024-08-13T21:00:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming",
]
+++
## 用途

自動でModを取る

## 計算量

$O(1)$

## 宣言

```cpp
ModInt<1000000007> mi = 0;
```

## 実装

```cpp
template <int Mod>
class ModInt {
public:
  int n;
  constexpr ModInt(const int x = 0) noexcept : n((x % Mod + Mod) % Mod) {}
  constexpr int &value() noexcept { return n; }
  constexpr const int &value() const noexcept { return n; }
  constexpr ModInt operator+(const ModInt rhs) const noexcept { return ModInt(*this) += rhs; }
  constexpr ModInt operator-(const ModInt rhs) const noexcept {    return ModInt(*this) -= rhs;  }
  constexpr ModInt operator*(const ModInt rhs) const noexcept {    return ModInt(*this) *= rhs;  }
  constexpr ModInt operator/(const ModInt rhs) const noexcept {    return ModInt(*this) /= rhs;  }
  constexpr ModInt &operator+=(const ModInt rhs) noexcept {
    n += rhs.n;
    if (n >= Mod)
      n -= Mod;
    return *this;
  }
  constexpr ModInt &operator-=(const ModInt rhs) noexcept {
    if (n < rhs.n)
      n += Mod;
    n -= rhs.n;
    return *this;
  }
  constexpr ModInt &operator*=(const ModInt rhs) noexcept {
    n = n * rhs.n % Mod;
    return *this;
  }
  constexpr ModInt &operator/=(ModInt rhs) noexcept {
    int exp = Mod - 2;
    while (exp) {
      if (exp % 2)
        *this *= rhs;
      rhs *= rhs;
      exp /= 2;
    }
    return *this;
  }
  friend std::istream &operator>>(std::istream &_istr, ModInt &rhs) {
    _istr >> rhs.n;
    rhs.n = (rhs.n % Mod + Mod) % Mod;
    return _istr;
  }
  friend std::ostream &operator<<(std::ostream &_ostr, const ModInt &rhs) {
    return _ostr << rhs.n;
  }
};
```

## Verify

//TODO
