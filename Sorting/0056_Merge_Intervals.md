## **56. Merge Intervals**

[LeetCode 56. Merge Intervals [Medium]](https://leetcode.com/problems/merge-intervals/description/)

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

```markdown
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
```

### **思路**
* **先根据 `intervals` 第一项进行排序 之后从左到右不断检测 后面 `intervals` 第一项是否与前一个 `intervals` 重合 如果是则 `merge` 如果不是则加入 `return list`**
* **利用 `sorted(intervals, key = lambda x: x[0])` 可根据 `intervals` 第一项进行排序 更改 `key` 可将 `sorted()` 运用到更多地方**
* **注意：`sorted()` 不改变原 `list` 而 `list.sort()` 则在 `list` 本身进行排序**
* **利用 `sorted()` 的 Average Time Complexity 为 O(nlog(n))**

### **代码**

``` python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        sorted_intervals = sorted(intervals, key = lambda x: x[0])
        res = [sorted_intervals[0]]

        for i in range(1, len(sorted_intervals)):
            if res[-1][0] <= sorted_intervals[i][0] <= res[-1][1]:
                res[-1] = [min(sorted_intervals[i][0], res[-1][0]), max(sorted_intervals[i][1], res[-1][1])]
            else:
                res.append(sorted_intervals[i])

        return res
```
### **复杂度分析**
* **时间复杂度：O(nlog(n))**
* **空间复杂度：O(n)**
