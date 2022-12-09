## **105. Construct Binary Tree from Preorder and Inorder Traversal**

[LeetCode 105. Construct Binary Tree from Preorder and Inorder Traversal [Medium]](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return the binary tree.

```markdown
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

### **理解**

<p align="center">
<img src="img/LeetCode0094_Preorder-from-Inorder-and-Postorder-traversals.jpg" width="500">
</p>

根据 `preorder` 和 `inorder` 的两个 `list` 还原 `binary tree`


### **思路**
* **`preorder` 的排列顺序为从最上面开始 依次从上往下从左到右排列 `inorder` 则以 `node` 为中心 将 `left` `right` 依次排在中心左右 可以根据 `preorder` 从上往下的特性不断选取中心点构建 `node` 并在 `inorder` 中找到中心点 并根据中心点将 `inorder` 分成左右两部分 继续构造 `subtree`**


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
        if preorder and inorder:
            i = inorder.index(preorder[0])
            sub_tree = TreeNode(preorder.pop(0))
            sub_tree.left = self.buildTree(preorder, inorder[:i])
            sub_tree.right = self.buildTree(preorder, inorder[i+1:])
            return sub_tree
        else:
            return None

```


### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(n)**
