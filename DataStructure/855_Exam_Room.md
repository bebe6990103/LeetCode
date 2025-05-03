## 855. Exam Room

- Medium
- 題目: 假設有一考場，其內有一排共 N 個座位，索引分別是[0 .. N-1]，考生會陸續進場，並可能隨時離場。現需安排考生座位，每當一個考生進場時，需要最大化他和最近其他人的距離，而如果有多個滿足條件的座位，則安排該考生到索引較小的座位。

- Example
    - Input: ["ExamRoom", "seat", "seat", "seat", "seat", "leave", "seat"]
[[10], [], [], [], [], [4], []]
    - Output: [null, 0, 9, 4, 2, null, 5]

- 思路
    - 藉由 set 紀錄已入座考生，se t會自動完成排序。先對已知座位作尋訪，找出最適合之座位，再將其與尾端距離作比較，以找出最適合的座位。

```cpp

class ExamRoom {
private:
    int n; // 表示座位總數
    set<int> seats; // 存放已有人坐的座位號，排序自動完成

public:
    ExamRoom(int n) : n(n) {}

    int seat() {
        if (seats.empty()) { // 沒人的話直接坐0號座位
            seats.insert(0);
            return 0;
        }

        int maxDist = *seats.begin(); // 距離開頭的距離
        int candidate = 0;

        // 遍歷座位，找中間的最大距離點
        int prev = -1; // 要避免第一次就計算距離，但 0 是可能的座位，因此 prev = 0 不適合拿來做判斷
        for (int s : seats) {
            if (prev != -1) {
                int d = (s - prev) / 2; // 藉由除以2，避免ex [0,4],[4,9]的distance值不同而選後者的情況
                if (d > maxDist) {
                    maxDist = d;
                    candidate = prev + d; // 決定學生坐哪個座位
                }
            }
            prev = s;
        }

        // 檢查尾端
        if (n - 1 - *seats.rbegin() > maxDist) { // seats.rbegin() 以排序好，rbegin指向最大元素(最右邊有人坐的座位編號)
            candidate = n - 1;
        }

        seats.insert(candidate);
        return candidate;
    }

    void leave(int p) {
        seats.erase(p);
    }
};

```
