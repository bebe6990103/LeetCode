## 222. Count Complete Tree Nodes
- 題目: 給一顆完全二元樹(Complete Binary Tree)，計算總節點數
- Example
    - Input: root = [1,2,3,4,5,6]
    - Output: 6
- 思路
    - 因為完全二元樹的結構，左右子樹其中一邊一定是滿二元樹的結構，所以只有一定有一側會觸發"left_height == right_height"。
```cpp
class Solution {
public:
    int countNodes(TreeNode* root) {
        TreeNode* left_node = root;
        TreeNode* right_node = root;

        // 紀錄左右子樹的高度
        int left_height = 0;
        int right_height = 0;

        while(left_node != NULL) //計算左子樹(最左)的高度
        {
            left_node = left_node->left;
            left_height++;
        }
        while(right_node != NULL) //計算右子樹(最右)的高度
        {
            right_node = right_node->right;
            right_height++;
        }

        if (left_height == right_height) //如果左右子樹高度相同，代表此樹為 "滿二元樹(perfect binary tree)"，就可用次方計算
        {
            return ( pow(2, left_height) -1 );
        }

        return ( 1 + countNodes(root->left) + countNodes(root->right) ); //如果左右子樹高度不同，用一般方法計算
    }
};
```
