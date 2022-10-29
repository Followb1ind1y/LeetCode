## **23. Merge k Sorted Lists**

[LeetCode 23. Merge k Sorted Lists [Hard]](https://leetcode.com/problems/merge-k-sorted-lists/description/)

You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

```markdown
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6
```

### **思路**
* **将 Merge k Sorted Lists 问题转化为多个 Merge Two Sorted Lists 问题 将首尾的 `lists` 合并并存储在前面的位次 最终不算缩短 lists (e.g. `1, 2, 3, 4, 5 -> 15, 24, 3 -> 153, 24 -> 15324`)**
* **注意 `round()` 的特殊情况: 四舍五入至最接近的偶数 (e.g. `round(5/2) -> 2, round(7/2) -> 4`)**
* 可使用`ceil()` 于 rounding up 情况 (e.g. `ceil(5/2) -> 3, ceil(7/2) -> 4`) **
* 可使用`floor()` 于 rounding down 情况 (e.g. `floor(5/2) -> 2, floor(7/2) -> 3`) **

### **代码**

``` python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        merge_num = len(lists)
        if merge_num == 0: return None

        while(merge_num > 1):
            for i in range(merge_num // 2):
                lists[i] = self.mergeTwoLists(lists[i], lists[merge_num - 1 - i])
            merge_num = merge_num // 2 + merge_num % 2
        return lists[0]

    def mergeTwoLists(self, list1, list2):
            temp_node = temp_head = ListNode(-1)

            while(list1 and list2):
                if list1.val < list2.val:
                    temp_node.next = list1
                    list1 = list1.next
                else:
                    temp_node.next = list2
                    list2 = list2.next
                temp_node = temp_node.next
            if list1:
                temp_node.next = list1
            if list2:
                temp_node.next = list2

            return temp_head.next
```
### **复杂度分析**
* **时间复杂度：O(nlog(n))**
* **空间复杂度：O(n)**
