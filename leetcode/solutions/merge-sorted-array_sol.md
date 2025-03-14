## LeetCode: Merge Sorted Array (Easy)

## Topics
- Array
- Two Pointers
- Sorting

### 1. Naive Approach: Merge and Sort

A straightforward approach is to copy all elements from `nums2` into the end of `nums1` and then sort the entire array.

#### Time Complexity: O((m+n)log(m+n)) due to sorting
#### Space Complexity: O(1) or O(m+n) depending on the sorting algorithm

```python
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: None Do not return anything, modify nums1 in-place instead.
        """
        # Copy nums2 elements to the end of nums1
        for i in range(n):
            nums1[m + i] = nums2[i]
        
        # Sort the entire array
        nums1.sort()
```

### 2. Two Pointers (Start to End)

We can use two pointers to merge the arrays, but this approach requires additional space.

#### Time Complexity: O(m+n)
#### Space Complexity: O(m+n) for the temporary array

```python
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: None Do not return anything, modify nums1 in-place instead.
        """
        # Create a copy of the first m elements in nums1
        nums1_copy = nums1[:m]
        
        # Initialize pointers for nums1_copy and nums2
        p1 = 0
        p2 = 0
        
        # Merge elements from nums1_copy and nums2 into nums1
        for p in range(m + n):
            # If nums2 is exhausted or nums1_copy element is smaller
            if p2 >= n or (p1 < m and nums1_copy[p1] <= nums2[p2]):
                nums1[p] = nums1_copy[p1]
                p1 += 1
            else:
                nums1[p] = nums2[p2]
                p2 += 1
```

### 3. Two Pointers (End to Start) - Optimal

The most efficient approach is to fill `nums1` from the end, using the largest elements first.

#### Time Complexity: O(m+n)
#### Space Complexity: O(1)

```python
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: None Do not return anything, modify nums1 in-place instead.
        """
        # Initialize pointers for nums1 and nums2
        p1 = m - 1  # Pointer for the last element in nums1
        p2 = n - 1  # Pointer for the last element in nums2
        p = m + n - 1  # Pointer for the last position in the merged array
        
        # Merge from the end
        while p1 >= 0 and p2 >= 0:
            if nums1[p1] > nums2[p2]:
                nums1[p] = nums1[p1]
                p1 -= 1
            else:
                nums1[p] = nums2[p2]
                p2 -= 1
            p -= 1
        
        # If there are remaining elements in nums2, copy them
        # Note: no need to copy remaining elements from nums1 as they are already in place
        while p2 >= 0:
            nums1[p] = nums2[p2]
            p2 -= 1
            p -= 1
```

## Key Insights

1. **Work from the End**: The key insight is to merge the arrays from the end rather than the beginning. This allows us to fill `nums1` without overwriting elements that haven't been processed yet.

2. **In-place Modification**: The problem requires modifying `nums1` in-place, making the third approach ideal as it doesn't require extra space.

3. **Handling Remaining Elements**: After the main merge loop, we only need to check for remaining elements in `nums2`. Any remaining elements in `nums1` are already in their correct positions.

4. **Edge Cases**: The solution handles cases where one array might be empty or much shorter than the other.

## Common Mistakes

1. Trying to merge from the beginning without using extra space, which would overwrite elements in `nums1` that haven't been processed yet.
2. Forgetting to copy remaining elements from `nums2` when `nums1` is exhausted first.
3. Not handling edge cases properly, such as when either `m` or `n` is zero.
4. Returning a new array instead of modifying `nums1` in-place as required.

## Performance Comparison

The three solutions have different performance characteristics:

1. **Merge and Sort**: Simple but inefficient (O((m+n)log(m+n))) because it doesn't take advantage of the fact that the arrays are already sorted.
2. **Two Pointers (Start to End)**: More efficient (O(m+n)) but requires additional space (O(m)).
3. **Two Pointers (End to Start)**: Optimal solution with O(m+n) time complexity and O(1) space complexity, taking advantage of the extra space in `nums1`.

For most practical purposes, the third approach (end-to-start) is recommended for its efficiency and minimal space usage.