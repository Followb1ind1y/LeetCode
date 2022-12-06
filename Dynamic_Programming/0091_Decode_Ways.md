## **91. Decode Ways**

[LeetCode 91. Decode Ways [Medium]](https://leetcode.com/problems/decode-ways/description/)

A message containing letters from `A-Z` can be encoded into numbers using the following mapping:

```markdown
'A' -> "1"
'B' -> "2"
...
'Z' -> "26"
```

To decode an encoded message, all the digits must be grouped then mapped back into letters using the reverse of the mapping above (there may be multiple ways). For example, `"11106"` can be mapped into:

* `"AAJF"` with the grouping `(1 1 10 6)`
* `"KJF"` with the grouping `(11 10 6)`

Note that the grouping `(1 11 06)` is invalid because `"06"` cannot be mapped into `'F'` since `"6"` is different from `"06"`.

Given a string `s` containing only digits, return the **number** of ways to **decode** it.

The test cases are generated so that the answer fits in a **32-bit** integer.

```markdown
Input: s = "226"
Output: 3
Explanation: "226" could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```

### **理解**
将一串数字进行分割 使分割后的数字其能够匹配 `A-Z (1-26)` 分割后的数字不可以 `0` 开头

### **思路**
* **分割主要分为三种情况：`0-9` 的数字， 头两位数字为 `10-26` 的数字 大于 `26` 的数字 通过 `dfs` 不断累计数字相加**
* **注意: 不能像一般 `backtracking` 一样 在开始设置 `res` 的 `list` 在 `backtracking` 过程中对 `res` 进行更新**
* **`@cache` 和 `@lru_cache` 可以在 `function` 前 `declear` 用于缓存遇到过的 `function` `input` 和 `output` 例如: 在跑过一遍 `df(1,2)` 后得出结果 `5` 之后在需要跑 `df(1,2)` 时则不需要再花时间 `run` 可以直接得出结果 节省时间**

### **代码**

``` python
class Solution:
    def numDecodings(self, s: str) -> int:
        if s == "": return 0

        @lru_cache
        def dfs(string):
            if len(string) == 0:
                return 1
            elif string[0] == "0":
                return 0
            elif len(string) == 1:
                return 1
            elif int(string[0:2]) <= 26:
                return dfs(string[1:]) + dfs(string[2:])
            else:
                return dfs(string[1:])

        return dfs(s)
```

### **复杂度分析**
* **时间复杂度：O(n!)**
* **空间复杂度：O(1)**
