# UVa 12503 - Robot Instructions

**題目連結**：  
[ZeroJudge - e567](https://zerojudge.tw/ShowProblem?problemid=e567) 

**解題思路**：
- 機器人從位置 0 開始，執行一系列指令
- `LEFT` → 位置 -1
- `RIGHT` → 位置 +1
- `SAME AS i` → 執行和第 i 步完全一樣的指令（向左或向右）
- 使用 `vector` 記錄每一步的移動方向（0 代表 LEFT，1 代表 RIGHT），方便後續 `SAME AS` 查詢
- 最後輸出機器人結束時的位置

**遇到問題與解決**：
- 最大的困難在於處理 `SAME AS i` 的輸入格式
- 一開始不知道怎麼同時讀取 "SAME" "AS" 和數字，導致輸入混亂
- 後來採用 `cin >> str`，如果不是 LEFT/RIGHT，就再讀 `as` 和 `index`，才成功處理
- 程式碼寫得比較醜，未來希望能優化輸入處理方式（例如使用 `stringstream`）

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int t;
    cin >> t;
    while (t--) {
        int c;
        cin >> c;
        
        vector<int> check(c);  // 0: LEFT, 1: RIGHT
        int pos = 0;
        
        for (int i = 0; i < c; i++) {
            string str;
            cin >> str;
            
            if (str == "LEFT") {
                check[i] = 0;
                pos -= 1;
            } 
            else if (str == "RIGHT") {
                check[i] = 1;
                pos += 1;
            } 
            else {
                // SAME AS x
                string as;
                int index;
                cin >> as >> index;
                check[i] = check[index - 1];
                
                if (check[i] == 0) pos -= 1;
                else pos += 1;
            }
        }
        cout << pos << "\n";
    }
    return 0;
}
```
**時間複雜度**：O(T × C) （T 為測資組數，C 為指令數）

**空間複雜度**：O(C)
