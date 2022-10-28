## **3. Longest Substring Without Repeating Characters**

[LeetCode 3. Longest Substring Without Repeating Characters [Medium]](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

Given a string s, find the length of the longest
substring without repeating characters.

```markdown
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

```markdown
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

### **思路**
* **创建 hashmap 保存录入 str 的位次 (e.g. `{"str", index}`) 创建指针 `start_point` 用来记录起始位置 用loop 的 i 记录当前位置**
* **若当前位次的 str 未出现在 hashmap 中时 将当前位次的 str 录入 hashmap 或者 若当前位次的 str 出现在 `start_point` 之前 则更新 hashmap 记录的 index 之后更新 `max_len (i - start_point + 1)`**
* **当搜索到当前位次的 str 曾出现在 hashmap 中时 检查它是否出现在起始位置前 若不是 则重置起始位置 i 并更新 hashmap 记录的 index**

### **代码**

``` python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        start_point = 0
        hashmap = {}
        max_len = 0

        for i in range(len(s)):
            if s[i] not in hashmap or hashmap[s[i]] < start_point:
                hashmap[s[i]] = i
                max_len = max(max_len, i - start_point + 1)
                continue
            else:
                start_point = hashmap[s[i]] + 1
                hashmap[s[i]] = i
        return max_len
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(n)**
