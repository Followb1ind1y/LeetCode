## **95. Unique Binary Search Trees II**

[LeetCode 95. Unique Binary Search Trees II [Medium]](https://leetcode.com/problems/unique-binary-search-trees-ii/description/)

Given an integer `n`, return all the structurally unique BST's (binary search trees), which has exactly `n` nodes of unique values from `1` to `n`. Return the answer in any order.

```markdown
Input: n = 3
Output: [[1,null,2,null,3],[1,null,3,2],[2,1,3],[3,1,null,null,2],[3,2,null,1]]
```
### **理解**
给定一个数字 `n` 找到所有由 `[1,n]` 数字组成的 `Binary Search Tree`

**Binary Search Tree** is a node-based binary tree data structure which has the following properties:

* The left subtree of a node contains only nodes with keys lesser than the node’s key.
* The right subtree of a node contains only nodes with keys greater than the node’s key.
* The left and right subtree each must also be a binary search tree.

<p align="center">
<img src="img/LeetCode0095_BSTSearch.png" width="300">
</p>

### **思路**
* **设置 start 和 end 两个起始值 将其中的每一个起始值作为 node.val 将剩下的数字传递到新的 function 中 分别寻找左右两侧的  subtree 并不断向下寻找直至为空**
* **注意: function 的 output 为 一个包含所有 subtree 的 list 通过对左右两个 subtree list 相互组合构建新的 tree 并保存到新的 list 中输出**
* **当 n 值变大后可能会出现 find_subtree(start, end) 重复的情况 即有相同 start end 的 function 被反复运算 可以利用 @cache 或者 @lru_cache 提升速度**


### **代码**

``` python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def generateTrees(self, n: int) -> List[Optional[TreeNode]]:
        return self.find_subtree(1, n)

    @cache          
    def find_subtree(self, start, end):
        res = []
        if start > end:
            return [None]

        for i in range(start, end + 1):
            left_subtree = self.find_subtree(start, i-1)
            right_subtree = self.find_subtree(i+1, end)

            for left in left_subtree:
                for right in right_subtree:
                    curr_node = TreeNode(i)
                    curr_node.left = left
                    curr_node.right = right
                    res.append(curr_node)
        return res
```

### **复杂度分析**
* **时间复杂度：O([Catalan(n)](https://en.wikipedia.org/wiki/Catalan_number))**
* **空间复杂度：O(n)**

### **类似问题**
* [LeetCode 96. Unique Binary Search Trees [Medium]](https://leetcode.com/problems/unique-binary-search-trees/description/)
