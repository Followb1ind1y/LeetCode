## **51. N-Queens**

[LeetCode 51. N-Queens [Hard]](https://leetcode.com/problems/n-queens/description/)

The n-queens puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return all distinct solutions to the **n-queens puzzle**. You may return the answer in any order.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.

```markdown
Input: n = 4
Output: [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
Explanation: There exist two distinct solutions to the 4-queens puzzle
```

### **思路**
* **规则：`Queen` 所在的行，列，两个斜对角线都不得放置其他棋子**
* **在一个合理的解中 每一行和每一列都需要有一个 `Queen` 从第一行开始 在每一行中按照规则寻找可以放置的位置并不断进行 Backtracking 直到每一行都被放置 `Queen`**

### **代码**

``` python
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        res = []
        self.find_next_Q(n, 0, [], res)
        return res

    def find_next_Q(self, n, row, col_list, res):
        if len(col_list) == n:
            board = ["." * i + "Q" + "." * (n - i - 1) for i in col_list]
            res.append(board)
            return None

        col, row_col_sum, row_col_sub = {}, {}, {}

        for i in range(len(col_list)):
            if col_list[i] not in col:
                col[col_list[i]] = 1
            if i + col_list[i] not in row_col_sum:
                row_col_sum[i + col_list[i]] = 1
            if i - col_list[i] not in row_col_sub:
                row_col_sub[i - col_list[i]] = 1

        for j in range(n):
            if j not in col and row + j not in row_col_sum and row - j not in row_col_sub:
                self.find_next_Q(n, row + 1, col_list + [j], res)
```

### **复杂度分析**
* **时间复杂度：O(n!)**
* **空间复杂度：O(n^2)**
