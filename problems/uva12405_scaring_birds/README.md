# UVa 12405 - Scaring Birds

**題目連結**：  
[ZeroJudge - Scaring Birds](https://zerojudge.tw/ShowProblem?problemid=a465)  

**解題思路**：
- 農田由一排格子組成，`.` 代表需要保護的田，`#` 代表廢田（不需要保護，但可以插稻草人）
- 每個稻草人可以保護**自己所在的位置 + 左右兩邊**（共 3 格）
- 目標是使用**最少數量的稻草人**保護所有 `.`
- **貪婪策略**：從左到右掃描，遇到 `.` 就插稻草人，然後跳過後面兩格（因為已被保護）

**遇到問題與解決**：
- 一開始想用複雜的陣列記錄每個位置是否被保護，寫得很繁瑣
- 後來發現只需要**遇到 `.` 就插稻草人並跳 3 格**，大幅簡化程式碼
- 也學會了貪婪演算法在區間覆蓋問題上的應用

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int t;
    cin >> t;
    int case_num = 1;
    
    while (t--) {
        int n;
        cin >> n;
        string field;
        cin >> field;                    // 直接讀字串更方便
        
        int i = 0;
        int scarecrows = 0;
        
        while (i < n) {
            if (field[i] == '.') {
                scarecrows++;            // 插稻草人
                i += 3;                  // 保護後面兩格 + 自己，共跳 3 格
            } else {
                i++;
            }
        }
        
        cout << "Case " << case_num++ << ": " << scarecrows << "\n";
    }
```
**時間複雜度**：O(T × N)

**空間複雜度**：O(N)
    return 0;
}
