## 757. Set Intersection Size At Least Two
- Hard
- 題目: 給定一個 2D 整數陣列 intervals，其中每個 intervals[i] = [starti, endi] 代表一個整數區間。找出一個最小的整數集合 nums，使得每個區間 [starti, endi] 至少包含 2 個數字
- Example
    - Input: intervals = [[1,3],[3,7],[8,9]]
    - Output: 5
- 思路
    - 每次維護區間的最大的兩個數last1, last2，接著以下個區間頭去比較last2，若不重疊，直接再挑該區間最大的兩個數字，若區間頭小於last2而大於last1則代表只覆蓋到最後一個數，需要再挑一個數字加入。
    - Greedy策略: 由左至右尋訪每個區間，每次都確保至少包含到兩個數。
```cpp
class Solution {
public:
    int intersectionSizeTwo(vector<vector<int>>& intervals) {
        int len = intervals.size();
        
        // 先根據 end 進行排序，先結束的放前面，若 end 相同，則依 start 點排列，先開始的放後面(較符合判斷式)
        sort(intervals.begin(), intervals.end(), [](const vector<int>& a, const vector<int>& b) {
            if (a[1] == b[1]) {
                return a[0] > b[0];
            }
            return a[1] < b[1];
        });

        int last1 = intervals[0][1] - 1; // 選擇區間內的倒數第二個數
        int last2 = intervals[0][1];     // 選擇區間內的最後一個數
        int ans = 2; // 初始選擇 2 個數

        for (int i = 1; i < len; i++) {
            if (intervals[i][0] > last2) { 
                // 當前區間與 last2 沒有重疊，所以直接將最後兩個數更新成last
                last1 = intervals[i][1] - 1;
                last2 = intervals[i][1];
                ans = ans + 2;
            } else if (intervals[i][0] > last1) { 
                // 當前區間只覆蓋 last2，但沒覆蓋 last1，需要再選一個新數字
                last1 = last2;
                last2 = intervals[i][1];
                ans = ans + 1;
            }
            // 如果 intervals[i][0] < last1 代表已經覆蓋2個數以上 就不管
        }
        return ans;
    }
};
```
