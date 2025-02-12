## 239. Sliding Window Maximum
- 題目:輸入一個陣列 nums 和一個正整數 k，有一個大小為 k 的視窗在 nums 上從左至右滑動，請輸出每次滑動時視窗的最大值。
- Example
    - Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
    - Output: [3,3,5,5,6,7]
- 思路
    - 自訂一個 class MonotonicQueue，來動態處理對列排序，在push時持續移除對列尾，直到小於前一個對列值，以透過單調對列處理。
    - 單調對列
        - 對列中的元素皆是單調的 遞增 or 遞減。
```cpp
class MonotonicQueue {
private:
    deque<int> q; // 單調隊列，deque支援pop_front()和pop_back()
public:
    void push(int n) {
        while (!q.empty() && q.back() < n) {
            q.pop_back(); // 如果 隊列尾 小於 要加入的 n ，移除隊列尾的 element
        }
        q.push_back(n); // 再將 n 加入，這樣可以做到保持 對列的大到小排序
    }

    int max() {
        return q.front(); //回傳對列頭，即最大的值
    }

    void pop(int n) {
        if (q.front() == n) {
            q.pop_front(); // 如果 要刪除的n == 對列頭，就將其刪除，反之不管(可能在排序中就被刪除了)
        }
    }
};
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        MonotonicQueue window; //單調隊列
        vector<int> answer;
        for (int i = 0; i < k - 1; i++)
        {  
            window.push(nums[i]);  // 先填滿前 k-1 個元素
        }

        for (int i = k - 1; i < nums.size(); i++)
        {  
            window.push(nums[i]);  // 滑動窗口加入新值
            answer.push_back(window.max());  // 記錄當前最大值
            window.pop(nums[i - k + 1]);  // 移除窗口左側舊值
        }

        return answer;
    }
};
```
