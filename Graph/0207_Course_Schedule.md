## **207. Course Schedule**

[LeetCode 207. Course Schedule [Medium]](https://leetcode.com/problems/course-schedule/description/)

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you must take course `bi` first if you want to take course `ai`.

* For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.

```markdown
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
```

```markdown
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
```

### **理解**
给定一个 `list` 包含 `Course` 以及其对应的 `prerequisite course` 检查是否能够完成所有课程 即检查是否有相互矛盾的情况 (存在 `Circle`)

### **思路**
* **先创建两个 `list` 分别用来记录对应 `index` `course` 的 `prerequisite course` 和 检查情况**
* **用 `0` 表示 `course` 还没有被检查过是否存在 `circle` 用 `1` 表示已经检查完毕 用 `-1` 表示正在检查 当发现 `-1` 的 `course` 被检查两次 即出现了 `circle`**
* **如果该 `course` 所有的 `prerequisite` 都被检查过 则将其标注为 `1`**

### **代码**

``` python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        pre_list, check_list = [[] for _ in range(numCourses)], [0] * numCourses
        for i in range(len(prerequisites)):
            pre_list[prerequisites[i][0]].append(prerequisites[i][1])
        for i in range(numCourses):
            if not self.check_pre(i, pre_list, check_list):
                return False
        return True

    def check_pre(self, course, pre_list, check_list):
        if check_list[course] == 1:
            return True
        elif check_list[course] == -1:
            return False
        else:
            check_list[course] = -1
            for i in range(len(pre_list[course])):
                if not self.check_pre(pre_list[course][i], pre_list, check_list):
                    return False
            check_list[course] = 1
            return True
```

### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(n)**
