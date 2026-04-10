# UVa 272 - Tex Quotes

**題目連結**：  
https://zerojudge.tw/ShowProblem?problemid=c007

**解題思路**：


**遇到問題與解決**：


**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() 
{
    cin.sync_with_stdio(0);
    cin.tie(0);
    string str;
    bool check = true;
    while(getline(cin,str)){
      for(int i = 0;i<str.length();++i){
        if(str[i] == '"'){
          if(check){
            cout<<"``";
            check = false;
          }
          else {
            cout<<"''";
            check = true;
          }
        }
        else cout<<str[i];
      }
      cout<<"\n";
    }
}
```
