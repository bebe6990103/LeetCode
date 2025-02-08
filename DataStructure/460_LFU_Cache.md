## 460. LFU Cache

- 題目:設計 LFU 演算法，淘汰使用次數最少的資料，若頻率相同則淘汰最早插入的資料。
- Example
    - Input:
        - ["LFUCache", "put", "put", "get", "put", "get", "get", "put", "get", "get", "get"]
        - [[2], [1, 1], [2, 2], [1], [3, 3], [2], [3], [4, 4], [1], [3], [4]]
    - Output:
        - [null, null, null, 1, null, -1, 3, null, -1, 3, 4]
- 思路
    - 透過三個mapping表處理 keyToValue, keyToFreq, freqToKey。 針對 get function，若該key值存在則回傳對應value並freq+1，不存在則回傳"-1"。針對 put function 若 key 值存在則修該 key 對應的value，並增加該key對應的freq; 若key值不存在則插入(key, val)並將key對應的freq設為"1"，如果插入前發現容量已滿則先淘汰freq最小的key。
```cpp
class LFUCache {
public:
    int capacity;  // 緩存容量
    int minFreq;   // 最小訪問頻率
    unordered_map<int, int> keyToValue;      // key -> value
    unordered_map<int, int> keyToFreq;       // key -> frequency
    unordered_map<int, list<int>> freqToKey; // frequency -> list of keys with that frequency
    unordered_map<int, list<int>::iterator> keyIter;  // 儲存 key 在 freqToKey 中的迭代器

    LFUCache (int cap){
        capacity = cap;
        minFreq = 0;
    } // 初始化
    
    int get(int key) {
        if (keyToValue.find(key) == keyToValue.end()) {
            return -1;  // 不存在該 key
        }
        // 更新頻率
        int frequency = keyToFreq[key];
        keyToFreq[key] = frequency + 1;
        freqToKey[frequency].erase(keyIter[key]); // 刪除 key 在舊頻率 freq 的 freqToKey 列表中的位置
        freqToKey[frequency + 1].push_back(key); // 將 key 放入到更新後的頻率列表
        
        auto it = freqToKey[frequency + 1].end();  // 取得 freq+1 頻率列表的尾部迭代器，（超出範圍）
        it--;  // 移動到該列表的最後一個元素
        keyIter[key] = it;  // 將迭代器賦值給 keyIter[key]
        
        // 更新最小頻率
        if (freqToKey[minFreq].empty()) {
            minFreq++;
        }

        return keyToValue[key];
    }
    
    void put(int key, int value) {
        if (keyToValue.find(key) != keyToValue.end()) {
            // 如果 key 已存在，更新它的值並增加頻率
            keyToValue[key] = value;
            get(key);  // 重複調用 get() 會自動更新頻率
            return;
        }
        // 如果緩存已滿，則刪除最不常用的元素
        if (keyToValue.size() == capacity) {
            int evictKey = freqToKey[minFreq].front();
            keyToValue.erase(evictKey);
            keyToFreq.erase(evictKey);
            keyIter.erase(evictKey);
            freqToKey[minFreq].pop_front();
        }
        // 插入新元素
        keyToValue[key] = value;
        keyToFreq[key] = 1;
        freqToKey[1].push_back(key);
        auto it = freqToKey[1].end();  // 取得 freqToKey[1] 列表的尾部迭代器
        it--;  // 移動到該列表的最後一個元素
        keyIter[key] = it;  // 將該迭代器儲存到 keyIter 中
        minFreq = 1;  // 設定最小頻率為 1
    }
};

/**
 * Your LFUCache object will be instantiated and called as such:
 * LFUCache* obj = new LFUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```
