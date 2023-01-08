## **153. Find Minimum in Rotated Sorted Array**

[LeetCode 153. Find Minimum in Rotated Sorted Array [Medium]](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

Suppose an array of length `n` sorted in ascending order is rotated between `1` and `n` times. For example, the array `nums = [0,1,2,4,5,6,7]` might become:

* `[4,5,6,7,0,1,2]` if it was rotated `4` times.
* `[0,1,2,4,5,6,7]` if it was rotated `7` times.

Notice that rotating an array `[a[0], a[1], a[2], ..., a[n-1]]` 1 time results in the array `[a[n-1], a[0], a[1], a[2], ..., a[n-2]]`.

Given the sorted rotated array `nums` of unique elements, return the minimum element of this array.

You must write an algorithm that runs in `O(log n) time`.

```markdown
Input: nums = [4,5,6,7,0,1,2]
Output: 0
Explanation: The original array was [0,1,2,4,5,6,7] and it was rotated 4 times.
```

### **理解**
在一个左右平移过的 `Sorted Array` 中寻找最小值 要求时间复杂度为`O(log n)`

### **思路**
* **因为是 `Sorted Array` 所以想到利用 `Binary Search` 解决问题 设置左右两个 `Pointer` 不断和 `Center` 比对移动**
* **在 `Array` 中没有重复数字情况时 先对比 `Center` 和 `right` 如果 `Center` 大于 `right` 则最小值肯定在 `Center` 右侧 其余情况则在其左侧**
* **在 `Array` 中有重复数字情况时 需要考虑 `Center`, `left` 和 `right` 相同的情况 (i.e. `[3,3,1,3]`) 因为无法判断最小值出现在 `Center` 左侧还是右侧 所以将左右两个 `Pointer` 各往里移动一格 缩小搜索范围**

### **代码**

``` python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        left, right = 0, len(nums)-1

        while(left < right):
            center = (left+right)//2
            if nums[center] > nums[right]:
                left = center + 1
            else:
                right = center
        
        return nums[left]
```
### **复杂度分析**
* **时间复杂度：O(log(n))**
* **空间复杂度：O(1)**

### **类似问题**
* [LeetCode 154. Find Minimum in Rotated Sorted Array II [Hard]](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii//)
