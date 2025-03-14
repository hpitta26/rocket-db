# LeetCode: Best Time to Buy and Sell Stock (Easy)

## Topics
- Array
- Dynamic Programming
- Greedy

## Problem Statement

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return `0`.

### Example 1:

```
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
```

### Example 2:

```
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.
```

### Constraints:

- `1 <= prices.length <= 10^5`
- `0 <= prices[i] <= 10^4`

## Hints

1. The points of interest are the peaks and valleys in the given graph.
2. Try to find the largest peak following the smallest valley.
3. You need to buy before you can sell, so keep track of the minimum price you've seen so far.
4. For each price, calculate the profit if you were to sell at that price after buying at the minimum price seen so far.
5. Remember that you can only make one transaction (one buy, one sell).

## Function Signature

```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
```