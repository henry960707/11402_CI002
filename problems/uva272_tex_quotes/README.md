# UVa 272 - Tex Quotes

**題目連結**：  
https://zerojudge.tw/ShowProblem?problemid=c007

**解題思路**：
- 主程式前兩段程式碼用來提高效率
- 用getline解決換行問題
- bool check判斷當前句子是否被括起來


**遇到問題與解決**：
- 初次遇到題目嘗試創個大陣列包含所有的字(失敗)
- 不知怎麼處理換行問題(使用getline)
- 對getline語法稍顯不熟

  
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
