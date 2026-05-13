# UVa 11615 - Family Tree

**題目連結**：  
[ZeroJudge - Family Tree](https://onlinejudge.org/external/116/11615.pdf)

**解題思路**：
- 這是一棵**完整二元樹**（Complete Binary Tree），總共有 n 層
- 給定兩個節點 n1 和 n2，求它們的**最近共同祖先（LCA）**所在的子樹有多少個節點
- 關鍵觀察：只需計算兩個節點各自所在的**層數**，然後計算從該層到樹底部的節點數即可

**解題心得**：
- 一開始想實際建立整棵樹或用 map 記錄每一層的節點，導致 TLE
- 後來發現**完全不需要建樹**，只要計算每個節點在第幾層（不斷除以 2），再用數學公式計算子樹大小即可大幅優化

**程式碼（優化後版本）**：

```cpp
#include <bits/stdc++.h>
using namespace std;

// 計算節點位於第幾層（root 為第 1 層）
int getLevel(int node) {
    int level = 0;
    while (node > 0) {
        node /= 2;
        level++;
    }
    return level;
}

int main() {
    int t;
    cin >> t;
    while (t--) {
        int n, n1, n2;
        cin >> n >> n1 >> n2;
        
        int lev1 = getLevel(n1);
        int lev2 = getLevel(n2);
        int max_lev = max(lev1, lev2);        // 最近共同祖先所在的層數
        
        // 從 max_lev 層到第 n 層的節點總數
        long long total = (1LL << n) - 1;           // 完整 n 層的節點數
        long long remove = (1LL << (n - max_lev + 1)) - 2;  // 要移除的子樹部分
        
        cout << total - remove << "\n";
    }
    return 0;
}
```
**時間複雜度**：O(T × log N)

**空間複雜度**：O(1)
