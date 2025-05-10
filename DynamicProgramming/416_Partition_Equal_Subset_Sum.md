## 416. Partition Equal Subset Sum

- Midium
- 題目: 判斷一個整數陣列是否可以被分成兩個子集合，且這兩個子集合的元素總和相等。

- Example
    - Input: nums = [1,5,11,5]
    - Output: true
    - Explanation: The array can be partitioned as [1, 5, 5] and [11].

- 思路
    - 先判斷整體和是否為奇數，如果是則不可能平分。建立dp[j] 表示「是否可以用目前處理過的數字湊出總和為 j 的子集合」。再倒序遍歷 j 值（從 sum 到 0），保證每個數字只能使用一次。對每個 nums[i]，檢查 dp[j - nums[i]] 是否為 true，若是，代表可以用它來組成 j。

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
    int sum = 0, n = nums.size();
    for (int num : nums) sum += num;

    // 和為奇數時，不可能分為兩個和相等的集合
    if (sum % 2 != 0) return false;

    sum = sum / 2;
    vector<bool> dp(sum + 1, false); // dp[j] 表示：是否能用 nums 中的部分元素湊出總和為 j
    // base case
    dp[0] = true;
    
    // 開始狀態轉移
    for (int i = 0; i < n; i++) // 把 nums 中的每個數拿出來一次。 在第 i 次迴圈結束時，dp 就代表「只用前 i+1 個數字能湊出的所有和」
        for (int j = sum; j >= 0; j--) // 從右往左掃每個目標和 j， 由大到小更新以確保同一次處理 nums[i] 時，它至多被放進背包一次
            if (j - nums[i] >= 0) // 只有當 j ≥ nums[i] 時，才有機會用目前這顆數字去湊出 j
                dp[j] = dp[j] || dp[j - nums[i]];  // dp[j - nums[i]] 為 true 代表：在不使用 nums[i] 的情況下已能湊出金額 j - nums[i]；現在再加上這個 nums[i]，就能達到 j。

    return dp[sum];
    }
};
