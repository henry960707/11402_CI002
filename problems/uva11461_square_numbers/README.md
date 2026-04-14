# UVa 11461 - Square Numbers

**題目連結**：  
[ZeroJudge - d186](https://zerojudge.tw/ShowProblem?problemid=d186)  

**解題思路**：
- 給定兩個整數 a 和 b，計算區間 [a, b] 內有多少個**完全平方數**（1, 4, 9, 16, 25...）
- 利用數學特性：區間內完全平方數的個數 = floor(sqrt(b)) - floor(sqrt(a-1))
- 當 a = 1 時需特別處理（sqrt(0) = 0）

**遇到問題與解決**：
- 一開始使用 for 迴圈從 a 跑到 b 逐一判斷是否為完全平方數（較慢且容易 TLE）
- 後來理解可以直接對區間兩端取 floor(sqrt)，然後相減即可快速得到答案，大幅簡化程式碼

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int a, b;
    while (cin >> a >> b && (a != 0 || b != 0)) {
        // floor(sqrt(b)) - floor(sqrt(a-1))
        int ans = (int)floor(sqrt(b)) - (int)floor(sqrt(a - 1));
        cout << ans << "\n";
    }
    return 0;
}
```
**時間複雜度**：O(1)

**空間複雜度**：O(1)
