## **11. Container With Most Water**

[LeetCode 11. Container With Most Water [Medium]](https://leetcode.com/problems/container-with-most-water/)

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return *the maximum amount of water a container can store*.

**Notice** that you may not slant the container.

```markdown
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7].
In this case, the max area of water (blue section) the container can contain is 49.
```

### **思路**
* **设置left, right 从最左最右开始记录面积 之后不断选择左右两边中矮的一边忘另一侧移动**

### **代码**

``` python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        left = 0
        right = len(height) - 1
        max_area = 0

        while(left < right):
            curr_area = min(height[left],height[right]) * (right - left)
            max_area = max(curr_area, max_area)
            if height[left] < height[right]:
                left += 1
            else:
                right -= 1
        return max_area
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**
