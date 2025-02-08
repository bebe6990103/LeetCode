## 496. Next Greater Element I
- 題目: 對於 nums1 的每個元素 x，紀錄 x 在 nums2 中的索引位置"j"，在 nums2 中找到nums2[j] 右邊的第一個比它大的數，沒有比它大的數，則返回 "-1"。
- Example
    - Input1: nums1 = [4,1,2], nums2 = [1,3,4,2]
    - Output1: [-1,3,-1]
    - Input2: nums1 = [2,4], nums2 = [1,2,3,4]
    - Output2: [3,-1]
- 思路
    - 用 單調stack 去紀錄，逐個比較nums2與stack_top，若將stack_top小於 nums[i]，及代表找到下一個Greater element了，就將兩者進行mapping，接著再把nums2丟入stack_top。
```
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
        unordered_map<int, int> NextGreater;
        stack<int> s;
        for (int i=0; i<nums2.size(); i++)
        {
            while(s.empty()!=true && nums2[i] > s.top())
            {
                NextGreater[s.top()] =  nums2[i];
                s.pop();
            }
            s.push(nums2[i]);
        }

        vector<int> ans;
        for(int i=0; i<nums1.size(); i++)
        {
            if ( NextGreater.count(nums1[i]) == true )
            {
                ans.push_back( NextGreater[nums1[i]] );
            }
            else
            {
                ans.push_back(-1);
            }
        }
        return ans;
    }
};
```
