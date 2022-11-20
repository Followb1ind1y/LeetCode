## **39. Combination Sum**

[LeetCode 39. Combination Sum [Medium]](https://leetcode.com/problems/combination-sum/description/)

Given an array of distinct integers `candidates` and a `target` integer target, return a list of all unique combinations of `candidates` where the chosen numbers sum to `target`. You may return the combinations in any order.

The same number may be chosen from `candidates` an unlimited number of times. Two combinations are unique if the
frequency
 of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to `target` is less than 150 combinations for the given input.

```markdown
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
```

### **思路**
* **利用 Depth-first search (DFS) 反复在 `candidates` 中寻找 当 `target` 为 0 时将当前的 list 并入最终结果 `res`**

### **代码**

``` python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        res = []

        def helper(candidates, target, store):
            if target < 0:
                return
            if target == 0:
                res.append(store)
            for j in range(len(candidates)):
                helper(candidates[j:], target - candidates[j], store + [candidates[j]])

        helper(candidates, target, [])

        return res
```
### **复杂度分析**
* **时间复杂度：O(n+m)**
* **空间复杂度：O(n)**
