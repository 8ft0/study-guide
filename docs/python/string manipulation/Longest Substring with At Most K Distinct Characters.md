# Longest Substring with At Most K Distinct Characters

### Problem Statement

Given a string \( S \) and an integer \( K \), find the length of the longest substring that contains at most \( K \) distinct characters.

### Input Format

- A single string \( S \) containing only ASCII characters. The length of \( S \) will not exceed 1000 characters.
- An integer \( K \) (1 \leq K \leq 100).

### Output Format

- An integer representing the length of the longest substring that contains at most \( K \) distinct characters.

### Constraints

- \( S \) will contain only ASCII characters.
- \( K \) will be at least 1 and at most the length of \( S \).

### Example

Input 
```
S: "eceba"
K: 2
```

Output 
```
3
```

### Explanation

In the input string "eceba" with \( K = 2 \):
- The longest substring with at most 2 distinct characters is "ece", which has a length of 3.

### Function Signature
```python
def length_of_longest_substring_k_distinct(S: str, K: int) -> int:
    # Your code here
```

Sample Input 1
```
S: "aa"
K: 1
```

Sample Output 1
```
2
```

Sample Input 2
```
S: "a"
K: 1
```

Sample Output 2
```
1
```

## Solution

Here's a solution in Python for the "Longest Substring with At Most K Distinct Characters" problem:

```python
from collections import defaultdict

def length_of_longest_substring_k_distinct(S: str, K: int) -> int:
    if K == 0 or not S:
        return 0

    char_count = defaultdict(int)
    start = 0
    max_length = 0

    for end in range(len(S)):
        char_count[S[end]] += 1
        
        while len(char_count) > K:
            char_count[S[start]] -= 1
            if char_count[S[start]] == 0:
                del char_count[S[start]]
            start += 1
        
        max_length = max(max_length, end - start + 1)

    return max_length

# Test cases
assert length_of_longest_substring_k_distinct("eceba", 2) == 3
assert length_of_longest_substring_k_distinct("aa", 1) == 2
assert length_of_longest_substring_k_distinct("a", 1) == 1
assert length_of_longest_substring_k_distinct("abaccc", 2) == 4
assert length_of_longest_substring_k_distinct("aabbcc", 1) == 2
assert length_of_longest_substring_k_distinct("aabbcc", 3) == 6

print("All tests passed!")
```

### Explanation

1. **Character Count**: Use a `defaultdict` to count the frequency of characters in the current window.
2. **Sliding Window**:
   - Use two pointers (`start` and `end`) to represent the sliding window.
   - Expand the window by moving the `end` pointer and updating `char_count`.
3. **Maintain Window**: If the number of distinct characters in the current window exceeds \( K \), move the `start` pointer to the right until the window has at most \( K \) distinct characters, updating `char_count` accordingly.
4. **Update Maximum Length**: Track the maximum length of the window that satisfies the condition of having at most \( K \) distinct characters.
5. **Return Result**: Return the maximum length found during the process.

This solution efficiently finds the length of the longest substring with at most \( K \) distinct characters using a sliding window approach and a dictionary for tracking character frequencies.