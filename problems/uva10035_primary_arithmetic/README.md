# UVa 10035 - Primary Arithmetic

**題目連結**：  
https://zerojudge.tw/ShowProblem?problemid=c014

**解題思路**：


**遇到問題與解決**：


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

