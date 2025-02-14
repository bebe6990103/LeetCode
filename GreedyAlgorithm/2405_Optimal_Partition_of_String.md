## 2405. Optimal Partition of String
- 題目: 給定一個字串 s，嘗試切割 string 成最少的 sub string，sub string 中字元不可重複。
- Example
    - Input: s = "abacaba"
    - Output: 4
- 思路
    - 透過 find() 來檢查 s[i] 是否已經存在於 臨時字串 temp 中
    - Greedy策略: 遇到不得不切割時再拆出新字串。
```cpp
class Solution {
public:
    int partitionString(string s) {
        int ans = 1;
        string temp ="";
        for ( int i=0; i<s.length(); i++)
        {
            if (temp.find(s[i]) != std::string::npos)
            {
                ans++;
                temp = "";
            }
            temp = temp + s[i];
        }

        return ans;
    }
};
```
