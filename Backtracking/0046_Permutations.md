## **46. Permutations**

[LeetCode 46. Permutations [Medium]](https://leetcode.com/problems/permutations/description/)

Given an array `nums` of distinct integers, return all the possible permutations. You can return the answer in any order.

```markdown
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

### **思路**
* **从完整的 `nums` 开始不断进行 backtracking 每次将 `nums` 中已用的数字移去 加入 `curr_list` 中  直到 `len(nums)` 为 0**

### **代码**

``` python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        res = []
        self.backtracking(nums, res, [])
        return res

    def backtracking(self, nums, res, curr_list):
        if len(nums) == 0:
            res.append(curr_list)
        else:
            for i in range(len(nums)):
                self.backtracking(nums[:i] + nums[i+1:], res, curr_list + [nums[i]])
```
### **复杂度分析**
* **时间复杂度：O(n!)**
* **空间复杂度：O(n)**
