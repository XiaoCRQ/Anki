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

static inline void fast_io() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
}

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

template <class F> long long bsearch_first(long long l, long long r, F f) {
  long long L = l, R = r;
  while (L < R) {
    long long m = L + (R - L) / 2;
    if (f(m))
      R = m;
    else
      L = m + 1;
  }
  return L;
}

inline ll gcd(ll a, ll b) { return b == 0 ? a : gcd(b, a % b); }
inline ll lcm(ll a, ll b) { return a / gcd(a, b) * b; }

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
