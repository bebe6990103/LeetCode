## 435. Non-overlapping Intervals

- 題目:輸入一個區間集合，若想使其中的區間互不重疊，計算至少需要移除多少個區間。
- Example
    - Input: intervals = [[1,2],[2,3],[3,4],[1,3]]
    - Output: 1
- 思路
    - 先將區間集合(vector)依照結束的時間點進行排序，接著每次都看最早結束的區間為何，接著找下一個區間，藉此就能得到最多有幾個區間不相交。隨之用 總區間數 - 有幾個區間不相交，即可得到需移除多少個區間。
    - 運用貪婪演算法，儘量選擇最早結束的區間，以保留更多不重疊的區間。

```cpp
class Solution {
public:
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        if (intervals.empty()) return 0;  // 防止空陣列

        // 依據區間的結束點（intervals[i][1]）進行排序
        sort(intervals.begin(), intervals.end(), [](const vector<int>& a, const vector<int>& b) {
            return a[1] < b[1];
        });

        int count = 1;  // 計算不重疊的區間數，因必須取起始區間再開始比較，因此 default值為 1

        // intervals[0] 表示第一個區間，通常為 [start, end]
        // intervals[0][1] → 代表第一個區間的結束時間（end = 2）
        int end = intervals[0][1];

        // 遍歷排序後的區間，選擇不重疊的
        for (const auto& intvs : intervals) {
            int start = intvs[0];
            if (start >= end) {
                count++;       // 如果當前區間的起點不重疊，計數+1
                end = intvs[1]; // 更新當前結束時間
            }
        }

        return intervals.size() - count;  // 移除的最少的重疊區間 = 全部區間數 - 最多有多少區間不相交
    }
};
```
