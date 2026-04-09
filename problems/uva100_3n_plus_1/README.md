# UVa 00100 - The 3n + 1 problem

**題目連結**：  
https://zerojudge.tw/ShowProblem?problemid=c039

**解題思路**：
- 經典 Collatz 猜想模擬題（3n+1 問題）
- 給定區間 [a, b]，計算區間內每個數字走到 1 所需的步數（cycle length）
- 找出區間內最大的步數後輸出


**遇到問題**:
- 一開始想用**遞迴**寫，但一直寫不出來（容易 stack overflow 或邏輯錯誤）
- 後來改用 `while(true)` + `break` 的方式模擬循環，才成功跑出正確結果
- 目前程式碼可以通過，但寫得比較直白，未來會繼續優化



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


**時間複雜度**：O((b - a) × log n)  
**空間複雜度**：O(1)
