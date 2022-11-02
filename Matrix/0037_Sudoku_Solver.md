## **37. Sudoku Solver**

[LeetCode 37. Sudoku Solver [Hard]](https://leetcode.com/problems/sudoku-solver/description/)

Write a program to solve a Sudoku puzzle by filling the empty cells.

A sudoku solution must satisfy all of the following rules:

Each of the digits `1-9` must occur exactly once in each row.
Each of the digits `1-9` must occur exactly once in each column.
Each of the digits `1-9` must occur exactly once in each of the 9 `3x3` sub-boxes of the grid.
The `'.'` character indicates empty cells.

```markdown
Input: board = [["5","3",".",".","7",".",".",".","."],
["6",".",".","1","9","5",".",".","."],
[".","9","8",".",".",".",".","6","."],
["8",".",".",".","6",".",".",".","3"],
["4",".",".","8",".","3",".",".","1"],
["7",".",".",".","2",".",".",".","6"],
[".","6",".",".",".",".","2","8","."],
[".",".",".","4","1","9",".",".","5"],
[".",".",".",".","8",".",".","7","9"]]
Output: [["5","3","4","6","7","8","9","1","2"],
["6","7","2","1","9","5","3","4","8"],
["1","9","8","3","4","2","5","6","7"],
["8","5","9","7","6","1","4","2","3"],
["4","2","6","8","5","3","7","9","1"],
["7","1","3","9","2","4","8","5","6"],
["9","6","1","5","3","7","2","8","4"],
["2","8","7","4","1","9","6","3","5"],
["3","4","5","2","8","6","1","7","9"]]
Explanation: The input board is shown above and the only valid solution
```

### **思路**
* **创建一个长度为3的 list 分别用来储存行，列和同一个 3x3 区间内的情况 list 内创建 9个 hashtable 用来记录方便查找**

### **代码**

``` python
class Solution:
    def solveSudoku(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        res_store = [[{},{},{},{},{},{},{},{},{}], [{},{},{},{},{},{},{},{},{}], [{},{},{},{},{},{},{},{},{}]]
        dot_count = 0

        for i in range(len(board)):
            for j in range(len(board[i])):
                if board[i][j] == ".":
                    dot_count += 1
                    continue
                else:
                    res_store[0][i][board[i][j]] = res_store[1][j][board[i][j]] = res_store[2][3 * (i // 3) + j // 3][board[i][j]] = 1

        #while(dot_count > 0):
        for k in range(50):
            for i in range(len(board)):
                for j in range(len(board[i])):
                    if board[i][j] == ".":
                        dot_count = self.fill_num(board, i, j, res_store, dot_count)
                        print(dot_count)

        return board

    def fill_num(self, board, row, col, res_store, dot_count):
        find_list = []

        for i in range(1,10):
            if str(i) not in res_store[0][row] and str(i) not in res_store[1][col] and str(i) not in res_store[2][3 * (row // 3) + col // 3]:
                find_list.append(str(i))

        if len(find_list) == 1:
            board[row][col] = find_list[0]
            res_store[0][row][find_list[0]] = res_store[1][col][find_list[0]] = res_store[2][3 * (row // 3) + col // 3][find_list[0]] = 1
            dot_count -= 1
        return dot_count

```
### **复杂度分析**
* **时间复杂度：O(n^2)**
* **空间复杂度：O(n^2)**
