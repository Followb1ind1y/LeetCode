## **146. LRU Cache**

[LeetCode 146. LRU Cache [Medium]](https://leetcode.com/problems/lru-cache/description/)

Design a data structure that follows the constraints of a **Least Recently Used (LRU) cache**.

Implement the `LRUCache` class:

* `LRUCache(int capacity)` Initialize the LRU cache with positive size `capacity`.
* `int get(int key)` Return the value of the `key` if the key exists, otherwise return `-1`.
* `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the `capacity` from this operation, evict the least recently used key.

The functions `get` and `put` must each run in `O(1)` average time complexity.

```markdown
Input
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
Output
[null, null, null, 1, null, -1, null, -1, 3, 4]

Explanation
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4
```

### **理解**
设计一个遵循 `Least Recently Used (LRU) cache` 约束的数据结构 当 `cache` 达到容量上限时 先删除最近使用最少的 `key-value pair` 其中 `capacity` 为容量上限 `int get(int key)` 返回 `key` 对应的 `value` 若没有则返回 `-1` `void put(int key, int value)` 更新 `cache` 中存储的的 `key-value pair`

### **思路**
* **创建一个 collections.OrderedDict() 的 cache 当使用 `int get(int key)` 时 将 `key-value pair` 先 pop 出后再放回 当使用 `void put(int key, int value)`  时 若 key 在 cache 出现过 则将 `key-value pair` 先 pop 出后再放回 若 key 没有出现过并容量到达上限 则 pop 出最近使用最少的 `key-value pair` 并将新的 `key-value pair` 放入**
* **注意：`collections.OrderedDict()` 是记忆条目添加顺序的 `Dict` 子类 使用 `.pop(key)` 输出 `key-value pair` 使用 `.popitem(last=True)` 按照 `LIFO order` 输出 使用 `.popitem(last=False)` 按照 `FIFO order` 输出**

### **代码**

``` python
class LRUCache:

    def __init__(self, capacity: int):
        self.capacity = capacity
        self.cache = collections.OrderedDict()
        
    def get(self, key: int) -> int:
        if key in self.cache:
            get_value = self.cache.pop(key)
            self.cache[key] = get_value
            return get_value
        else:
            return -1

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            self.cache.pop(key)
        else:
            if len(self.cache) >= self.capacity:
                self.cache.popitem(last=False)
                
        self.cache[key] = value

        
# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```
### **复杂度分析**
* **时间复杂度：O(1)**
* **空间复杂度：O(n)**
