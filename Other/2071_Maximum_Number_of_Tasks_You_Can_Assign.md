## 2071. Maximum Number of Tasks You Can Assign

- Hard
- 題目: 給定有一批任務（tasks）與一批工人（workers）。每個任務需要一定的「strength」才能完成，而每位工人也各自有一個固定的「strength」。此外，還有一些藥丸（pills），每顆藥丸可以提升一位工人的 strength 值，但每位工人最多只能吃一顆藥丸。每位工人最多只能執行一個任務，並只能執行其「strength」值大於需求的任務。在給定的工人、任務、藥丸數量與藥效強度下，請找出最多可以分配的任務數量。

- Example
    - Input: tasks = [3,2,1], workers = [0,3,3], pills = 1, strength = 1
    - 3

- 思路
    - 先將對任務與工人排序，使用 二分搜尋，猜測可以完成的最多任務數 k，對於每個 k，嘗試從最難的 k 個任務中找到 k 個能對應的工人(greedy)

```cpp
class Solution {
public:
    bool canAssign(int k, vector<int>& tasks, vector<int>& workers, int pills, int strength) { 
        // 判斷是否有辦法完成 k 個最難的任務（任務陣列已排序），在給定的工人、藥丸數量與增強力量條件下
        multiset<int> available(workers.end() - k, workers.end()); // multiset 為自動排序的容器、支援lower_bound()與erase()
        int p = pills; //剩餘藥丸數量

        for (int i = k - 1; i >= 0; --i) { //從最難的任務開始做
            int task = tasks[i];
            auto it = available.lower_bound(task); // 找出第一個 ≥ task 的工人
            if (it != available.end()) { //如果找得到則直接指派任務，並從 multiset 中移除這個工人
                available.erase(it);
            } else {
                it = available.lower_bound(task - strength); // 嘗試找出一個  ≥ task - strength 的工人 
                if (it == available.end()) return false; // 沒找到合適工人 → 任務做不了
                if (--p < 0) return false; // 沒藥了則任務無法完成
                available.erase(it); // 把吃藥的工人從集合中移除
            }
        }

        return true;
    }

    int maxTaskAssign(vector<int>& tasks, vector<int>& workers, int pills, int strength) {
        sort(tasks.begin(), tasks.end()); // 將 tasks 由小至大排序
        sort(workers.begin(), workers.end()); // 將 workers 由小至大排序

        int left = 0, right = min( (int)tasks.size(), (int)workers.size()) ; // left:最少能做的任務為 0, right:最多能做的任務為 min(任務數, 工人數)
        int answer = 0;

        while (left <= right) {
            int mid = left + (right - left) / 2; //  二分搜尋
            if (canAssign(mid, tasks, workers, pills, strength)) {
                answer = mid; // 如果成功，更新答案
                left = mid + 1; // 嘗試做更多
            } else {
                right = mid - 1;  // 失敗，試試看做更少
            }
        }

        return answer;
    }
};

```
