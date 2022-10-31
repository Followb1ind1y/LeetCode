## **36. Valid Sudoku**

[LeetCode 36. Valid Sudoku [Medium]](https://leetcode.com/problems/valid-sudoku/description/)

Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

Each row must contain the digits `1-9` without repetition.
Each column must contain the digits `1-9` without repetition.
Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.

**Note:**
- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.

```markdown
Input: board =
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
```

### **思路**
* **创建一个长度为3的 list 分别用来储存行，列和同一个 3x3 区间内的情况 list 内创建 9个 hashtable 用来记录方便查找**

### **代码**

``` python
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        res_store = [[{},{},{},{},{},{},{},{},{}], [{},{},{},{},{},{},{},{},{}], [{},{},{},{},{},{},{},{},{}]]

        for i in range(len(board)):
            for j in range(len(board[i])):
                if board[i][j] == ".":
                    continue
                elif board[i][j] in res_store[0][i] or board[i][j] in res_store[1][j] or board[i][j] in res_store[2][3 * (i // 3) + j // 3]:
                    return False
                else:
                    res_store[0][i][board[i][j]] = res_store[1][j][board[i][j]] = res_store[2][3 * (i // 3) + j // 3][board[i][j]] = 1

        return True
```
### **复杂度分析**
* **时间复杂度：O(n^2)**
* **空间复杂度：O(n^2)**
