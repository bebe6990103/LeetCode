## 2. Add Two Numbers
- Medium
- 題目:將兩個ListNode的Element值相加並回傳新ListNode
- Example
    - Input: l1 = [2,4,3], l2 = [5,6,4]
    - Output: [7,0,8]
    - Explanation: 342 + 465 = 807.
- 思路
    - 其實只是做直式的逐位計算，確保所有個位都被處理到。
    - 使用結果 dummy 去建構鏈結串列的頂部頭節點，後續用 curr 去往後逐個新增節點，最終回傳 dummy 即可。
    - dummy 頭節點也可刪除釋放記憶體空間。
- Time Complexity: O(1) * max(m, n) = O(max(m, n)) ; m, n 為鏈結串列長度。
```cpp
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* dummy = new ListNode(0);
        ListNode* curr = dummy;
        int carry = 0; //用來存進位

        while ( l1!=NULL || l2!=NULL || carry!=0 ){
            
            int sum = carry;
            if( l1!= NULL){
                sum = sum + l1->val;
                l1 = l1->next;
            }

            if( l2!= NULL){
                sum = sum + l2->val;
                l2 = l2->next;
            }

            carry = sum/10; // 計算新的進位
            curr->next = new ListNode(sum%10); // 存入目前的餘數
            curr = curr->next;
        }

        return dummy->next;
    }
};
```
