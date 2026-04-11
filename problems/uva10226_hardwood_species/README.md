# UVa 10226 - Hardwood Species

**題目連結**：  
[ZeroJudge - d492](https://zerojudge.tw/ShowProblem?problemid=d492)  

**解題思路**：
- 統計每種樹木（Hardwood）出現的次數與百分比
- 使用 `map<string, int>` 自動排序並統計樹木數量
- 計算每種樹木佔總樹木數的比例（保留 4 位小數）
- 多筆測資，每組測資之間以空行分隔，需小心處理輸入

**遇到問題與解決**：
- 一開始對 `map` 和 `getline` 的使用不熟悉
- 處理測資之間的空行時，容易多讀或少讀一行，導致部分樹木消失
- 後來先用 `getline` 吃掉換行，並正確判斷空行作為一組測資的結束，才解決輸入問題

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    string enter;
    getline(cin, enter);  // 吃掉第一組測資前的換行
    getline(cin, enter);  // 吃掉測資開始前的空行
    
    while (n--) {
        map<string, int> tree_count;
        string tree;
        
        while (getline(cin, tree)) {
            if (tree == "") break;        // 空行代表一組測資結束
            tree_count[tree]++;
        }
        
        double sum = 0;
        for (auto &p : tree_count) {
            sum += p.second;
        }
        
        for (auto &p : tree_count) {
            double ans = p.second / sum * 100;
            cout << p.first << " " << fixed << setprecision(4) << ans << "\n";
        }
        
        if (n > 0) cout << "\n";   // 組與組之間空一行
    }
    return 0;
}
```
**時間複雜度**：O(T × N log N) （T 為測資組數，N 為樹木總數）

**空間複雜度**：O(N)
