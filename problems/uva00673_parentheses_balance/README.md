# UVa 00673 - Parentheses Balance

**題目連結**：  
[ZeroJudge - Parentheses Balance](https://zerojudge.tw/ShowProblem?problemid=b304)  

**解題思路**：
- 使用 Stack 判斷括號是否匹配且平衡
- 遇到 `'('` 或 `'['` 就 push 進 stack
- 遇到 `')'` 或 `']'` 時，檢查 stack 是否為空，以及 stack top 是否為對應的左括號
- 最後 stack 必須為空，才是合法的括號序列

**遇到問題與解決**：
- 一開始對 stack 的使用不熟悉，容易搞錯 index 或在 stack 為空時就呼叫 `top()`
- 後來理解必須**先檢查 `!st.empty()`**，再去取 `top()`，否則會出錯
- 也學會了如何正確處理多筆測資的輸入（`cin >> n` 後接 `getline` 需要小心換行）

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    string line;
    getline(cin, line);   // 吃掉 cin 後的換行
    
    while (n--) {
        stack<char> st;
        bool valid = true;
        
        getline(cin, line);
        
        for (char c : line) {
            if (c == '(' || c == '[') {
                st.push(c);
            }
            else if (c == ')' || c == ']') {
                if (st.empty()) {
                    valid = false;
                    break;
                }
                char top = st.top();
                if ((c == ')' && top != '(') || (c == ']' && top != '[')) {
                    valid = false;
                    break;
                }
                st.pop();
            }
        }
        
        if (!st.empty()) valid = false;
        
        if (valid)
            cout << "Yes\n";
        else
            cout << "No\n";
    }
    return 0;
}
```
**時間複雜度**：O(L) （L 為字串長度）

**空間複雜度**：O(L)
