## LeetCode: Two Sum (Easy)

## Topics
- Array
- Hash Table
- Data Structure

### 1. Brute Force Approach

The most straightforward approach is to check all possible pairs of numbers in the array.

#### Time Complexity: O(n²)
#### Space Complexity: O(1)

```python
def twoSum(nums, target):
    n = len(nums)
    for i in range(n):
        for j in range(i + 1, n):
            if nums[i] + nums[j] == target:
                return [i, j]
    return []  # No solution found
```

### 2. Two-Pass Hash Table Approach

Build a hash map in the first pass, then look for complements in the second pass.

#### Time Complexity: O(n)
#### Space Complexity: O(n)

```python
def twoSum(nums, target):
    # Create a hash map to store numbers and their indices
    num_map = {}
    
    # First pass: Build the hash map
    for i, num in enumerate(nums):
        num_map[num] = i
    
    # Second pass: Check for complements
    for i, num in enumerate(nums):
        complement = target - num
        if complement in num_map and num_map[complement] != i:
            return [i, num_map[complement]]
    
    return []  # No solution found
```

### 3. One-Pass Hash Table Approach (Optimal)

We can combine the two passes into one by checking for the complement as we build the hash map.

#### Time Complexity: O(n)
#### Space Complexity: O(n)

```python
def twoSum(nums, target):
    # Create a hash map to store numbers and their indices
    num_map = {}
    
    # Iterate through the array
    for i, num in enumerate(nums):
        # Calculate the complement
        complement = target - num
        
        # Check if the complement exists in the hash map
        if complement in num_map:
            # Return the indices of the two numbers
            return [num_map[complement], i]
        
        # Add the current number and its index to the hash map
        num_map[num] = i
    
    return []  # No solution found
```


## Key Insights

1. **Hash Map Efficiency**: The hash map approach reduces the time complexity from O(n²) to O(n) by trading space for time.

2. **One-pass Solution**: We only need to go through the array once, checking for the complement as we go.

3. **Early Return**: As soon as we find a pair that sums to the target, we can return immediately, which can save time.

4. **Problem Understanding**: Remember that the problem guarantees exactly one solution, which simplifies our implementation.

## Common Mistakes

1. Returning the numbers instead of their indices.
2. Not checking if the complement exists before adding the current number to the hash map.
3. Using the same element twice (which is not allowed).

## Performance Comparison

The three solutions have different performance characteristics:

1. **Brute Force**: Simple but inefficient for large inputs (O(n²))
2. **Two-Pass Hash Table**: More efficient (O(n)) but requires two passes through the array
3. **One-Pass Hash Table**: Most efficient (O(n)) and requires only a single pass