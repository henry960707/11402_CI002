# UVa 00514 - Rails

**題目連結**：  
[ZeroJudge - Rails](https://zerojudge.tw/ShowProblem?problemid=c123)  

**解題思路**：
- 模擬火車重排的過程，判斷給定的目標順序是否能透過一個車站（Stack）達成
- 火車依序從 A 站進入（1, 2, 3, ..., n）
- 可以選擇把車廂推進 Stack，或直接開往 B 站
- 使用 Stack 模擬車站，依序將車廂 push 進去
- 每 push 一節車廂後，就檢查 stack top 是否等於目前目標順序的下一個車廂，如果是就 pop 出來
- 最後如果 stack 為空，代表可以達成該順序，輸出 `Yes`，否則 `No`

**遇到問題與解決**：
- 這題最大的困難在於**測資輸入格式非常複雜**
  - 先讀 n（車廂數），若 n=0 則結束
  - 再讀目標順序的第一個數字，若為 0 則這組測資結束
  - 之後繼續讀剩餘 n-1 個數字
- 多次 debug 後才正確處理多組測資與每組測資結束的條件

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    while (cin >> n && n != 0) {
        int first;
        while (cin >> first && first != 0) {
            vector<int> target(n);
            target[0] = first;
            for (int i = 1; i < n; i++) {
                cin >> target[i];
            }
            
            stack<int> st;
            int index = 0;   // 指向目前目標順序的下一個位置
            
            for (int i = 1; i <= n; i++) {
                st.push(i);
                
                // 能 pop 就一直 pop
                while (!st.empty() && st.top() == target[index]) {
                    st.pop();
                    index++;
                }
            }
            
            if (st.empty())
                cout << "Yes\n";
            else
                cout << "No\n";
        }
        cout << "\n";   // 每組測資（n）結束後輸出一個空行
    }
    return 0;
}
```
**時間複雜度**：O(N)

**空間複雜度**：O(N)
