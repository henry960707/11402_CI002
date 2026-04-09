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
時間複雜度：O((b - a) × log n)
空間複雜度：O(1)
