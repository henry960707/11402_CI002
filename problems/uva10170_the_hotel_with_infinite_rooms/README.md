# UVa 10170 - The Hotel with Infinite Rooms

**題目連結**：  
[ZeroJudge - e555](https://zerojudge.tw/ShowProblem?problemid=e555) 

**解題思路**：
- 酒店有無限多間房間，第 k 團客人會住 k 天，且每團人數比前一團多 1 人
- 給定第一團人數 `S` 和總天數 `D`
- 找出第 D 天時，是第幾團客人在住（輸出該團的人數）

**數學優化解法（二分搜尋）**：
- 從第 S 團到第 x 團的總天數 = (S + x) * (x - S + 1) / 2
- 使用二分搜尋找出最小的 x，使得總天數 >= D
- 這比線性模擬更快，尤其當 D 很大時

**遇到問題與解決**：
- 一開始用線性模擬寫法，雖然正確但較慢
- 後來改用二分搜尋，透過設定左右界（L = S, R = 一個足夠大的數）快速找到答案
- 也練習了如何用二分搜尋處理「最小滿足條件」的問題

**程式碼**：

```cpp
#include <iostream>
using namespace std;

int main() {
    long long s, d;
    while (cin >> s >> d) {
        while (true) {
            d -= s;
            if (d <= 0) {
                cout << s << "\n";
                break;
            } else {
                s++;
            }
        }
    }
    return 0;
}
```

**時間複雜度**：O(√D) （最壞情況下需模擬到第 √(2D) 團左右）

**空間複雜度**：O(1)

**程式碼（二分搜尋版本）**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    long long s, d;
    while (cin >> s >> d) {
        long long L = s, R = 50000000LL, ans = s;
        while (L <= R) {
            long long mid = L + (R - L) / 2;
            long long total_day = (s + mid) * (mid - s + 1) / 2;
            if (total_day >= d) {
                ans = mid;
                R = mid - 1;
            } else {
                L = mid + 1;
            }
        }
        cout << ans << "\n";
    }
    return 0;
}
```

**時間複雜度**：O(log D)

**空間複雜度**：O(1)
