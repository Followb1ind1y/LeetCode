## **98. Validate Binary Search Tree**

[LeetCode 98. Validate Binary Search Tree [Medium]](https://leetcode.com/problems/validate-binary-search-tree/description/)

Given the `root` of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:

* The left **subtree** of a node contains only nodes with keys less than the node's key.
* The right subtree of a node contains only nodes with keys greater than the node's key.
* Both the left and right subtrees must also be binary search trees.

```markdown
Input: root = [2,1,3]
Output: true
```

```markdown
Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```

### **理解**
检查一个 `Binary Search Tree` 是否符合规则 判断规则为 `node` 左边的所以数字都比 `node.val` 小 `node` 右边的所以数字都比 `node.val` 大 并且每一个 `subtree` 符合 `Binary Search Tree` 的规则

### **思路**
* **为每一个 `node` 设置 `left` 和 `right` 两个约束条件 即 `node.val` 必须在 `left` 和 `right` 的区间内 若 `tree` 往左侧延伸则更新 `left` 取当前 `node` 的值和 `left` 中的最小值 因为上方 `node` 的约束条件对下方一样有效 所以只需要记录最小值即可 同理 若 `tree` 往右侧延伸则更新 `right` 取当前 `node` 的值和 `right` 中的最大值 通过不断对 `tree` 左右两侧进行更深入的 `DFs` `check` 完成全部的检测**


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
