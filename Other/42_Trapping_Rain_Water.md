## 42. Trapping Rain Water

- Hard
- 題目: 給定一個長度為n的 nums 非負整數陣列，代表二維平面內一排寬度為 1 的柱子，nums[i]表示第 i 個柱子的高度，請計算下雨後這些柱子能夠裝下多少雨水。

- Example
    - Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
    - Output: 6

- 思路
    - 假設 l_max < r_max ， height[i] 能夠裝多少水只和 l_max 有關，與 r_max 是不是右邊最大無關，反之亦然。接著藉由雙指標去維護兩邊最高柱子高度。

```cpp

class Solution {
public:
    int trap(vector<int>& height) {
        if(height.empty()) return 0;
        int n = height.size();
        int left = 0;
        int right = n - 1;
        int ans = 0;

        int l_max = height[0];
        int r_max = height[n-1];

        while( left <= right ){
            l_max = max( l_max, height[left] );
            r_max = max( r_max, height[right] );

            if( l_max < r_max){
                ans = ans + l_max -height[left];
                left++;
            }
            else{
                ans = ans + r_max -height[right];
                right--;
            }
        }
        return ans;
    }
};

```
