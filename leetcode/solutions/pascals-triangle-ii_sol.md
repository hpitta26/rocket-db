## LeetCode: Pascal's Triangle II (Easy)

## Topics
- Array
- Dynamic Programming
- Math

### 1. Generate Full Triangle Approach

One approach is to generate the entire Pascal's triangle up to the desired row.

#### Time Complexity: O(rowIndex²)
#### Space Complexity: O(rowIndex²)

```python
class Solution(object):
    def getRow(self, rowIndex):
        """
        :type rowIndex: int
        :rtype: List[int]
        """
        # Initialize triangle with the first row
        triangle = [[1]]
        
        # Generate each row based on the previous row
        for row_num in range(1, rowIndex + 1):
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
        
        return triangle[rowIndex]
```

### 2. O(rowIndex) Space Approach

We can optimize space by only keeping track of the current row as we build it.

#### Time Complexity: O(rowIndex²)
#### Space Complexity: O(rowIndex)

```python
class Solution(object):
    def getRow(self, rowIndex):
        """
        :type rowIndex: int
        :rtype: List[int]
        """
        # Initialize with first element
        row = [1]
        
        # Generate each row
        for i in range(1, rowIndex + 1):
            # Create a new row starting with 1
            new_row = [1]
            
            # Calculate middle elements
            for j in range(1, i):
                new_row.append(row[j-1] + row[j])
            
            # End with 1
            new_row.append(1)
            
            # Update row for next iteration
            row = new_row
        
        return row
```

### 3. In-place Calculation (Optimal Space)

We can optimize further by updating the row in-place from right to left.

#### Time Complexity: O(rowIndex²)
#### Space Complexity: O(rowIndex)

```python
class Solution(object):
    def getRow(self, rowIndex):
        """
        :type rowIndex: int
        :rtype: List[int]
        """
        # Initialize row with all 1's
        row = [1] * (rowIndex + 1)
        
        # Generate the row
        for i in range(1, rowIndex + 1):
            # Update elements from right to left
            for j in range(i - 1, 0, -1):
                row[j] = row[j] + row[j-1]
        
        return row
```

### 4. Combinatorial Formula Approach

We can use the combinatorial formula: C(n,k) = n! / (k! * (n-k)!) to calculate each element.

#### Time Complexity: O(rowIndex)
#### Space Complexity: O(rowIndex)

```python
class Solution(object):
    def getRow(self, rowIndex):
        """
        :type rowIndex: int
        :rtype: List[int]
        """
        # Initialize result array
        result = [1]
        
        # Calculate using combinatorial formula
        for i in range(1, rowIndex + 1):
            # C(n,k) = C(n,k-1) * (n-k+1) / k
            next_val = result[i-1] * (rowIndex - i + 1) // i
            result.append(next_val)
        
        return result
```

## Key Insights

1. **Space Optimization**: The problem explicitly asks for O(rowIndex) space complexity, which is achieved by the 2nd, 3rd, and 4th approaches.

2. **In-place Updates**: By updating from right to left, we can avoid overwriting values we still need.

3. **Mathematical Shortcut**: Using the combinatorial formula allows us to calculate each value directly without needing previous rows.

4. **Pattern Observation**: In Pascal's triangle, each row starts and ends with 1, and each internal element is the sum of the two elements above it.

5. **Zero-indexing**: Note that the problem uses 0-indexing, so rowIndex = 3 refers to the 4th row (which is [1,3,3,1]).

## Common Mistakes

1. Forgetting about the 0-indexing specified in the problem.
2. Updating elements in the wrong order when trying to do in-place calculations.
3. Off-by-one errors when accessing elements from previous rows.
4. Overflow issues when dealing with large rowIndex values using factorial calculations.

## Performance Comparison

1. **Generate Full Triangle**: Simple but uses O(rowIndex²) space, which doesn't meet the problem's optimization request.
2. **O(rowIndex) Space**: More efficient space usage but still creates a new array in each iteration.
3. **In-place Calculation**: Optimal solution with O(rowIndex) space, updating values in-place without requiring additional arrays.
4. **Combinatorial Formula**: Mathematically elegant approach that also achieves O(rowIndex) space complexity.

For rowIndex <= 33 (as constrained by the problem), the in-place calculation (Approach 3) and combinatorial formula (Approach 4) are the most efficient in terms of both time and space complexity.