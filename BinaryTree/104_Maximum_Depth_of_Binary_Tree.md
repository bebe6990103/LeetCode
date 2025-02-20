## 104. Maximum Depth of Binary Tree
- Easy
- 題目: 計算二元樹的最大深度
- Example
    - ![104_Example](https://github.com/bebe6990103/LeetCode/blob/main/Image/104_Example.png)
    - Input: root = [3,9,20,null,null,15,7]
    - Output: 3
- 思路
    - 透過 BFS（廣度優先搜尋）搭配 Queue 去計算。BFS特性，每當 Depth 增加一次，所有節點都往前推一步。
    - Queue 的 pop, push funtion 適合作 FIFO 操作，如 BFS。
```cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == nullptr) return 0;
        queue<TreeNode*> q; // queue 包含 pop(), push()，適合 FIFO 操作
        q.push(root); // 將 root 存入佇列中
        int depth = 0;

        while( !q.empty() ) //當 queue 為空代表已經走到底
        {
            int size = q.size();
            for(int i=0; i<size; i++) // 將佇列中的向外擴散
            {
                TreeNode* cur = q.front(); //取柱列頭
                q.pop(); // 將柱列頭從 q 中去掉
                if(cur->left != nullptr)
                {
                    q.push(cur->left); // 若左子樹有值則加入佇列
                }
                if(cur->right != nullptr)
                {
                    q.push(cur->right); // 若右子樹有值則加入佇列
                }
            }
            depth++; // 深度 +1
        }
        return depth;
    }
};
```
