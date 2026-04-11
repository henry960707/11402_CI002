# UVa 11057 - Exact Sum

**題目連結**：  
[ZeroJudge - Exact Sum](https://onlinejudge.org/external/110/11057.pdf)  

**解題思路**：
- 給定多本書的價格和 Peter 擁有的錢（money）
- 找出兩本書的價格加起來**正好等於** money
- 若有多組解，選擇**價格差最小**的那一組
- 使用排序 + 雙指標（Two Pointers）從兩端往中間逼近，效率高且容易找到最小差

**遇到問題與解決**：
- 一開始想得太複雜，打算用 stringstream 處理輸入，並額外建立陣列記錄所有可能組合
- 後來發現排序後使用雙指標（left、right）就可輕鬆解決，還能直接找到差最小的組合
- 也學會了如何在多筆測資中使用 `while(cin >> n)` 處理輸入

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    while (cin >> n) {
        vector<int> book(n);
        for (int i = 0; i < n; i++) {
            cin >> book[i];
        }
        
        int money;
        cin >> money;
        
        sort(book.begin(), book.end());
        
        int left = 0, right = n - 1;
        int book1 = 0, book2 = 0;
        
        while (left < right) {
            int sum = book[left] + book[right];
            
            if (sum > money) {
                right--;
            } else if (sum < money) {
                left++;
            } else {
                // 找到一組解，記錄下來（因為從外往內找，後面找到的會更接近）
                book1 = book[left];
                book2 = book[right];
                left++;
                right--;
            }
        }
        
        cout << "Peter should buy books whose prices are " 
             << book1 << " and " << book2 << ".\n\n";
    }
    return 0;
}
```
**時間複雜度**：O(N log N) （主要花在排序）

**空間複雜度**：O(N)
