## **143. Reorder List**

[LeetCode 143. Reorder List [Medium]](https://leetcode.com/problems/reorder-list/description/)

You are given the head of a singly linked-list. The list can be represented as:

```markdown
L0 → L1 → … → Ln - 1 → Ln
```

Reorder the list to be on the following form:

```markdown
L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
```

You may not modify the values in the list's nodes. Only nodes themselves may be changed.

```markdown
Input: head = [1,2,3,4,5]
Output: [1,5,2,4,3]
```

### **理解**
 将一个 `LinkedList` 重新连接 最头和最尾相连 最尾和第二位相连 以此类推

### **思路**
* **首先将整个 `LinkedList` 过一遍 将每一个 `Node` 的地址保存在 `Stack` 中 之后再从头开始 从 `Stack` 中 `pop` 出尾部和尾部前的 `Node` 依次修改他们的 `next`**

### **代码**

``` python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        stack, left, track_head = [], head, head
        while(track_head):
            stack.append(track_head)
            track_head = track_head.next
        while(left and left.next):
            right, prev = stack.pop(), stack.pop()
            prev.next = None
            stack.append(prev)
            right.next = left.next
            left.next = right
            left = right.next
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**
