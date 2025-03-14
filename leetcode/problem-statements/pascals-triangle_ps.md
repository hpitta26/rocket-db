# LeetCode: Pascal's Triangle (Easy)

## Topics
- Array
- Dynamic Programming
- Math

## Problem Statement

Given an integer `numRows`, return the first `numRows` of Pascal's triangle.

In Pascal's triangle, each number is the sum of the two numbers directly above it as shown:

```
    1
   1 1
  1 2 1
 1 3 3 1
1 4 6 4 1
```

### Example 1:

```
Input: numRows = 5
Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
```

### Example 2:

```
Input: numRows = 1
Output: [[1]]
```

### Constraints:

- `1 <= numRows <= 30`

## Hints

1. Think of each row as an array where we need to compute each element.
2. The first and last element of each row is always 1.
3. For other positions, the value is the sum of the two values directly above it from the previous row.
4. Use dynamic programming by building each row based on the previous row.
5. Consider how you can efficiently access the elements from the previous row to calculate the current row.

## Function Signature

```python
class Solution(object):
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """
```