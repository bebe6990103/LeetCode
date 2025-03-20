## 912. Sort an Array
- Medium
- 題目: 對一個整數陣列 nums 進行遞增排序，時間複雜度必須在 O(nlogn) 內，並盡量壓低空間複雜度
- Example
    - Input: nums = [5,2,3,1]
    - Output: [1,2,3,5]
- 思路
    - 使用 Merge Sort 對陣列作遞增排序，透過mergeSort function不停將陣列拆成子陣列，再透過merge function將其作排序，接著合併。

```cpp
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
    	mergeSort(nums, 0, (int)nums.size() - 1);
    	return nums;
    }
    void mergeSort(vector<int>& nums, int start, int end) {
    	if (start >= end) return;
    	int mid = (start + end) / 2;
    	mergeSort(nums, start, mid);
    	mergeSort(nums, mid + 1, end);
    	merge(nums, start, mid, end);
    }
    void merge(vector<int>& nums, int start, int mid, int end) {
    // 建立一個暫存陣列來儲存合併後的結果
    vector<int> tmp(end - start + 1);

    // 用來遍歷兩個子陣列的指標
    int i = start;      // 左半邊子陣列的指標
    int j = mid + 1;    // 右半邊子陣列的指標
    int k = 0;          // 暫存陣列的指標

    // 比較兩個子陣列中的元素，將較小的元素放入暫存陣列
    while (i <= mid && j <= end) {  // 當兩邊都有元素時
        if (nums[i] < nums[j]) {
            tmp[k++] = nums[i++];   // 如果左邊的元素較小，就放到暫存陣列
        } else {
            tmp[k++] = nums[j++];   // 否則，放右邊的元素
        }
    }

    // 如果左半邊還有剩餘元素，就把它們加進暫存陣列
    while (i <= mid) {
        tmp[k++] = nums[i++];
    }

    // 如果右半邊還有剩餘元素，就把它們加進暫存陣列
    while (j <= end) {
        tmp[k++] = nums[j++];
    }

    // 把合併後的結果從暫存陣列複製回原來的 `nums` 陣列
    for (int idx = 0; idx < tmp.size(); ++idx) {
        nums[idx + start] = tmp[idx];
    }
    
    }
};
```
