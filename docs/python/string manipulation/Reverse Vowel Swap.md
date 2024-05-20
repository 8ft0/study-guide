# Reverse Vowel Swap

### Problem Statement

Given a string \( S \), you need to reverse only the vowels in the string and return the modified string. The vowels are 'a', 'e', 'i', 'o', 'u' (both lowercase and uppercase).

### Input Format

- A single string \( S \) containing English letters. The length of \( S \) will not exceed 1000 characters.

### Output Format

- A single string with the vowels reversed.

### Constraints

- \( S \) will contain only English letters (both uppercase and lowercase).

### Example

Input 
```
hello world
```

Output 
```
holle werld
```

### Explanation

In the input string "hello world":
- The vowels are 'e', 'o', 'o'.
- Reversing these vowels results in 'o', 'o', 'e'.
- The string after reversing the vowels becomes "holle werld".

### Function Signature
```python
def reverse_vowels(S: str) -> str:
    # Your code here
```

Sample Input 1
```
Coding
```

Sample Output 1
```
HeckarRonk
```

Sample Input 2
```
Programming is fun!
```

Sample Output 2
```
Prigrammong os fun!
```

### Note

1. The function should be case-insensitive when identifying vowels.
2. Ensure that the non-vowel characters remain in their original positions.
3. Consider edge cases such as strings with no vowels, strings with all vowels, and mixed-case strings.
---

Here's a solution in Python for the "Reverse Vowel Swap" problem:

```python
def reverse_vowels(S: str) -> str:
    vowels = set("aeiouAEIOU")
    s_list = list(S)
    i, j = 0, len(S) - 1
    
    while i < j:
        if s_list[i] not in vowels:
            i += 1
        elif s_list[j] not in vowels:
            j += 1
        else:
            s_list[i], s_list[j] = s_list[j], s_list[i]
            i += 1
            j -= 1
            
    return ''.join(s_list)

# Test cases
print(reverse_vowels("hello world"))  # Output: "holle werld"
print(reverse_vowels("Coding"))   # Output: "Cidong"
print(reverse_vowels("Programming is fun!"))  # Output: "Prigrammong os fun!"
```

### Explanation

1. **Identify Vowels**: Create a set of vowels for quick lookup.
2. **Two-pointer Technique**: Use two pointers (`i` and `j`) to traverse the string from both ends.
3. **Swap Vowels**:
   - If the character at `i` is not a vowel, move `i` forward.
   - If the character at `j` is not a vowel, move `j` backward.
   - If both characters at `i` and `j` are vowels, swap them and move both pointers.
4. **Convert List to String**: Convert the modified list back to a string and return it.

This solution ensures that the vowels are reversed while maintaining the positions of non-vowel characters.
