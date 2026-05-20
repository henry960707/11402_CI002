# UVa 11349 - Symmetric Matrix

**題目連結**：  
[ZeroJudge - Symmetric Matrix](https://zerojudge.tw/ShowProblem?problemid=e513) 

**解題思路**：
- 判斷一個 N × N 的矩陣是否為**對稱矩陣**（Symmetric Matrix）
- 條件：
  1. 所有元素必須為**非負整數**（≥ 0）
  2. 矩陣必須沿**主對角線對稱**（即 `matrix[i][j] == matrix[j][i]`）
- 將矩陣壓成一維陣列後，使用雙指標（left、right）從兩端往中間比較

**遇到問題與解決**：
- 一開始 `cin` 處理 "N = " 時容易出錯，導致讀入多餘資料或亂碼
- 忽略題目要求的「所有元素必須非負」，導致一直 WA
- 後來改用一維陣列 + 雙指標比較，同時檢查負數，才順利通過

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int t;
    cin >> t;
    int case_num = 1;
    
    while (t--) {
        // 處理 "N = " 
        string s;
        int n;
        cin >> s >> s >> n;   // 吃掉 "N" 和 "="
        
        vector<long long> arr(n * n);
        bool isSymmetric = true;
        
        // 讀取所有數字並檢查負數
        for (int i = 0; i < n * n; i++) {
            cin >> arr[i];
            if (arr[i] < 0) isSymmetric = false;
        }
        
        // 雙指標檢查對稱性
        int left = 0, right = n * n - 1;
        while (left <= right) {
            if (arr[left] != arr[right]) {
                isSymmetric = false;
                break;
            }
            left++;
            right--;
        }
        
        cout << "Test #" << case_num++ << ": ";
        if (isSymmetric)
            cout << "Symmetric.\n";
        else
            cout << "Non-symmetric.\n";
    }
    return 0;
}
```
**時間複雜度**：O(T × N²)

**空間複雜度**：O(N²)
