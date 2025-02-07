## 100. Same Tree
- 題目:判斷兩顆 binary tree 是否相同。
- Example
    - ![image](https://hackmd.io/_uploads/HJ7fBcfKkg.png)
- 思路
    - 遞迴比較左子樹與右子樹。
```
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (p == NULL && q == NULL)
        {
            return true;
        }
        if (p == NULL || q == NULL)
        {
            return false;
        }
        if (p->val != q->val)
        {
            return false;
        }
        return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
    }
    
};
```
