## **31. Next Permutation**

[LeetCode 31. Next Permutation [Medium]](https://leetcode.com/problems/next-permutation/description/)

A permutation of an array of integers is an arrangement of its members into a sequence or linear order.

For example, for `arr = [1,2,3]`, the following are all the permutations of `arr: [1,2,3], [1,3,2], [2, 1, 3], [2, 3, 1], [3,1,2], [3,2,1]`.
The next permutation of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the next permutation of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).

For example, the next permutation of `arr = [1,2,3]` is `[1,3,2]`.
Similarly, the next permutation of `arr = [2,3,1]` is `[3,1,2]`.
While the next permutation of `arr = [3,2,1]` is `[1,2,3]` because `[3,2,1]` does not have a lexicographical larger rearrangement.
Given an array of integers `nums`, find the next permutation of `nums`.

The replacement must be **in place** and use only constant extra memory.

```markdown
Input: nums = [1,2,3]
Output: [1,3,2]
```

```markdown
Input: nums = [1,1,5]
Output: [1,5,1]
```

### **思路**
* **从最右侧开始往左侧寻找第一个右侧比左侧大的数 标记左侧（较小）得数 并在这个数的右侧寻找比其大的最小数 然后将这个数和标记数交换位置 最后将标记数位置往右的所有数 reverse 即可完成变换**
* **如果所有的数字都比左边的数小 将整个数组 reverse**

### **代码**

``` python
class Solution:
    def nextPermutation(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        for i in range(len(nums) - 1, 0, -1):
            if nums[i] > nums[i - 1]:
                switch1, switch2 = i - 1, i
                for j in range(i, len(nums)):
                    if nums[j] > nums[switch1] and nums[j] <= nums[switch2]:
                        switch2 = j
                nums[switch1], nums[switch2] = nums[switch2], nums[switch1]

                left, right = i , len(nums) - 1
                while(left < right):
                    nums[left], nums[right] = nums[right], nums[left]
                    left += 1
                    right -= 1
                return None

        nums.reverse()
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**
