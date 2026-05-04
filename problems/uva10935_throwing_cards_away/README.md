# UVa 10935 - Throwing cards away I

**題目連結**：  
[ZeroJudge - Throwing cards away I](https://zerojudge.tw/ShowProblem?problemid=e155) 

**解題思路**：
- 將 1 到 n 張牌由上到下依序放入 queue（最上面是 front）
- 重複以下動作直到只剩一張牌：
  - 丟棄目前最上面的牌（`q.front()` 並 `pop()`）
  - 把新的最上面那張牌移到最下面（`pop()` 後再 `push()`）
- 最後輸出所有被丟棄的牌的順序，以及剩下的最後一張牌

**遇到問題與解決**：
- 第一次系統性地使用 `queue`，對 `front()`、`pop()`、`push()` 的搭配還不夠熟練
- 輸出格式（逗號分隔、最後一張不加逗號）需要特別處理
- 經過練習後，逐漸掌握 queue 模擬過程的技巧

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    while (cin >> n && n != 0) {
        queue<int> q;
        for (int i = 1; i <= n; i++) {
            q.push(i);
        }
        
        cout << "Discarded cards:";
        bool first = true;
        
        while (q.size() > 1) {
            if (!first) cout << ",";
            cout << " " << q.front();
            q.pop();
            
            // 把下一張牌移到最下面
            q.push(q.front());
            q.pop();
            
            first = false;
        }
        
        cout << "\nRemaining card: " << q.front() << "\n";
    }
    return 0;
}
```
**時間複雜度**：O(N)

**空間複雜度**：O(N)
