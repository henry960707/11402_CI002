# UVa 10474 - Where is the Marble?

**題目連結**：  
[ZeroJudge - e541](https://zerojudge.tw/ShowProblem?problemid=e541) 

**解題思路**：
- 將所有大理石的數字**由小到大排序**
- 對於每個查詢數字，使用 `lower_bound` 找出它**第一次出現的位置**
- 位置需從 **1** 開始計算
- 若該數字不存在，輸出 `not found`

**遇到問題與解決**：
- 一開始想得太複雜，同時使用 `map` + 二分搜尋，導致程式碼非常混亂
- 後來理解 `lower_bound` 的用法後，發現它非常適合這題（回傳第一個 >= query 的位置）
- 對於 iterator（`it - str.begin()`）的使用還不熟，經過研究後才正確計算位置

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, q, case_num = 1;
    
    while (cin >> n >> q && (n > 0 || q > 0)) {
        vector<int> marble(n);
        for (int &x : marble) cin >> x;
        
        sort(marble.begin(), marble.end());
        
        cout << "CASE# " << case_num++ << ":\n";
        
        while (q--) {
            int query;
            cin >> query;
            
            auto it = lower_bound(marble.begin(), marble.end(), query);
            
            if (it != marble.end() && *it == query) {
                int pos = (it - marble.begin()) + 1;   // 位置從 1 開始
                cout << query << " found at " << pos << "\n";
            } else {
                cout << query << " not found\n";
            }
        }
    }
    return 0;
}
```
**時間複雜度**：O(N log N + Q log N)

**空間複雜度**：O(N)
