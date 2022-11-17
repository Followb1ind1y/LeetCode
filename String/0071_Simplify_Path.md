## **71. Simplify Path**

[LeetCode 71. Simplify Path [Medium]](https://leetcode.com/problems/simplify-path/description/)

Given a string `path`, which is an absolute path (starting with a slash `'/'`) to a file or directory in a Unix-style file system, convert it to the simplified canonical path.

In a Unix-style file system, a period `'.'` refers to the current directory, a double period `'..'` refers to the directory up a level, and any multiple consecutive slashes (i.e. `'//'`) are treated as a single slash `'/'`. For this problem, any other format of periods such as `'...'` are treated as file/directory names.

The **canonical path** should have the following format:

The path starts with a single slash `'/'`.
Any two directories are separated by a single slash `'/'`.
The path does not end with a trailing `'/'`.
The path only contains the directories on the path from the root directory to the target file or directory (i.e., no period `'.'` or double period `'..'`)
Return the simplified **canonical path**.

```markdown
Input: path = "/../"
Output: "/"
Explanation: Going one level up from the root directory is a no-op, as the root level is the highest level you can go.
```

```markdown
Input: path = "/home//foo/"
Output: "/home/foo"
Explanation: In the canonical path, multiple consecutive slashes are replaced by a single one.
```

### **思路**
* **首先通过 `.split('/')` 将原先的 `path` 去除 `/` 并分割为单独的 `str` 建立一个 `stack` (first in last out) 忽略字符串中的 `''` 和 `'.'` 当遇到 `'..'` 时需要返回上一级 即在 `stack` 中去除最顶部的 `str` 其余情况正常录入 `stack` 最后通过 ` "/".join()` 在各个字符间插入 `"/"` 输出结果**

### **代码**

``` python
class Solution:
    def simplifyPath(self, path: str) -> str:
        res = []
        path_split = path.split('/')

        for i in range(len(path_split)):
            if path_split[i] == '' or path_split[i] == '.':
                continue
            elif path_split[i] == '..':
                if res:
                    res.pop()
            else:
                res.append(path_split[i])

        return "/" + "/".join(res)
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(n)**
