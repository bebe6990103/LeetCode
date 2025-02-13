## 236. Lowest Common Ancestor of a Binary Tree
- 題目:透過節點 q, p，找到其在二元樹的最低共用源始(LCA)
- Example
    - Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
    - Output: 3
- 思路
    - 透過後序尋訪，由下往上檢查第一個相交的節點
```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root == NULL)
        {
            return NULL;
        }
        if (root == p || root == q)
        {
            return root;
        }
        TreeNode* left = lowestCommonAncestor(root->left, p, q); //先從左側找
        TreeNode* right = lowestCommonAncestor(root->right, p, q); // 再從左側找
        
        if(left != NULL && right != NULL) // 條件1: 以 root 為根的 左右子樹找到 p 和 q，那 LCA 祖先一定是 root
        {
            return root;
        }
        if(left == NULL && right == NULL) // 條件2: 以 root 為根的 左右子樹找不到 p 和 q
        {
            return NULL;
        }
        if (left == NULL) // 條件3: 只有其中一側子樹有找到 p or q，回傳該節點
        {
            return right;
        }
        else
        {
            return left;
        }
    }
};
```
