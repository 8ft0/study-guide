# Challenge: Binary Search

#### Problem Statement

You are given a sorted list of integers and a target value. Your task is to implement a function that performs a binary search to find the index of the target value in the list. If the target value is not present in the list, return `-1`.

#### Function Signature

```python
def binary_search(arr: List[int], target: int) -> int:
    pass
```

#### Input

- `arr` (1 ≤ |arr| ≤ 10^5): A list of integers sorted in ascending order.
- `target` (−10^9 ≤ target ≤ 10^9): An integer target value to search for in the list.

#### Output

- Return the index of `target` in the list if it exists, otherwise return `-1`.

#### Example

```python
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
target = 5
result = binary_search(arr, target)
# result should be: 4

arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
target = 10
result = binary_search(arr, target)
# result should be: -1
```

#### Constraints

- The list is sorted in ascending order.
- The length of the list is between 1 and 100,000.

### Reference Solution

To solve this problem using binary search, we can follow these steps:

1. Initialize two pointers: `left` to the start of the list and `right` to the end of the list.
2. Calculate the middle index of the list.
3. Compare the middle element with the target value.
   - If the middle element is equal to the target, return the middle index.
   - If the middle element is less than the target, move the left pointer to `mid + 1`.
   - If the middle element is greater than the target, move the right pointer to `mid - 1`.
4. Repeat steps 2-3 until the target is found or the search space is exhausted (i.e., `left` exceeds `right`).
5. If the target is not found, return `-1`.

### Reference Solution Code

```python
from typing import List

def binary_search(arr: List[int], target: int) -> int:
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1

# Example usage
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
target = 5
print(binary_search(arr, target))  # Output: 4

target = 10
print(binary_search(arr, target))  # Output: -1
```

### Explanation

1. **Initialization**: Start with `left` at the beginning (index 0) and `right` at the end of the list (index `len(arr) - 1`).
2. **Middle Calculation**: Calculate the middle index as `(left + right) // 2`.
3. **Comparison**:
   - If the middle element equals the target, return the middle index.
   - If the middle element is less than the target, adjust `left` to `mid + 1` (search in the right half).
   - If the middle element is greater than the target, adjust `right` to `mid - 1` (search in the left half).
4. **Repeat**: Continue the process until `left` exceeds `right`.
5. **Not Found**: If the loop exits without finding the target, return `-1`.

Binary search is efficient with a time complexity of \(O(\log n)\), making it suitable for large input sizes up to 100,000 elements.