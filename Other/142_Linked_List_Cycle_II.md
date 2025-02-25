## 142. Linked List Cycle II
- Medium
- 題目:已知鏈結串列含有環，返回這個環的起始位置 
- Example
    - Input: head = [3,2,0,-4], pos = 1
    - Output: tail connects to node index 1
- 思路
    - 先透過快,慢指標找到起始位置，找到起始位置後將一指標指到 head，接著兩個指標每次各走一步，當它們相遇時，就是環的起始點。(數學邏輯)。
```cpp
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode *fast, *slow; // 快,慢指標
        fast = head;
        slow = head;
        
        while ( (fast!=NULL)&&(fast->next!=NULL) ){
            fast = fast->next->next;
            slow = slow->next;

            if( fast == slow){
                slow = head;

                while (slow != fast){
                    fast = fast->next;
                    slow = slow->next;
                }
                return slow;
            }
        }
        return NULL;
    }
};
```
