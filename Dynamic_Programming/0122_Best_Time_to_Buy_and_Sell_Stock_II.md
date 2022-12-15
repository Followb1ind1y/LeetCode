## **122. Best Time to Buy and Sell Stock II**

[LeetCode 122. Best Time to Buy and Sell Stock II [Medium]](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

On each day, you may decide to buy and/or sell the stock. You can only hold at most one share of the stock at any time. However, you can buy it then immediately sell it on the same day.

Find and return the maximum profit you can achieve.

```markdown
Input: prices = [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
Total profit is 4 + 3 = 7.
```

### **理解**
给定一个 `list` 代表不同日期的股票价格 一次最多持有一个 `share` 的股票 可以多次买卖 寻找可以获得的最大收入

### **思路**
* **寻找 `list` 从左到右方向的各个局部最小值和与其对应的局部最大值 并将它们的差累加到 `res` 输出**
* **记录当前的最大值和最小值 当出现下个数字小于最大值的情况时 记录差值 并重置最大最小值**


### **代码**

``` python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        res = 0
        local_min, local_max = prices[0], prices[0]

        for i in range(1, len(prices)):
            if prices[i] > local_max:
                local_max = prices[i]
            else:
                res += local_max - local_min
                local_min = local_max = prices[i]

        return res + local_max - local_min
```

### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(1)**

###  **类似问题**
* [LeetCode 121. Best Time to Buy and Sell Stock I [Medium]](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-i/)
* [LeetCode 123. Best Time to Buy and Sell Stock III [Medium]](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)
