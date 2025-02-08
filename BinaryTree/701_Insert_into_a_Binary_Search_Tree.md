## 701. Insert into a Binary Search Tree
- 題目:在BTS中插入一個值。
- Example
    - ![image](https://github.com/bebe6990103/LeetCode/blob/main/Image/701_Example.png)
- 思路
    - 利用 BTS 左小右大的特性去做遞迴尋訪，當發現子樹為"NULL"則創建一個新的Node並賦值"Value"。
```cpp
class Solution {
public:
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        if (root == NULL)
        {
            return new TreeNode(val);
        }
        if (val > root->val ) // 往右子樹
        {
            root->right = insertIntoBST(root->right, val);
        }
        else // 往左子樹 
        {
            root->left = insertIntoBST(root->left, val);  
        }
        return root;  // return root，保持 BST 結構
    }

};
```
