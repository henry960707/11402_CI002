# UVa 490 - Rotating Sentences

**題目連結**：  
https://zerojudge.tw/ShowProblem?problemid=c045

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
    vector<string> str;
    string s;
    int max_line = 0;
    while(getline(cin,s)){
      str.push_back(s);
      if(s.length()>max_line) max_line = s.length();
    }
    for(int i = 0;i<max_line;++i){
      for(int j = str.size()-1;j>=0;--j){
        if(i>=str[j].length()) cout<<" ";
        else cout<<str[j][i];
      }
      cout<<"\n";
    }
}
```
