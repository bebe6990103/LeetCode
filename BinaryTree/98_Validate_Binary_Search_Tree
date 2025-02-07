## 98. Validate Binary Search Tree
- 題目:給定二元樹的root，確定它是否是有效的二元搜尋樹（BST），即任意節點的值要大於左子樹所有節點的值，且要小於等於右子樹所有節點的值。
- Example
    - ![image](https://github.com/bebe6990103/LeetCode/blob/main/BinaryTree/Image/98_Example.png)
- 思路
    - 透過在函式中增加 max 和 min 兩個節點，以在遞迴檢查過程中確認是否有超出邊界的狀況。
```
class Solution {
public:
    bool check (TreeNode* root, TreeNode* maxNode, TreeNode* minNode){
        if (root == NULL)
        {
            return true;
        } 
        if (maxNode != NULL && root->val >= maxNode->val )
        {
            return false;
        }
        if (minNode != NULL && root->val <= minNode->val )
        {
            return false;
        }
        return ( check(root->left, root, minNode) && check(root->right, maxNode, root) );
    }
    bool isValidBST(TreeNode* root) {
       return (check(root, NULL, NULL));
    }
};
```
