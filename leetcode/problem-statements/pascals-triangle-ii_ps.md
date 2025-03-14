# LeetCode: Pascal's Triangle II (Easy)

## Topics
- Array
- Dynamic Programming
- Math

## Problem Statement

Given an integer `rowIndex`, return the `rowIndex`th (0-indexed) row of Pascal's triangle.

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
Input: rowIndex = 3
Output: [1,3,3,1]
```

### Example 2:

```
Input: rowIndex = 0
Output: [1]
```

### Example 3:

```
Input: rowIndex = 1
Output: [1,1]
```

### Constraints:

- `0 <= rowIndex <= 33`

## Hints

1. Could you optimize your algorithm to use only O(rowIndex) extra space?
2. Notice that each element in a row is the sum of the elements above it to the left and to the right.
3. Think about calculating the elements from right to left in the row.
4. Remember that we only need to return the final row, not the entire triangle.
5. Consider the combinatorial formula for calculating elements in Pascal's triangle.

## Function Signature

```python
class Solution(object):
    def getRow(self, rowIndex):
        """
        :type rowIndex: int
        :rtype: List[int]
        """
```