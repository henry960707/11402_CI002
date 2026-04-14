# UVa 12250 - Language Detection

**題目連結**：  
[ZeroJudge - a135](https://zerojudge.tw/ShowProblem?problemid=a135)  

**解題思路**：
- 根據輸入的問候語判斷是哪種語言
- 使用 `map<string, string>` 建立問候語與語言的對應關係
- 輸入 `#` 代表結束
- 若不在字典中則輸出 `UNKNOWN`

**遇到問題與解決**：
- 挖掘了 `map` 更多的用法（`find()`、`[]` 運算子）
- 原本寫法有小 bug（while 條件中的 `s` 未定義），修正後使用 `str != "#"`
- 更加熟悉 `map` 的查詢與對應操作，認為這對未來寫程式會很有幫助

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    map<string, string> country = {
        {"HELLO", "ENGLISH"},
        {"HOLA", "SPANISH"},
        {"HALLO", "GERMAN"},
        {"BONJOUR", "FRENCH"},
        {"CIAO", "ITALIAN"},
        {"ZDRAVSTVUJTE", "RUSSIAN"}
    };
    
    string str;
    int t = 1;
    
    while (cin >> str && str != "#") {
        cout << "Case " << t++ << ": ";
        
        if (country.find(str) != country.end()) {
            cout << country[str] << "\n";
        } else {
            cout << "UNKNOWN\n";
        }
    }
    return 0;
}
```
**時間複雜度**：O(1)（每筆測資 map 查詢為 O(log 6)）

**空間複雜度**：O(1)
