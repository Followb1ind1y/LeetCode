## **133. Clone Graph**

[LeetCode 133. Clone Graph [Medium]](https://leetcode.com/problems/clone-graph/description/)

Given a reference of a node in a **connected** undirected graph.

Return a **deep copy** (clone) of the graph.

Each node in the graph contains a value (`int`) and a list (`List[Node]`) of its neighbors.

```markdown
class Node {
    public int val;
    public List<Node> neighbors;
}
```

Test case format:

For simplicity, each node's value is the same as the node's index (1-indexed). For example, the first node with `val == 1`, the second node with `val == 2`, and so on. The graph is represented in the test case using an adjacency list.

An adjacency list is a collection of unordered lists used to represent a finite graph. Each list describes the set of neighbors of a node in the graph.

The given node will always be the first node with `val = 1`. You must return the copy of the given node as a reference to the cloned graph.

```markdown
Input: adjList = [[2,4],[1,3],[2,4],[1,3]]
Output: [[2,4],[1,3],[2,4],[1,3]]
Explanation: There are 4 nodes in the graph.
1st node (val = 1)'s neighbors are 2nd node (val = 2) and 4th node (val = 4).
2nd node (val = 2)'s neighbors are 1st node (val = 1) and 3rd node (val = 3).
3rd node (val = 3)'s neighbors are 2nd node (val = 2) and 4th node (val = 4).
4th node (val = 4)'s neighbors are 1st node (val = 1) and 3rd node (val = 3).
```

### **理解**
给定一个 `Node` 制成的 `graph` 其结构为 `node.val` 是从 `1` 开始的 `index` `node.neighbors` 是保存与该 `node` 相邻的所有 `node` 的地址的 `list` 将这个 `graph` 作 `deep copy`

### **思路**
* **创建 `head_node` 和 `hashmap` 分别用来记录 头部和所有已经复制过的 `Node` 和其地址 之后依次寻找当前 `Node` 的 `neighbors` 如果没出现过则创建 并将他们不断 `append` 到新创建的 `Node.neighbors` `list` 中**


### **代码**

``` python
"""
# Definition for a Node.
class Node:
    def __init__(self, val = 0, neighbors = None):
        self.val = val
        self.neighbors = neighbors if neighbors is not None else []
"""

class Solution:
    def cloneGraph(self, node: 'Node') -> 'Node':
        if node:
            hashmap, head_node = {}, Node(node.val)
            hashmap[node.val] = head_node
            self.cloneNode(node, head_node, hashmap)
            return head_node
    
    def cloneNode(self, node, curr_node, hashmap):
        for i in range(len(node.neighbors)):
            if node.neighbors[i].val not in hashmap:
                new_node = Node(node.neighbors[i].val)
                hashmap[node.neighbors[i].val] = new_node
            if hashmap[node.neighbors[i].val] not in curr_node.neighbors:
                curr_node.neighbors.append(hashmap[node.neighbors[i].val])
                self.cloneNode(node.neighbors[i], hashmap[node.neighbors[i].val], hashmap)
```

### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(n)**
