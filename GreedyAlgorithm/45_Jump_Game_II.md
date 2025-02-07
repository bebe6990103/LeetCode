## 45. Jump Game II

- 題目
    - You are given a 0-indexed array of integers nums of length n. You are initially positioned at nums[0].Each element nums[i] represents the maximum length of a forward jump from index i. In other words, if you are at nums[i], you can jump to any nums[i + j] where:0 <= j <= nums[i] and i + j < n
    - Return the minimum number of jumps to reach nums[n - 1]. The test cases are generated such that you can reach nums[n - 1].

- Example
    - Input: nums = [2,3,1,1,4]
    - Output:2
    - Explanation: The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.

- 思路
    - 在回圈中，透過further一值紀錄當前可達最遠位置，同時比較further和原地起跳(nums[i])哪種較遠去更新 further，再藉由maxReach去精確計算步數，避免ex: [1,2,1,1,2]這種會重複計算步數的情況發生
- 時間複雜度：O(n)
- 空間複雜度：O(1)

```
class Solution {
public:
    int jump(vector<int>& nums){
        int length = nums.size();
        int maxReach = 0; // 目前這一步內可以到達的最遠位置。
        int steps = 0;
        int further = 0; // 從目前遍歷到的所有位置中，下一步能夠到達的最遠位置。
        for(int i=0;maxReach < nums.size()-1;i++)
        {
            further = max(further, i+nums[i]); //  挑選是 先前紀錄的further 或 本次從nums[i]起跳 哪個更遠
            if (maxReach == i) //判斷當遍歷到目前位置 i 時，是否已經走到了上次可達的最遠距離 maxReach？
            {
                steps = steps+1;
                maxReach = further; 
            }
        }
        return steps;
    }
};
```
