## **114. Flatten Binary Tree to Linked List**

[LeetCode 114. Flatten Binary Tree to Linked List [Medium]](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/description/)

Given the `root` of a binary tree, flatten the tree into a "linked list":

* The "linked list" should use the same `TreeNode` class where the `right` child pointer points to the next node in the list and the `left` child pointer is always `null`.
* The "linked list" should be in the same order as a **pre-order traversal** of the binary tree.

```markdown
Input: root = [1,2,5,3,4,null,6]
Output: [1,null,2,null,3,null,4,null,5,null,6]
```

### **理解**
将一颗 `Binary Tree` 转换为 `LinkedList` 即将 `Binary Tree` 的 `left node` 按照 `pre-order traversal` 移到右侧 并将左边设为 `Null`

### **思路**
* **先将左右两个 `subtree` 作 `flatten` 然后寻找到左侧 `flatten` 好的 `subtree` 的最底部的 `node` 将 这个 `node` 和 右边的 `subtree` 的头部作连接 之后只需交换左右 `subtree` 位置 并将左侧设为 `Null`**

### **代码**

``` python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def flatten(self, root: Optional[TreeNode]) -> None:
        """
        Do not return anything, modify root in-place instead.
        """
        if root:
            self.flatten(root.left)
            self.flatten(root.right)

            bot_node = root.left
            if bot_node:
                while(bot_node.right):
                    bot_node = bot_node.right
                bot_node.right = root.right
                root.right = root.left
                root.left = None
```


### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(n)**
