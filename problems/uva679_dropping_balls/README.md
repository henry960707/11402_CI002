# UVa 679 - Dropping Balls

**題目連結**：  
[ZeroJudge - Dropping Balls](https://zerojudge.tw/ShowProblem?problemid=a249)  

**解題思路**：
- 有一棵深度為 D 的完整二叉樹（最多 2^D - 1 個節點）
- 從根節點（編號 1）開始丟 I 顆小球
- 每個節點的小球如果遇到**奇數**顆就往左走，**偶數**顆就往右走
- 要求找出第 I 顆小球最後落在哪一個葉子節點

**優化解法（數學模擬）**：
- 不需要實際建立樹
- 透過觀察小球的奇偶性來決定往左或往右
- 每次根據 `i` 是奇數或偶數決定路徑，並更新 `i`（`i = i/2` 或 `i/2 + 1`）
- 最終走到第 `D` 層的節點編號即為答案

**遇到問題與解決**：
- 一開始想用陣列實際模擬建樹，結果 TLE
- 後來發現可以用數學方式直接模擬小球路徑，大幅提升效率
- 加上 `ios_base::sync_with_stdio(0);` 和 `cin.tie(NULL);` 加速輸入

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios_base::sync_with_stdio(0);
    cin.tie(NULL);
    
    int t;
    cin >> t;
    while (t--) {
        int d, i;
        cin >> d >> i;
        
        int k = 1;           // 目前所在節點
        int h = d - 1;       // 需要走 d-1 步
        
        while (h--) {
            if (i % 2 == 1) {    // 奇數往左
                k = k * 2;
                i = i / 2 + 1;
            } else {             // 偶數往右
                k = k * 2 + 1;
                i = i / 2;
            }
        }
        cout << k << "\n";
    }
    return 0;
}
```
**時間複雜度**：O(T × D)

**空間複雜度**：O(1)
