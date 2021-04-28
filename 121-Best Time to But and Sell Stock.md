## Problem
You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

## Example
```bash
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
```

## Solution
**Dynamic programming**
![avatar](https://pic.leetcode-cn.com/4eaadab491f2bf88639d66c9d51bb0115e694ae08d637841ac18172b631cb21f-0121.gif)
```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        minPrice = int(1e9)
        maxProfit = 0
        for price in prices:
            minPrice = min(minPrice,price)
            maxProfit = max(price-minPrice,maxProfit)
            
        return maxProfit
```