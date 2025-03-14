## LeetCode: Best Time to Buy and Sell Stock (Easy)

## Topics
- Array
- Dynamic Programming
- Greedy

### 1. Brute Force Approach

The brute force approach considers every possible pair of buy and sell days.

#### Time Complexity: O(n²)
#### Space Complexity: O(1)

```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        max_profit = 0
        n = len(prices)
        
        for i in range(n):
            for j in range(i + 1, n):
                profit = prices[j] - prices[i]
                max_profit = max(max_profit, profit)
        
        return max_profit
```

However, this approach will exceed the time limit for large inputs.

### 2. One-Pass Solution (Optimal)

We can solve this in a single pass by keeping track of the minimum price so far and the maximum profit.

#### Time Complexity: O(n)
#### Space Complexity: O(1)

```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if not prices:
            return 0
        
        min_price = float('inf')
        max_profit = 0
        
        for price in prices:
            # Update minimum price seen so far
            min_price = min(min_price, price)
            
            # Calculate profit if we sell at current price
            current_profit = price - min_price
            
            # Update maximum profit if current profit is higher
            max_profit = max(max_profit, current_profit)
        
        return max_profit
```

### 3. Kadane's Algorithm Variation

This problem can also be viewed as finding the maximum subarray of price differences.

#### Time Complexity: O(n)
#### Space Complexity: O(1)

```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if not prices:
            return 0
        
        max_profit = 0
        max_current = 0
        
        # Calculate price differences
        for i in range(1, len(prices)):
            # Current price change
            price_change = prices[i] - prices[i-1]
            
            # Update current max profit ending at this position
            max_current = max(0, max_current + price_change)
            
            # Update global max profit
            max_profit = max(max_profit, max_current)
        
        return max_profit
```

### 4. Dynamic Programming Approach

We can formulate this as a dynamic programming problem.

#### Time Complexity: O(n)
#### Space Complexity: O(1)

```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if not prices:
            return 0
            
        # Initialize states
        # hold: maximum profit if we are holding a stock at the end of day i
        # cash: maximum profit if we have cash (no stock) at the end of day i
        hold = -float('inf')
        cash = 0
        
        for price in prices:
            # We can either keep our cash or sell the stock we're holding
            cash = max(cash, hold + price)
            
            # We can either keep the stock we're holding or buy a new one
            hold = max(hold, -price)  # -price because we're spending money
        
        # We want maximum profit with cash in hand (no stock)
        return cash
```

## Key Insights

1. **Single Transaction**: The problem asks for the maximum profit from a single buy-sell transaction.

2. **Buy Low, Sell High**: The optimal strategy is to buy at the lowest price and sell at the highest price afterward.

3. **Minimum Price Tracking**: By keeping track of the minimum price seen so far, we can easily calculate the potential profit for each day.

4. **No Profit Case**: If the prices are continuously decreasing, the best strategy is to not perform any transaction (profit = 0).

5. **Problem Variations**: This is the simplest version of stock trading problems. LeetCode has several variations with multiple buy-sell opportunities or transaction fees.

## Common Mistakes

1. Calculating profit by selling before buying (i.e., using a future minimum price).
2. Not handling the case where no profit is possible (should return 0).
3. Using excessive space by creating additional arrays when not needed.
4. Misunderstanding the problem as allowing multiple transactions.

## Performance Comparison

1. **Brute Force (O(n²))**: Simple but inefficient for large arrays, and will likely exceed time limits on LeetCode.
2. **One-Pass Solution (O(n))**: Optimal approach with minimal time and space complexity.
3. **Kadane's Algorithm Variation (O(n))**: Another optimal approach, viewing the problem as finding the maximum subarray of price differences.
4. **Dynamic Programming (O(n))**: Provides a framework that can be extended to more complex stock trading problems.

For this specific problem, the one-pass solution (Approach 2) is recommended for its simplicity and efficiency. It clearly captures the intuition of the problem by tracking the minimum price and maximum profit in a single pass.