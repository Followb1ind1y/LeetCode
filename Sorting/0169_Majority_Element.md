## **169. Majority Element**

[LeetCode 169. Majority Element [Easy]](https://leetcode.com/problems/majority-element/description/)

Given an array `nums` of size `n`, return the majority element.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

**Follow-up**: Could you solve the problem in linear time and in `O(1)` space?

```markdown
Input: nums = [3,2,3]
Output: 3
```

```markdown
Input: nums = [2,2,1,1,1,2,2]
Output: 2
```
### 理解
在 linear time and in `O(1)` space 下 寻找出现的最主要的数字

### **思路**
* **设置 `candidate`, `count` 记录当前出现的最高频数字和出现次数 按次序过一遍 `list` 如果和当前高频数字相同则增加 `count` 如果不一样则减少 `count` 如果 `count` 被减少为 `0` 则更新新的 `candidate`** -> [Boyer–Moore majority vote algorithm](https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_majority_vote_algorithm)

### **代码**

``` python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        candidate, count = nums[0], 0
        for num in nums:
            if num == candidate:
                count += 1
            elif count == 0:
                candidate, count = num, 1
            else:
                count -= 1
        return candidate
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**
