## 322. Coin Change
- Medium
- 題目: 給定一組不同面額的硬幣 coins 和一個目標金額 amount，找出能夠湊出該金額的最少硬幣數量。如果無法湊出 amount，則返回 -1。
- Example
    - Input: coins = [1,2,5], amount = 11
    - Output: 3
- 思路
    - 遍歷所有金額 i，從 0 到 amount，內層迴圈再遍歷每個可用的硬幣 coin，每當有個可能結果就做比較
```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<int> dp(amount+1, amount+1); // 創建dp陣列儲存每個金額所需的最少硬幣，default先設為amount+1 代表無效的值

        dp[0]=0; // base case，金額0 需要0的硬幣
        for (int i=0; i<dp.size(); i++) //對每個金額做尋訪
        {
            for (int coin : coins ) // 嘗試使用不同面額的硬幣來更新
            {
                if( i - coin < 0) // 如果目前金額 < 該硬幣幣值，則跳過
                {
                    continue;
                }
                dp[i] =min( dp[i], 1+dp[i-coin]); // 比較 目前陣列紀錄的硬幣數量 or 1+dp[i-coin] 硬幣數量少。  1+dp[i-coin] 代表 加上 coin 這一枚硬幣
            }
        }
        if (dp[amount] == amount + 1)
        {
            return -1;  // 無法湊出 amount，回傳 -1
        }
        else
        {
            return dp[amount];  // 回傳最少硬幣數量
        }
    }
};
```
