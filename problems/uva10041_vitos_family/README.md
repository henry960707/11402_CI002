# UVa 10041 - Vito's Family

**題目連結**：  
[ZeroJudge - Vito's Family](https://zerojudge.tw/ShowProblem?problemid=a737) 

**解題思路**：
- Vito 要找一個位置（街道上的某一個房子），使得他與所有家族成員家的**總距離最短**
- 輸入多筆測資，每筆先給家族成員數量 `N`，再給 `N` 個成員的住址
- **關鍵**：在一維座標上，要最小化所有點到某點的**絕對距離總和**，最佳位置就是**中位數**

**為什麼要找中位數？（詳細解釋）**

這是經典的最佳化問題：

- 如果你選的位置在中位數**左邊**，那麼中位數右邊的所有人（人數 ≥ 左邊）都會把 Vito 往右拉。
- 如果你選的位置在中位數**右邊**，那麼中位數左邊的所有人（人數 ≥ 右邊）都會把 Vito 往左拉。
- 只有在中位數這個點，左右兩邊的拉力達到平衡，此時總距離和最小。

**簡單來說**：在中位數左邊或右邊移動，都會讓總距離增加。

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int t;
    cin >> t;
    while (t--) {
        int n;
        cin >> n;
        vector<int> arr(n);
        for (int i = 0; i < n; i++) {
            cin >> arr[i];
        }
        
        sort(arr.begin(), arr.end());
        
        int mid = n / 2;           // 中位數位置
        long long sum = 0;
        
        for (int i = 0; i < n; i++) {
            sum += abs(arr[i] - arr[mid]);
        }
        
        cout << sum << "\n";
    }
    return 0;
}
```
**時間複雜度**：O(T × N log N)

**空間複雜度**：O(N)
