## **95. Unique Binary Search Trees II**

[LeetCode 95. Unique Binary Search Trees II [Medium]](https://leetcode.com/problems/unique-binary-search-trees-ii/description/)

Given an integer `n`, return all the structurally unique BST's (binary search trees), which has exactly `n` nodes of unique values from `1` to `n`. Return the answer in any order.

```markdown
Input: n = 3
Output: [[1,null,2,null,3],[1,null,3,2],[2,1,3],[3,1,null,null,2],[3,2,null,1]]
```

**Binary Search Tree** is a node-based binary tree data structure which has the following properties:

* The left subtree of a node contains only nodes with keys lesser than the node’s key.
* The right subtree of a node contains only nodes with keys greater than the node’s key.
* The left and right subtree each must also be a binary search tree.

<p align="center">
<img src="img/LeetCode0095_BSTSearch.png" width="300">
</p>

### **思路**
* ** **


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

```

### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(n)**
