## **79. Word Search**

[LeetCode 79. Word Search [Medium]](https://leetcode.com/problems/word-search/)

Given an `m x n` grid of characters `board` and a string `word`, return `true` if `word` exists in the grid.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

```markdown
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```

```markdown
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
Output: false
```
### **理解**
在 `matrix` 中寻找符合要求的单词 每个位置的字符最多被使用一次 前后字符在 `matrix` 中必须相连 (即必须在上下左右的位置)

### **思路**
* **首先过一整遍 matrix 找到符合要求的首字母 确定位置 (row, col) 之后通过 backtracking 不断更新 board 和 word 直到 word 中的所有字符都被找到**
* **注意：因为 board 需要重复利用 所以在一次 backtracking 之后必须将更改的字符改回 否则会影响接下来的步骤**

### **代码**

``` python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] == word[0]:
                    if self.word_search(board, word[1:], i, j):
                        return True
        return False

    def word_search(self, board, word, row, col):
        track_word = board[row][col]
        board[row][col] = ""

        if len(word) == 0:
            return True
        else:
            if col != 0 and board[row][col - 1] == word[0]:
                if self.word_search(board, word[1:], row, col - 1): return True
            if col != len(board[0]) - 1 and board[row][col + 1] == word[0]:
                if self.word_search(board, word[1:], row, col + 1): return True
            if row != 0 and board[row - 1][col] == word[0]:
                if self.word_search(board, word[1:], row - 1, col): return True
            if row != len(board) - 1 and board[row + 1][col] == word[0]:
                if self.word_search(board, word[1:], row + 1, col): return True

        board[row][col] = track_word
        return False
```

### **复杂度分析**
* **时间复杂度：O(n!)**
* **空间复杂度：O(1)**
