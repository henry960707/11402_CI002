# UVa 12100 - Printer Queue

**題目連結**：  
[ZeroJudge - Printer Queue](https://onlinejudge.org/external/121/12100.pdf)  

**解題思路**：
- 印表機每次只會印出目前優先級最高的檔案
- 若目前檔案不是最高優先級，就會被移到隊伍最後面
- 給定每個檔案的優先級與目標檔案的位置，求目標檔案需要等待多久才會被印出來
- 使用 `queue<pair<int,bool>>` 儲存 (優先級, 是否為目標檔案)
- 使用 `count[10]` 陣列快速判斷目前最高優先級

**遇到問題與解決**：
- 一開始完全不知道該如何同時處理「優先級比較」和「位置追蹤」
- 後來使用 `count` 陣列記錄各優先級數量 + `pair` 記錄是否為目標檔案，才成功模擬過程
- 也發現 `queue` 無法直接用 index 存取，必須用 `pair` 來標記目標
- 變數命名與邊界處理花了不少時間 debug

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int t;
    cin >> t;
    while (t--) {
        int n, m;
        cin >> n >> m;
        
        int count[10] = {0};
        queue<pair<int, bool>> q;   // (優先級, 是否為目標)
        
        for (int i = 0; i < n; i++) {
            int priority;
            cin >> priority;
            count[priority]++;
            q.push({priority, (i == m)});
        }
        
        int time = 0;
        while (!q.empty()) {
            auto front = q.front();
            q.pop();
            
            // 檢查是否為目前最高優先級
            bool is_highest = true;
            for (int i = 9; i > front.first; i--) {
                if (count[i] > 0) {
                    is_highest = false;
                    break;
                }
            }
            
            if (!is_highest) {
                // 不是最高優先級 → 移到隊尾
                q.push(front);
            } else {
                // 是最高優先級 → 印出來
                time++;
                count[front.first]--;
                
                if (front.second) {   // 是目標檔案
                    cout << time << "\n";
                    break;
                }
            }
        }
    }
    return 0;
}
```
**時間複雜度**：O(T × N × 9) ≈ O(T × N)

**空間複雜度**：O(N)
