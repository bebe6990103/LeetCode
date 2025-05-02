## 875. Koko Eating Bananas

- Medium
- 題目: 給定一個長度為 N 的正整數陣列 piles 代表 N 堆香蕉，piles[i] 則是第 i 堆香蕉的數量。Koko 需要在 H 小時之內吃完這些香蕉，Koko 吃香蕉的速度為每小時 K 根，而且每小時最多吃一堆香蕉，若吃不下則留到下一小時再吃。如果吃完這堆還有胃口，他也要等到下一小時才吃下一堆。在以上條件下，回傳 Koko 每小時至少要吃幾根香蕉，才能在 H 小時之內吃完?

- Example
    - Input: piles = [3,6,7,11], h = 8
    - Output: 4

- 思路
    - 先思考暴力解法，接著透過二分搜尋法去代替線性搜尋，提升效率

```cpp
class Solution {
public:
    int minEatingSpeed(vector<int>& piles, int h) {
        int left = 1, right = getMax(piles) + 1;
        while(left<right){
            int mid = left + (right - left) /2;
            if( canFinish(piles, mid, h)){
                right = mid;
            }else{
                left = mid +1;
            }
        }
        return left;
    }
    bool canFinish(vector<int>& piles, int speed, int h) {
        int time = 0;
        for (int n : piles) {
            time += timeOf(n, speed);
        }
        return time <= h;
    }

    int timeOf(int n, int speed) {
        return (int) ceil((double) n / speed);
    }

    // 計算陣列的最大值
    int getMax(vector<int>& piles) {
        int maxVal = 0;
        for (int n : piles)
            maxVal = max(n, maxVal);
        return maxVal;
    }
};
```
