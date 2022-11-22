## **75. Sort Colors**

[LeetCode 75. Sort Colors [Medium]](https://leetcode.com/problems/sort-colors/description/)

Given an array `nums` with `n` objects colored red, white, or blue, sort them **in-place** so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers `0`, `1`, and `2` to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

```markdown
Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

```markdown
Input: nums = [2,0,1]
Output: [0,1,2]
```
### 理解
在不能使用 `sort()` 的情况下 完成 in-place 的三个数字 `Array` 排序 类似于国旗排序问题 -> [Dutch national flag problem](https://en.wikipedia.org/wiki/Dutch_national_flag_problem)

### **思路**
* **设置三个 `pointer` 分别代表 `zeros`, `ones`, `twos` 的位置, `zeros` 和 `ones` 的起始位置 为 `0`, `twos` 的起始位置为 `len(nums) - 1`**
* **`zeros` 左侧的所有数字都为 `0` `twos` 右侧的所有数字都为 `2`**
* **在 loop 过程中 以 `ones` 的 pointer 为标准不断移动 当当前位次的数字为 `0` 时 将当前位次的数字和 `zeros` 对应的数字 (即 `1`) 交换 并将 `zeros` 和 `ones` 都向右移动**
* **当当前位次的数字为 `1` 时 将 `ones` 向右侧移动**
* **当当前位次的数字为 `2` 时 将当前位次的数字和 `twos` 对应的数字交换 并将 `twos` 都向左移动 `ones` 不需要移动 因为换到前面的数字还没有判断**

### **代码**

``` python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        zeros, ones, twos = 0, 0, len(nums) - 1

        while(ones <= twos):
            if nums[ones] == 0:
                nums[ones], nums[zeros] = nums[zeros], nums[ones]
                zeros += 1
                ones += 1
            elif nums[ones] == 1:
                ones += 1
            else:
                nums[ones], nums[twos] = nums[twos], nums[ones]
                twos -= 1

        return nums
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**
