## **16. 3Sum Closest**

[LeetCode 16. 3Sum Closest [Medium]](https://leetcode.com/problems/3sum-closest/description/)

Given an integer array `nums` of length `n` and an integer `target`, find three integers in `nums` such that the sum is closest to `target`.

Return *the sum of the three integers*.

You may assume that each input would have exactly one solution.

```markdown
Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

### **思路**
* **总体思路基本和 3Sum 一致 设置 res 为 `float('inf')` 通过对三个指针的不断移动逼近最小值**

### **代码**

``` python
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        res = float('inf')
        nums.sort()

        for i in range(len(nums) - 2):
            start_point = i + 1
            end_point = len(nums) - 1
            while(start_point < end_point):
                curr_sum = nums[i] + nums[start_point] + nums[end_point]
                if abs(curr_sum - target) < abs(res - target):
                    res = curr_sum
                if curr_sum - target < 0:
                    start_point += 1
                elif curr_sum - target > 0:
                    end_point -= 1
                else:
                    break
        return res
```
### **复杂度分析**
* **时间复杂度：O(n^2)**
* **空间复杂度：O(1)**
