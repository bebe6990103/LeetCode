## 685. Redundant Connection II

- Hard
- 題目: 有根樹的特點為 1.只有一個根節點（root），其餘所有節點都是這個 root 的後代 2.除了 root 以外，每個節點只能有一個父節點。現在有一個「本來是一棵有根樹」的有向圖，並給了一個2維陣列 edges，每個元素是 [u, v]，代表一條「u 指向 v」的有向邊。回傳哪一條邊可以被移除，能讓這個圖重新變回一棵有根樹，而若有多種選擇，則回傳在 edges 陣列中較後出現的邊。
- Example1
    - Input: edges = [[1,2],[1,3],[2,3]]
    - Output: [2,3]
- Example2
    - Input: edges = [[1,2],[2,3],[3,4],[4,1],[1,5]]
    - Output: [4,1]

- 思路
    - 先對所有邊作遍歷，紀錄所有節點的父節點，並找出有兩個父親的節點。接著用 Union-Find 檢查是否存在環，並根據兩步驟的結果決定移除哪條邊。

```cpp
class Solution {
public:
    vector<int> findRedundantDirectedConnection(vector<vector<int>>& edges) {
        int n = edges.size(); // 邊的數量
        vector<int> parent(n + 1, 0);   // 記錄每個節點的父親
        vector<int> can1, can2;         // can1, can2 用來記錄雙父邊

        // Step1: 找有無雙父節點
        for (auto &e : edges) {
            int u = e[0];
            int v = e[1];
            if (parent[v] == 0) {
                parent[v] = u; //紀錄v節點的父節點為u
            }
            else {
                // v 已經有一個父親了，這是第二條
                can1 = {parent[v], v};  // 第一條（較早的）
                can2 = {u, v};          // 第二條（較晚的）
                e[1] = 0; // 先把這條邊禁用
            }
        }
        // Step2: union-find 檢查環
        for (int i = 0; i <= n; i++) {
            parent[i] = i;
        }
        for (auto &e : edges) {
            int u = e[0];
            int v = e[1];
            if (v == 0) continue; // 跳過剛剛暫時禁用的邊
            int pu = find(parent, u);
            if (pu == v) {
                // 有環，分有無雙父
                if (can1.empty()) return e; // 沒有雙父，直接回傳這條環的邊
                return can1; // 有雙父，回傳第一條
            }
            parent[v] = pu;
        }
        // 沒有環，但有雙父，回傳第二條
        return can2;
    }
        
    int find(vector<int> &parent, int x) { // 路徑壓縮，把 x 這條路徑上的所有點直接連到根，未來再查找就直接跳到根，幾乎不需要遞迴
        if (parent[x] != x){
            parent[x] = find(parent, parent[x]);
        } 
        return parent[x];
    }

};
```
