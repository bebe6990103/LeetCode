- 題目:在BTS中刪除一個值。
- Example
    - ![image](https://github.com/bebe6990103/LeetCode/blob/main/Image/450_Example.png)
- 思路
    - 在查詢BST的架構下增加"刪除"的功能，情況一: 若KEY Node為末端節點，則直接刪除即可。情況二: KEY Node 有一側右 or 左子樹，則直接使該子樹直接繼承。情況三: 若KEY Node左右皆有子樹，則選擇右子樹中最左側(最小值)的節點取代KEY Node，就不會破壞BST的架構。
```
class Solution {
public:
    TreeNode* GetMin(TreeNode* theNode) {
        // 抓取右子樹(theNode)中最小的Node
        while (theNode->left != NULL)
        {
            theNode = theNode->left;
        }
        return theNode;
        }
    TreeNode* deleteNode(TreeNode* root, int key) {
        if (root == NULL)
        {
            return NULL;
        }
        if (root->val == key)
        {
            if(root->left == NULL && root->right == NULL )
            {
                return NULL; // 若為末端node，沒有左右節點，則直接刪除
            }
            else if (root->left == NULL && root->right != NULL)
            {
                return root->right; // 如果左子樹為空，則直接讓右子樹繼承
            }
            else if (root->left != NULL && root->right == NULL)
            {
                return root->left; // 如果右子樹為空，則直接讓左子樹繼承
            }
            else // 如果左右子樹都有值，就用右子樹中最小的NODE取代 key node
            {
                TreeNode* tempt = GetMin(root->right); // 找到右子樹中最小的NODE
                root->val = tempt->val; // 複製他的值
                root->right = deleteNode(root->right, root->val); // 再次將相同 val 的刪掉
            }
        }
        else if (root->val < key) // 往右子樹
        {
            root->right = deleteNode(root->right, key);
        }
        else if (root->val > key) // 往左子樹 
        {
            root->left = deleteNode(root->left, key);  
        }
        return root;  // return root，保持 BST 結構
    }
};
```
