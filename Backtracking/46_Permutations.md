## 46. Permutations
- Medium
- 題目: 給定一個包含互不相同整數的陣列 nums，找出所有可能的排列組合（Permutation），並以任意順序返回這些排列組合的結果。
- Example
    - Input: nums = [1,2,3]
    - Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
- 思路
    - 建立一個 track 陣列存放目前正在構造的排列，使用 backtrack 進行遞迴，在 backtrack 內依序檢查包含 nums[i] ，若有則跳過，若無則將其加入 track 並進行下一層遞迴。而找到解後，會執行回溯將選擇的 element 從 track 刪掉，繼續嘗試下一個組合。

```cpp
class Solution {
public:
    vector<vector<int>> ans;

    vector<vector<int>> permute(vector<int>& nums) {
    vector<int> track;
    backtrack(track, nums);
    return ans;
    }
    
    //路經: 紀錄至 track 中
    //選擇清單: 不在 track 中的 nums 元素
    //結束條件: nums 元素全都位於 track
    void  backtrack( vector<int>& track, vector<int>& nums){
        if ( track.size() == nums.size() ){ 
            ans.push_back(track); // 如果 track 的長度等於 nums 即代表 nums 元素全都在 track 中了
            return;
        }

        for(int i=0; i<nums.size(); i++){
            if(find(track.begin(), track.end(), nums[i]) != track.end() ){ 
                continue; // 若 nums[i] 已經存在於 track，則跳過
            }

            track.push_back(nums[i]); // 選擇為包含的nums[i]
            backtrack(track, nums); // 繼續下一層
            track.pop_back(); // 撤回選擇 回溯
        }    
    }
};
```
