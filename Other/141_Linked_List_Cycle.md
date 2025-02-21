## 141. Linked List Cycle
- Easy
- 題目:判斷鏈結串列是否含有環 
- Example
    - Input: head = [3,2,0,-4], pos = 1
    - Output: true
    - ![141_Example](https://hackmd.io/_uploads/SkfiaZUqJg.png)
- 思路
    - 如果鏈結串列不含環，指標最終會遇到空指標 NULL，若含有環則會進入閉迴圈。
    - 經典的判斷解法為透過兩個指標，一快一慢，若為閉環，最終快指標會多跑一圈，兩個指標會相遇。
```cpp
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode *fast, *slow;
        fast = head;
        slow = head;

        while ( (fast != NULL)&&(fast->next != NULL) ){
            fast = fast->next->next;
            slow = slow->next;
            if(fast == slow) return true;
        }
        return false;
    }
};
```
