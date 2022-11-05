## **42. Trapping Rain Water**

[LeetCode 42. Trapping Rain Water [Hard]](https://leetcode.com/problems/trapping-rain-water/description/)

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

```markdown
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1].
In this case, 6 units of rain water (blue section) are being trapped.
```

### **思路**
* **设置 `left` `right` 两个指针分别指向起始和终止位置 分别以从左到右和从右到左两种方式 找到比当前 `left` 和 `right` 指针所指的值大（或相等）的位置并计算雨量**

### **代码**

``` python
class Solution:
    def trap(self, height: List[int]) -> int:
        left, right = 0, len(height) - 1
        res = 0

        def cal_rain(left, right):
            box = (right - left - 1) * min(height[left], height[right])
            for i in range(left + 1, right):
                box -= height[i]
            return box

        for i in range(1, len(height)):
            if height[left] <= height[i]:
                res += cal_rain(left, i)
                left = i
            if height[right] < height[len(height) - 1 - i]:
                res += cal_rain(len(height) - 1 - i, right)
                right = len(height) - 1 - i

        return res
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**
