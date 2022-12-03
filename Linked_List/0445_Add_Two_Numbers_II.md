## **445. Add Two Numbers II**

[LeetCode 445. Add Two Numbers II [Medium]](https://leetcode.com/problems/add-two-numbers-ii/description/)

You are given two **non-empty** linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

```markdown
Input: l1 = [7,2,4,3], l2 = [5,6,4]
Output: [7,8,0,7]
```

### **理解**
两个 `LinkedList` 相加 储存规则为最高位储存在最开始 最低位在最底部 得出两个 `LinkedList` 相加结果  需要考虑进位情况

### **思路**
* **因为 `LinkedList` 长度未知且是以最高位起点记录的 所以需要先将两个 `LinkedList` 全部过一遍并记录储存的数字 将两个数字直接相加得出结果 之后选择 `l1`, `l2` 中较长的 一个 从头开始更新里面 `val`**
* **注意: 两数字相加后 有可能会发生进位情况 有可能得出的 `LinkedList` 长度大于 `l1`, `l2` 需要在开头加一位 `1`**

### **代码**

``` python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        l1_str, l2_str = "", ""
        l1_track, l2_track = l1, l2

        while(l1_track):
            l1_str = l1_str + str(l1_track.val)
            l1_track = l1_track.next
        while(l2_track):
            l2_str = l2_str + str(l2_track.val)
            l2_track = l2_track.next

        sum_num = str(int(l1_str) + int(l2_str))

        res_head = res_node = ListNode(-1)
        if len(sum_num) > len(l1_str) and len(sum_num) > len(l2_str):
            res_node.next = ListNode(int(sum_num[0]))
            sum_num = sum_num[1:]
            res_node = res_node.next

        if len(l1_str) > len(l2_str):
            res_node.next = l1
            res_node = res_node.next

            while(res_node):
                res_node.val = int(sum_num[0])
                sum_num = sum_num[1:]
                res_node = res_node.next
        else:
            res_node.next = l2
            res_node = res_node.next

            while(res_node):
                res_node.val = int(sum_num[0])
                sum_num = sum_num[1:]
                res_node = res_node.next

        return res_head.next
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**

### **类似问题**
* [LeetCode 2. Add Two Numbers [Medium]](https://leetcode.com/problems/add-two-numbers/)
