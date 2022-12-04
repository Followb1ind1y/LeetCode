## **86. Partition List**

[LeetCode 86. Partition List [Medium]](https://leetcode.com/problems/partition-list/description/)

Given the `head` of a linked list and a value `x`, partition it such that all nodes less than `x` come before nodes greater than or equal to `x`.

You should preserve the original relative order of the nodes in each of the two partitions.

```markdown
Input: head = [1,4,3,2,5,2], x = 3
Output: [1,2,2,4,3,5]
```

### **理解**
 将一个 `LinkedList` 进行分区 使得所有小于 `x` 的数全部位于 大于等于 `x` 数的前面

### **思路**
* **创建两个新的 `LinkedList` 分别用来记录大于等于的数和小于的数并记录他们的 `head` 将全部 `LinkedList` 的数过一遍之后 将小于的 `LinkedList` 和 大于等于的 `LinkedList` 连接 得出最终结果

### **代码**

``` python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def partition(self, head: Optional[ListNode], x: int) -> Optional[ListNode]:
        res_node = ListNode(-1)
        large_node = large_head = ListNode(-1)
        small_node = small_head = ListNode(-1)
        res_node.next = head
        res_node = res_node.next

        while(res_node):
            if res_node.val < x:
                small_node.next = res_node
                small_node = small_node.next
            else:
                large_node.next = res_node
                large_node = large_node.next
            res_node = res_node.next

        small_node.next = large_head.next
        large_node.next = None

        return small_head.next
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(n)**
