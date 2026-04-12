# UVa 11150 - Cola

**題目連結**：  
[ZeroJudge - d189](https://zerojudge.tw/ShowProblem?problemid=d189) 

**解題思路**：
- 買 n 瓶可樂，喝完後會有 n 個空瓶
- 規則：3 個空瓶可以換 1 瓶可樂（喝完又多一個空瓶）
- 特殊情況：如果最後剩下 2 個空瓶，可以跟老闆借 1 個空瓶，湊成 3 個換 1 瓶（喝完後要把借的還回去）
- 目標是計算總共可以喝到幾瓶可樂

**遇到問題與解決**：
- 一開始以為只有單純的模擬（n/3 + n%3）即可，後來發現有「借瓶子」的情況
- 在模擬過程中，因為 `n` 會一直被更新，導致餘數加回去時出錯
- 解決方式：先用變數 `total` 記錄總喝到的瓶數，並在每次換瓶後正確更新 `n = n/3 + n%3`

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    while (cin >> n) {
        int total = n;          // 一開始買的瓶數
        int bottles = n;        // 目前的空瓶數
        
        while (bottles >= 3) {
            int new_cola = bottles / 3;     // 可以換的新可樂
            total += new_cola;
            bottles = new_cola + (bottles % 3);  // 換到的 + 剩下的空瓶
        }
        
        // 如果最後剩下 2 瓶，可以借 1 瓶再換
        if (bottles == 2) {
            total += 1;
        }
        
        cout << total << "\n";
    }
    return 0;
}
```
**時間複雜度**：O(log N) （每次空瓶數約變成原本的 1/3）

**空間複雜度**：O(1)
