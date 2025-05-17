## 895. Maximum Frequency Stack

- Hard
- 題目: 設計一個特殊的 Stack，除了 push(val) 以外，pop() 時要根據「元素出現的頻率」來決定要移除哪個元素，若有多個頻率一樣，則回傳「最接近 stack 頂端的那個元素」。

- Example
    - Input: ["FreqStack", "push", "push", "push", "push", "push", "push", "pop", "pop", "pop", "pop"] [[], [5], [7], [5], [7], [4], [5], [], [], [], []]
    - Output: [null, null, null, null, null, null, null, 5, 7, 5, 4]

- 思路
    - 藉由 valFreq 紀錄每個元素對應的出現頻率，接著 freqStack 根據頻率創建對應的 stack 以根據「頻率」取出元素，同時透過 pop 能保證取出的元素最接近頂端

```cpp
class FreqStack {
private:
    unordered_map<int, int> valFreq; // 記錄每個值的頻率
    unordered_map<int, stack<int>> freqStack; // 每個頻率對應一個 stack
    int maxFreq = 0; // 當前最大頻率

public:
    FreqStack() {}

    void push(int val) {
        valFreq[val] = valFreq[val] + 1; // 頻率 +1
        int freq = valFreq[val];
        freqStack[freq].push(val); // 把它加到對應頻率的 stack
        if (freq > maxFreq) {
            maxFreq = freq; // 更新最大頻率
        }
    }

    int pop() {
        int val = freqStack[maxFreq].top();
        freqStack[maxFreq].pop();

        valFreq[val]--; // 該 val 頻率-1

        // 如果這個頻率已經沒東西了，降低 maxFreq
        if (freqStack[maxFreq].empty()) {
            maxFreq--; // 一定會有值，只有當 上一層清空時 才會往下，而下一層之前是確實存在過元素的
        }

        return val;
    }
};
```
