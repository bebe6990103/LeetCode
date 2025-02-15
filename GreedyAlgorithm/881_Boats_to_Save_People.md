## 881. Boats to Save People
- 題目: 每艘船最多載兩個人，且船有限重，給定一組vector，回傳最少需要幾艘船
- Example
    - Input: people = [3,2,2,1], limit = 3
    - Output: 3
- 思路
    - 從頭和尾檢查，只檢查最重的能不能和最輕的共乘，若否，則自己搭一艘。
    - Greedy策略: 局部最優選擇->每次都檢查最輕與最重的人，並選擇後不再重考慮這個搭配。

```cpp
class Solution {
public:
    int numRescueBoats(vector<int>& people, int limit) {
        sort(people.begin(), people.end()); //小到大排序

        int boat = 0;
        int i = 0;
        int j = people.size()-1;

        while (i <= j) // 從頭和尾(最重和最輕)配對，若超過限重limit，則使最重的j自己搭一艘。 若i==j代表剩一人，仍需進入迴圈
        {
            boat++;
            if ( people[i]+people[j] <= limit) //檢查是否可共乘
            {
                i++; //最輕的搭乘
                j--; //最重的搭乘
            }
            else
            {
                j--; // j 獨自搭乘
            }
        }
        return boat;
    }
};
```
