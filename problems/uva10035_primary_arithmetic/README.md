# UVa 10035 - Primary Arithmetic

**題目連結**：  
[ZeroJudge - c014](https://zerojudge.tw/ShowProblem?problemid=c014)

**解題思路**：
- 計算兩個大數相加時總共產生幾次進位（carry）
- 因為數字可能很長，不能直接用一般整數相加
- 從個位數開始逐位相加，並記錄進位情況，最後統計總進位次數
- 輸入以兩個 0 結束

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


