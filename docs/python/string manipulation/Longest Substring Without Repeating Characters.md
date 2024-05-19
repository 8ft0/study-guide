## HackerRank Challenge: Longest Substring Without Repeating Characters

### Problem Statement

Given a string \( S \), find the length of the longest substring without repeating characters.

### Input Format

- A single string \( S \) containing only ASCII characters. The length of \( S \) will not exceed 1000 characters.

### Output Format

- An integer representing the length of the longest substring without repeating characters.

### Constraints

- \( S \) will contain only ASCII characters.

### Example

#### Input
```
abcabcbb
```

#### Output
```
3
```

### Explanation

In the input string "abcabcbb":
- The longest substring without repeating characters is "abc", which has a length of 3.

### Function Signature
```python
def length_of_longest_substring(S: str) -> int:
    # Your code here
```

### Sample Input 1
```
bbbbb
```

### Sample Output 1
```
1
```

### Sample Input 2
```
pwwkew
```

### Sample Output 2
```
3
```

## Solution

Here's a solution in Python for the "Longest Substring Without Repeating Characters" problem:

```python
def length_of_longest_substring(S: str) -> int:
    char_index = {}
    longest = 0
    start = 0
    
    for i, char in enumerate(S):
        if char in char_index and char_index[char] >= start:
            start = char_index[char] + 1
        char_index[char] = i
        longest = max(longest, i - start + 1)
    
    return longest

# Test cases
assert length_of_longest_substring("abcabcbb") == 3
assert length_of_longest_substring("bbbbb") == 1
assert length_of_longest_substring("pwwkew") == 3
assert length_of_longest_substring("") == 0
assert length_of_longest_substring(" ") == 1
assert length_of_longest_substring("au") == 2
assert length_of_longest_substring("dvdf") == 3

print("All tests passed!")
```

### Explanation

1. **Track Characters**: Use a dictionary `char_index` to keep track of the last seen index of each character.
2. **Sliding Window**:
   - Use a sliding window approach with a `start` pointer to indicate the beginning of the current substring.
   - Iterate through the string with an `i` pointer.
   - If the character at `i` has been seen before and its last seen index is within the current window, move the `start` pointer to the right of the last seen index of that character.
3. **Update Longest Substring**: Calculate the length of the current substring (from `start` to `i`) and update the longest length if necessary.
4. **Return Result**: Return the length of the longest substring without repeating characters.

This solution efficiently finds the length of the longest substring without repeating characters using a sliding window and dictionary for tracking indices, ensuring optimal performance.