## **149. Max Points on a Line**

[LeetCode 149. Max Points on a Line [Hard]](https://leetcode.com/problems/max-points-on-a-line/description/)

Given an array of `points` where `points[i] = [xi, yi]` represents a point on the X-Y plane, return the maximum number of points that lie on the same straight line.

```markdown
Input: points = [[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]
Output: 4
```

### **理解**
给定一些 `2D` 的点 找出在一条直线上最多的点的数量

### **思路**
* **从第一个点开始 单独创建该点位的 hashmap 记录他与其他点位的 slope 和对应点位的数量 在过完所有其他点位后更新最大值**
* **必须在每个 loop 开始时创建新的 hashmap 因为即便 slope 相同 点也有可能不在一条直线上(平行) 在每个 loop 开始时以出发点为依据创建 hashmap 可以解决这个问题**

### **代码**

``` python
class Solution:
    def maxPoints(self, points: List[List[int]]) -> int:
        res = 0
        if len(points) <= 2: return len(points)
        for i in range(len(points)-1):
            hashmap = {}
            for j in range(i+1, len(points)):
                slope = self.find_slope(points[i], points[j])
                if slope not in hashmap:
                    hashmap[slope] = 1
                else:
                    hashmap[slope] += 1
            res = max(res, max([n+1 for n in hashmap.values()]))

        return res
    
    def find_slope(self, p1, p2):
        if p1[1] - p2[1] == 0:
            return math.inf
        else:
            return (p1[0] - p2[0]) / (p1[1] - p2[1])
```

### **复杂度分析**
* **时间复杂度：O(n^2)**
* **空间复杂度：O(1)**
