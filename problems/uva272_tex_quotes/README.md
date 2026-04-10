# UVa 272 - Tex Quotes

**題目連結**：  
[ZeroJudge - c007](https://zerojudge.tw/ShowProblem?problemid=c007)

**解題思路**：
- 將輸入文字中的雙引號 `"` 轉換成 TeX 格式的引號
- 第一個 `"` 轉成 ```` (兩個反引號)
- 之後的 `"` 輪流轉成 `''` (兩個單引號)
- 使用 `getline` 處理多行輸入，並用 `bool` 變數記錄目前引號狀態

**遇到問題與解決**：
- 一開始不知道要怎麼處理多行輸入，後來使用 `getline(cin, str)` 解決
- 初次嘗試用陣列存所有字元失敗，改用逐字元處理 + bool flag 來切換引號格式
- 對 `getline` 和 EOF 處理較不熟悉，練習後已掌握

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string str;
    bool check = true;  // true 代表下一個 " 要轉成 ``

    while (getline(cin, str)) {
        for (char c : str) {
            if (c == '"') {
                if (check) {
                    cout << "``";
                } else {
                    cout << "''";
                }
                check = !check;
            } else {
                cout << c;
            }
        }
        cout << endl;
    }
    return 0;
}
```
**時間複雜度**：O(N) （N 為總字元數）

**空間複雜度**：O(1)
