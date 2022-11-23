## **76. Minimum Window Substring**

[LeetCode 76. Minimum Window Substring [Hard]](https://leetcode.com/problems/minimum-window-substring/description/)

Given two strings `s` and `t` of lengths `m` and `n` respectively, return the minimum window
**substring** of `s` such that every character in `t` (**including duplicates**) is included in the window. If there is no such substring, return the empty string `""`.

The testcases will be generated such that the answer is **unique**.

```markdown
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.
```

```markdown
Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
```
### **理解**
给定两个 `string` 在前一个  `string` 中找到满足 后一个 `string` 所有单词都出现的 `substring` 的最短距离

### **思路**
* **首先创建 `hashmap` 将 `t` 中出现的所以的字母和数量存储 并统计长度 创建 `queue` 用来存储 `hashmap` 中出现的单词和位置 用 `start` 和 `end` 存储当前满足条件的最短区间**
* **从一位次开始 `loop` 寻找对象 `s` 并将 `t` 中出现的字母和其位置储存在 `queue` 中, `loop` 过程中分为两个阶段: 1.确定 `t` 中的所有字母都已出现 (即将 `missinng_length` 减为 `0`) 2.从前往后删除当前 `queue` 中的多余字母 直到 `missinng_length` 大于 `0` (即将满足条件的区间进行缩减以找到满足条件的最小区间 并将头号位删除 重新返回第一阶段往后进行寻找) 最终返回 `string[start:end]` 的最小区间**
* **可以利用 `collections.Counter(t)` 进行快速的 `hashmap` 录入**
* **`queue` 的存储规则为 `first-in-first-out` 利用这个规则不断更新录入并计算最小区间**

### **代码**

``` python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        hashmap = collections.Counter(t)
        queue = []
        missing_length = len(t)
        start, end = 0, -1

        for i in range(len(s)):
            if s[i] in hashmap:
                queue.append([i, s[i]])
                if hashmap[s[i]] > 0:
                    missing_length -= 1
                hashmap[s[i]] -= 1

                if missing_length == 0:
                    while(missing_length == 0):
                        if end == -1 or queue[-1][0] - queue[0][0] < end - start:
                            start, end = queue[0][0], queue[-1][0]
                        hashmap[queue[0][1]] += 1
                        if hashmap[queue[0][1]] > 0:
                            missing_length += 1
                        queue.pop(0)

        return s[start:end+1]
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(n)**
