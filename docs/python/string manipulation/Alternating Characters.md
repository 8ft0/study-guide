# Alternating Characters

### Problem Statement

You are given a string containing characters 'A' and 'B' only. Your task is to change it into a string such that there are no matching adjacent characters. To do this, you are allowed to delete zero or more characters in the string.

### Input Format

- A single string \( S \) containing only characters 'A' and 'B'. The length of \( S \) will not exceed 1000 characters.

### Output Format

- An integer representing the minimum number of deletions required to make the string alternate.

### Constraints

- \( S \) will contain only characters 'A' and 'B'.

### Example

Input 
```
AABAAB
```

Output 
```
2
```

### Explanation

In the input string "AABAAB":
- The first and second 'A' are the same and adjacent, so we can delete one 'A' to make it "ABAAB".
- The fourth and fifth 'A' are the same and adjacent, so we can delete one 'A' to make it "ABAB".
- The string "ABAB" has no matching adjacent characters.

### Function Signature
```python
def alternating_characters(S: str) -> int:
    # Your code here
```

Sample Input 1
```
AAAA
```

Sample Output 1
```
3
```

Sample Input 2
```
BBBBB
```

Sample Output 2
```
4
```

Sample Input 3
```
ABABABAB
```

Sample Output 3
```
0
```

## Solution

Here's a solution in Python for the "Alternating Characters" problem:

```python
def alternating_characters(S: str) -> int:
    deletions = 0
    for i in range(1, len(S)):
        if S[i] == S[i - 1]:
            deletions += 1
    return deletions

# Test cases
print(alternating_characters("AABAAB"))  # Output: 2
print(alternating_characters("AAAA"))    # Output: 3
print(alternating_characters("BBBBB"))   # Output: 4
print(alternating_characters("ABABABAB"))  # Output: 0
```

### Explanation

1. **Initial Setup**: Initialize a counter `deletions` to zero.
2. **Traverse the String**: Iterate through the string starting from the second character.
3. **Count Deletions**:
   - If the current character is the same as the previous character, increment the `deletions` counter.
4. **Return Result**: Return the total count of deletions required to make the string alternate.

This solution efficiently counts the minimum number of deletions needed to ensure no matching adjacent characters.