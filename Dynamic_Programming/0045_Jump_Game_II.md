## **45. Jump Game II**

[LeetCode 45. Jump Game II [Medium]](https://leetcode.com/problems/jump-game-ii/)

You are given a **0-indexed** array of integers `nums` of length `n`. You are initially positioned at `nums[0]`.

Each element `nums[i]` represents the maximum length of a forward jump from index `i`. In other words, if you are at `nums[i]`, you can jump to any `nums[i + j]` where:

* `0 <= j <= nums[i]` and
* `i + j < n`

Return the minimum number of jumps to reach `nums[n - 1]`. The test cases are generated such that you can reach `nums[n - 1]`.

```markdown
Input: nums = [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

### **思路**
* **每次跳跃选择最贪心的方式 即满足当前可走的步数 `i` 内 `i` 加上其 `index` 对应数值之和的最大值 也可以理解为未来两步的最大值 直到到达最终点**

### **代码**

``` python
class Solution:
    def jump(self, nums: List[int]) -> int:
        goal = len(nums) - 1
        res = cur_spot = 0

        while(goal > 0):
            res +=1
            cur_num = nums[cur_spot]
            max_num = next_spot = 0
            if cur_num >= goal :
                return res
            for i in range(cur_num):
                if nums[cur_spot + 1 + i] + i >= max_num:
                    max_num = nums[cur_spot + 1 + i] + i
                    next_spot = i + 1
            goal -= next_spot
            cur_spot += next_spot

        return res
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**
