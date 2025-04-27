## 847. Shortest Path Visiting All Nodes

- Hard
- 題目: 有一張無向且連通的圖，圖上有 n 個節點，編號從 0 到 n-1，給定一個陣列 graph，其中 graph[i] 表示「節點 i 直接連接的所有其他節點」的列表。請回傳找到的一條最短路徑，這條路徑要至少拜訪過每一個節點一次，路徑可以從任何一個節點開始或結束，也可以重複拜訪同一個節點。

- Example
    - Input: graph = [[1,2,3],[0],[0],[0]]
    - Output: 4

- 思路
    - 透過visited[i][mask]來記錄當「目前停在節點 i」時，拜訪過的節點狀態，mask為二進制，位數表示一個節點，0/1表示是否拜訪過。 尋訪主要透過BFS演算法搭配queue，逐層遍歷，也因此能確定找到的路徑為最短路徑之一。

```cpp
class Solution {
public:
    int shortestPathLength(vector<vector<int>>& graph) {
        int n = graph.size();
        if (n == 1) return 0;

        // 狀態：(目前節點, 已經經過的節點mask)
        queue<pair<int, int>> q;
        vector<vector<bool>> visited(n, vector<bool>(1 << n, false)); // 1 << n 表示 "2 的 n 次方"
        // visited[i][mask] 表示 當「目前停在節點 i」時，拜訪過的節點狀態是 mask（一個二進位數字，記錄哪些點走過）

        // 所有節點都可以作為起點
        for (int i = 0; i < n; ++i) {
            q.push({i, 1 << i}); // 1 << i 把數字 1 向左移動 i 位元
            visited[i][1 << i] = true;
        }

        int target = (1 << n) - 1; // 全部節點都經過的狀態
        int steps = 0;

        while (!q.empty()) {
            int size = q.size();
            while (size--) {
                auto [node, mask] = q.front(); // node 是目前位置，mask 是目前已經拜訪過的節點集合
                q.pop();

                // 如果所有節點都經過了
                if (mask == target) return steps; // mask == target 為 所有節點都已經拜訪

                // 往所有鄰居擴展
                for (int nei : graph[node]) {
                    int next_mask = mask | (1 << nei); // 用 bitwise OR，把「目前已拜訪狀態」加上這次要走的新鄰居，表示新狀態下多拜訪一個點。 ex:mask=1011, nei=2，1<<2=0100, 1011|0100=1111
                    if (!visited[nei][next_mask]) { // 判斷「同樣在鄰居點、同樣的拜訪狀態」這個組合有沒有處理過，避免重複
                        visited[nei][next_mask] = true; // 標記這個新狀態已經處理過
                        q.push({nei, next_mask}); //把新狀態推進 queue，等下一層繼續擴展
                    }
                }
            }
            steps++; // 每走完一層（代表走了一步），步數加一
        }
        return -1; // 不會發生
    }
};
```
