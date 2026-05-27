# UVa 10252 - Common Permutation

**題目連結**：  
[ZeroJudge - Common Permutation](https://zerojudge.tw/ShowProblem?problemid=e507)  

**解題思路**：
- 給定兩個字串，找出它們**共同出現的字母**（每個字母取出現次數的最小值）
- 輸出結果需**按照字母由小到大排序**
- 本質上是求兩個字串的「共同多重集」（multiset intersection）

**遇到問題與解決**：
- 一開始想用 `set` 處理，但 `set` 無法處理重複字母
- 後來改用 `vector<bool>` 標記已使用過的字母，避免重複計數
- 也練習了如何用雙重迴圈找出共同字母，並且正確排序輸出

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string l1, l2;
    while (getline(cin, l1) && getline(cin, l2)) {
        if (l1.empty() && l2.empty()) {
            cout << "\n";
            continue;
        }
        
        vector<bool> used(l1.length(), true);
        vector<char> ans;
        
        for (char c : l2) {
            for (int j = 0; j < (int)l1.length(); j++) {
                if (used[j] && l1[j] == c) {
                    used[j] = false;
                    ans.push_back(c);
                    break;
                }
            }
        }
        
        sort(ans.begin(), ans.end());
        
        for (char c : ans) {
            cout << c;
        }
        cout << "\n";
    }
    return 0;
}
```
**時間複雜度**：O(L1 × L2 + L log L)

**空間複雜度**：O(L1 + L2)

**優化程式碼**

**解題思路**：
- 給定兩個字串，找出它們**共同出現的字母**（每個字母取出現次數的最小值）
- 輸出結果需**按照字母由小到大排序**
- 本質上是求兩個字串的「共同多重集」（multiset intersection）

**解題過程**：
- 一開始使用 `vector<bool>` + 雙重迴圈，雖然正確但效率較低
- 後來改用**頻率陣列（count array）**，大幅簡化程式碼並提升效率

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string s1, s2;
    while (getline(cin, s1) && getline(cin, s2)) {
        int count1[26] = {0};
        int count2[26] = {0};
        
        // 統計兩個字串中各字母出現次數
        for (char c : s1) {
            if (islower(c)) count1[c - 'a']++;
        }
        for (char c : s2) {
            if (islower(c)) count2[c - 'a']++;
        }
        
        // 輸出共同字母（取最小次數）
        for (int i = 0; i < 26; i++) {
            int common = min(count1[i], count2[i]);
            for (int j = 0; j < common; j++) {
                cout << (char)(i + 'a');
            }
        }
        cout << "\n";
    }
    return 0;
}
