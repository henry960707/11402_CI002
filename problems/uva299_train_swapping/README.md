# UVa 299 - Train Swapping

**題目連結**：  
[ZeroJudge - e561](https://zerojudge.tw/ShowProblem?problemid=e561) 

**解題思路**：
- 火車車廂需要重新排列成由小到大的順序
- 每次只能**相鄰兩節車廂對調**（Swap）
- 要求計算出**最少需要幾次 Swap** 才能排好
- 本質就是計算「逆序對」（Inversion）的數量，使用 **Bubble Sort** 模擬過程即可得到答案

**遇到問題與解決**：
- 一開始不太理解 Bubble Sort 的程式碼要怎麼寫，尤其是內層迴圈的邊界條件（`j < c-1-i`）
- 經過理解後，掌握了「每一輪把最大值沉到最後」的概念，才正確寫出雙層迴圈

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    while (n--) {
        int c;
        cin >> c;
        vector<int> train(c);
        for (int i = 0; i < c; i++) {
            cin >> train[i];
        }
        
        int count = 0;
        // Bubble Sort 計算交換次數
        for (int i = 0; i < c; i++) {
            for (int j = 0; j < c - 1 - i; j++) {
                if (train[j] > train[j + 1]) {
                    swap(train[j], train[j + 1]);
                    count++;
                }
            }
        }
        
        cout << "Optimal train swapping takes " << count << " swaps.\n";
    }
    return 0;
}
```
**時間複雜度**：O(N²)

**空間複雜度**：O(N)
