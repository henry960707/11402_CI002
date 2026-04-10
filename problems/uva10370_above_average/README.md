# UVa 10370 - Above Average

**題目連結**：  
https://zerojudge.tw/ShowProblem?problemid=n768

**解題思路**：
- 計算全班的平均成績
- 統計有多少人的成績高於平均值
- 輸出高於平均的人數佔全班的百分比（保留 3 位小數 + %）

**遇到問題與解決**：
- 本題概念較簡單，寫起來沒有太大負擔
- 使用 `vector` 儲存成績，並用 `setprecision` 處理輸出格式
- 未來希望能把程式碼寫得更簡潔優雅

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int c;
    cin >> c;
    while (c--) {
        int n;
        cin >> n;
        vector<int> score(n);
        double sum = 0;
        
        for (int i = 0; i < n; i++) {
            cin >> score[i];
            sum += score[i];
        }
        
        double avg = sum / n;
        int high = 0;
        
        for (int i = 0; i < n; i++) {
            if (score[i] > avg) high++;
        }
        
        double answer = (double)high / n * 100;
        cout << fixed << setprecision(3) << answer << "%\n";
    }
    return 0;
}
```
**時間複雜度**：O(C × N) （C 為測資組數，N 為學生人數）

**空間複雜度**：O(N)
