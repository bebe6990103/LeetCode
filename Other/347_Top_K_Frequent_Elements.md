## 347. Top K Frequent Elements

- Medium
- 題目: 給定一個整數陣列 nums 和一個整數 k，請找出出現頻率最高的前 k 個元素。不需要對結果排序，但演算法的時間複雜度必須優於 O(n log n)

- Example
    - Input: nums = [1,1,1,2,2,3], k = 2
    - Output: [1,2]

- 思路
    - 先統計每個數字的出現頻率，接著建立 n+1 個 Buckets，buckets[i]表示剛好出現 i 次的所有數字，最後從高頻率往下取 k 個數字即可。

```cpp
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> freq;

        // 統計每個元素的出現次數
        for (int num : nums) {
            freq[num]++;
        }

        // 建立bucket ：bucket 的 index 表示頻率，值是該頻率對應的數值集合
        int n = nums.size();

        // Buckets 是一種用陣列當作分類容器的技巧
        vector<vector<int>> buckets(n + 1); // 建立了 n+1 個 Buckets

        for (auto& [num, count] : freq) {
            buckets[count].push_back(num); //根據 num 出現的次數 count，把這個 num 放到第 count 個 bucket 中
        }

        // 從高頻率開始取，直到取得 k 個元素為止
        vector<int> result;
        for (int i = n; i >= 0 && result.size() < k; --i) {
            for (int num : buckets[i]) {
                result.push_back(num); // 取較高頻率的值
                if (result.size() == k) break; // 若已足夠 k 個則直接跳出
            }
        }

        return result;
    }
};
```
