## 455. Assign Cookies
- 題目: 將不同大小的餅乾分配給具有不同餅乾大小需求的小孩，回傳最多可以滿足幾個小孩。
- Example
    - Input: g = [1,2,3], s = [1,1]
    - Output: 1
- 思路
    - 先將餅乾大小和小孩需求進行排序，使用兩個指標 g, s 去做遍歷。
    - Greedy策略: 嘗試用最小的餅乾滿足最小需求的小孩，若不滿足小孩胃口則si++，直到遍歷完所有小孩或餅乾

```cpp
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(g.begin(), g.end()); // 由小到大排序
        sort(s.begin(), s.end()); // 由小到大排序

        int ans = 0;
        int gi = 0, si = 0; // 透過兩個指標處理
        
        while (gi < g.size() && si < s.size()) //檢查是否有超出邊界
        {
            if (s[si] >= g[gi])  // 如果餅乾大小足夠滿足小孩
            { 
                ans++;  // 滿足一個小孩
                gi++;   // 移動到下一個小孩
            }
            si++; // 無論是否滿足，餅乾都要消耗掉
        }
        
        return ans;
    }
};
```
