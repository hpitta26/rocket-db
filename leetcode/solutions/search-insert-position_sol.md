## LeetCode: Search Insert Position (Easy)

## Topics
- Array
- Binary Search
- Algorithm

### 1. Linear Search Approach

A straightforward but suboptimal approach is to iterate through the array until we find the target or a number greater than the target.

#### Time Complexity: O(n)
#### Space Complexity: O(1)

```python
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        for i in range(len(nums)):
            if nums[i] >= target:
                return i
        return len(nums)  # If we get here, target is greater than all elements
```

### 2. Binary Search Approach (Optimal)

Since the array is sorted, we can use binary search to find the position in O(log n) time.

#### Time Complexity: O(log n)
#### Space Complexity: O(1)

```python
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        left, right = 0, len(nums) - 1
        
        while left <= right:
            mid = (left + right) // 2
            
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
                
        return left  # Insertion point is at 'left'
```

### 3. Clean Binary Search Implementation

A more concise implementation that directly focuses on finding the correct insertion position.

#### Time Complexity: O(log n)
#### Space Complexity: O(1)

```python
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        left, right = 0, len(nums)
        
        while left < right:
            mid = (left + right) // 2
            
            if nums[mid] < target:
                left = mid + 1
            else:
                right = mid
                
        return left
```

## Key Insights

1. **Binary Search Advantage**: The binary search approach provides O(log n) time complexity, which is much more efficient than the linear O(n) approach for large inputs.

2. **Insertion Point**: The key insight is that after binary search ends, the 'left' pointer points to the correct insertion position, whether the target is found or not.

3. **Boundary Cases**: The algorithm handles all boundary cases naturally:
   - Target found in the array
   - Target should be inserted at the beginning
   - Target should be inserted at the end
   - Target should be inserted somewhere in the middle

4. **Early Termination**: In the second approach, we return immediately if we find the exact match. However, this is not necessary for correctness.

## Common Mistakes

1. Not handling the case where the target is larger than all elements in the array.
2. Incorrect calculation of the middle index (potential integer overflow in some languages).
3. Improper handling of the boundaries in the binary search algorithm.
4. Returning 'right + 1' instead of 'left' after the loop terminates.

## Performance Comparison

The two solutions have different performance characteristics:

1. **Linear Search**: Simple but inefficient for large inputs (O(n))
2. **Binary Search**: More efficient (O(log n)) and is the recommended approach given the constraint in the problem statement

For a sorted array with 1,000,000 elements, binary search would need at most ~20 comparisons, while linear search could require up to 1,000,000 comparisons in the worst case.