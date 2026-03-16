## 3. Longest Substring Without Repeating Characters

- Medium
- 題目: 檢查字串中最長的非重複字元子字串

- Example1
    - Input: s = "abcabcbb"
    - Output: 3

- Example2
    - Input: s = "pwwkew"
    - Output: 3

- 思路
    -  首先用vector來記錄字元的最後出現位置(與是否出現過)，並用滑動視窗的概念，去維護左邊界與右邊界，持續鎖定非重複字元的字串
    -  當發現重複字元，從上次紀錄的位置切掉
    -  持續用 max 比較目前最大值與目前視窗長度，以紀錄長度最大值

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        // 使用 vector 當作雜湊表，記錄字元最後出現的索引位置
        // ASCII 字元共 128 個，初始化為 -1
        vector<int> lastPos(128, -1);
        
        int longest = 0;
        int left = 0; // 視窗的左邊界

        for (int right = 0; right < s.length(); right++) {
            char c = s[right];

            // 如果這個字元之前出現過，且位置在當前視窗 [left, right] 內
            if (lastPos[c] >= left) {
                // 跳轉 left 到重複字元下一位，直接「切掉」重複的部分
                left = lastPos[c] + 1;
            }

            // 更新字元最新的位置
            lastPos[c] = right;

            // 計算當前視窗長度並更新最大值
            longest = max(longest, right - left + 1);
        }

        return longest;
    }
};
```
