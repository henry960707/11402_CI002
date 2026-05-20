# UVa 00100 - The 3n + 1 problem

**題目連結**：  
[ZeroJudge - c039](https://zerojudge.tw/ShowProblem?problemid=c039)

**解題思路**：
- 經典 Collatz 猜想模擬題（3n+1 問題）
- 給定區間 [a, b]，計算每個數字走到 1 所需的步數（cycle length）
- 找出區間內最大的步數後輸出

**遇到問題與解決**：
- 一開始想用遞迴寫，但一直寫不出來（容易 stack overflow）
- 後來改用 `while(true) + break` 的方式模擬循環，才成功通過

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int a, b;
    while (cin >> a >> b) {
        int m = min(a, b);
        int M = max(a, b);
        int max_length = 0;
        
        for (int i = m; i <= M; i++) {
            int k = i;
            int cycle = 0;
            while (true) {
                cycle++;
                if (k == 1) break;
                else if (k % 2 == 0) k = k / 2;
                else k = k * 3 + 1;
            }
            max_length = max(max_length, cycle);
        }
        cout << a << " " << b << " " << max_length << endl;
    }
    return 0;
```
**時間複雜度**：O((b - a) × log n)

**空間複雜度**：O(1)

**改良後的程式碼**

**解題思路**：
- 經典 Collatz 猜想模擬題
- 給定區間 [n1, n2]，找出區間內每個數字走到 1 所需的**最大步數**（cycle length）
- 使用**記憶化搜尋（DP）**優化，避免重複計算相同的數字

**程式碼（優化版）**：

```cpp
#include <bits/stdc++.h>
using namespace std;

const int MAXN = 1000005;
int dp[MAXN];

int cal(long long x) {
    if (x == 1) return 1;
    if (x < MAXN && dp[x] != 0) return dp[x];
    
    int step = 1 + (x % 2 == 0 ? cal(x / 2) : cal(3 * x + 1));
    if (x < MAXN) dp[x] = step;
    return step;
}

int main() {
    memset(dp, 0, sizeof(dp));
    long long n1, n2;
    while (cin >> n1 >> n2) {
        long long m = min(n1, n2);
        long long M = max(n1, n2);
        long long ans = 0;
        for (long long i = m; i <= M; i++) {
            ans = max(ans, (long long)cal(i));
        }
        cout << n1 << " " << n2 << " " << ans << "\n";
    }
    return 0;
}
```
**時間複雜度**：O(N + 計算過的數字)

**空間複雜度**：O(MAXN)
