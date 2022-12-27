## **139. Word Break**

[LeetCode 139. Word Break [Medium]](https://leetcode.com/problems/word-break/)

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

Note that the same word in the dictionary may be reused multiple times in the segmentation.

```markdown
Input: s = "leetcode", wordDict = ["leet","code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```

```markdown
Input: s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
Output: false
```
### **理解**
给定一个由 `string` 组成的 `list` 判断 另一个 `string` 通过这个 `list` 中的 `string` 组合而成 `list` 中的 `string` 可以重复使用

### **思路**
* **先过一遍 `wordDict` 保存所有其中 `string` 的长度 方便之后查找时 只需在保存的长度区间中寻找 通过 `backtracking` 不断截断 `s` 判断 截断部分是否在 `wordDict` 中 直到 `s` 本身出现在其中**
* **注意: `list` 可以直接用来查找 (e.g. `x in list`)**
* **注意: `list` 和 `dict` 是 `unhashable` 所以在需要用到 `cache` 提升速度时 可以尝试使用 `tuple` 传递**

### **代码**

``` python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        hashrange = []
        for i in range(len(wordDict)):
            hashrange.append(len(wordDict[i]))
        return self.checkBreak(s, tuple(wordDict), tuple(set(hashrange)))

    @cache
    def checkBreak(self, s, hashmap, hashrange):
        if s in hashmap:
            return True
        for i in hashrange:
            if s[:i] in hashmap:
                if self.checkBreak(s[i:], hashmap, hashrange):
                    return True
        return False
```
### **复杂度分析**
* **时间复杂度：$O(n)$**
* **空间复杂度：$O(n)$**
