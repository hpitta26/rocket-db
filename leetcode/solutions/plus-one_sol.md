## LeetCode: Plus One (Easy)

## Topics
- Array
- Math
- Data Structure

### 1. Iterative Approach with Carry

The most intuitive approach is to start from the rightmost digit, add 1, and handle any carry that might propagate to the left.

#### Time Complexity: O(n)
#### Space Complexity: O(1) or O(n) if we count the output array

```python
class Solution(object):
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        n = len(digits)
        
        # Start from the rightmost digit
        for i in range(n - 1, -1, -1):
            # If the current digit is less than 9, we can simply increment it and return
            if digits[i] < 9:
                digits[i] += 1
                return digits
            
            # If the current digit is 9, set it to 0 and continue to the next digit
            digits[i] = 0
        
        # If we're here, it means all digits were 9, so we need to add a 1 at the beginning
        return [1] + digits
```

### 2. Recursive Approach

We can also solve this problem recursively, though it's less common and may not be as efficient in practice.

#### Time Complexity: O(n)
#### Space Complexity: O(n) due to recursive call stack

```python
class Solution(object):
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        def add_one(idx):
            # Base case: reached beyond the leftmost digit
            if idx < 0:
                digits.insert(0, 1)
                return digits
            
            # If current digit is less than 9
            if digits[idx] < 9:
                digits[idx] += 1
                return digits
            
            # If current digit is 9
            digits[idx] = 0
            return add_one(idx - 1)
        
        return add_one(len(digits) - 1)
```

### 3. Concise Pythonic Approach

Python allows for a more concise solution by converting the array to an integer, adding 1, and converting back to an array.

#### Time Complexity: O(n)
#### Space Complexity: O(n)

```python
class Solution(object):
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        # Convert array to integer, add 1, and convert back to array
        number = int(''.join(map(str, digits))) + 1
        return [int(digit) for digit in str(number)]
```

## Key Insights

1. **Handle Digits Individually**: The core of the solution is to handle each digit individually, starting from the least significant (rightmost) digit.

2. **Carry Propagation**: The main challenge is to correctly propagate carries when digits become 10 after adding 1.

3. **Edge Case - All 9's**: When all digits are 9 (e.g., [9,9,9]), adding 1 results in a number with one more digit (e.g., [1,0,0,0]).

4. **Early Return**: If there's no carry (any digit less than 9), we can return immediately after incrementing that digit.

5. **In-place Modification**: The first approach modifies the input array in-place, which is memory efficient.

## Common Mistakes

1. Not handling the case where all digits are 9, which requires a new digit at the beginning.
2. Incorrectly propagating the carry through the digits.
3. Using the Pythonic approach in languages with integer size limitations, which could cause overflow for very large numbers.
4. Forgetting that the digits are ordered from most to least significant (left to right).

## Performance Comparison

The three solutions have different characteristics:

1. **Iterative Approach**: Most efficient and straightforward, with clear logic and O(1) space complexity (excluding the output).
2. **Recursive Approach**: Elegant but less efficient due to call stack overhead.
3. **Pythonic Approach**: Concise but limited by integer size constraints in other languages and involves multiple conversions.

For most practical purposes, the iterative approach is recommended for its clarity and efficiency.