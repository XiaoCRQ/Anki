# Anki卡组下载目录

- [英语单词](https://github.com/xiaoCRQ/Anki/raw/refs/heads/main/English/英语单词.apkg)
- [英语词组](https://github.com/xiaoCRQ/Anki/raw/refs/heads/main/English/英语词组.apkg)
- [【英语兔】40篇短文](https://github.com/xiaoCRQ/Anki/raw/refs/heads/main/English/【英语兔】40篇短文.apkg)

![image](./Preview/English.png)

```cpp
#include <bits/stdc++.h>
#define PB push_back
#define MP make_pair
#define F first
#define S second
#define ALL(x) (x).begin(), (x).end()
#define SZ(x) ((int)(x).size())
#define REP(i, n) for (int i = 0; i < (int)(n); i++)
#define FOR(i, a, b) for (int i = (a); i <= (b); i++)
#define FORD(i, a, b) for (int i = (a); i >= (b); i--)
#define RESET(a, b) memset(a, b, sizeof(a))
#define array_two(value, n, m, type)                                           \
  vector<vector<type>> value(n, vector<type>(m, 0))

using namespace std;
typedef long long ll;
typedef unsigned long long ull;
typedef pair<int, int> pii;
typedef pair<int, string> pis;
typedef pair<ll, ll> pll;
typedef vector<int> vi;
typedef vector<ll> vl;
typedef vector<pii> vpi;
typedef vector<pis> vpis;

const int INF = 1e9;
const ll LINF = 1e18;
const double PI = acos(-1.0);
const int MOD = 1e9 + 7;
const int MAXN = 1e6 + 5;
const int dx4[4] = {1, -1, 0, 0};
const int dy4[4] = {0, 0, 1, -1};
const int dx8[8] = {1, 1, 1, 0, 0, -1, -1, -1};
const int dy8[8] = {1, 0, -1, 1, -1, 1, 0, -1};

static inline void fast_io() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
}

// ===================== 函数模板 =====================
inline ll gcd(ll a, ll b) { return b == 0 ? a : gcd(b, a % b); }
inline ll lcm(ll a, ll b) { return a / gcd(a, b) * b; }

// 快速加法防止溢出 (适合模数较大时)
inline ll qadd(ll a, ll b, ll mod = MOD) {
  a %= mod;
  b %= mod;
  ll r = a + b;
  return (r >= mod ? r - mod : r);
}

// 快速乘法防止溢出 (适合 a,b <= 1e18)
inline ll qmul(ll a, ll b, ll mod = MOD) {
  __int128 r = (__int128)a * b;
  return (ll)(r % mod);
}

// 快速幂防止溢出 (适合 a,b <= 1e18)
inline ll qpow(ll a, ll b, ll mod = MOD) {
  ll res = 1;
  a %= mod;
  while (b) {
    if (b & 1)
      res = res * a % mod;
    a = a * a % mod;
    b >>= 1;
  }
  return res;
}

// 二分查找
template <class F> ll bsearch_first(ll l, ll r, F f) {
  ll L = l, R = r;
  while (L < R) {
    ll m = L + (R - L) / 2;
    if (f(m))
      R = m;
    else
      L = m + 1;
  }
  return L;
}

// --- 前缀和/差分 ---
// 构建前缀和
template <typename T> vector<T> prefix_sum(const vector<T> &a) {
  ll n = a.size();
  vector<T> p(n + 1);
  FOR(i, 1, n) p[i] = p[i - 1] + a[i - 1];
  return p;
}

// O(1) 查询区间和 [l, r] (0-index)
template <typename T> inline T range_sum(const vector<T> &p, int l, int r) {
  return p[r + 1] - p[l];
}

// --- 快速最小值最大值 ---
template <typename T> inline T max3(T a, T b, T c) { return max(a, max(b, c)); }
template <typename T> inline T min3(T a, T b, T c) { return min(a, min(b, c)); }

// ===================== 高精度 BigInteger =====================
struct BigInt {
  static const int base = 1000000000; // 1e9
  vector<int> s;                      // 低位在前

  BigInt(long long num = 0) { *this = num; }

  BigInt &operator=(long long num) {
    s.clear();
    if (num == 0) {
      s.push_back(0);
      return *this;
    }
    while (num > 0) {
      s.push_back(num % base);
      num /= base;
    }
    return *this;
  }

  BigInt(const string &str) { *this = str; }

  BigInt &operator=(const string &str) {
    s.clear();
    int len = str.size();
    for (int i = len; i > 0; i -= 9) {
      int x = 0;
      int l = max(0, i - 9);
      for (int j = l; j < i; j++)
        x = x * 10 + (str[j] - '0');
      s.push_back(x);
    }
    trim();
    return *this;
  }

  // 去除前导零
  void trim() {
    while (s.size() > 1 && s.back() == 0)
      s.pop_back();
  }

  // 比较
  bool operator<(const BigInt &b) const {
    if (s.size() != b.s.size())
      return s.size() < b.s.size();
    for (int i = s.size() - 1; i >= 0; i--)
      if (s[i] != b.s[i])
        return s[i] < b.s[i];
    return false;
  }
  bool operator>(const BigInt &b) const { return b < *this; }
  bool operator<=(const BigInt &b) const { return !(b < *this); }
  bool operator>=(const BigInt &b) const { return !(*this < b); }
  bool operator==(const BigInt &b) const { return s == b.s; }
  bool operator!=(const BigInt &b) const { return !(*this == b); }

  // 加法
  BigInt operator+(const BigInt &b) const {
    BigInt c;
    c.s.clear();
    int n = max(s.size(), b.s.size());
    long long carry = 0;
    for (int i = 0; i < n; i++) {
      long long x = carry;
      if (i < (int)s.size())
        x += s[i];
      if (i < (int)b.s.size())
        x += b.s[i];
      c.s.push_back(x % base);
      carry = x / base;
    }
    if (carry)
      c.s.push_back(carry);
    return c;
  }

  // 减法（假设 *this >= b）
  BigInt operator-(const BigInt &b) const {
    BigInt c;
    c.s.clear();
    long long carry = 0;
    for (int i = 0; i < (int)s.size(); i++) {
      long long x = s[i] - carry - (i < (int)b.s.size() ? b.s[i] : 0);
      if (x < 0)
        x += base, carry = 1;
      else
        carry = 0;
      c.s.push_back(x);
    }
    c.trim();
    return c;
  }

  // 高精度 × int
  BigInt operator*(long long m) const {
    BigInt c;
    c.s.clear();
    long long carry = 0;
    for (int i = 0; i < (int)s.size(); i++) {
      __int128 x = (__int128)s[i] * m + carry;
      c.s.push_back((long long)(x % base));
      carry = (long long)(x / base);
    }
    if (carry)
      c.s.push_back(carry);
    return c;
  }

  // 高精度 × 高精度
  BigInt operator*(const BigInt &b) const {
    BigInt c;
    c.s.assign(s.size() + b.s.size(), 0);

    for (int i = 0; i < (int)s.size(); i++) {
      long long carry = 0;
      for (int j = 0; j < (int)b.s.size() || carry; j++) {
        __int128 x = c.s[i + j] +
                     (__int128)s[i] * (j < (int)b.s.size() ? b.s[j] : 0) +
                     carry;
        c.s[i + j] = (long long)(x % base);
        carry = (long long)(x / base);
      }
    }
    c.trim();
    return c;
  }

  // 输出
  friend ostream &operator<<(ostream &os, const BigInt &x) {
    os << x.s.back();
    for (int i = x.s.size() - 2; i >= 0; i--)
      os << setw(9) << setfill('0') << x.s[i];
    return os;
  }
};

istream &operator>>(istream &is, BigInt &x) {
  string s;
  is >> s;
  x = BigInt(s);
  return is;
}

void solve() {}

int main() {
  fast_io();

  ll T = 1;
  // if (!(cin >> T)) return 0;

  while (T--) {
    solve();
  }
  return 0;
}
```
