## 25. Reverse Nodes in k-Group
- 題目:輸入一個單向鏈結串列與整數k，k個節點為一組持續做反轉，最後不足k的節點保持原先順序不動。
- Example
    - Input: head = [1,2,3,4,5], k = 2
    - Output: [2,1,4,3,5]
- 思路
    - 先完成一個將節點a~b區間做反轉的函式reverse()，並回傳反轉後的頭節點。而主函式持續計算區間節點數量，滿足k時就丟入reverse，並將其作串接。
```cpp
class Solution {
public:
    ListNode* reverse(ListNode* a, ListNode* b){ // 針對區間做反轉
        ListNode* preNode = nullptr;
        ListNode* currentNode = a;
        ListNode* nextNode = a;

        while(currentNode != b)
        {
            nextNode = currentNode->next;
            currentNode->next = preNode;
            preNode = currentNode;
            currentNode = nextNode;
        }
        return preNode; // 回傳反轉後的頭節點 node b, 因 currentNode 為 b+1
    }
    ListNode* reverseKGroup(ListNode* head, int k){
        ListNode* a = head;
        ListNode* b = head;
        for(int i=0; i<k; i++) // 將a~b設定到符合k的範圍
        {
            if (b == nullptr)
            {
                return head;
            }
            b = b->next;
        }
        ListNode* newhead = reverse(a, b);
        a->next = reverseKGroup(b, k); // 接續上後面的反轉
        return newhead; //回傳反轉後的 node head
    }
};
```
