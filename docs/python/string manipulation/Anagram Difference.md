## HackerRank Challenge: Anagram Difference

### Problem Statement

You are given two strings, \( A \) and \( B \), both consisting of lowercase English letters. Your task is to determine the minimum number of character deletions required to make \( A \) and \( B \) anagrams of each other.

### Input Format

- Two strings \( A \) and \( B \), each containing only lowercase English letters. The length of each string will not exceed 1000 characters.

### Output Format

- An integer representing the minimum number of deletions required to make \( A \) and \( B \) anagrams.

### Constraints

- Both \( A \) and \( B \) will contain only lowercase English letters.

### Example

#### Input
```
A: cde
B: abc
```

#### Output
```
4
```

### Explanation

In the input strings:
- To make "cde" and "abc" anagrams, we need to delete:
  - 'c' from "cde"
  - 'd' and 'e' from "cde"
  - 'a' and 'b' from "abc"
- Total deletions = 4.

### Function Signature
```python
def make_anagram(A: str, B: str) -> int:
    # Your code here
```

### Sample Input 1
```
A: hello
B: billion
```

### Sample Output 1
```
6
```

### Sample Input 2
```
A: abc
B: cde
```

### Sample Output 2
```
4
```

## Solution

Here's a solution in Python for the "Anagram Difference" problem:

```python
from collections import Counter

def make_anagram(A: str, B: str) -> int:
    # Count the frequency of each character in both strings
    count_A = Counter(A)
    count_B = Counter(B)
    
    # Initialize the number of deletions required
    deletions = 0
    
    # Find the characters that need to be deleted from A
    for char in count_A:
        if char in count_B:
            deletions += abs(count_A[char] - count_B[char])
        else:
            deletions += count_A[char]
    
    # Find the characters that need to be deleted from B
    for char in count_B:
        if char not in count_A:
            deletions += count_B[char]
    
    return deletions

# Test cases
print(make_anagram("cde", "abc"))    # Output: 4
print(make_anagram("hello", "billion"))  # Output: 6
print(make_anagram("abc", "cde"))    # Output: 4
```

### Explanation

1. **Count Frequencies**: Use the `Counter` from the `collections` module to count the frequency of each character in both strings \( A \) and \( B \).
2. **Initialize Deletions**: Initialize a variable `deletions` to count the number of deletions required.
3. **Compare Frequencies**:
   - For each character in \( A \), check if it exists in \( B \):
     - If it exists, add the absolute difference of their counts to `deletions`.
     - If it doesn't exist, add the count of the character in \( A \) to `deletions`.
   - For each character in \( B \) that is not in \( A \), add the count of the character in \( B \) to `deletions`.
4. **Return Result**: Return the total count of deletions required.

This solution ensures that the minimum number of deletions needed to make the two strings anagrams of each other is correctly calculated.
