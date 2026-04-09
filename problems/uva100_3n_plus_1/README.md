# UVa 00100 - The 3n + 1 problem

**題目連結**：  
https://zerojudge.tw/ShowProblem?problemid=c039

**解題思路**：


**遇到問題**:


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
