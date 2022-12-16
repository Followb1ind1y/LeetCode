## **5. Longest Palindromic Substring**

[LeetCode 5. Longest Palindromic Substring [Medium]](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

Given a string `s`, return the longest palindromic substring in `s`.

A string is called a palindrome string if the reverse of that string is the same as the original string.

```markdown
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
```

```markdown
Input: s = "cbbd"
Output: "bb"
```

### **思路**
* **首先确定中心 分奇数偶数两种情况创建 helper function 不断移动中心来检测所以情况 最终返回最大值**
* **`max()` function的用法：`max_val = max(var1, var2, var3, key=len)` 通过设置 `key = len` 使得 `max()` 返回的值不为最大长度的数值 而为最大长度的 str**

### **代码**

``` python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        res = ""

        def find_sub(start, end):
            sub = ""
            for i in range(len(s)):
                if start >= 0 and end < len(s) and s[start] == s[end]:
                    sub = s[start:end+1]
                    start -= 1
                    end += 1
                else:
                  break
            return sub

        for i in range(len(s)):
            res = max(find_sub(i,i), find_sub(i,i+1), res, key=len)
        return res
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**

### **类似问题**
* [LeetCode 131. Palindrome Partitioning [Medium]](https://leetcode.com/problems/palindrome-partitioning/)
