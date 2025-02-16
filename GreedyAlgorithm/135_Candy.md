## 135. Candy
- 題目: 有n個小朋友排成一排，要分糖果，每個人最少一顆，陣列 rating 代表每個人的分數，若 rating 比鄰近兩人高，則必須獲得相比兩人更多的糖果，問最少需要幾顆糖。
- Example
    - Input: ratings = [1,2,2]
    - Output: 4
- 思路
    - 先給每個人發一顆糖，接著從兩側檢查，先由左到右，若當前人比前面人評分高，確保他拿的糖不會比前面人少。再由右到左，若當前人比後面人評分高，就確保他的糖不會比後面人少。
    - Greedy策略: 先從左向右確保「局部最優」再從右向左確保「局部最優」，即得全域最優解
```cpp
class Solution {
public:
    int candy(vector<int>& ratings) {
        int len = ratings.size();
        int total = 0;
        vector<int> candy(len, 1); // 初始化，每個人都先發一顆糖
        
        for(int i=1; i<len; i++) // 先由左到右，與自己前方的比較，若自己比較大，則 candy+1
        {
            if( ratings[i]>ratings[i-1])
            {
                candy[i] = candy[i-1]+1; //繼承對方的顆數
            }
        }

        for(int i=len-2; i>=0; i--) // 由右到左，與自己後方的比較，必須由右到左，否則無法得知比較關係 ex: 5,4,3,2,1 -> candy 2,2,2,2,1
        {
            if( ratings[i]>ratings[i+1])
            {
                if(candy[i]<=candy[i+1]) //若還沒比後方的多再加一顆糖，否則可能會不需再加但卻加
                {
                    candy[i] = candy[i+1]+1; //繼承後方的顆數
                }
            }
        }
        
        for (int i=0; i<candy.size(); i++)
        {
            total = total + candy[i];
        }
        return total;
    }
};
```
