# UVa 10170 - The Hotel with Infinite Rooms

**題目連結**：  
[ZeroJudge - e555](https://zerojudge.tw/ShowProblem?problemid=e555) 

**解題思路**：
- 酒店有無限多間房間，每一團客人的人數會比前一團多 1 人（1, 2, 3, 4, ...）
- 第 k 團客人會住 k 天
- 給定第一團人數 `S` 和總天數 `D`
- 找出第 D 天時，是第幾團客人在住（輸出該團的人數）

**遇到問題與解決**：
- 一開始題目邏輯看不太懂，容易把「團數」和「天數」搞混
- 曾嘗試用數學公式推導，但一直出錯
- 後來改用簡單的模擬方式（每次減去當前團的人數），雖然較暴力，但邏輯清晰且容易理解
- 之後學習如何使用公式

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
