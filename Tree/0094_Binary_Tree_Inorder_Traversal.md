## **94. Binary Tree Inorder Traversal**

[LeetCode 94. Binary Tree Inorder Traversal [Easy]](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)

Given the `root` of a binary tree, return the inorder traversal of its nodes' values.

```markdown
Input: root = [1,null,2,3]
Output: [1,3,2]
```
<p align="center">
<img src="img/LeetCode0094_Preorder-from-Inorder-and-Postorder-traversals.jpg" width="500">
</p>

### **思路**
* **`Recursive` 解决方法即反复筛查左侧和右侧 并将结果直接加在 list上输出**
* **`Iterative` 方法则通过建立 `(node, visited)` 的格式存入 `Stack` (first in last out) 每一个 `val` 都会被经过两次 第一次为存入时 `visited = False` 第二次为录入时 `visited = True`**
* **`right` 将先被存入 `stack` 中 最后被取出结算 之后是当前 `node` 最上层放的是 `left` 从上到下依次完成 `tree` 的展开和录入过程 完成 Inorder Traversal**

<p align="center">
<img src="img/LeetCode0094_stack-operations.png" width="500">
</p>

### **代码**

**Recursive solution**

``` python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []
        else:
            return self.inorderTraversal(root.left) + [root.val] + self.inorderTraversal(root.right)
```

**Iterative solution**

``` python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res, stack = [], [(root, False)]

        while(stack):
            cur_node, visited = stack.pop()
            if cur_node:
                if visited:
                    res.append(cur_node.val)
                else:
                    stack.append((cur_node.right, False))
                    stack.append((cur_node, True))
                    stack.append((cur_node.left, False))

        return res
```

### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(n)**
