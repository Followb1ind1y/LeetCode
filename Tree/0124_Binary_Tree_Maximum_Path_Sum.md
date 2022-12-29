## **124. Binary Tree Maximum Path Sum**

[LeetCode 124. Binary Tree Maximum Path Sum [Hard]](https://leetcode.com/problems/binary-tree-maximum-path-sum/description/)

A path in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence at most once. Note that the path does not need to pass through the root.

The path sum of a path is the sum of the node's values in the path.

Given the `root` of a binary tree, return the maximum path sum of any non-empty path.

```markdown
Input: root = [1,2,3]
Output: 6
Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.
```

### **理解**
计算一颗树的任意一条 path 合的最大值 不必须需要经过 root 单独一个 Node 也可以构成 path

### **思路**
* **分别计算 left 和 right subtree 中单条 path 的最大值 将 left right 和 node.val 的合储存 将 left 和 right 中较大的返回以供上一级判断**

### **代码**

``` python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        res = []
        self.find_max_path(root, res)
        return max(res)
    
    def find_max_path(self, root, res):
        if root:
            left_max = max(self.find_max_path(root.left, res), 0)
            right_max = max(self.find_max_path(root.right, res), 0)
            res.append(left_max + root.val + right_max)
            return max(left_max, right_max) + root.val
        else:
            return 0

```


### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(n)**