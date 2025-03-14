## LeetCode: Pascal's Triangle (Easy)

## Topics
- Array
- Dynamic Programming
- Math

### 1. Iterative Approach (Row by Row)

The most straightforward approach is to build each row based on the previous row.

#### Time Complexity: O(numRows²)
#### Space Complexity: O(numRows²) for the output triangle

```python
class Solution(object):
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """
        # Initialize triangle with the first row
        triangle = [[1]]
        
        # Generate each row based on the previous row
        for row_num in range(1, numRows):
            # Start with 1
            row = [1]
            
            # Calculate the middle elements
            for j in range(1, row_num):
                # Each element is the sum of the two elements above it
                row.append(triangle[row_num-1][j-1] + triangle[row_num-1][j])
            
            # End with 1
            row.append(1)
            
            # Add the row to the triangle
            triangle.append(row)
        
        return triangle
```

### 2. Combinatorial Formula Approach

We can use the combinatorial formula for Pascal's triangle: `C(n,k) = n! / (k! * (n-k)!)`.

#### Time Complexity: O(numRows²)
#### Space Complexity: O(numRows²) for the output triangle

```python
class Solution(object):
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """
        triangle = []
        
        for row_num in range(numRows):
            # Create a new row
            row = []
            
            for k in range(row_num + 1):
                # Calculate C(row_num, k)
                if k == 0 or k == row_num:
                    row.append(1)
                else:
                    # Use the formula: C(n,k) = C(n,k-1) * (n-k+1) / k
                    value = row[k-1] * (row_num - k + 1) // k
                    row.append(value)
            
            triangle.append(row)
        
        return triangle
```

### 3. Memory-Optimized Approach

We can optimize memory usage by only keeping track of the current row as we build it.

#### Time Complexity: O(numRows²)
#### Space Complexity: O(numRows²) for the output triangle

```python
class Solution(object):
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """
        triangle = []
        
        for row_num in range(numRows):
            # Create a new row with all 1's
            row = [1] * (row_num + 1)
            
            # Fill in the middle elements
            for j in range(1, row_num):
                row[j] = triangle[row_num-1][j-1] + triangle[row_num-1][j]
            
            triangle.append(row)
        
        return triangle
```

## Key Insights

1. **Pattern Recognition**: Each element in Pascal's triangle is the sum of the two elements directly above it.

2. **Edge Elements**: The first and last element of each row is always 1.

3. **Dynamic Programming**: Each row depends only on the previous row, making this a classic dynamic programming problem.

4. **Symmetry**: Pascal's triangle is symmetric, so you could potentially optimize by calculating only half of each row and mirroring it.

5. **Mathematical Properties**: Pascal's triangle has many mathematical properties, including its relationship to combinations and binomial coefficients.

## Common Mistakes

1. Not handling the first and last elements of each row correctly (they should always be 1).
2. Incorrect indexing when accessing elements from the previous row.
3. Not initializing a new row for each iteration.
4. Forgetting that row indices start at 0 in the array representation.

## Performance Comparison

All three solutions have similar asymptotic time complexity of O(numRows²) since we need to generate all elements in the triangle:

1. **Iterative Approach**: Most intuitive and straightforward to understand.
2. **Combinatorial Formula Approach**: Potentially more efficient for larger values but may have numerical precision issues for very large inputs.
3. **Memory-Optimized Approach**: Slightly more efficient in terms of code execution as we pre-allocate the row with the correct size.

The space complexity for all approaches is O(numRows²) because we need to store all elements in the triangle, which is required by the problem statement.

For most purposes, the third approach (memory-optimized) strikes a good balance between readability and efficiency.