## 509. Fibonacci Number
- Easy
- 題目: 計算費氏數，規則為: F(0) = 0, F(1) = 1, F(n) = F(n - 1) + F(n - 2)
- Example
    - Input: n = 4
    - Output: 3
- 思路
    - 不同於遞迴的"由上往下"方式，透過以"由下往上"計算，並將已知結果存於陣列中，就可避免多餘的再次計算。
```cpp
class Solution {
public:
    int fib(int n) {
        if (n == 0) return 0;
        if (n == 1) return 1;
        vector<int> dic(n+1, 0);
        
        dic[1] = 1;
        dic[2] = 1;

        for (int i=3; i<=n; i++)
        {
            dic[i] = dic[i-1] +dic[i-2];
        }
        return dic[n];
    }
};
```
