# LeetCode: Two Sum (Easy)

## Topics
- Array
- Hash Table
- Data Structure

## Problem Statement

Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

### Example 1:

```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

### Example 2:

```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

### Example 3:

```
Input: nums = [3,3], target = 6
Output: [0,1]
```

### Constraints:

- `2 <= nums.length <= 10^4`
- `-10^9 <= nums[i] <= 10^9`
- `-10^9 <= target <= 10^9`
- Only one valid answer exists.

## Hints

1. A really brute force way would be to search for all possible pairs of numbers but that would be too slow.
2. Can you optimize it to O(n log n) using a different data structure? Sort the array first?
3. A more optimal approach is to use a hash table to reduce the lookup time.
4. For each element, check if its complement (target - nums[i]) exists in the hash table.
5. If not, add the current element to the hash table for future lookups.