# Cheet Sheet

<details>
  <summary>Python Arithmetic Operators</summary>
<div class="heatMap">

| Operator | Example |  Meaning |
| --- | --- | --- |
| `+` | 3 + 2 = 5 | Addition |
| `-` |	3 - 2 = 1 | Subtraction |
| `*` |	3 * 2 = 6 |	Multiplication |
| `/` |	3 / 2 = 1.5 | Division |
| `%` |	3 % 2 = 1 | Modulus |
| `**` | 3 ** 2 = 9 | Exponentiation |
| `//` | 5 // 2 = 2 | Floor division |
| `math.sqrt()` | math.sqrt(4) = 2 | Square root |
| `math.inf` | x = math.inf | Infinity |
</div>
</details>

<details>
  <summary>Python Bitwise Operators</summary>
<div class="heatMap">

| Operator | Example |  Meaning |
| --- | --- | --- |
| `&` | a & b | Bitwise AND |
| `｜` |	a ｜ b |	Bitwise OR |
| `^` |	a ^ b |	Bitwise XOR (exclusive OR) |
| `~` |	~a |	Bitwise NOT |
| `<<` |	a << n |	Bitwise left shift |
| `>>` |	a >> n |	Bitwise right shift |

</div>
</details>

<details>
  <summary>Collections</summary>

* **collections.Counter()**
``` python
from collections import Counter

hashmap = collections.Counter("hello") # Counter({'h': 1, 'e': 1, 'l': 2, 'o': 1})
hashmap['l'] # 2
```
* **collections.deque()**
``` python
from collections import deque

deq = collections.deque([1, 2, 3]) # deque([1, 2, 3])
deq.appendleft(5) # deque([5, 1, 2, 3])
deq.append(6) # deque([5, 1, 2, 3, 6])
deq.popleft() # -> 5
deq.pop() # -> 6
```

* **collections.defaultdict()**
``` python
from collections import defaultdict
s = 'mississippi'
d = collections.defaultdict(int) # defaultdict(int, {})
for k in s:
    d[k] += 1
d # defaultdict(int, {'m': 1, 'i': 4, 's': 4, 'p': 2})
d.items() # dict_items([('m', 1), ('i', 4), ('s', 4), ('p', 2)])
# --------------------------------------------------------------
s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]
d = collections.defaultdict(list) # defaultdict(list, {})
for k, v in s:
    d[k].append(v)
d # defaultdict(list, {'yellow': [1, 3], 'blue': [2, 4], 'red': [1]})
d.items() # dict_items([('yellow', [1, 3]), ('blue', [2, 4]), ('red', [1])])
```

* **collections.OrderedDict()**
``` python
from collections import OrderedDict

hashmap = collections.OrderedDict.fromkeys("hello") # OrderedDict([('h', None), ('e', None), ('l', None), ('o', None)])
hashmap.popitem(last=True) # Returned in LIFO order if last is True -> ('o', None)
hashmap.popitem(last=False) # Returned in FIFO order if last is False -> ('h', None)
```

</details>

<details>
  <summary>Binary Tree</summary>
<p align="center">
<img src="Tree/img/LeetCode0094_Preorder-from-Inorder-and-Postorder-traversals.jpg" width="500">
</p>
</details>