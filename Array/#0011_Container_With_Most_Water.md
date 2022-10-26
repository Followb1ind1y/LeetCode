## **11. Container With Most Water**

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return *the maximum amount of water a container can store*.

**Notice** that you may not slant the container.

![Q11_Example](/img/Q11_Example.png)

```markdown
**Input:** height = [1,8,6,2,5,4,8,3,7]
**Output:** 49
**Explanation:** The above vertical lines are represented by array
[1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section)
 the container can contain is 49.
```

### **思路**
* 设置left, right 从最左最右开始记录面积 之后不断选择左右两边中矮的一边忘另一侧移动

### **代码**

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        max_amount = 0
        left = 0
        right = len(height)  - 1

        while(left < right) :
            hi = min(height[left],height[right])
            le = right - left
            max_amount = max(max_amount, hi*le)
            if height[left] < height[right]:
                left += 1
            else:
                right -=1
        return max_amount
```
### **复杂度分析**
* **时间复杂度：**
* **空间复杂度：**

[LeetCode 11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
