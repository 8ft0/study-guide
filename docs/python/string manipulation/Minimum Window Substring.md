## Coding Challenge: Minimum Window Substring

### Problem Statement

Given two strings \( S \) and \( T \), find the minimum window in \( S \) which will contain all the characters in \( T \) in complexity \( O(n) \).

### Input Format

- Two strings \( S \) and \( T \) containing only ASCII characters. The length of \( S \) will not exceed 1000 characters. The length of \( T \) will not exceed 100 characters.

### Output Format

- A single string representing the minimum window in \( S \) which contains all the characters in \( T \). If no such window exists, return an empty string.

### Constraints

- \( S \) and \( T \) will contain only ASCII characters.
- All characters in \( T \) are guaranteed to be unique.

### Example

#### Input
```
S: ADOBECODEBANC
T: ABC
```

#### Output
```
BANC
```

### Explanation

In the input strings:
- The minimum window substring of "ADOBECODEBANC" that contains all characters of "ABC" is "BANC".

### Function Signature
```python
def min_window(S: str, T: str) -> str:
    # Your code here
```

### Sample Input 1
```
S: A
T: AA
```

### Sample Output 1
```
""
```

### Sample Input 2
```
S: A
T: A
```

### Sample Output 2
```
A
```

## Solution

Here's a solution in Python for the "Minimum Window Substring" problem:

```python
from collections import Counter

def min_window(S: str, T: str) -> str:
    if not S or not T:
        return ""
    
    t_count = Counter(T)
    current_count = Counter()
    
    start = 0
    min_length = float('inf')
    min_window_start = 0
    have, need = 0, len(t_count)
    
    for end in range(len(S)):
        char = S[end]
        current_count[char] += 1
        
        if char in t_count and current_count[char] == t_count[char]:
            have += 1
        
        while have == need:
            if (end - start + 1) < min_length:
                min_length = end - start + 1
                min_window_start = start
            
            current_count[S[start]] -= 1
            if S[start] in t_count and current_count[S[start]] < t_count[S[start]]:
                have -= 1
            start += 1
    
    if min_length == float('inf'):
        return ""
    else:
        return S[min_window_start:min_window_start + min_length]

# Test cases
assert min_window("ADOBECODEBANC", "ABC") == "BANC"
assert min_window("A", "AA") == ""
assert min_window("A", "A") == "A"
assert min_window("aa", "aa") == "aa"
assert min_window("a", "b") == ""

print("All tests passed!")
```

### Explanation

1. **Character Count**: Use a `Counter` to count the characters in \( T \) (`t_count`).
2. **Sliding Window**:
   - Use two pointers (`start` and `end`) to represent the sliding window.
   - Maintain a `current_count` counter to track characters in the current window.
3. **Expand Window**: Expand the window by moving the `end` pointer and updating `current_count`.
4. **Contract Window**: When all characters from \( T \) are included in the current window (i.e., `have == need`):
   - Update the minimum window size if the current window is smaller.
   - Move the `start` pointer to the right to find a smaller valid window.
5. **Check Validity**: If the current character at `start` is part of \( T \) and its count in `current_count` falls below the required count, decrement `have`.
6. **Return Result**: After the loop, if `min_length` is still infinity, return an empty string. Otherwise, return the minimum window substring.

This solution ensures optimal performance using a sliding window approach and counters for efficient character counting.

