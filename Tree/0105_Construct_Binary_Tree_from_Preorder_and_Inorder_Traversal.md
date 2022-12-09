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
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        return self.build_tree(preorder, inorder)

    def build_tree(self, preorder, inorder):
        if preorder and inorder:
            i = inorder.index(preorder[0])
            sub_tree = TreeNode(preorder.pop(0))
            sub_tree.left = self.build_tree(preorder, inorder[:i])
            sub_tree.right = self.build_tree(preorder, inorder[i+1:])
            return sub_tree
        else:
            return None
```


### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**
