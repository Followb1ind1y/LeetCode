## **150. Evaluate Reverse Polish Notation**

[LeetCode 150. Evaluate Reverse Polish Notation [Medium]](https://leetcode.com/problems/evaluate-reverse-polish-notation/description/)

You are given an array of strings `tokens` that represents an arithmetic expression in a Reverse Polish Notation.

Evaluate the expression. Return an integer that represents the value of the expression.

Note that:

* The valid operators are `'+'`, `'-'`, `'*'`, and `'/'`.
* Each operand may be an integer or another expression.
* The division between two integers always truncates toward zero.
* There will not be any division by zero.
* The input represents a valid arithmetic expression in a reverse polish notation.
* The answer and all the intermediate calculations can be represented in a 32-bit integer.

```markdown
Input: tokens = ["4","13","5","/","+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
```

```markdown
Input: tokens = ["10","6","9","3","+","-11","+","/","+","17","+","5","+"]
Output: 22
Explanation: ((10 + (6 / ((9 + 3) + -11))) + 17) + 5
= ((10 + (6 / (12 + -11))) + 17) + 5
= ((10 + (6 / -132)) + 17) + 5
= ((10 + 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```

### **理解**
按照 `Reverse Polish notation` 来计算 `list` 中数字的合 即依次将运算符号前的两个数字进行运算


### **思路**
* **从前往后寻找运算符号 并 pop 出他的前两个位的数字进行运算 将结果储存回 list 中**
* **在 list pop 过后 index 会发生变化 最好在草稿上列出来以免出错**
* **可以利用 dict 储存 str 的运算符号 和其对应的运算规则 用 lambda 表达运算**

### **代码**

``` python
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        ops = {'+': lambda x, y: x + y, 
              '-': lambda x, y: x - y,
              '*': lambda x, y: x * y, 
              '/': lambda x, y: int(x / y)}
        i = 0
        while(len(tokens) > 1):
            if tokens[i] in ['+', '-', '*', '/']:
                second, first = int(tokens.pop(i-1)), int(tokens.pop(i-2))
                tokens[i-2] = ops[tokens[i-2]](first, second)
                i -= 1
            else:
                i += 1

        return int(tokens[0])
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**
