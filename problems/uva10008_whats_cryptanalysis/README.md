# UVa 10008 - What's Cryptanalysis

**題目連結**：  
[ZeroJudge - c044](https://zerojudge.tw/ShowProblem?problemid=c044)  

**解題思路**：
- 統計輸入文字中每個英文字母出現的次數（忽略非字母字元）
- 輸出時需**按照出現次數由高到低排序**，若次數相同則按照字母由小到大排序
- 使用 `map<char, int>` 統計字母出現次數，再轉成 `vector<pair<char,int>>` 進行自訂排序

**遇到問題與解決**：
- 一開始不會使用 `toupper()` 和 `isalpha()`，後來理解後就能正確將字母轉成大寫並過濾
- `map` 本身會按照字母順序排序，但題目要求**依出現次數排序**，因此把 map 轉成 vector 後，自訂 comparator 進行排序
- 學會如何撰寫自訂比較函式（custom comparator）

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

// 自訂比較函式：次數由大到小，次數相同則字母由小到大
bool compare(const pair<char, int> &a, const pair<char, int> &b) {
    if (a.second != b.second) 
        return a.second > b.second;   // 次數多的排前面
    return a.first < b.first;         // 次數相同，字母小的排前面
}

int main() {
    int n;
    cin >> n;
    string enter;
    getline(cin, enter);   // 吃掉換行
    
    map<char, int> counts;
    
    while (n--) {
        string str;
        getline(cin, str);
        for (char c : str) {
            if (isalpha(c)) {
                char upC = toupper(c);
                counts[upC]++;
            }
        }
    }
    
    // 轉成 vector 才能自訂排序
    vector<pair<char, int>> vec(counts.begin(), counts.end());
    sort(vec.begin(), vec.end(), compare);
    
    for (auto &p : vec) {
        cout << p.first << " " << p.second << "\n";
    }
    
    return 0;
}
```
**時間複雜度**：O(N + K log K) （N 為總字元數，K 為不同字母數，最多 26）

**空間複雜度**：O(K)
