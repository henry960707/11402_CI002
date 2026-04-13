# UVa 11063 - B2-Sequence

**題目連結**：  
[ZeroJudge - B2-Sequence](https://onlinejudge.org/external/110/11063.pdf)  

**解題思路**：
- 判斷一個數列是否為 **B2-Sequence**：
  - 所有數字必須是**正整數**且**嚴格遞增**
  - 任意兩個數字的和（包含自己與自己相加）都不能重複
- 使用 `vector` 儲存數列，先檢查正整數與嚴格遞增條件
- 再用雙重迴圈計算所有兩數之和，用 `map` 統計是否出現重複

**遇到問題與解決**：
- 一開始不太清楚題目「B2-Sequence」的定義，導致出現 Presentation Error（PE）
- 理解題目後，先檢查基本條件（正整數 + 嚴格遞增），再檢查兩數和是否唯一
- 原本擔心雙重迴圈會太慢，後來發現 n 很小（通常 ≤ 100），O(n²) 完全可以接受

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, case_num = 1;
    while (cin >> n) {
        vector<int> seq(n);
        for (int &x : seq) cin >> x;
        
        bool isB2 = true;
        
        // 檢查是否為正整數且嚴格遞增
        for (int i = 0; i < n; i++) {
            if (seq[i] <= 0 || (i > 0 && seq[i] <= seq[i-1])) {
                isB2 = false;
                break;
            }
        }
        
        // 檢查兩數之和是否唯一
        if (isB2) {
            map<int, int> sum_count;
            for (int i = 0; i < n; i++) {
                for (int j = i; j < n; j++) {     // j 從 i 開始，包含自己加自己
                    int s = seq[i] + seq[j];
                    sum_count[s]++;
                    if (sum_count[s] > 1) {
                        isB2 = false;
                        break;
                    }
                }
                if (!isB2) break;
            }
        }
        
        cout << "Case #" << case_num++ << ": ";
        if (isB2)
            cout << "It is a B2-Sequence.\n\n";
        else
            cout << "It is not a B2-Sequence.\n\n";
    }
    return 0;
}
```
**時間複雜度**：O(N²)

**空間複雜度**：O(N²)（最壞情況下所有和都不一樣）
