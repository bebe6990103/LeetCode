## 1029. Two City Scheduling
- 題目: 總共有2n個人，n個去 A 城市, n個去 B 城市，給定一組陣列costs，代表每個人去A,B城市的成本，求分配後最小的總成本。
- Example
    - Input: costs = [[10,20],[30,200],[400,50],[30,20]]
    - Output: 110
- 思路
    - 計算出每個人去 B 城市的成本，接著排序，即可得到誰該去 B 城市，而誰該去 A 城市。
    - Greedy策略: 只考慮讓「去 B 城市比較划算」的人去 B 城市，這樣保證整體成本最低。
```cpp
class Solution {
public:
    int twoCitySchedCost(vector<vector<int>>& costs) {

        // 根據「去 B 城市 - 去 A 城市」的成本由小到大排序 ，即去B城市的成本，越小就代表去B城市適合。
        sort(costs.begin(), costs.end(), [](vector<int>& a, vector<int>& b) {
            return (a[1] - a[0]) < (b[1] - b[0]);
        });

        int people = costs.size()/2; //每個城市去的人數
        int totalCost = 0;

        for (int i=0; i<people; i++) // 去B城市的成本相加
        {
            totalCost = totalCost + costs[i][1];
        }

        for (int i=people; i< 2*people; i++) // 去A城市的成本相加
        {
            totalCost = totalCost + costs[i][0];
        }
        return totalCost;
    }
};
```
