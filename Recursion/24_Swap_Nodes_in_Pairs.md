## 24. Swap Nodes in Pairs
- Medium
- 題目:已知鏈結串列含有環，返回這個環的起始位置 
- Example
    - Input: head = [1,2,3,4]
    - Output: [2,1,4,3]
- 思路
    - 給定一個 單向鏈結串列（Singly Linked List），要求將相鄰的兩個節點進行交換，並返回交換後的鏈結串列頭節點。
```cpp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        
        // 基本情況：如果鏈結串列為空或只有一個節點，則不需要交換
        if (head == nullptr || head->next == nullptr) {
            return head;
        }
        ListNode* a = head;
        ListNode* b = head->next;
        
        a->next = swapPairs(b->next);
        b->next = a;

        return b;
    }
};
```
