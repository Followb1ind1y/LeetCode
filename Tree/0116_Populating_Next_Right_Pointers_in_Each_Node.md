## **116. Populating Next Right Pointers in Each Node**

[LeetCode 116. Populating Next Right Pointers in Each Node [Medium]](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)

You are given a perfect binary tree where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

```markdown
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

```markdown
Input: root = [1,2,3,4,5,6,7]
Output: [1,#,2,3,#,4,5,6,7,#]
Explanation: Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```

### **理解**
一颗 `Binary Tree` 除了 left 和 right 两个 node 外 增加一个新的 Pointer next 将其指向树的同一层的右边的node

### **思路**
* **先将左右两个 `subtree` 连接 若当前 node 有 next 则需要将其 `subtree` 继续连接到 当前 node 的 next 的最左边 之后继续对 right 和 left  两个 `subtree` 作 Recursion**
* **注意: 在最后对 left 和 right 作 Recursion 时 最好将 right  放在前 因为是从左往右连接 右边必须先连接完成**

### **代码**

``` python
"""
# Definition for a Node.
class Node:
    def __init__(self, val: int = 0, left: 'Node' = None, right: 'Node' = None, next: 'Node' = None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""

class Solution:
    def connect(self, root: 'Optional[Node]') -> 'Optional[Node]':
        if root and root.left:
            root.left.next = root.right
            if root.next:
                root.right.next = root.next.left
            self.connect(root.right)
            self.connect(root.left)
        return root
```


### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**

### **类似问题**
*  [LeetCode 117. Populating Next Right Pointers in Each Node II [Medium]](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/)
