## **109. Convert Sorted List to Binary Search Tree**

[LeetCode 109. Convert Sorted List to Binary Search Tree [Medium]](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/)

Given the `head` of a singly linked list where elements are sorted in ascending order, convert it to a **height-balanced** binary search tree.

```markdown
Input: head = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: One possible answer is [0,-3,9,-10,null,5], which represents the shown height balanced BST.
```

### **理解**

**height-balanced:** A height-balanced binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

将一个 `Sorted LinkedList` 转换为一个平衡二叉树 (任一节点对应的两棵子树的最大高度差为 `1`)


### **思路**
* **大致思路为不断寻找中心点 将 `List` 分成左右两部分进行 `Recursion` 因为是 `LinkedList` 所以没法直接找到中心点 所以需要设置 `prev_node`, `center`, `next_node` 三个 `pointer` 分别用来记录头部, 中心和尾部 注意 `pointer `设置为指向头部, 中心和尾部位置 即它们的前一个位置**
* **过程中三个 `pointer` 都从 `head` 开始 `prev_node` 保持不变用来记录初始位置 `next_node` 作为标准不断移动 一次可以移动两个位置 当 `next_node` 成功移动两个位置时 `center` 移动一个位置 直到 `next_node` 到头为止 通过移动一个位置和移动两个位置的差值找到中心点 注意当 `next_node` 最多只能移动一个位置时 `center` 不发生移动**
* **之后只需要根据 `center` 创建 `TreeNode` 并将 分割好的左右两部分: `prev_node` 和 `center.next` 传递下去进行 `Recursion`**

### **代码**

``` python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sortedListToBST(self, head: Optional[ListNode]) -> Optional[TreeNode]:
        prev_node = center = next_node = ListNode(-1)
        center.next = head

        if next_node.next:
            while(next_node.next):
                next_node = next_node.next
                if next_node.next:
                    next_node = next_node.next
                    center = center.next

            center_point = center.next
            center.next = None

            node = TreeNode(center_point.val)
            node.left = self.sortedListToBST(prev_node.next)
            node.right = self.sortedListToBST(center_point.next)

            return node
```


### **复杂度分析**
* **时间复杂度：O(nlogn)**
* **空间复杂度：O(n)**
