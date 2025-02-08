## 700. Search in a Binary Search Tree
- 題目:在BTS中找尋一個樹是否存在，若是則回傳該NODE，若否則回傳 NULL。
- Example
    - ![image](https://github.com/bebe6990103/LeetCode/blob/main/Image/700_Example.png)
- 思路
    - 利用 BTS 左小右大的特性去做遞迴尋訪。
```cpp
class Solution {
public:
    TreeNode* searchBST(TreeNode* root, int val) {
        if (root == NULL)
        {
            return NULL;  // 先檢查是否為 NULL，否則無法做後續的比較。且若為NULL則代表全都比較完了，並未找到目標值。
        }
        else if (root->val == val)
        {
            return (root); // 檢查是否相同
        }
        else if ( val < root->val )
        {
           return searchBST(root->left, val); // 向左子樹繼續搜尋
        }
        return searchBST(root->right, val); // 最後的情況為向右子樹繼續搜尋
    }
        
};
```
