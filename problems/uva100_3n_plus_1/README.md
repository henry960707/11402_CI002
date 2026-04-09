# UVa 00100 - The 3n + 1 problem

**題目連結**：  
https://zerojudge.tw/ShowProblem?problemid=c039

**解題思路**：
- 經典 Collatz 猜想模擬題
- 先將變數"較小、較大"的數(m M) 以及用來算最大的數列(max_length)設出來
- 從最小的數字開始 算出其數列長度 和前一個數列的長度進行比較 若較大則放進max_length
- 輸出maxlength結果


**遇到問題**:
- 嘗試用遞迴 但寫不出來
- 改成用while(true) k == 1後break
- 若有更好解法再補充



**程式碼**：
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() 
{
    int a,b;
    while(cin>>a>>b){
      int m = min(a,b);
      int M = max(a,b);
      int max_length = 0;
      for(int i = m;i<=M;++i){
        int k = i;
        int cycle = 0;
        while(true){
          cycle++;
          if(k == 1) break;
          else if(k%2!=0) k = k*3+1;
          else k/=2;
        }
        max_length = max(max_length,cycle);
      }
      cout<<a<<" "<<b<<" "<<max_length<<"\n";
    }
}
