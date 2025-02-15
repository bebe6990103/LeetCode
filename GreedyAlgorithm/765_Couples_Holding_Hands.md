## 765. Couples Holding Hands
- 題目: 有2n個人坐在一排椅子上，(0,1)是一對，(2,3)是一對，透過最少的對調次數讓每對情侶都可以做在一起
- Example
    - Input: row = [0,2,1,3]
    - Output: 1
- 思路
    - 先透過另一個vector來記錄每個人的座位，接著做尋訪，在每一對座位 (i, i+1) 中，找出第一個人 row[i] 的伴侶 partner = row[i] ^ 1。如果伴侶的位置不是下一個座位，則馬上進行一次交換，把 partner 放到 i+1 位置，這樣這一對座位立刻變成正確的情侶。
    - Greedy策略: 從頭尋訪，每當遇到下一位不是伴侶後，立刻與伴侶交換位置，這樣即可透過最少的交換次數(全局最佳解)完成目標。

```cpp
class Solution {
public:
    int minSwapsCouples(vector<int>& row) {
        int ans;
        int n = row.size();
        vector<int> pos(n);

        for(int i=0; i<n; i++)
        {
            pos[row[i]] = i; // 用 pos 紀錄每個人的座位引索值
        }

        for(int i=0; i<n; i=i+2)
        {
            int partner = row[i] ^ 1; // ^為互斥或 2^1 =3, 3^1=2，找情侶是誰
            int partner_pos = pos[partner];
            if( i+1 != partner_pos) //檢查情侶的位置是否等於下一個座位
            {
                ans++; //增加對調數
                swap(row[i+1], row[partner_pos]); // 將兩者對調

                pos[row[i+1]] = i+1; // 更新座位表pos
                pos[row[partner_pos]] = partner_pos; // 更新座位表pos
            }
        }
        return ans;
    }
};
```
