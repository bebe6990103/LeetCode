## 55. Jump Game

- 題目
    - You are given an integer array nums. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position.Return true if you can reach the last index, or false otherwise.
- Example
    - Input: nums = [2,3,1,1,4]
    - Output: true
    - Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.

### solution 1 動態規劃!?

- 思路
    - 額外建立一矩陣dp[]以標註對應的格子是否可以到達(dp[i]>0)，依序讀取nums[]的值，再透過第二個迴圈更新矩陣dp[]。
- 說明
    - 宣告一陣列dp[]，值代表該位置能跳至的最遠距離，default為-1，代表無法到達該位置。一開始將除第0格外的dp[]皆設為-1，從至第0格開始向後檢查，若遇到dp[]值為-1則 return false，若非，則更新可到達最遠的dp[]為0。

- 時間複雜度: O(n²)
- 最壞情況
    - 當 nums 中的值全是 1（如 [1, 1, 1, 1, ..., 1]），每次只能往前跳一步，內層迴圈會遍歷接下來的每個元素。
```cpp
#include <vector>
#include <algorithm>  // For std::fill

class Solution {
public:
    bool canJump(std::vector<int>& nums) {
        int length = nums.size();
        std::vector<int> dp(length, -1);  // Initialize with -1
        dp[0] = 0;  // Starting position

        for (int i = 0; i < length; i++) {
            if (dp[i] == -1) {
                return false;  // Cannot reach this position
            }
            
            dp[i] = i + nums[i];  // Corrected assignment

            if (dp[i] >= length - 1) {
                return true;  // Can reach or exceed the last index
            }

            // Mark reachable positions
            for (int j = i + 1; j <= dp[i] && j < length; j++) {
                dp[j] = 0;
            }
        }
        return false;
    }
};
```

### solution 2 Greedy Algorithm 解法

- 思路
    - 透過一 maxReach 值標註目前最遠可到達的格子，若目前 maxReach<i 即 return false，若非則更新 maxReach，當maxReach >= nums.size() - 1 代表能夠越過最後一格。
- 時間複雜度：O(n)

```cpp
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int maxReach = 0;
        for(int i=0; i < nums.size(); i++ )
        {
            if (maxReach<i)
            {
                return false;
            }
            if(maxReach < i + nums[i])
            {
                maxReach = i + nums[i]; 
            }
            
            if (maxReach >= nums.size() - 1)
            {
                return true;  // 已可到達最後一個位置
            }
        }
        return true;
    }
};
```
