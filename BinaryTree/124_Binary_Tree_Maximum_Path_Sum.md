## 124. Binary Tree Maximum Path Sum
- Hard
- 題目: 題目: 給定一棵二元，需要找出該樹中 任意一條路徑的節點值總和最大 的那條路徑，並回傳這個「最大路徑和」的值
- Example
    - Input: root = [-10,9,20,null,null,15,7]
    - Output: 42
    - ![image](https://hackmd.io/_uploads/rys3i6vAkl.png)
- 思路
    - 從頂點開始一直向下遞迴計算，並每次紀錄該路徑的總和值，若小於0則選擇拋棄該側子樹。

```cpp
class Solution {
public:
    int maxSum = INT_MIN; // 全域變數，用來儲存目前為止的最大路徑和

    int dfs(TreeNode* node) {
        if (!node) return 0;

        // 遞迴計算左右子樹的最大貢獻值，如果小於0就捨棄該側
        int leftGain = max(0, dfs(node->left));
        int rightGain = max(0, dfs(node->right));

        // 計算包含左右子樹的當前節點最大路徑和
        int currentMax = node->val + leftGain + rightGain;

        // 更新全域最大值
        maxSum = max(maxSum, currentMax);

        // 回傳給從這個節點出發往下延伸的最大值
        return node->val + max(leftGain, rightGain);
    }

    int maxPathSum(TreeNode* root) {
        dfs(root); // 從 root 開始 DFS
        return maxSum;
    }
};
```
