## 2366. Minimum Replacements to Sort the Array
- 題目: 給一個正整數數列，可以將其中的元素切割成總和相同的兩個值，最少需要幾次切割讓數列變成非遞減序列
- Example
    - Input: nums = [3,9,3]
    - Output: 2
- 思路
    -　從數列後面往前推，維護一個值min，確保前面的值沒有超過min，若遇到element比min大，則計算需要對其做幾次切割動作，並更新min。
    -　Greedy策略: 只對min值做檢查，即能達到非遞減序列的需求
```cpp
class Solution {
public:
    long long minimumReplacement(vector<int>& nums) {
        long long ans = 0;
        int size = nums.size();
        int min = nums[size-1]; // 先取最後一個數
        
        for( int i = size-2; i>=0; i--)
        {
            if( nums[i] > min)
            {
                int parts = (nums[i] + min - 1) / min;
                ans = ans + (parts -1);  //這兩行做到計算拆成幾份 ex: 3->0份, 4->1份
                min = nums[i] / parts; //更新min值 nums[i] / parts 代表 一份的大小為何
            }
            else
            {
                min = nums[i]; //更新min值
            }
        }

        return ans;
    }
};
```
