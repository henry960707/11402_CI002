# UVa 490 - Rotating Sentences

**題目連結**：  
[ZeroJudge - c045](https://zerojudge.tw/ShowProblem?problemid=c045)

**解題思路**：
- 將輸入的多行句子「順時針旋轉 90 度」後輸出
- 原本最下面的一行會變成最左邊的一列
- 先把所有句子存起來，並找出最長的句子長度（決定輸出列數）
- 使用雙層迴圈：外層控制列，內層從最後一行往前取每個字元

**遇到問題與解決**：
- 第一次看到題目時完全沒有頭緒，不知道該如何將句子旋轉 90 度
- 花了很多時間理解題意與轉換邏輯，最後決定用 `vector<string>` 儲存所有行，再用雙迴圈反向輸出才通過
- 這題讓我練習了二維思維與字串處理

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    cin.sync_with_stdio(0);
    cin.tie(0);
    
    vector<string> str;
    string s;
    int max_line = 0;
    
    while (getline(cin, s)) {
        str.push_back(s);
        if (s.length() > max_line) max_line = s.length();
    }
    
    for (int i = 0; i < max_line; i++) {
        for (int j = str.size() - 1; j >= 0; j--) {
            if (i < str[j].length()) {
                cout << str[j][i];
            } else {
                cout << " ";
            }
        }
        cout << "\n";
    }
    return 0;
}
