## LeetCode: Remove Duplicates from Sorted Array (Easy)

## Topics
- Array
- Two Pointers
- Data Structure

### 1. Two Pointers Approach

The most efficient approach uses two pointers to modify the array in-place.

#### Time Complexity: O(n)
#### Space Complexity: O(1)

```python
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # Edge case: empty array
        if not nums:
            return 0
        
        # Initialize the pointer for the position to place the next unique element
        slow = 0
        
        # Iterate through the array using the fast pointer
        for fast in range(1, len(nums)):
            # If the current element is different from the previous unique element
            if nums[fast] != nums[slow]:
                # Move the slow pointer forward
                slow += 1
                # Place the unique element at the slow pointer position
                nums[slow] = nums[fast]
        
        # Return the number of unique elements (slow pointer position + 1)
        return slow + 1
```

### 2. Using a Set (Not In-Place)

This approach uses a set to identify unique elements, but doesn't fulfill the requirement of in-place modification.

#### Time Complexity: O(n)
#### Space Complexity: O(n)

```python
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # Create a set of unique elements
        unique_set = set(nums)
        
        # Sort the unique elements
        unique_list = sorted(list(unique_set))
        
        # Update the original array
        for i, val in enumerate(unique_list):
            nums[i] = val
        
        # Return the number of unique elements
        return len(unique_list)
```

### 3. Two Pointers With While Loop

Another implementation of the two-pointer approach using a while loop.

#### Time Complexity: O(n)
#### Space Complexity: O(1)

```python
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        
        n = len(nums)
        if n == 1:
            return 1
        
        # Initialize pointers
        i = 0  # Position to place the next unique element
        j = 1  # Scanning pointer
        
        while j < n:
            if nums[j] != nums[i]:
                i += 1
                nums[i] = nums[j]
            j += 1
        
        return i + 1
```

## Key Insights

1. **In-Place Modification**: The problem requires modifying the array in-place without using extra space (except for a few variables).

2. **Two Pointers Pattern**: This is a classic application of the two pointers technique, where one pointer keeps track of the position for the next unique element, and the other scans through the array.

3. **Sorted Array Advantage**: Since the array is already sorted, duplicates will be adjacent to each other, which simplifies our solution.

4. **Return Value**: The problem asks for the number of unique elements (k), not the modified array itself, though the array must be correctly modified for the first k positions.

## Common Mistakes

1. Creating a new array instead of modifying the original one in-place.
2. Not updating the array correctly, only returning the count of unique elements.
3. Shifting elements incorrectly, leading to loss of some unique values.
4. Incorrectly handling edge cases like empty arrays or arrays with a single element.

## Performance Comparison

The two pointers approach is clearly superior for this problem because:

1. It achieves O(1) space complexity, meeting the in-place requirement.
2. It makes a single pass through the array, resulting in O(n) time complexity.
3. It correctly maintains the relative order of elements as required.

The set-based approach, while conceptually simpler, uses O(n) extra space and does not meet the in-place requirement of the problem.