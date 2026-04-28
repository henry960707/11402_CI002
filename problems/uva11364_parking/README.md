# UVa 11364 - Parking

**題目連結**：  
[ZeroJudge - Parking](https://zerojudge.tw/ShowProblem?problemid=e511)  

**解題思路**：
- 車子停在某一位置，必須走到所有商店買東西後，再回到車上
- 目標是找出**最短的行走距離**
- 關鍵觀察：最優解一定是走到**最左邊的商店**和**最右邊的商店**，再回到車上
- 因此最短距離 = `(max_position - min_position) × 2`

**遇到問題與解決**：
- 一開始完全看不懂題目在問什麼
- 後來把題目畫成圖後，才發現不管車子停在哪裡，最短路徑都只需要來回於「最小位置」和「最大位置」之間
- 理解後直接使用 `max - min` 再乘以 2 即可得到答案

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    while (n--) {
        int p;
        cin >> p;
        
        int min_pos = INT_MAX;
        int max_pos = INT_MIN;
        
        for (int i = 0; i < p; i++) {
            int a;
            cin >> a;
            min_pos = min(min_pos, a);
            max_pos = max(max_pos, a);
        }
        
        int ans = 2 * (max_pos - min_pos);
        cout << ans << "\n";
    }
    return 0;
}
```
**時間複雜度**：O(P) （P 為商店數量）

**空間複雜度**：O(1)
