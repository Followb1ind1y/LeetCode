## **24. Swap Nodes in Pairs**

[LeetCode 24. Swap Nodes in Pairs [Medium]](https://leetcode.com/problems/swap-nodes-in-pairs/description/)

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

```markdown
Input: head = [1,2,3,4]
Output: [2,1,4,3]
```

### **思路**
* **以两个为一组 通过 Recursion 不断交换前后两个数的位置**
* **指针指向 `ListNode`, 改变箭头则改变 `ListNode` 所指方向**
* **注意区分 `pointer` 和 `node.next` 通过画图的方式来解决问题**

### **代码**

``` python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        res_node = res_head = ListNode(-1)
        res_node.next = head

        while(res_node.next and res_node.next.next):
            after = res_node.next
            after_after = after.next
            res_node.next = after_after
            after.next = after_after.next
            after_after.next = after
            res_node = after

        return res_head.next
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(n)**
