## 23. Merge k Sorted Lists
- Hard
- 題目: 有 k 條已排序的遞增 ListNode，要求將它們合併成一條排序後的 ListNode，並返回新 ListNode 的 head。
- Example
    - Input: lists = [[1,4,5],[1,3,4],[2,6]]
    - Output: [1,1,2,3,4,4,5,6]
- 思路
    - 透過 mergeLists function 將 lists 拆分成兩半，直到只剩單個 ListNode，接著再透過 mergeTwoLists function 將 兩兩 ListNode 做合併排序。合併過程透過遞迴，每次取較小的節點。
    -將 lists 逐步拆成兩半做合併排序效率會比逐個合併高，可能是因為樹的深度的關係
```cpp
class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        if (lists.empty()) return nullptr;
        return mergeLists(lists, 0, lists.size() - 1);
    }

    ListNode* mergeLists(vector<ListNode*>& lists, int left, int right) {
        // 將 lists 逐步拆成兩半，再透過 mergeTwoLists 來合併已排序的鏈結串列
        // 這種方式的 時間複雜度 比 逐個合併高，因為樹的深度的關係
        if (left == right) return lists[left];
        int mid = left + (right - left) / 2;
        ListNode* l1 = mergeLists(lists, left, mid);
        ListNode* l2 = mergeLists(lists, mid + 1, right);
        return mergeTwoLists(l1, l2);
    }

    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) { //藉由比較各個節點大小，合併兩個排序後的ListNode
        if (l1 == nullptr) return l2;
        if (l2 == nullptr) return l1;
        if (l1->val < l2->val) {
            l1->next = mergeTwoLists(l1->next, l2);
            return l1;
        } else {
            l2->next = mergeTwoLists(l1, l2->next);
            return l2;
        }
    }
};
```
