## 1. Two Sum
- Easy
- 題目: 給定一 Array nums 與 Integer target，判定 nums 中哪兩數值相加之值相等於 target
- Example
    - Input: nums = [2,7,11,15], target = 9
    - Output: [0,1]
- 思路1
    - Brute Force 暴力法
    - Time complexity: O(n^2)
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int ans = 0;
        for (int i=0; i<nums.size()-1; i++)
        {
            for(int j=i+1; j<nums.size(); j++)
            {
                if( nums[i] + nums[j] == target )
                {
                    return { i, j };
                }
            }
        }
        return { };
    }
};
```

- 思路2
    - 使用 Hash map, 遍歷時直接計算對應成target的值是否存在於 hashmap，並將當個 element 添加入 hashmap。
    - Time complexity: O(n)
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> hash_map;

        for(int i=0; i<nums.size(); i++)
        {
            int complement = target - nums[i]; // key: 值, value: nums index
            if (hash_map.find( complement) != hash_map.end() )
            {
                return { hash_map[complement], i };
            }
            else
            {
                hash_map[nums[i]] = i;
            }
        }
        return { };
    }
};
```
