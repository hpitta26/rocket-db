# LeetCode: Search Insert Position (Easy)

## Topics
- Array
- Binary Search
- Algorithm

## Problem Statement

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with O(log n) runtime complexity.

### Example 1:

```
Input: nums = [1,3,5,7], target = 5
Output: 2
Explanation: Target 5 is found at index 2.
```

### Example 2:

```
Input: nums = [1,3,5,7], target = 2
Output: 1
Explanation: Target 2 is not found in the array. It would be inserted at index 1.
```

### Example 3:

```
Input: nums = [1,3,5,7], target = 8
Output: 4
Explanation: Target 8 is not found in the array. It would be inserted at index 4 (at the end of the array).
```

### Example 4:

```
Input: nums = [1,3,5,7], target = 0
Output: 0
Explanation: Target 0 is not found in the array. It would be inserted at index 0 (at the beginning of the array).
```

### Constraints:

- `1 <= nums.length <= 10^4`
- `-10^4 <= nums[i] <= 10^4`
- `nums` contains distinct values sorted in ascending order.
- `-10^4 <= target <= 10^4`

## Hints

1. Think about using binary search since the array is sorted.
2. Consider the case where the target does not exist in the array.
3. How can you modify a standard binary search algorithm to return the insertion position?
4. Remember that the position to insert is determined by how many elements are less than the target.
5. Handle the cases where the target should be inserted at the beginning or end of the array.

## Function Signature

```python
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
```