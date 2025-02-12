```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        
        int right = s.length() - 1;
        int left = 0;

        while(left < right)
        {
            // 跳過非字母數字的字元
            while (left < right && !isalnum(s[left])) // isalnum(char) 可以檢查字元 c 是否為英文字母或數字，忽略標點符號與空格
            {
                left++;
            }   
            while (left < right && !isalnum(s[right])) //當 left >= right 時，停止迴圈，避免 left 超出 right。
            {
                right--;
            }
            if (tolower(s[left]) != tolower(s[right]))
            {
                return false;
            }
            right--;
            left++;
        }

        return true;
    }
};
```
