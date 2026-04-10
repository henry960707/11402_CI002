# UVa 10611 - The Playboy Chimp

**題目連結**：  
[ZeroJudge - The Playboy Chimp](https://onlinejudge.org/external/106/10611.pdf)

**解題思路**：
- Lady 的身高已排序
- 對每個 Luchu 的身高，找出：
  - 小於他的最大身高（前一個）
  - 大於他的最小身高（後一個）
- 使用二分搜尋（lower_bound / upper_bound）快速查找

**遇到問題與解決**：
- 一開始想用兩個 for 迴圈暴力搜尋，擔心 TLE
- 後來改用二分搜尋（lower_bound + upper_bound）
- 曾忘記指標操作（it-1）和邊界判斷（begin() / end()），花了一些時間 debug

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<int> lady(n);
    for (int i = 0; i < n; i++) cin >> lady[i];
    
    int q;
    cin >> q;
    for (int i = 0; i < q; i++) {
        int luchu;
        cin >> luchu;
        
        // 找小於 luchu 的最大值
        auto it = lower_bound(lady.begin(), lady.end(), luchu);
        if (it == lady.begin()) {
            cout << "X ";
        } else {
            cout << *(it - 1) << " ";
        }
        
        // 找大於 luchu 的最小值
        auto ot = upper_bound(lady.begin(), lady.end(), luchu);
        if (ot == lady.end()) {
            cout << "X\n";
        } else {
            cout << *ot << "\n";
        }
    }
    return 0;
}
```
**時間複雜度**：O(N log N + Q log N)

**空間複雜度**：O(N)
