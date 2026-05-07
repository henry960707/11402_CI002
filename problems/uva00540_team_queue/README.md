# UVa 00540 - Team Queue

**題目連結**：  
[ZeroJudge - Team Queue](https://zerojudge.tw/ShowProblem?problemid=e564) 

**解題思路**：
- 整個隊伍由多個**小隊（Team）**組成
- 當一個人要排隊時：
  - 如果他的小隊已經有人在排隊，就直接排在**自己小隊的最後面**
  - 如果他的小隊還沒人，就在**整個大隊伍的最後面**新開一個小隊
- 使用以下結構模擬：
  - `map<int,int>`：記錄每個成員屬於哪一個小隊
  - `queue<int> m_line`：記錄目前大隊伍中有哪些小隊（只存 team id）
  - `vector<queue<int>> t_line`：每個小隊內部的成員排隊順序

**遇到問題與解決**：
- 一開始完全沒有頭緒，上網看過資料後才理解「小隊優先」的概念
- 對於 `vector<queue<int>>` 的使用不熟悉，一開始忘記正確初始化
- 後來把結構拆清楚（大隊伍 + 各小隊內部 queue）後，程式架構就清晰很多

**程式碼**：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int t, scenario = 1;
    while (cin >> t && t != 0) {
        cout << "Scenario #" << scenario++ << "\n";
        
        map<int, int> team;                    // 成員 -> 所屬隊伍編號
        for (int i = 0; i < t; i++) {
            int mem;
            cin >> mem;
            for (int j = 0; j < mem; j++) {
                int m;
                cin >> m;
                team[m] = i;
            }
        }
        
        vector<queue<int>> t_line(t);          // 每個小隊內部的 queue
        queue<int> m_line;                     // 大隊伍（存小隊編號）
        
        string cmd;
        while (cin >> cmd && cmd != "STOP") {
            if (cmd == "ENQUEUE") {
                int num;
                cin >> num;
                int group = team[num];
                
                if (t_line[group].empty()) {
                    m_line.push(group);        // 新開一個小隊在大隊伍後面
                }
                t_line[group].push(num);       // 加入小隊內部
            } 
            else if (cmd == "DEQUEUE") {
                int front_team = m_line.front();
                cout << t_line[front_team].front() << "\n";
                t_line[front_team].pop();
                
                // 如果該小隊已經沒人，則從大隊伍移除
                if (t_line[front_team].empty()) {
                    m_line.pop();
                }
            }
        }
        cout << "\n";
    }
    return 0;
}
```
**時間複雜度**：O(Q)（Q 為指令總數）

**空間複雜度**：O(N + T)
