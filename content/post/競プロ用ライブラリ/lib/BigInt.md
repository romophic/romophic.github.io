+++
title = 'BigInt'
date = 2024-07-30T22:01:37+09:00
description = "romophic-library"
categories = [
  "c++",
  "competitive programming"
]
+++
## 用途

多倍長整数.

## 使い方

### 宣言

```cpp
BigInt a(10);
```

`a.to_string()`で`std::string`に変換された数値を得る.

## 実装

```cpp
class BigInt {
public:
  BigInt() : sign(1) {}
  BigInt(const string &s) {
    int pos = 0;
    if (s[0] == '-') {
      sign = -1;
      pos = 1;
    } else
      sign = 1;
    for (int i = s.size(); i > pos; i -= base_digits) {
      int end = i;
      int start = max(pos, i - base_digits);
      int num = stoll(s.substr(start, end - start));
      digits.push_back(num);
    }
    trim();
  }
  BigInt(long long v) {
    if (v < 0) {
      sign = -1;
      v = -v;
    } else
      sign = 1;
    while (v > 0) {
      digits.push_back(v % base);
      v /= base;
    }
  }
  BigInt operator+(const BigInt &other) const {
    if (sign == other.sign) {
      BigInt result = *this;
      result.add(other);
      return result;
    } else
      return *this - (-other);
  }
  BigInt operator-(const BigInt &other) const {
    if (sign == other.sign)
      if (abs() >= other.abs()) {
        BigInt result = *this;
        result.subtract(other);
        return result;
      } else {
        BigInt result = other;
        result.subtract(*this);
        result.sign = -result.sign;
        return result;
      }
    else
      return *this + (-other);
  }
  BigInt operator*(const BigInt &other) const {
    BigInt result;
    result.digits.resize(digits.size() + other.digits.size());
    result.sign = sign * other.sign;
    for (size_t i = 0; i < digits.size(); ++i) {
      long long carry = 0;
      for (size_t j = 0; j < other.digits.size() || carry > 0; ++j) {
        long long cur = result.digits[i + j] + carry + digits[i] * 1LL * (j < other.digits.size() ? other.digits[j] : 0);
        carry = cur / base;
        result.digits[i + j] = cur % base;
      }
    }
    result.trim();
    return result;
  }
  BigInt &operator++() {
    *this = *this + BigInt(1);
    return *this;
  }
  BigInt operator++(signed) {
    BigInt temp = *this;
    ++(*this);
    return temp;
  }
  BigInt &operator--() {
    *this = *this - BigInt(1);
    return *this;
  }
  BigInt operator--(signed) {
    BigInt temp = *this;
    --(*this);
    return temp;
  }
  BigInt operator-() const {
    BigInt result = *this;
    if (!is_zero())
      result.sign = -result.sign;
    return result;
  }
  strong_ordering operator<=>(const BigInt &other) const {
    if (sign != other.sign)
      return sign <=> other.sign;
    return (sign == 1) ? abs_compare(other) : other.abs_compare(*this);
  }
  bool operator==(const BigInt &other) const { return (*this <=> other) == 0; }
  string to_string() const {
    string result = (sign == -1 ? "-" : "") + (digits.empty() ? "0" : std::to_string(digits.back()));
    for (int i = digits.size() - 2; i >= 0; --i)
      result += string(base_digits - std::to_string(digits[i]).length(), '0') + std::to_string(digits[i]);
    return result;
  }

private:
  vector<int> digits;
  int sign;
  static const int base = 1000000000000000000LL;
  static const int base_digits = 18;
  void add(const BigInt &other) {
    int carry = 0;
    for (size_t i = 0; i < other.digits.size() || carry > 0; ++i) {
      if (i == digits.size())
        digits.push_back(0);
      digits[i] += carry + (i < other.digits.size() ? other.digits[i] : 0);
      carry = digits[i] >= base;
      if (carry)
        digits[i] -= base;
    }
  }
  void subtract(const BigInt &other) {
    int borrow = 0;
    for (size_t i = 0; i < other.digits.size() || borrow > 0; ++i) {
      digits[i] -= borrow + (i < other.digits.size() ? other.digits[i] : 0);
      borrow = digits[i] < 0;
      if (borrow)
        digits[i] += base;
    }
    trim();
  }
  strong_ordering abs_compare(const BigInt &other) const {
    if (digits.size() != other.digits.size())
      return digits.size() <=> other.digits.size();
    for (int i = digits.size() - 1; i >= 0; --i)
      if (digits[i] != other.digits[i])
        return digits[i] <=> other.digits[i];
    return strong_ordering::equal;
  }
  BigInt abs() const {
    BigInt result = *this;
    result.sign = 1;
    return result;
  }
  bool is_zero() const { return digits.empty(); }
  void trim() {
    while (!digits.empty() && digits.back() == 0)
      digits.pop_back();
    if (digits.empty())
      sign = 1;
  }
};
```
