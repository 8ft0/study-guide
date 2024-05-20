# Puzzle 9 (Algorithm)

#### Problem Statement

You are given a 3x3 grid of numbers. Your task is to find the missing number (represented as `0`) such that the sum of the numbers in each row, column, and both diagonals equals the same value. This puzzle is known as a "magic square."

#### Function Signature

```python
def solve_magic_square(grid: List[List[int]]) -> int:
    pass
```

#### Input

- `grid`: A 3x3 list of integers where one cell contains `0`, representing the missing number.

#### Output

- Return the value of the missing number that makes the grid a magic square.

#### Example

```python
grid = [
    [8, 1, 6],
    [3, 0, 7],
    [4, 9, 2]
]

result = solve_magic_square(grid)
# result should be: 5
```

#### Constraints

- The grid will always be a 3x3 grid.
- Exactly one cell in the grid will be `0`.

### Reference Solution

To solve this problem, we need to understand the properties of a magic square:
- The sum of the numbers in each row, column, and both diagonals must be the same.
- For a 3x3 magic square using numbers 1 to 9, this sum is always 15.

Here's the step-by-step approach to solve this:

1. Calculate the expected sum of each row, column, and diagonal, which is 15.
2. Find the row, column, and both diagonals that contain the missing number `0`.
3. Calculate the actual sums of the row, column, and diagonals where `0` is located.
4. Determine the missing number by comparing the actual sums to the expected sum (15).

### Reference Solution Code

```python
from typing import List

def solve_magic_square(grid: List[List[int]]) -> int:
    n = 3
    expected_sum = 15
    
    row, col = -1, -1
    for i in range(n):
        for j in range(n):
            if grid[i][j] == 0:
                row, col = i, j
                break
        if row != -1:
            break
    
    row_sum = sum(grid[row])
    col_sum = sum(grid[i][col] for i in range(n))
    
    diag1_sum = sum(grid[i][i] for i in range(n)) if row == col else expected_sum
    diag2_sum = sum(grid[i][n - 1 - i] for i in range(n)) if row == n - 1 - col else expected_sum
    
    missing_number = expected_sum - row_sum + grid[row][col]
    
    return missing_number

# Example usage
grid = [
    [8, 1, 6],
    [3, 0, 7],
    [4, 9, 2]
]

print(solve_magic_square(grid))  # Output: 5
```

### Explanation

1. **Identify the Position of `0`**: Iterate through the grid to find the position `(row, col)` of the missing number.
2. **Calculate Row and Column Sums**: Compute the sum of the elements in the row and column containing `0`.
3. **Calculate Diagonal Sums**: Check if `0` is part of either diagonal. If it is, compute the diagonal sums.
4. **Determine Missing Number**: The missing number is the difference between the expected sum (15) and the actual sum of the row (or column, since both must be the same in a magic square).

This approach ensures that the grid becomes a magic square by correctly computing the missing number.

---

## Another Version

#### Problem Statement

You are given a 3x3 grid where each cell contains an integer from 1 to 9 or the value 0, which represents a missing number. The grid is supposed to be a magic square when the missing number is filled in. Your task is to find the missing number so that the sum of the numbers in each row, column, and both diagonals equals the same value.

#### Function Signature

```python
def solve_magic_square(grid: List[List[int]]) -> int:
    pass
```

#### Input

- `grid`: A 3x3 list of integers where one cell contains `0`, representing the missing number.

#### Output

- Return the value of the missing number that makes the grid a magic square.

#### Example

```python
grid = [
    [8, 1, 6],
    [3, 0, 7],
    [4, 9, 2]
]

result = solve_magic_square(grid)
# result should be: 5
```

#### Constraints

- The grid will always be a 3x3 grid.
- Exactly one cell in the grid will be `0`.

### Reference Solution

To solve this problem, we need to ensure that the sum of the numbers in each row, column, and diagonal is equal. For a 3x3 magic square, this sum is always 15.

### Step-by-Step Approach

1. Calculate the sum of the numbers in each row, column, and diagonal.
2. Find the row, column, and diagonal where the missing number (0) is located.
3. Calculate the actual sums of the row, column, and diagonals where 0 is located.
4. Determine the missing number by comparing the actual sums to the expected sum (15).

### Reference Solution Code

```python
from typing import List

def solve_magic_square(grid: List[List[int]]) -> int:
    n = 3
    expected_sum = 15
    
    # Find the position of the missing number (0)
    row, col = -1, -1
    for i in range(n):
        for j in range(n):
            if grid[i][j] == 0:
                row, col = i, j
                break
        if row != -1:
            break
    
    # Calculate the sum of the row, column, and diagonals containing the missing number
    row_sum = sum(grid[row])
    col_sum = sum(grid[i][col] for i in range(n))
    
    diag1_sum = sum(grid[i][i] for i in range(n)) if row == col else expected_sum
    diag2_sum = sum(grid[i][n - 1 - i] for i in range(n)) if row == n - 1 - col else expected_sum
    
    # The missing number should balance the sums to reach the expected sum
    if row == col:
        missing_number = expected_sum - diag1_sum + 0
    elif row == n - 1 - col:
        missing_number = expected_sum - diag2_sum + 0
    else:
        missing_number = expected_sum - row_sum + 0
    
    # Return the missing number
    return missing_number

# Example usage
grid = [
    [8, 1, 6],
    [3, 0, 7],
    [4, 9, 2]
]

print(solve_magic_square(grid))  # Output: 5
```

### Explanation

1. **Identify the Position of `0`**: Iterate through the grid to find the position `(row, col)` of the missing number.
2. **Calculate Row and Column Sums**: Compute the sum of the elements in the row and column containing `0`.
3. **Calculate Diagonal Sums**: Check if `0` is part of either diagonal. If it is, compute the diagonal sums.
4. **Determine Missing Number**: The missing number is the difference between the expected sum (15) and the actual sum of the row (or column, or diagonal) where `0` is located.

By ensuring that all rows, columns, and diagonals sum up to the expected value (15), the function correctly finds the missing number that turns the grid into a magic square.

---


## Simple Solution

Certainly! Below is a Python solution implementing the streamlined approach of summing the visible numbers in the grid and subtracting from 45 to find the missing number. This method takes advantage of the specific characteristics of a 3x3 magic square where the numbers 1 through 9 are used exactly once.


```python
from typing import List

def solve_magic_square(grid: List[List[int]]) -> int:
    total_sum = 45  # Sum of numbers 1 through 9
    current_sum = 0  # Variable to hold the sum of the numbers in the grid

    # Iterate through each cell in the grid
    for row in grid:
        for num in row:
            current_sum += num  # Add each number to current_sum

    # The missing number is the difference between total_sum and current_sum
    missing_number = total_sum - current_sum

    return missing_number

# Example usage
grid = [
    [8, 1, 6],
    [3, 0, 7],
    [4, 9, 2]
]

print(solve_magic_square(grid))  # Output should be 5
```

### Explanation of the Code

1. **Initialize Constants and Variables**:
    - `total_sum` is set to 45, the sum of numbers from 1 to 9.
    - `current_sum` is initialized to 0 to accumulate the sum of the visible numbers in the grid.

2. **Loop Through the Grid**:
    - Two nested loops iterate through each cell in the 3x3 grid.
    - Each number found is added to `current_sum`.

3. **Calculate the Missing Number**:
    - Subtract `current_sum` from `total_sum` to find the missing number.
    - Return the missing number.

This simple Python function efficiently calculates the missing number using basic arithmetic, making it highly efficient for solving this type of magic square puzzle.

## Simpler

Yes, Python provides concise ways to sum all the numbers in a matrix. One common approach is to use list comprehension along with the `sum()` function. Here's how you can sum all the numbers in a matrix using this approach:

```python
def sum_matrix(matrix: List[List[int]]) -> int:
    return sum(sum(row) for row in matrix)
```

In this code:
- `sum(row) for row in matrix` iterates through each row in the matrix and calculates the sum of each row.
- The outer `sum()` function then adds up these row sums to get the total sum of all the numbers in the matrix.

This method is concise and Pythonic, making it a simple and elegant solution for summing all the numbers in a matrix.