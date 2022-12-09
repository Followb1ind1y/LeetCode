## **105. Construct Binary Tree from Preorder and Inorder Traversal**

[LeetCode 105. Construct Binary Tree from Preorder and Inorder Traversal [Medium]](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return the binary tree.

```markdown
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

### **理解**


### **思路**
* ****


### **代码**

``` python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        return self.BST(root, math.inf, -math.inf)

    def BST(self, root, left, right):
        if root:
            if root.val < left and root.val > right:
                return self.BST(root.left, min(left, root.val), right) and self.BST(root.right, left, max(right, root.val))
            else:
                return False
        else:
            return True
```


### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**
