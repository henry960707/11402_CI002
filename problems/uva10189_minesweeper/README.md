# UVa 10189 - Minesweeper

**題目連結**：  
[ZeroJudge - Minesweeper](https://zerojudge.tw/ShowProblem?problemid=e605)  

**解題思路**：
- 經典掃雷遊戲模擬
- 給定一張地圖（`.` 代表空地，`*` 代表地雷）
- 對每一個空地（`.`），計算其**周圍 8 個格子**中有幾顆地雷
- 輸出時，地雷位置輸出 `*`，空地位置輸出周圍地雷的數量

**解題技巧**：
- 使用方向陣列 `dx[], dy[]` 來枚舉周圍 8 個方向
- 建立兩個陣列：一個存原始地圖，一個存答案

**遇到問題與解決**：
- 一開始不知道要怎麼遍歷每個格子的周圍格子
- 後來使用 `dx, dy` 方向陣列，成功解決周圍 8 格的檢查
- 也學會了如何處理多筆測資之間的空行輸出

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int dx[] = {-1, -1, -1, 0, 0, 1, 1, 1};
    int dy[] = {-1, 0, 1, -1, 1, -1, 0, 1};
    
    int n, m, case_num = 1;
    while (cin >> n >> m && (n != 0 || m != 0)) {
        vector<string> arr(n);
        for (int i = 0; i < n; i++) {
            cin >> arr[i];
        }
        
        vector<vector<int>> ans(n, vector<int>(m, 0));
        
        // 計算每個空地的周圍地雷數
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (arr[i][j] == '.') {
                    int cnt = 0;
                    for (int k = 0; k < 8; k++) {
                        int nx = i + dx[k];
                        int ny = j + dy[k];
                        if (nx >= 0 && nx < n && ny >= 0 && ny < m && arr[nx][ny] == '*') {
                            cnt++;
                        }
                    }
                    ans[i][j] = cnt;
                }
            }
        }
        
        // 輸出格式
        if (case_num > 1) cout << "\n";
        cout << "Field #" << case_num++ << ":\n";
        
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (arr[i][j] == '*') cout << '*';
                else cout << ans[i][j];
            }
            cout << "\n";
        }
    }
    return 0;
}
```
**時間複雜度**：O(T × N × M)

**空間複雜度**：O(N × M)
