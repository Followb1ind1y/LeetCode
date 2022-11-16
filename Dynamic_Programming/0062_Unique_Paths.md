## **62. Unique Paths**

[LeetCode 62. Unique Paths [Medium]](https://leetcode.com/problems/unique-paths/description/)

There is a robot on an `m x n` grid. The robot is initially located at the top-left corner (i.e., `grid[0][0]`). The robot tries to move to the bottom-right corner (i.e., `grid[m - 1][n - 1]`). The robot can only move either down or right at any point in time.

Given the two integers `m` and `n`, return the number of possible unique paths that the robot can take to reach the bottom-right corner.

The test cases are generated so that the answer will be less than or equal to `2 * 10^9`.

```markdown
Input: m = 3, n = 2
Output: 3
Explanation: From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down
```

### **思路**
* **在 Dynamic Programming Solution 中 `res` 中储存的数值可以理解为到达此点位的可能路径 从第一行开始不断更新下一行的路径数量 更新方法为 将上方格子数字和左方格子的数字相加 因为到达此格的方法只有向右和向下 所以将他们相加即可累计总的路线数量**
* **Math Solution 则更为直接 直接通过 `(m+n-2)! / ((m-1)!*(n-1)!)` 得出结果**

### **代码**

**Dynamic Programming Solution**

``` python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        res = [0 for i in range(n)]
        res[0] = 1

        for i in range(m):
            for j in range(n):
                if j != 0:
                    res[j] = res[j] + res[j - 1]

        return res[-1]
```

**Math Solution**

``` python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        return int(math.factorial(m+n-2)/math.factorial(m-1)/math.factorial(n-1))
```

### **复杂度分析**
* **时间复杂度：O(m*n)**
* **空间复杂度：O(n)**

### **类似问题**
* [LeetCode 63. Unique Paths II [Medium]](https://leetcode.com/problems/unique-paths-ii/)
* [LeetCode 64. Minimum Path Sum [Medium]](https://leetcode.com/problems/minimum-path-sum/)
