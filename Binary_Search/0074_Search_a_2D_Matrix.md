## **74. Search a 2D Matrix**

[LeetCode 74. Search a 2D Matrix [Medium]](https://leetcode.com/problems/search-a-2d-matrix/description/)

Write an efficient algorithm that searches for a value `target` in an `m x n` integer matrix `matrix`. This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.

```markdown
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
```

```markdown
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: false
```

### **思路**
* **因为 `matrix` 内的数字是按顺序排列 所以可以将 `2D matrix` 看作普通 `1D list` 来进行 `binary search` 再将其转换回 `2D` 即可 `(mid_point -> mid_row, mid_col)`**

### **代码**

``` python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        left, right = 0, len(matrix) * len(matrix[0]) - 1

        while(left <= right):
            mid_point = (left + right) // 2
            mid_row = mid_point // len(matrix[0])
            mid_col = mid_point % len(matrix[0])

            if matrix[mid_row][mid_col] > target:
                right = mid_point - 1
            elif matrix[mid_row][mid_col] < target:
                left = mid_point + 1
            else:
                return True

        return False
```
### **复杂度分析**
* **时间复杂度：O(log(m+n))**
* **空间复杂度：O(1)**
