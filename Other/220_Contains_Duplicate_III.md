## 220. Contains Duplicate III

- Hard
- 題目: 找出在一個整數陣列 nums 中，是否存在一對索引 (i, j)，滿足以下三個條件：(1)i != j，即兩個位置不同 (2)兩個索引的距離不能超過 indexDiff (3)兩個值的差不能超過 valueDiff。若滿足上述三個條件，回傳 true，否則回傳 false。

- Example
    - Input: nums = [1,2,3,1], indexDiff = 3, valueDiff = 0
    - Output: true

- 思路
    - 藉由 滑動視窗與有序集合set去處理，對 nums 陣列逐一掃描，每次維護一個「最近的 indexDiff 個元素」的集合，再檢查是否符合第兩個條件 it <= (long long) nums[i] + valueDiff 。
    - |nums[i] - nums[j]| <= valueDiff 轉換成 nums[i] - valueDiff <= nums[j] <= nums[i] + valueDiff

```cpp
class Solution {
public:
    bool containsNearbyAlmostDuplicate(vector<int>& nums, int indexDiff, int valueDiff) {
        
        // set 為  有序容器，會自動把元素按照大小排序，並且不允許重複元素，支持insert()、erase()、find()、lower_bound() 等操作
        set<long long> window; // 用 long long 防止溢位， window 模擬一個滑動視窗，維持最近 indexDiff 個元素

        for (int i = 0; i < nums.size(); ++i) {
            // 找出大於等於 nums[i] - valueDiff 的最小值
            auto it = window.lower_bound( (long long) nums[i] - valueDiff); // lower_bound(target)，這會找出集合中第一個 ≥ target 的值。

            // 檢查這個值是否在 nums[i] + valueDiff 範圍內
            if (it != window.end() && *it <= (long long) nums[i] + valueDiff) { 
                // it == window.end() 表示「查無此元素」
                 
                return true;
            }

            window.insert(nums[i]);

            // 控制滑動視窗的大小
            if (i >= indexDiff) {
                window.erase(nums[i - indexDiff]);
            }
        }

        return false;
    }
};
```
