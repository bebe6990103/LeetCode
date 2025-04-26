## 210. Course Schedule II

- Medium
- 題目: 題目: 一共 numCourses 門課要修，課程編號從 0 到 numCourses - 1。每門課有可能會有「先修課」的限制，這些限制會用一個陣列 prerequisites [a, b] 呈現，即要先修完課程 b，才能去修課程 a。請回傳一個可行的「修課順序」陣列，若無法修完全部課程則回傳空陣列。
- Example
    - Input: numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]
    - Output: [0,2,1,3]
- 思路
    - 先透過vector adj，畫出修課關係之間的圖，並透過vector in_degree紀錄各課程的先修課程數量，接著用queue搭配BFS演算法下去做排查以規劃修課順序，最後檢查修課順序是否等於總課程數即可知道圖是否環。

```cpp
class Solution {
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> adj(numCourses);      // 鄰接表 adjacency list，表示途中每一個頂點相鄰的邊集的集合
        vector<int> in_degree(numCourses, 0);     // 入度表，指進入該節點（頂點）的邊的條數

        // 建立圖與入度表
        for (const auto& p : prerequisites) {
            int course = p[0];
            int pre = p[1];
            adj[pre].push_back(course); // adj[1].push_back(3) 則為課堂1為課堂3的先修課
            in_degree[course]++;
        }

        queue<int> q;
        vector<int> order; // 修課順序

        // 將所有in_degree為0的課程放進queue
        for (int i = 0; i < numCourses; i++) {
            if (in_degree[i] == 0){
                q.push(i);
            }
        }

        // BFS
        while (!q.empty()) {
            int curr = q.front();
            q.pop();
            order.push_back(curr);
            for (int next : adj[curr]) { // 遍歷目前課程 curr 的所有後續課程
                in_degree[next]--;         // 先修課修完，後修課的in_degree -1
                if (in_degree[next] == 0){  // 如果這門課已經沒有先修課了
                    q.push(next);          // 可以加入queue，等著修這門課
                }
            }
        }

        // 如果順序數量等於課程數量，表示可修完所有課
        if (order.size() == numCourses) return order;
        return {}; // 有環，無法修完

    }
};
```
