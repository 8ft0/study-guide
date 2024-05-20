# Longest Palindromic Substring

#### Problem Statement

Given a string `s`, find the longest palindromic substring in `s`. A palindrome is a string that reads the same backward as forward.

#### Function Signature

```python
def longest_palindromic_substring(s: str) -> str:
    pass
```

#### Input

- `s` (1 ≤ |s| ≤ 1000): A string consisting of lowercase and uppercase English letters.

#### Output

- Return the longest palindromic substring in `s`. If there are multiple longest palindromic substrings of the same length, return the first one that appears.

#### Example

```python
s = "babad"
result = longest_palindromic_substring(s)
# result should be: "bab" or "aba"

s = "cbbd"
result = longest_palindromic_substring(s)
# result should be: "bb"
```

#### Constraints

- The length of the string is between 1 and 1000.

### Reference Solution

To solve this problem, we can use dynamic programming. We'll create a 2D array `dp` where `dp[i][j]` will be `True` if the substring `s[i:j+1]` is a palindrome, and `False` otherwise.

### Steps

1. Initialize a 2D array `dp` with `False` values.
2. All substrings of length 1 are palindromes.
3. Check substrings of length 2. If the characters are the same, mark them as palindromes.
4. For substrings longer than 2, use the following relation:
   - `dp[i][j] = (s[i] == s[j]) and dp[i+1][j-1]`
5. Keep track of the longest palindrome found.

### Reference Solution Code

```python
def longest_palindromic_substring(s: str) -> str:
    n = len(s)
    if n == 0:
        return ""
    
    # Initialize the DP table
    dp = [[False] * n for _ in range(n)]
    
    # All substrings of length 1 are palindromes
    for i in range(n):
        dp[i][i] = True
    
    start = 0
    max_length = 1
    
    # Check substrings of length 2
    for i in range(n-1):
        if s[i] == s[i+1]:
            dp[i][i+1] = True
            start = i
            max_length = 2
    
    # Check substrings longer than 2
    for length in range(3, n+1):
        for i in range(n-length+1):
            j = i + length - 1
            if s[i] == s[j] and dp[i+1][j-1]:
                dp[i][j] = True
                start = i
                max_length = length
    
    return s[start:start + max_length]

# Example usage
s = "babad"
print(longest_palindromic_substring(s))  # Output: "bab" or "aba"

s = "cbbd"
print(longest_palindromic_substring(s))  # Output: "bb"
```

### Explanation

1. **Initialization**: We initialize a 2D list `dp` with `False`. The size of `dp` is `n x n`, where `n` is the length of the input string `s`.
2. **Single Character Palindromes**: All substrings of length 1 are palindromes, so we set `dp[i][i]` to `True` for all `i`.
3. **Two Character Palindromes**: For substrings of length 2, we check if the characters are the same. If they are, we set `dp[i][i+1]` to `True`.
4. **Longer Substrings**: For substrings longer than 2 characters, we use the relation `dp[i][j] = (s[i] == s[j]) and dp[i+1][j-1]` to determine if `s[i:j+1]` is a palindrome.
5. **Tracking the Longest Palindrome**: We keep track of the starting index and length of the longest palindromic substring found.

By the end of the process, `dp` will contain information about all palindromic substrings, and we can extract the longest one using the recorded starting index and length.