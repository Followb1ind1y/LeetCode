## **48. Rotate Image**

[LeetCode 48. Rotate Image [Medium]](https://leetcode.com/problems/rotate-image/description/)

You are given an `n x n` 2D `matrix` representing an image, rotate the image by 90 degrees (clockwise).

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

```markdown
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [[7,4,1],[8,5,2],[9,6,3]]
```

### **思路**
* **对图像先作 `transpose` (即 index 互换位置) 然后对图像最 `reverse` (即将图像左右按中心对换位置) 即可达到顺时针选择 90 度的效果**
* **注意：题目要求 `in-place` 进行变换 不得有多余的储存空间 可以用类似 `matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]` 的方式进行变换**

### **代码**

``` python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        self.transpose(matrix)
        self.reverse(matrix)
        return matrix

    def transpose(self, matrix):
        for i in range(len(matrix)):
            for j in range(i, len(matrix[0])):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

    def reverse(self, matrix):
        for i in range(len(matrix)):
            for j in range(len(matrix[0]) // 2):
                matrix[i][j], matrix[i][len(matrix[0]) - 1 - j] = matrix[i][len(matrix[0]) - 1 - j], matrix[i][j]

```
### **复杂度分析**
* **时间复杂度：O(n^2)**
* **空间复杂度：O(1)**
