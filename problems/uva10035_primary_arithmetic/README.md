# UVa 10035 - Primary Arithmetic

**題目連結**：  
https://zerojudge.tw/ShowProblem?problemid=c014

**解題思路**：
- 設變數(a b)並輸入 (若兩數中有0 則直接結束)
- 設是否進位(carry)和進位了幾次(operation)
- 當a||b還>0時 設一變數sum代表單獨一個位數中的加法加上前一位數的carry
- 若sum>=0 carry = 1 且operation++ 反之則carry = 0
- 持續/10直到a b皆為0
- 判斷operation為多少 輸出結果

**遇到問題與解決**：
- 本題概念較簡單，順利一次通過
- 未來會練習把程式碼寫得更簡潔優雅
  
**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() 
{
    long long a,b;
    while(cin>>a>>b&&(a!=0||b!=0)){
      int carry = 0;
      int operation = 0;
      while(a>0||b>0){
        int sum = a%10+b%10+carry;
        if(sum>=10){
          operation++;
          carry = 1;
        }
        else carry = 0;
        a/=10;b/=10;
      }
      if(operation>1) cout<<operation<<" carry operations.\n";
      else if(operation == 1) cout<<1<<" carry operation.\n";
      else cout<<"No carry operation.\n";
    }
}
```


