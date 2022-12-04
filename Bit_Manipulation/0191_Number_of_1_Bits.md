## **191. Number of 1 Bits**

[LeetCode 191. Number of 1 Bits [Easy]](https://leetcode.com/problems/number-of-1-bits/description/)

Write a function that takes an unsigned integer and returns the number of '1' bits it has (also known as the **Hamming weight**).

```markdown
Input: n = 00000000000000000000000000001011
Output: 3
Explanation: The input binary string 00000000000000000000000000001011 has a total of three '1' bits.
```

### **理解**
Hamming Weight 为一个二进制数所有位次中 1 个数的总和

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

* **用 `input` 数字 和 `1` 进行 `AND` 运算 不断判断 `input` 数字转换为二进制后最后一位数字是否为 `0`**

### **代码**

``` python
class Solution:
    def hammingWeight(self, n: int) -> int:
        res = 0

        while(n):
            res += n & 1
            n = n >> 1

        return res
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**

### **类似问题**
* [LeetCode 461. Hamming Distance [Medium]](https://leetcode.com/problems/hamming-distance/description/)
