## 312. Burst Balloons

- Hard
- 題目: 從一個整數陣列 nums 中戳破所有氣球，並讓你獲得的總硬幣數量最大。每次戳破一顆氣球，你會得到的分數為：左側氣球數值 × 當前氣球數值 × 右側氣球數值。如果左右超出陣列範圍，則當作是數值為 1 的虛擬氣球。

- Example
    - Input: nums = [3,1,5,8]
    - Output: 167
    - Explanation: nums = [3,1,5,8] --> [3,5,8] --> [3,8] --> [8] --> [], coins =  3*1*5 + 3*5*8 + 1*3*8 + 1*8*1 = 167

- 思路
    - 反向思考，將dp[i][j]設為開區間，考慮最後戳破哪一個氣球，所得到的分數最高，以此建構出狀態轉移方程。
    - 先在原始陣列 nums 左右補上虛擬氣球 1，然後建立 dp[i][j] 表示戳破區間 (i, j) 中間所有氣球所能獲得的最大分數。透過三層迴圈處理所有可能的區間與最後戳破的氣球位置，最終回傳 dp[0][n+1] 即為答案。這樣能確保每次戳破的決策都建立在已知最優的子問題解之上，達到整體最佳結果。

```cpp
class Solution {
public:
    int maxCoins(vector<int>& nums) {
        int n = nums.size();
        // 添加兩側的虛擬氣球

        vector<int> points(n + 2, 1);
        points[0] = points[n + 1] = 1;

        for (int i = 1; i <= n; i++) {
            points[i] = nums[i - 1];
        }

        // base case 已經都被初始化為 0
        vector<vector<int>> dp(n + 2, vector<int>(n + 2, 0));

        // 開始狀態轉移
        // i 區間左端（從右往左）
        for (int i = n; i >= 0; i--) {
            // j 區間右端（從左往右）
            for (int j = i + 1; j < n + 2; j++) {
                // 把 k 作為最後戳破的氣球
                for (int k = i + 1; k < j; k++) {
                    // 擇優作選擇
                    dp[i][j] = max( // 區間 (i, j) 中所有氣球被戳破的最大得分
                        dp[i][j], 
                        dp[i][k] + dp[k][j] + points[i]*points[j]*points[k]
                    );
                }
            }
        }
        return dp[0][n + 1]; 
    }
};
