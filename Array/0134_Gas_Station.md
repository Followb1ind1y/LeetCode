## **134. Gas Station**

[LeetCode 134. Gas Station [Hard]](https://leetcode.com/problems/gas-station/)

There are `n` gas stations along a circular route, where the amount of gas at the `ith` station is `gas[i]`.

You have a car with an unlimited gas tank and it costs `cost[i]` of gas to travel from the `ith` station to its next `(i + 1)th` station. You begin the journey with an empty tank at one of the gas stations.

Given two integer arrays `gas` and `cost`, return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return `-1`. If there exists a solution, it is guaranteed to be unique

```markdown
Input: gas = [1,2,3,4,5], cost = [3,4,5,1,2]
Output: 3
Explanation:
Start at station 3 (index 3) and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 4. Your tank = 4 - 1 + 5 = 8
Travel to station 0. Your tank = 8 - 2 + 1 = 7
Travel to station 1. Your tank = 7 - 3 + 2 = 6
Travel to station 2. Your tank = 6 - 4 + 3 = 5
Travel to station 3. The cost is 5. Your gas is just enough to travel back to station 3.
Therefore, return 3 as the starting index.
```
### **理解**
一辆汽车的油箱容量没有上限 给定长度为 n 的 gas 和 cost  两个 list 分别别代表了 n 个不同加油站可以加油的量 以及开至下一个加油站需要的油量 汽车可以从任意一个加油站出发 查看汽车能否在汽油耗尽前以顺时针完成循环 当有解时 只需考虑存在唯一解情况

### **思路**
* **因为只需考虑唯一解的情况 所以需要找到连续的 gas-cost > 0 的区间 并选择区间的第一点定为起始点 (e.g. gas = [1,2,3,4,5], cost = [3,4,5,1,2] -> index 3, 4 -> gas-cost > 0 若 index 4 能够完成循环 那 index 3 也必定可以完成 因为只需考虑唯一解情况 所以只需找到区间的第一点查看)**
* **当 cost 的总和大于 gas 的总和时 必不可能完成循环**

### **代码**

``` python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        if sum(gas) < sum(cost): return -1
        index, curr_gas = 0, 0
        for i in range(len(gas)):
            curr_gas += gas[i]
            if curr_gas < cost[i]:
                index = i + 1
                curr_gas = 0
                continue
            curr_gas -= cost[i]
        return index
```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**
