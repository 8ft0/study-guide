# Intersection of Two Arrays

#### Problem Statement

Given two arrays, `nums1` and `nums2`, return an array of their intersection. Each element in the result must appear as many times as it shows in both arrays. The result can be in any order.

#### Function Signature

```python
def intersect(nums1: List[int], nums2: List[int]) -> List[int]:
    pass
```

#### Input

- `nums1` and `nums2` (1 ≤ |nums1|, |nums2| ≤ 1000): Two arrays of integers.

#### Output

- Return an array of integers representing the intersection of `nums1` and `nums2`.

#### Example

```python
nums1 = [1, 2, 2, 1]
nums2 = [2, 2]
result = intersect(nums1, nums2)
# result should be: [2, 2]

nums1 = [4, 9, 5]
nums2 = [9, 4, 9, 8, 4]
result = intersect(nums1, nums2)
# result should be: [4, 9] or [9, 4]
```

#### Constraints

- The intersection must include all duplicate values present in both arrays.
- The order of elements in the result does not matter.

### Reference Solution

To solve this problem, we can use a hashmap (dictionary) to count the occurrences of each element in one of the arrays, and then iterate through the other array to find common elements.

### Steps

1. Create a dictionary to count the occurrences of each element in `nums1`.
2. Iterate through `nums2` and check if the element exists in the dictionary with a count greater than 0.
3. If it exists, add the element to the result and decrement the count in the dictionary.

### Reference Solution Code

```python
from typing import List
from collections import Counter

def intersect(nums1: List[int], nums2: List[int]) -> List[int]:
    # Count the occurrences of each element in nums1
    counts = Counter(nums1)
    
    result = []
    
    # Iterate through nums2 and find common elements
    for num in nums2:
        if counts[num] > 0:
            result.append(num)
            counts[num] -= 1
    
    return result

# Example usage
nums1 = [1, 2, 2, 1]
nums2 = [2, 2]
print(intersect(nums1, nums2))  # Output: [2, 2]

nums1 = [4, 9, 5]
nums2 = [9, 4, 9, 8, 4]
print(intersect(nums1, nums2))  # Output: [4, 9] or [9, 4]
```

### Explanation

1. **Counting Elements in `nums1`**: We use `Counter` from the `collections` module to create a dictionary that counts the occurrences of each element in `nums1`.
2. **Finding Common Elements**: We iterate through `nums2`, and for each element, we check if it is present in the `counts` dictionary with a count greater than 0.
   - If it is, we append the element to the `result` list and decrement the count in the dictionary.
3. **Return Result**: The `result` list will contain the intersection of the two arrays, including duplicate elements as many times as they appear in both arrays.

This approach ensures that the solution is efficient, with a time complexity of \(O(n + m)\), where \(n\) and \(m\) are the lengths of `nums1` and `nums2`, respectively. This is due to the linear scans required for counting and finding intersections.