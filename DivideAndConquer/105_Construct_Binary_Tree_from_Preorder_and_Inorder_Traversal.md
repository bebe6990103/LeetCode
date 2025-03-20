## 105. Construct Binary Tree from Preorder and Inorder Traversal
- Medium
- 題目: 給定兩個整數陣列，分別是二元樹的前序遍歷 preorder，與 中序遍歷 inoreder，根據這兩個遍歷結果 建構出該二元樹，並傳回根節點
- Example
    - Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
    - Output: [3,9,20,null,null,15,7]
    - https://github.com/bebe6990103/LeetCode/blob/main/Image/105_Example.png
- 思路
    - 透過D&C，以遞迴來構造 binary tree 的左右子樹
    - 先透過 unordered_map 紀錄 inorder的索引位置，根據前序遍歷的特性，初始將為root節點，去尋找root節點於 inorder中的索引位置，接著因中序排列的特性，root左側為左子樹，root右側為右子樹，建構出左右子樹

```cpp
class Solution {
public:
    unordered_map<int, int> inorder_map; // 快速查找 inorder 索引
    int preorderIndex = 0; // 記錄 preorder 目前的位置

    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        //preorder: 前序遍歷 ; inorder: 中序遍歷
        // 先建立一個哈希表，加速查找 inorder 索引
        for (int i = 0; i < inorder.size(); i++) {
            inorder_map[inorder[i]] = i;
        }
        return build(preorder, 0, inorder.size() - 1);
    }

    TreeNode* build(vector<int>& preorder, int left, int right) {
        if (left > right) return nullptr; // 遞迴終止條件

        // 取得當前根節點（preorder 的順序）
        int rootVal = preorder[preorderIndex++];
        TreeNode* root = new TreeNode(rootVal);

        // 找到根節點在 inorder 中的位置
        int inorderIndex = inorder_map[rootVal];

        // 遞迴構造左子樹和右子樹
        root->left = build(preorder, left, inorderIndex - 1); // 在preorder中的 root 前為左子樹
        root->right = build(preorder, inorderIndex + 1, right); // 在preorder中的 root 後為右子樹

        return root;
    }
};
```
