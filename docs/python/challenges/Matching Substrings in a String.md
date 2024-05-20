# Matching Substrings in a String

#### Problem Statement

You are given a string `s` and a list of substrings `patterns`. Your task is to implement a function that finds all occurrences of each substring in `patterns` within the string `s`. For each pattern, return a list of starting indices where the pattern is found in `s`. If a pattern is not found, return an empty list for that pattern.

#### Function Signature

```python
def find_substring_occurrences(s: str, patterns: List[str]) -> Dict[str, List[int]]:
    pass
```

#### Input

- `s` (1 ≤ |s| ≤ 10^4): A string consisting of lowercase English letters.
- `patterns` (1 ≤ |patterns| ≤ 10^3): A list of strings where each string is a substring pattern consisting of lowercase English letters. Each pattern has length between 1 and 100 inclusive.

#### Output

- A dictionary where each key is a pattern from the `patterns` list and the corresponding value is a list of starting indices (0-based) in `s` where the pattern occurs. The indices in the list should be in ascending order.

#### Example

```python
s = "ababcabc"
patterns = ["ab", "abc", "bca", "d"]

result = find_substring_occurrences(s, patterns)
# result should be: {"ab": [0, 2], "abc": [2, 5], "bca": [1], "d": []}
```

#### Constraints

- The length of `s` is between 1 and 10,000.
- The length of each pattern is between 1 and 100.
- The total number of patterns is between 1 and 1,000.

### Reference Solution

```python
from typing import List, Dict

def find_substring_occurrences(s: str, patterns: List[str]) -> Dict[str, List[int]]:
    result = {}
    
    for pattern in patterns:
        pattern_len = len(pattern)
        indices = []
        for i in range(len(s) - pattern_len + 1):
            if s[i:i + pattern_len] == pattern:
                indices.append(i)
        result[pattern] = indices
    
    return result

# Example usage
s = "ababcabc"
patterns = ["ab", "abc", "bca", "d"]
print(find_substring_occurrences(s, patterns))
```

#### Explanation

1. **Initialization**: Create an empty dictionary `result` to store the output.
2. **Pattern Matching**: For each pattern in `patterns`, determine the length of the pattern.
3. **Sliding Window**: Use a sliding window approach to check each substring of `s` of length equal to the pattern length. If a match is found, append the starting index to the `indices` list.
4. **Store Results**: After checking all possible starting indices in `s` for the current pattern, store the list of indices in the `result` dictionary with the pattern as the key.
5. **Return Results**: After processing all patterns, return the `result` dictionary.

This solution iterates over the string `s` for each pattern, making it efficient enough given the constraints.

