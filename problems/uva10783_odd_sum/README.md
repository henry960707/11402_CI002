# UVa 10783 - Odd Sum

**題目連結**：  
[ZeroJudge - c022](https://zerojudge.tw/ShowProblem?problemid=c022) 

**解題思路**：
- 給定多筆測資，每筆測資有兩個數字 a 和 b
- 計算區間 [min(a,b), max(a,b)] 內所有**奇數**的總和
- 輸出格式為 `Case X: 答案`

**遇到問題與解決**：
- 一開始不太懂 for 迴圈的邊界條件（<= 或 <），導致區間邊緣的奇數有時會少算
- 後來使用 `min()` 和 `max()` 先確定真正的區間範圍，再從 m 到 M 逐一檢查是否為奇數，才正確計算總和

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    
    for (int i = 1; i <= n; i++) {
        int a, b;
        cin >> a >> b;
        
        int M = max(a, b);
        int m = min(a, b);
        
        int sum = 0;
        for (int j = m; j <= M; j++) {
            if (j % 2 != 0) {
                sum += j;
            }
        }
        
        cout << "Case " << i << ": " << sum << "\n";
    }
    return 0;
}
```
**時間複雜度**：O(T × L) （T 為測資組數，L 為區間長度）

**空間複雜度**：O(1)
