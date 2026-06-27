# UVa 11292 - Dragon of Loowater

**題目連結**：  
[ZeroJudge - Dragon of Loowater](https://onlinejudge.org/external/112/11292.pdf)  

**解題思路**：
- 每個騎士只能砍一個龍頭，且騎士身高必須 ≥ 龍頭高度才能砍
- 目標是**用最少的金錢**（騎士的總身高）砍掉所有龍頭
- **貪婪策略**：把龍頭和騎士都排序後，從小到大配對
  - 如果騎士太矮，就換下一個騎士
  - 如果騎士夠高，就讓他砍這個龍頭，並累加花費

**遇到問題與解決**：
- 一開始最困難的地方是**讀懂題目**（要用最少金錢砍完所有龍頭，否則 Loowater 就完蛋了）
- 後來理解用**排序 + 雙指標**（greedy matching）就能高效解決
- 也練習了如何處理「多筆測資直到 0 0 結束」的輸入格式

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, m;
    while (cin >> n >> m && (n || m)) {
        vector<int> dragon(n);
        vector<int> knight(m);
        
        for (int i = 0; i < n; i++) cin >> dragon[i];
        for (int i = 0; i < m; i++) cin >> knight[i];
        
        sort(dragon.begin(), dragon.end());
        sort(knight.begin(), knight.end());
        
        long long cost = 0;
        int i = 0, j = 0;   // i: 龍頭, j: 騎士
        
        while (i < n && j < m) {
            if (knight[j] >= dragon[i]) {
                cost += knight[j];   // 這個騎士砍掉這顆龍頭
                i++;
                j++;
            } else {
                j++;                 // 騎士太矮，換下一個
            }
        }
        
        if (i < n) {
            cout << "Loowater is doomed!\n";
        } else {
            cout << cost << "\n";
        }
    }
}
```
**時間複雜度**：O(T × (N log N + M log M))

**空間複雜度**：O(N + M)
