## **33. Search in Rotated Sorted Array**

[LeetCode 33. Search in Rotated Sorted Array [Medium]](https://leetcode.com/problems/search-in-rotated-sorted-array/)

There is an integer array `nums` sorted in ascending order (with distinct values).

Prior to being passed to your function, `nums` is possibly rotated at an unknown pivot index `k` `(1 <= k < nums.length)` such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (0-indexed). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` after the possible rotation and an integer `target`, return the index of `target` if it is in `nums`, or `-1` if it is not in `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

```markdown
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

```markdown
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

### **思路**
* **设置 `left` `right` 两个 Pointer 通过计算中心点位不断 Binary Search 来更快的找到需要的值**
* **虽然 Array 被 Rotated 但被中心点位分割后至少有一侧还是 Sorted 通过这个规律来寻找所需要的值**

### **代码**

``` python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1

        while(left <= right):
            center = (left + right) // 2
            if nums[center] == target:
                return center
            elif nums[center] >= nums[left]:
                if target >= nums[left] and target <= nums[center]:
                    right = center - 1
                else:
                    left = center + 1
            else:
                if target >= nums[center] and target <= nums[right]:
                    left = center + 1
                else:
                    right = center - 1
        return -1
```
### **复杂度分析**
* **时间复杂度：O(log(n))**
* **空间复杂度：O(1)**

### **类似题目**
* [LeetCode 81. Search in Rotated Sorted Array II [Medium]](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)
