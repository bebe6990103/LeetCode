## 316. Remove Duplicate Letters

- Medium
- 題目: 給定一個字串 s，請移除重複字母，以達到每個字母只出現一次，並在所有符合條件的組合中，回傳字典序最小的那個字串作為答案，同時不能不能打亂原來字母的順序。

- Example
    - Input: s = "cbacdcbc"
    - Output: "acdb"

- 思路
    - 先記錄每個字母的最後出現位置，以確認字母未來還會不會再出現，用 stack 結構存字母結果、unordered_set 記錄哪些字母已經在 stack 裡，避免重複加入。主流程逐個處理字母，比較當前字母是否比 stack 頂部的字母還小，並確認 stack  頂部的字母之後是否還會出現，若皆是則將它從 stack 移除，讓字典序更小。

```cpp
class Solution {
public:
    string removeDuplicateLetters(string s) {
        unordered_map<char, int> lastIndex;
        unordered_set<char> seen;
        stack<char> tempStk;

        // 記錄每個字母的最後出現位置
        for (int i = 0; i < s.size(); ++i) {
            lastIndex[s[i]] = i;
        }

        for (int i = 0; i < s.size(); ++i) {
            char c = s[i];

            // 如果已經加入過，就跳過
            if (seen.count(c)) continue;

            // 如果 stack 裡面的字母比現在的字母大（字典序比較大）
            // 且後面還會再出現，則可以把它移除，讓字典序變小
            while (!tempStk.empty() && c < tempStk.top() && lastIndex[tempStk.top()] > i) { // c < tempStk.top() 可以直接比較字典序(ASCII)
                seen.erase(tempStk.top());
                tempStk.pop();
            }

            tempStk.push(c);
            seen.insert(c);
        }

        // 把 stack 轉成字串（注意 stack 是反的）
        string result;
        while (!tempStk.empty()) {
            result += tempStk.top();
            tempStk.pop();
        }
        reverse(result.begin(), result.end());
        return result;
        }
};
```
