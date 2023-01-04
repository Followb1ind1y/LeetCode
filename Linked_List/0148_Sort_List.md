## **148. Sort List**

[LeetCode 148. Sort List [Medium]](https://leetcode.com/problems/sort-list/description/)

Given the `head` of a linked list, return the list after sorting it in ascending order.

**Follow up**: Can you sort the linked list in `O(n logn)` time and `O(1)` memory (i.e. constant space)?

```markdown
Input: head = [-1,5,3,4,0]
Output: [-1,0,3,4,5]
```

### **理解**
给定一个 `list` 将其以 `O(n logn)` 时间复杂度 and `O(1)` 空间复杂度进行排序

### **思路**
* **设置 `slow` `fast` 两个 `pointer` 将 `list` 不断对半分成两部分 然后继续在分割完的 `list` 上进行分割 直到只剩单独一个 `ListNode` (因为在 `Merge` 过程中需要 `SortedList` 单个 `ListNode` 一定是 `Sorted`)**
* **创建 `merge_two_sorted_list` 将 两个 `SortedList` 进行 `Merge` 输出一个排序好的 `ListNode`**
* **通过不断分割再重新组合构造 `SortedList` 之后再不断将  `SortedList` 进行快速合并**

### **代码**

``` python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head or not head.next: return head
        slow, fast = head, head.next
        while(fast.next and fast.next.next):
            slow = slow.next
            fast = fast.next.next
        fast = self.sortList(slow.next)
        slow.next = None
        slow = self.sortList(head)
        return self.merge_two_sorted_list(slow, fast)
        
    
    def merge_two_sorted_list(self, l1, l2):
        res_node = ListNode(-1)
        res_node.next = l1
        prev_head = res_node

        while(l1 and l2):
            if l1.val > l2.val:
                prev_head.next = l2
                l2 = l2.next
                prev_head = prev_head.next
                prev_head.next = l1
            else:
                prev_head, l1 = prev_head.next, l1.next
        if l2:
            prev_head.next = l2
        
        return res_node.next
```
### **复杂度分析**
* **时间复杂度：O(nlogn)**
* **空间复杂度：O(1)**
