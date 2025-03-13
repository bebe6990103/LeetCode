## 50. Pow(x, n)
- Medium
- 題目:計算 x 的 n 次方
- Example
    - Input: x = 2.00000, n = 10
    - Output: 1024
- 思路
    - 用遞迴處理，先處理負次方問題。接著計算 n 的一半，再根據 n 的奇偶性看如何計算。偶數直接 half * half，奇數則 half * half * x。
    - 特別以 long 處理 溢位error
```cpp
class Solution {
public:
    double myPow(double x, int n) {
        if (n == 0) return 1;  // 基本情況：任何數字的0次方都是1

        long long N = n;  // 使用 long long 來避免 INT_MIN 溢出
        if (N < 0) {
            x = 1 / x;  // 如果是負數次方，將問題轉換為正數次方
            N = -N;     // 將n轉為正數
        }

        return helper(x, N);  // 使用函數進行遞迴計算
    }

    double helper(double x, long long n) {
        if (n == 0) return 1;  // 基本情況：x^0 = 1
        double half = helper(x, n / 2);  // 先計算 x^(n/2)
        if (n % 2 == 0) {
            return half * half;
        } else {
            return half * half * x; 
        }
    }
};
```
