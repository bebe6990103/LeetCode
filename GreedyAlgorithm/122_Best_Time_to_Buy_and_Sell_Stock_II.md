## 122. Best Time to Buy and Sell Stock II
- 題目: 取得股票的每日價格，先買後賣，每次只能買一個股，回傳最大獲利
- Example
    - Input: prices = [7,1,5,3,6,4]
    - Output: ７
- 思路
    - 遍歷 prices，並在每次股價上漲的情況下，選擇賣出股票
    - Greedy策略: 在每一天，選擇當下能賺到最多利潤的操作，可以保證每次的決策都是最好的，局部最佳解->全局最佳解
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int temp;
        int before;
        int profit = 0;
        for (int i=0; i<prices.size(); i++ )
        {
            temp = prices[i];
            if ( i != 0)
            {
                if (temp > before)
                {
                    profit = profit + (temp - before);
                }
            }
            before = prices[i];
        }
        return profit;
    }
};
```
