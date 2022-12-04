## **461. Hamming Distance**

[LeetCode 461. Hamming Distance [Medium]](https://leetcode.com/problems/hamming-distance/description/)

The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Given two integers `x` and `y`, return the Hamming distance between them.

```markdown
Input: x = 1, y = 4
Output: 2
Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑
The above arrows point to positions where the corresponding bits are different.
```

### **理解**
Hamming Distance 为两个二进制数相同位次上数字不同的个数

### **思路**
<div class="heatMap">

| Operator | Example |  Meaning |
| --- | --- | --- |
| `&` | a & b | Bitwise AND |
| `｜` |	a ｜ b |	Bitwise OR |
| `^` |	a ^ b |	Bitwise XOR (exclusive OR) |
| `~` |	~a |	Bitwise NOT |
| `<<` |	a << n |	Bitwise left shift |
| `>>` |	a >> n |	Bitwise right shift |

</div>

* **可用上面表格中的运算符号进行快速的 `Bit Manipulation` 输入为 `Integer` 输出也为 `Integer`**
* **寻找两个数相同位次不同数字的个数 可以用 `XOR` 输出为 十进制数 需要转化为二进制统计 `1` 的个数得出结果**

### **代码**

``` python
class Solution:
    def hammingDistance(self, x: int, y: int) -> int:
        xor = x ^ y
        res = 0

        while(xor > 0):
            res += xor % 2
            xor = xor // 2

        return res
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**

### **类似问题**
* [LeetCode 191. Number of 1 Bits [Easy]](https://leetcode.com/problems/number-of-1-bits/)
