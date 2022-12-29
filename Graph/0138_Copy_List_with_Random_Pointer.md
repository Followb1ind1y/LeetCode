## **138. Copy List with Random Pointer**

[LeetCode 138. Copy List with Random Pointer [Medium]](https://leetcode.com/problems/copy-list-with-random-pointer/description/)

A linked list of length `n` is given such that each node contains an additional random pointer, which could point to any node in the list, or `null`.

Construct a **deep copy** of the list. The deep copy should consist of exactly `n` brand new nodes, where each new node has its value set to the value of its corresponding original node. Both the `next` and `random` pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. None of the pointers in the new list should point to nodes in the original list.

For example, if there are two nodes `X` and `Y` in the original list, where `X.random --> Y`, then for the corresponding two nodes `x` and `y` in the copied list, `x.random --> y`.

Return the head of the copied linked list.

The linked list is represented in the input/output as a list of `n` nodes. Each node is represented as a pair of `[val, random_index]` where:

* `val`: an integer representing `Node.val`
* `random_index`: the index of the node (range from `0` to `n-1`) that the `random` pointer points to, or `null` if it does not point to any node.

Your code will only be given the `head` of the original linked list.

```markdown
Input: head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
Output: [[7,null],[13,0],[11,4],[10,2],[1,0]]
```

### **理解**


### **思路**
* ****


### **代码**

``` python
"""
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
"""

class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        if not head:
            return None

        res_node = head_node = Node(-1)
        hashmap = {}

        while(head):
            if head not in hashmap:
                hashmap[head] = Node(head.val)
            head_node.next = hashmap[head]
            head_node = head_node.next

            if head.random:
                if head.random not in hashmap:
                    hashmap[head.random] = Node(head.random.val)
                head_node.random = hashmap[head.random]

            head = head.next

        return res_node.next
```

### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(n)**
