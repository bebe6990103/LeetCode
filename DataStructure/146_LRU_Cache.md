## 146. LRU Cache

- 題目:設計 LRU 快取機制，接收"LRUCache"函式的參數"capacity"作為快取的最大容量。設計"put(key, val)" API 儲存 key pair，如果key的數量超過此操作的容量，則逐出最近最少使用的key。設計"get(key)" API 取得 key 對應的 value。
- Example
    - Input:
        - ["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
        - [[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
    - Output:
        - [null, null, null, 1, null, -1, null, -1, 3, 4]
- 思路
    - 透過一個雙向鏈結，cacheList拿來記錄順序，在前面的PAIR較新。
```
class LRUCache {
public:
    int capacity;  // LRU Cache 容量
    list<pair<int, int>> cacheList;  // 雙向鏈表存儲 Key-Value
    unordered_map<int, list<pair<int, int>>::iterator> cacheMap;  // 定義一個 unordered_map，它的作用是儲存每個 key 以及它在 cacheList 中的位置
    LRUCache(int cap) : capacity(cap) {} // 初始化
    
    int get(int key) {
        if (cacheMap.find(key) == cacheMap.end()) // cacheMap.end() 回傳的是 unordered_map 或 map 最後一個元素的下一個位置（超出範圍的位置）
        {
            return -1;
        }
        auto it = cacheMap[key]; // auto: 編譯器自動推斷變數的型別，根據變數的初始化值決定它的型別
        int value = it->second;  // first 代表 key, second 代表 value
        cacheList.erase(it); // 刪除 key 在 list 中的舊位置
        cacheList.push_front({key, value}); // push_front() 會將 {key, value} 插入 list 頭部，表示最新使用過的pair
        cacheMap[key] = cacheList.begin(); // 將 key 對應到 cacheList 的頭部

        return value;
    }
    
    void put(int key, int value) {
        if (cacheMap.find(key) != cacheMap.end()) { // 如果已有該key與value，則刪掉舊值
            cacheList.erase(cacheMap[key]);
        }

        // 插入新的 Key-Value 到最前
        cacheList.push_front({key, value});
        cacheMap[key] = cacheList.begin();

        // 若超過容量，則刪除最舊的 Key
        if (cacheList.size() > capacity) {
            int oldestKey = cacheList.back().first;
            cacheMap.erase(oldestKey);
            cacheList.pop_back(); // 刪除cacheList中的最後一個元素
        }
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */

//cacheList 中的值 是 pair<int, int>，表示每個緩存項的 key 和 value，並按照訪問順序存儲（最新的在最前面，最舊的在最後面）。
//cacheMap 中的值 是 list<pair<int, int>>::iterator，它是指向 cacheList 中對應元素的迭代器，用於快速定位和操作 cacheList 中的元素。
```
