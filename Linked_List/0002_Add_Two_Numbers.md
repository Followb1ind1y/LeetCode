## **2. Add Two Numbers**

[LeetCode 2. Add Two Numbers [Medium]](https://leetcode.com/problems/add-two-numbers/description/)

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

```markdown
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

### **理解**
两个 `LinkedList` 相加 储存规则为最低位储存在最开始 最高位在最底部 得出两个 `LinkedList` 相加结果  需要考虑进位情况

### **思路**
* **因为 `LinkedList` 储存规则为最低位储存在最开始 最高位在最底部 所以只需要从头开始相加即可 创建一个新的 `LinkedList` 用来记录相加的结果 另外创建一个 进位记录符号 carry**
* **只要  l1, l2 里还有数字或者 carry 为 1 都将计算数字 如果 l1 或者 l2 为 None 则记为 0 将 node_sum 除 10 的整数部分记为新的 carry 余数部分记录到储存的 `LinkedList` 中**

### **代码**

``` python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        carry = 0
        res_node = res_head = ListNode(-1)

        while(l1 or l2 or carry != 0):
            l1_val, l2_val = 0, 0
            if l1:
                l1_val = l1.val
                l1 = l1.next
            if l2:
                l2_val = l2.val
                l2 = l2.next
            node_sum = l1_val + l2_val + carry
            res_node.next = ListNode(node_sum % 10)
            res_node = res_node.next
            carry = node_sum // 10

        return res_head.next
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(n)**

### **类似问题**
* [LeetCode 445. Add Two Numbers II [Medium]](https://leetcode.com/problems/add-two-numbers-ii/description/)
