## 910. Smallest Range II
- 題目: 給一個陣列以及一整數k，陣列中的每個數字必須作+k或-k，求最後陣列中最大值最小值的差越小越好。
- Example
    - Input: nums = [1,3,6], k = 3
    - Output: 3
- 思路
    - 直覺為較大的值該-k，而較小的值該+k，但不知道哪個才是最佳分切點，用尋訪的方式將每個點作為分切點，再檢查是否會更新上下界。
    - Greedy策略: 只需考慮相鄰數字的變化，而不需要檢查所有可能的組合
```cpp
class Solution {
public:
    int smallestRangeII(vector<int>& nums, int k) {
        sort(nums.begin(), nums.end()); //排序
        int len = nums.size();
        int min_val = nums[0]; // // 原先最小值
        int max_val = nums[len - 1]; // 原先最大值
        int diff = max_val - min_val; // 初始範差距

        if (k > nums[len-1] - nums[0]) // 若 k > 原先最大與最小的差距，那一起 +k or -k　才可得最小差距
        {
            return nums[len-1] - nums[0];
        }
        
        // 若 k ＜ 原先最大與最小的差距，則計算
        for(int i=0; i<len-1; i++)
        {
            // 將比較大的那側 -k ， 比較小的那側 +k ，但不知該從哪邊最分隔點，因此做尋訪檢查 
            int new_max = max(max_val -k , nums[i]+k ); // 每次計算 i 為分隔點，作 +k ，並確認是否有更新 max_val
            int new_min = min(min_val +k , nums[i+1]-k); // 再檢查 (i+1) -k  後是否有更新 min_val ，
            diff = min(diff, new_max - new_min);
        }
        return diff;
    }
};
```
