## 92. Reverse Linked List II
- 題目:反轉鏈結串列的一部分
- Example
    - Input: head = [1,2,3,4,5], left = 2, right = 4
    - Output: [1,4,3,2,5]
- 思路
    - 將問題拆解成反轉鏈結串列的前 n 個節點 reverseTopN()，在這個 function 中繼續將問題拆成反轉node.next的前 n-1 個節點，最後 n=1時，紀錄successor為反轉後接續的點
```cpp
class Solution {
public:
    ListNode* successor = nullptr;
    ListNode* reverseTopN(ListNode* head, int n) { //反轉前 n 個節點
        if (n == 1)
        {
            successor = head->next; // 紀錄反轉後接續的節點
            return head;
        }
        ListNode* last = reverseTopN(head->next, n - 1); // 遞迴反轉前 n-1 個節點
        head->next->next = head; //reverse ex:head=node2, node2->node3->node4,會變 node2<-node3
        head->next = successor; // 讓 head 指向 n+1 節點
        return last; // 回傳新的頭節點
    }
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        if (left == 1) { 
            return reverseTopN(head, right); // 直接反轉前 right 個節點
        }
        head->next = reverseBetween(head->next, left - 1, right - 1);
        return head; // 回傳原始頭節點
    }
};
```
