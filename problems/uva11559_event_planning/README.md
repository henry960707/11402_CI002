# UVa 11559 - Event Planning

**題目連結**：  
[ZeroJudge - Event Planning](https://onlinejudge.org/external/115/11559.pdf) 

**解題思路**：
- 給定參加人數 `N`、預算 `B`、旅館數量 `H`、週末數 `W`
- 每間旅館有單人價格 `p`，以及 W 個週末各自的空房間數
- 目標是找出**總花費不超過預算**，且**空房間足夠**的最便宜方案
- 若沒有任何符合條件的方案，輸出 `stay home`

**遇到問題與解決**：
- 一開始想用 `stringstream` 處理輸入，寫得比較複雜
- 後來發現這題輸入格式固定，直接用 `cin` 依序讀取即可，大幅簡化程式碼
- 也提醒自己：`cin` 後接 `getline` 時要記得加上 `cin.ignore()`（雖然這題沒用到）

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, b, h, w;
    while (cin >> n >> b >> h >> w) {
        int min_cost = INT_MAX;        // 設一個極大值
        
        for (int i = 0; i < h; i++) {
            int p;
            cin >> p;                  // 這間旅館的單人價格
            
            for (int j = 0; j < w; j++) {
                int a;
                cin >> a;              // 這個週末的空房間數
                
                // 如果空房夠住，且總花費不超過預算
                if (a >= n && (long long)p * n <= b) {
                    min_cost = min(min_cost, p * n);
                }
            }
        }
        
        if (min_cost == INT_MAX || min_cost > b)
            cout << "stay home\n";
        else
            cout << min_cost << "\n";
    }
    return 0;
}
```
**時間複雜度**：O(H × W)

**空間複雜度**：O(1)
