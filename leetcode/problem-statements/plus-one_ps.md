# LeetCode: Plus One (Easy)

## Topics
- Array
- Math
- Data Structure

## Problem Statement

You are given a large integer represented as an integer array `digits`, where each `digits[i]` is the `ith` digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading 0's.

Increment the large integer by one and return the resulting array of digits.

### Example 1:

```
Input: digits = [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
Incrementing by one gives 123 + 1 = 124.
Thus, the result should be [1,2,4].
```

### Example 2:

```
Input: digits = [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
Incrementing by one gives 4321 + 1 = 4322.
Thus, the result should be [4,3,2,2].
```

### Example 3:

```
Input: digits = [9]
Output: [1,0]
Explanation: The array represents the integer 9.
Incrementing by one gives 9 + 1 = 10.
Thus, the result should be [1,0].
```

### Constraints:

- `1 <= digits.length <= 100`
- `0 <= digits[i] <= 9`
- The digits do not contain any leading 0's.

## Hints

1. Start with the rightmost digit and add 1 to it.
2. If there's a carry, continue to the next digit.
3. Be careful with the case where digits consist of all 9's (e.g., [9,9,9]).
4. Remember that you need to return an array of digits, not the actual integer.
5. Consider the case where the result has more digits than the input (like [9] -> [1,0]).

## Function Signature

```python
class Solution(object):
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
```