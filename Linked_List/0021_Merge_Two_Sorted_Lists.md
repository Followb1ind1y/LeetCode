## **21. Merge Two Sorted Lists**

[LeetCode 21. Merge Two Sorted Lists [Easy]](https://leetcode.com/problems/merge-two-sorted-lists/)

You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the *head of the merged linked list*.

```markdown
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]
```

### **思路**
* **先 initial 一个空的 Linked List 用来存放 之后不断选择两个 Linked List 中 val 小的插入 直到一个 Linked List 为空 最后将没有空的另一个 Linked List 全部插入最终的 output 即可完成 Merge**

### **代码**

``` python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        prehead = ListNode(-1)
        prev = prehead

        while(list1 and list2):
            if list1.val <= list2.val:
                prev.next = list1
                list1 = list1.next
            else:
                prev.next = list2
                list2 = list2.next
            prev = prev.next
        if list1: prev.next = list1
        if list2: prev.next = list2

        return prehead.next
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(n)**
