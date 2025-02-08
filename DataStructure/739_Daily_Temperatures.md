## 739. Daily Temperatures
- 題目:給一個陣列存放不同天的溫度，回傳一個陣列，其值為還要幾天才回暖，若無則回傳"0";
- Example
    - Input: temperatures = [73,74,75,71,69,72,76,73]
    - Output: [1,1,4,2,1,1,0,0]
- 思路
    - 透過 stack 存入引索(即為第幾天)，若發現該天溫度大於 stack.top 的當天溫度，就將兩者引索相減，就能取得回暖所的天數，接著將計算後的引索 stack.pop 掉。
```
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temperatures) {
        vector<int> ans(temperatures.size(), 0); // 預設所有天數為 0
        stack<int> s;// 存放溫度的「索引」

        for (int i=0; i<temperatures.size(); i++)
        {
            while(s.empty()!=true && temperatures[i] > temperatures[s.top()]) //若 目前這天的溫度 大於 stack.top 的溫度，則代表發現回暖了
            {
                int Index = s.top(); // 先抓取 stack.top 的是第幾天
                ans[Index] = i - Index; // 與目前索引相扣後即為差距幾天回暖
                s.pop(); // pop掉計算完的day
            }
            s.push(i); // push目前的day，即索引值
        }
        return ans;
    }
};
```
