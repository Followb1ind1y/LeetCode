## **22. Generate Parentheses**

[[Medium] LeetCode 22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)

Given `n` pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

```markdown
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```

### **思路**
* **创建 helper function 用于 Recursion 从空的string ("") 开始记录括号 用 left 和 right 来记录剩余需要补充的括号**
* **当剩余 left 大于 0 时 我们始终可以添加新的 "(" 当剩余 left 小于 right 时 我们可以选择添加新的 ")" 当 left 和 right 均为 0 时 将 string 记录到最终的 res 中**

### **代码**

``` python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        res = []

        def helper(res, curr, left, right):
            if left == 0 and right == 0:
                res.append(curr)
            if left > 0:
                helper(res, curr + "(", left - 1, right)
            if left < right:
                helper(res, curr + ")", left, right - 1)

        helper(res, "", n, n)

        return res
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(n)**
