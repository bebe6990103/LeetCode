## 51. N-Queens
- Hard
- 題目: 給定一個 n × n 的棋盤，請擺放 n 個皇后，使得任意兩個皇后不會相互攻擊（即不能在同一列、同一行或同一對角線上）。請返回可能的擺放方式，解法以 字串陣列 表示，其中：'Q' 代表皇后, '.' 代表空格。
- Example
    - Input: n = 4
    - Output: [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
    - ![51_Example](https://github.com/bebe6990103/LeetCode/blob/main/Image/51_Example.png)
- 思路
    - 先初始化棋盤，接著以每行column開始檢查，再以列row檢查，若無可能之解則透過 board[row][col] = '.' 將走過的路徑進行回溯，只要找到一個解即return，後面的遞迴會被取消。
```cpp
class Solution {
public:
    vector<vector<string>> ans;
    vector<vector<string>> solveNQueens(int n) {
        vector<string> board( n, string(n, '.') ); // 初始化，每一列有 n 個 "."
        backtrack(board, 0); // 從 row = 0 開始
        return ans;
    }
    // row:列 _ , column:行 l
    // 路徑: board中小於row的列都已經放置 Queen
    // 選擇清單: 第 row 列的每一個所有行都是放置 Queen 的選擇之一
    void backtrack(vector<string>& board, int row)
    {
        // 結束backtrack的條件 若 row 等於 棋盤board的最後一列，代表已經放滿
        if(row == board.size())
        {
            ans.push_back(board);
            return ;
        }

        int n = board.size();
        for (int col=0; col<n; col++)
        {
            if( !isvalid(board, row, col) )
            {
                continue;
            }
            board[row][col] = 'Q'; // 放皇后
            backtrack(board, row+1); // 嘗試下一列
            board[row][col] = '.'; //回溯 (跳過這一步)
        }
    }
    bool isvalid(vector<string>& board, int row, int col) // 檢查是否可以在 board[row][col] 放置 Queen
    {
        int n = board.size(); 
        for(int i=0; i<n; i++) // 檢查同一列(row)是否有 Queen
        {
            if( board[i][col] == 'Q' )
            {
                return false;
            }
        }
        for(int i=row-1, j=col+1; i>=0 && j<n; i--, j++) // 檢查右上角是否有 Queen
        {
            if( board[i][j] == 'Q')
            {
                return false;
            }
        }
        for(int i=row-1, j=col-1; i>=0 && j>=0; i--, j--) // 檢查左上角是否有 Queen
        {
            if( board[i][j] == 'Q')
            {
                return false;
            }
        }
        return true;
    }
};
```
