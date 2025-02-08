## 452. Minimum Number of Arrows to Burst Balloons

- 題目:假設二為平面上有很多圓型氣球，這些圓形投影到x軸時會形成一個區間。問沿著x軸前進，可以垂直向上射箭，至少需要設幾箭，才能將氣球全部射破。
- Example
    - points = [[10,16],[2,8],[1,6],[7,12]]
    - Output: 2
- 思路
    - 先按照 開始時間 排序，若 開始時間 相同則按照 結束時間 排序
        - 若下個開始點大於連續區間的結束點則無法射破，即Arrow+1，每次比較結束點，以較短的結束點作為連續區間的結束點。
    - 選擇當前最早結束的氣球 (end = min(end, this_end)) 作為射箭範圍，確保能夠射穿最多的氣球
```cpp
class Solution {
public:
    int findMinArrowShots(vector<vector<int>>& points) {

        if (points.empty()) return 0;  // 沒有氣球時，返回 0

        // 先按照 xstart 排序，若 xstart 相同則按照 xend 排序
        sort(points.begin(), points.end(), [](const vector<int>& a, const vector<int>& b)
        {
            if (a[0] == b[0]) 
                return a[1] < b[1];  // 若 xstart 相同，則按 xend 排序
            return a[0] < b[0];  // 依據起始點升序排序
        });

        int arrows = 1;
        int end = points[0][1];

        for (const auto& balloon : points)
        {
            int this_strat = balloon[0];
            int this_end = balloon[1];

            if (this_strat > end)
            {
                arrows = arrows +1;
                end = this_end;
            }
            else
            {
                if (this_end < end)
                {
                    end = this_end;
                }
            }

        }
        return arrows;
    }
};
```
