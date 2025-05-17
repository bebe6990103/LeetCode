## 1209. Remove All Adjacent Duplicates in String II

- Medium
- 題目: 給定一個字串 s 和一個整數 k，每次移除k 個相鄰且相同的字母，然後把剩下的字串重新接在一起。這個移除過程會一直重複，直到無法再移除為止。

- Example
    - Input: s = "deeedbbcccbdaa", k = 3
    - Output: "aa"

- 思路
    - 藉由 pair 去追蹤每個字母出現的次數，並利用 stack 結構去儲存，每當處理一個字母即檢查已出現次數，當達到 k 時就從 stack 中 pop 掉。

```cpp
class Solution {
public:
    string removeDuplicates(string s, int k) {
        stack<pair<char, int>> tempStk;

        for (char c : s) {
            if (!tempStk.empty() && tempStk.top().first == c) { // 若字母與stack頂部一樣則做處理
                tempStk.top().second++;  // 相同字母，次數+1
                if (tempStk.top().second == k) {
                    tempStk.pop();  // 數量達到 k，移除
                }
            } else {
                tempStk.push({c, 1});  // 新字母放進 stack
            }
        }

        // 重建結果字串
        string result;
        while (!tempStk.empty()) {
            // 反向加字串，因stack為後進先出
            result.insert(0, tempStk.top().second, tempStk.top().first);  // 在字串最前面插入 stk.top().first（字母）重複 stk.top().second（次數）次
            tempStk.pop();
        }

        return result;
        }
};
```
