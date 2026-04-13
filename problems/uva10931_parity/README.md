# UVa 10931 - Parity

**題目連結**：  
[ZeroJudge - a132](https://zerojudge.tw/ShowProblem?problemid=a132)  

**解題思路**：
- 將輸入的十進位數字轉換成二進位
- 計算二進位中 `1` 的個數（稱為 Parity）
- 輸出該數字的二進位表示，以及 `1` 的個數 mod 2 的結果
- 需注意：二進位輸出**不能有前導零**（Leading Zero）

**遇到問題與解決**：
- 第一次接觸 `bitset`，因此先找教學了解用法
- 一開始用迴圈手動計算 `1` 的數量，後來發現 `bitset` 內建 `.count()` 可以直接計算，程式更簡潔
- 處理二進位輸出時，需要找出最高位的 `1`，避免輸出前導零

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int a;
    while (cin >> a && a != 0) {
        bitset<32> b(a);
        
        // 計算 1 的個數
        int ones = b.count();
        
        // 找出最高位的 1（避免前導零）
        int highest = 31;
        while (highest >= 0 && b[highest] == 0) {
            highest--;
        }
        
        cout << "The parity of ";
        // 從最高位開始輸出二進位
        for (int i = highest; i >= 0; i--) {
            cout << b[i];
        }
        cout << " is " << ones << " (mod 2).\n";
    }
    return 0;
}
```
**時間複雜度**：O(1) （因為固定處理 32 位元）

**空間複雜度**：O(1)
