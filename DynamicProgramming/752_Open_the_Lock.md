## 752. Open the Lock
- Medium
- 題目: 有一個四位數的密碼鎖，每個輪盤可以向前或向後轉動 0-9。起始狀態為 "0000"。給定一組 deadends（無法轉動的狀態），如果密碼鎖進入這些狀態則無法繼續操作。打開的數字組合為 target。找出解開密碼鎖的最少次數，即需要多少步才能從 "0000" 轉到 target，如果無法達到，返回 -1。 
- Example
    - Input: deadends = ["0201","0101","0102","1212","2002"], target = "0202"
    - Output: 6
- 思路
    - 使用 BFS（廣度優先搜尋） 來求解，因為 BFS 能夠確保最先找到的解就是最短路徑。
```cpp
class Solution {
public:
    int openLock(vector<string>& deadends, string target) {
        
        unordered_set<string> deads; 
        deads.insert(deadends.begin(), deadends.end()); // 紀錄被禁止的密碼，用mapping以供查詢
        
        unordered_set<string> visited; // 紀錄已經尋訪過的密碼

        int steps = 0; //紀錄轉動次數
        queue<string> q;
        q.push("0000"); //先加入初始化的 0000 進queue
        visited.insert("0000"); //先加入初始化的 0000

        while( !q.empty() ){

            int size = q.size();
            for(int i=0; i<size; i++){
                string cur = q.front(); //取出目前的最前的queue
                q.pop(); //pop掉
                if ( deads.count(cur) ){ // 檢查是否為被禁止的密碼
                    continue;
                }
                if ( cur == target ){ // 檢查是否為目標
                    return steps;
                }
                for (int j=0; j<4; j++){ //嘗試將每一個輪盤都 +1
                    string up = plusOne(cur, j);
                    if ( !visited.count(up) ){ // 檢查是否尋訪過
                        q.push(up);
                        visited.insert(up);
                    }
                }
                for (int j=0; j<4; j++){ //嘗試將每一個輪盤都 -1
                    string down = minusOne(cur, j);
                    if ( !visited.count(down) ){ // 檢查是否尋訪過
                        q.push(down);
                        visited.insert(down);
                    }
                }
            }
            steps++;
        }
        return -1;
    }
    string plusOne (string s, int index){ //針對密碼鎖 9往上滑動變0
        if ( s[index] == '9' ){
            s[index] = '0';
        }
        else s[index] = s[index] = s[index] + 1 ;
        
        return s;
    }
    string minusOne (string s, int index){ //針對密碼鎖 0往下滑動變9
        if ( s[index] == '0' ){
            s[index] = '9';
        }
        else s[index] = s[index] = s[index] - 1 ;
        
        return s;
    }
};
```
