## **206. Reverse Linked List**

[LeetCode 206. Reverse Linked List [Easy]](https://leetcode.com/problems/reverse-linked-list/description/)

Given the head of a singly linked list, reverse the list, and return the reversed list.

```markdown
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
```

###  **理解**

将一个 `LinkedList` 倒转过来

### **思路**
* **设置两个指针分别记录当前位置和前一个位置 从头开始 更新当前指针位置的 `next` 至 前一个位置 并更新地址**
* **不能以普通 `Array` 思路做 `LinkedList` 题目 时刻记得需要保留的地址 分步解决问题 不能看的太往后**

### **代码**

``` python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head == None or head.next == None: return head
        prev_Node, head_Node = ListNode(0).next, head

        while(head_Node):
            next_node = head_Node.next
            head_Node.next = prev_Node
            prev_Node = head_Node
            head_Node = next_node

        return prev_Node
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**
