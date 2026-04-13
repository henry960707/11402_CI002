# UVa 10062 - Tell me the frequencies!

**題目連結**：  
[ZeroJudge - c012](https://zerojudge.tw/ShowProblem?problemid=c012)  

**解題思路**：
- 統計輸入字串中**每個字元（包含所有 ASCII）**出現的次數
- 輸出需按照以下規則排序：
  - 頻率（出現次數）由小到大
  - 若頻率相同，則按照 ASCII 值由大到小排序
- 多筆測資，每組測資之間輸出一個空行

**遇到問題與解決**：
- 一開始不知道要怎麼輸出 ASCII 值，後來理解 `(int)char` 可以直接轉換
- `map` 預設會按照 ASCII 由小到大排序，但題目要求**頻率由小到大**，因此轉成 `vector<pair<char,int>>` 後使用自訂 comparator 排序
- 處理多筆測資時，需小心在每組輸出前先換行（使用 `first` 旗標控制）

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

// 自訂比較：頻率由小到大，頻率相同則 ASCII 由大到小
bool compare(const pair<char, int> &a, const pair<char, int> &b) {
    if (a.second != b.second) 
        return a.second < b.second;      // 頻率小的排前面
    return (int)a.first > (int)b.first;  // 頻率相同，ASCII 大的排前面
}

int main() {
    string str;
    bool first = true;
    
    while (getline(cin, str)) {
        if (!first) cout << "\n";
        first = false;
        
        map<char, int> counts;
        for (char c : str) {
            counts[c]++;
        }
        
        vector<pair<char, int>> vec(counts.begin(), counts.end());
        sort(vec.begin(), vec.end(), compare);
        
        for (auto &p : vec) {
            cout << (int)p.first << " " << p.second << "\n";
        }
    }
    return 0;
}
```
**時間複雜度**：O(N log K) （N 為字串長度，K 為不同字元數）

**空間複雜度**：O(K)
