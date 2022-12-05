## **89. Gray Code**

[LeetCode 89. Gray Code [Medium]](https://leetcode.com/problems/gray-code/)

An **n-bit gray code sequence** is a sequence of `2^n` integers where:

* Every integer is in the inclusive range `[0, 2^n - 1]`,
* The first integer is `0`,
* An integer appears **no more than once** in the sequence,
* The binary representation of every pair of adjacent integers differs by **exactly one bit**, and
* The binary representation of the **first** and **last** integers differs by **exactly one bit**.

Given an integer `n`, return any valid **n-bit gray code sequence**.

```markdown
Input: n = 2
Output: [0,1,3,2]
Explanation:
The binary representation of [0,1,3,2] is [00,01,11,10].
- 00 and 01 differ by one bit
- 01 and 11 differ by one bit
- 11 and 10 differ by one bit
- 10 and 00 differ by one bit
[0,2,3,1] is also a valid gray code sequence, whose binary representation is [00,10,11,01].
- 00 and 10 differ by one bit
- 10 and 11 differ by one bit
- 11 and 01 differ by one bit
- 01 and 00 differ by one bit
```

### **理解**
需要对一个 `[0, 2^n - 1]` 的 sequence 进行排序 排序规则为: 第一位为 0, 相邻的两个数转换为二进制数有一个位次不同, 最后一位和第一位数转换为二进制数也有一个位次不同, 并且每个数字只能用一次

### **思路**
* 通过观察 n = 1, n = 2, n = 3 可以发现规律: 当 n 变大 1 之后 list 会扩大一倍 并且 前一半数字不发生变化 后一半数字则是前一半数字相反排序并加上 2^(n-1)
* n = 2: [0, 1, 3, 2] -> [00, 01, 11, 10]
* n = 3: [00, 01, 11, 10] + [10, 11, 01, 00] (Reverse) -> 在前一半 list 数字前加 0 在后一半加 1 -> [000, 001, 011, 010] + [110, 111, 101, 100] -> [000, 001, 011, 010, 110, 111, 101, 100] -> [0, 1, 3, 2, 6, 7, 5, 4]


### **代码**

``` python
class Solution:
    def grayCode(self, n: int) -> List[int]:
        res = [0, 1]
        for i in range(n-1):
            for j in range(len(res)-1,-1,-1):
                res.append(res[j] + 2**(i+1))
        return res
```
### **复杂度分析**
* **时间复杂度：O(2^n)**
* **空间复杂度：O(1)**
