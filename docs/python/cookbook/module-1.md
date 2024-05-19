# Basic Coding

A set of reference examples that cover the expected knowledge areas and types of questions you might encounter. Each example will focus on basic operations with numbers, string manipulation, and array handling. These solutions are designed to be concise and efficient, ideally matching the requirement to be solvable within 10 minutes.

### 1: Number Operations and Conditional Logic
**Problem**: Write a function that accepts an integer and returns the sum of its digits only if the number is even. If the number is odd, return the product of its digits.

```python
def process_number(n):
    digits = [int(d) for d in str(abs(n))]  # Convert the number to a list of its digits
    if n % 2 == 0:
        return sum(digits)
    else:
        product = 1
        for d in digits:
            product *= d
        return product

# Example usage:
print(process_number(1234))  # Output will be the sum of the digits: 10
print(process_number(1235))  # Output will be the product of the digits: 30
```

### 2: String Manipulation
**Problem**: Given a string, split it into substrings at every comma, reverse each substring, and join them back into a single string with commas.

```python
def reverse_substrings(s):
    substrings = s.split(',')  # Split the string into substrings on commas
    reversed_substrings = [sub[::-1] for sub in substrings]  # Reverse each substring
    return ','.join(reversed_substrings)  # Join them back into a single string

# Example usage:
print(reverse_substrings("hello,world,python"))  # Output: "olleh,dlrow,nohtyp"
```

### 3: Array Manipulation
**Problem**: Given an array of integers, return a new array where each element at index `i` is the sum of the original element and its neighbors. Use 0 for non-existing neighbors.

```python
def sum_neighbors(arr):
    n = len(arr)
    result = []
    for i in range(n):
        left = arr[i - 1] if i > 0 else 0
        right = arr[i + 1] if i < n - 1 else 0
        result.append(left + arr[i] + right)
    return result

# Example usage:
print(sum_neighbors([1, 2, 3, 4]))  # Output: [3, 6, 9, 7]
```

### 4: Conditional Array Iteration
**Problem**: Iterate through an array and create a new list containing only the odd numbers multiplied by their index.

```python
def odd_multiplied_by_index(arr):
    result = [num * i for i, num in enumerate(arr) if num % 2 != 0]
    return result

# Example usage:
print(odd_multiplied_by_index([10, 21, 32, 43, 54]))  # Output: [21, 129]
```


### 5: Filter and Transform
**Problem**: Given a list of integers, return a new list containing only the even numbers, each multiplied by 2.

```python
def filter_and_transform(arr):
    filtered = [x * 2 for x in arr if x % 2 == 0]
    return filtered

# Example usage:
print(filter_and_transform([1, 2, 3, 4, 5, 6]))  # Output: [4, 8, 12]
```

### 6: Basic String Operations
**Problem**: Given a string, return a new string where each character is replaced by its corresponding ordinal value separated by dashes.

```python
def char_to_ordinal(s):
    return '-'.join(str(ord(c)) for c in s)

# Example usage:
print(char_to_ordinal("abc"))  # Output: "97-98-99"
```

### 7: Array Rotation
**Problem**: Rotate an array to the right by one position. The last element should wrap around to the front.

```python
def rotate_array(arr):
    if len(arr) > 1:
        return [arr[-1]] + arr[:-1]
    return arr

# Example usage:
print(rotate_array([1, 2, 3, 4]))  # Output: [4, 1, 2, 3]
```

### 8: Conditional String Splitting
**Problem**: Given a sentence, split it into words and return a list containing only the words that are longer than 3 characters.

```python
def filter_long_words(sentence):
    words = sentence.split()
    return [word for word in words if len(word) > 3]

# Example usage:
print(filter_long_words("The quick brown fox jumps over the lazy dog"))  # Output: ['quick', 'brown', 'jumps', 'over', 'lazy']
```

### 9: Summing Specific Array Elements
**Problem**: Given an array of integers, sum only the positive numbers.

```python
def sum_positive_numbers(arr):
    return sum(x for x in arr if x > 0)

# Example usage:
print(sum_positive_numbers([-1, 2, 3, -4, 5]))  # Output: 10
```

### 10: Modify Elements Based on Condition
**Problem**: Given a list of integers, return a new list where each element is increased by 10% if the element is even, or decreased by 10% if the element is odd.

```python
def adjust_numbers(arr):
    return [x * 1.1 if x % 2 == 0 else x * 0.9 for x in arr]

# Example usage:
print(adjust_numbers([10, 21, 32, 43, 54]))  # Output: [11.0, 18.9, 35.2, 38.7, 59.4]
```

### 11: Count Specific Characters
**Problem**: Given a string, count the number of vowels in it.

```python
def count_vowels(s):
    vowels = 'aeiouAEIOU'
    return sum(1 for char in s if char in vowels)

# Example usage:
print(count_vowels("Hello World"))  # Output: 3
```

### 12: Find Maximum in Array Segments
**Problem**: Given an array of integers, find the maximum number in each consecutive subarray of size 3.

```python
def max_in_subarrays(arr, k=3):
    return [max(arr[i:i+k]) for i in range(len(arr)-k+1)]

# Example usage:
print(max_in_subarrays([1, 2, 3, 4, 5, 6, 7]))  # Output: [3, 4, 5, 6, 7]
```

### 13: Alternating Sum
**Problem**: Calculate the alternating sum of an array's elements (subtract odd-indexed elements from even-indexed ones).

```python
def alternating_sum(arr):
    return sum(arr[i] if i % 2 == 0 else -arr[i] for i in range(len(arr)))

# Example usage:
print(alternating_sum([10, 20, 30, 40, 50]))  # Output: 10 (10 - 20 + 30 - 40 + 50)
```

### 14: Normalize Text
**Problem**: Normalize a given string by lowercasing it and removing all non-alphanumeric characters.

```python
def normalize_text(s):
    return ''.join(c.lower() for c in s if c.isalnum())

# Example usage:
print(normalize_text("Hello, World!"))  # Output: "helloworld"
```

### 15: Increment Dictionary Values
**Problem**: Given a dictionary, increment each value by 1.

```python
def increment_values(d):
    return {k: v + 1 for k, v in d.items()}

# Example usage:
print(increment_values({'a': 1, 'b': 2, 'c': 3}))  # Output: {'a': 2, 'b': 3, 'c': 4}
```

### 16: Generate Ranges
**Problem**: Given a number, generate a list of tuples representing ranges from 0 to that number, incrementing by 1 each time.

```python
def generate_ranges(n):
    return [(i, i+1) for i in range(n)]

# Example usage:
print(generate_ranges(5))  # Output: [(0, 1), (1, 2), (2, 3), (3, 4), (4, 5)]
```

### 17: String Character Swap
**Problem**: Swap the first and last characters of a string.

```python
def swap_first_last(s):
    if len(s) > 1:
        return s[-1] + s[1:-1] + s[0]
    return s

# Example usage:
print(swap_first_last("hello"))  # Output: "oellh"
```

### 18: Prime Check
**Problem**: Write a function to check if a given number is prime.

```python
def is_prime(n):
    if n <= 1:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True

# Example usage:
print(is_prime(29))  # Output: True
print(is_prime(10))  # Output: False
```

### 19: Concatenate and Sort Array
**Problem**: Given two arrays, concatenate them and then sort the resulting array.

```python
def concatenate_and_sort(arr1, arr2):
    combined = arr1 + arr2
    return sorted(combined)

# Example usage:
print(concatenate_and_sort([5, 3, 1], [2, 4, 6]))  # Output: [1, 2, 3, 4, 5, 6]
```

### 20: Capitalize First Letters
**Problem**: Given a sentence, capitalize the first letter of each word.

```python
def capitalize_words(sentence):
    return ' '.join(word.capitalize() for word in sentence.split())

# Example usage:
print(capitalize_words("hello world"))  # Output: "Hello World"
```

### 21: Sum of Even Indices
**Problem**: Calculate the sum of elements at even indices in an array.

```python
def sum_even_indices(arr):
    return sum(arr[i] for i in range(len(arr)) if i % 2 == 0)

# Example usage:
print(sum_even_indices([10, 15, 20, 25, 30]))  # Output: 60 (10 + 20 + 30)
```

### 22: Reverse Each Word
**Problem**: Given a sentence, reverse each word in the sentence.

```python
def reverse_each_word(sentence):
    words = sentence.split()
    reversed_words = [word[::-1] for word in words]
    return ' '.join(reversed_words)

# Example usage:
print(reverse_each_word("Hello world"))  # Output: "olleH dlrow"
```

### 23: Remove Duplicates from List
**Problem**: Write a function to remove all duplicates from a list and return a list of only unique elements.

```python
def remove_duplicates(arr):
    unique_elements = list(dict.fromkeys(arr))  # Using dict to preserve order
    return unique_elements

# Example usage:
print(remove_duplicates([1, 2, 2, 3, 4, 4, 5]))  # Output: [1, 2, 3, 4, 5]
```

### 24: Find Longest Word
**Problem**: From a list of words, find the longest word.

```python
def find_longest_word(words):
    return max(words, key=len)

# Example usage:
print(find_longest_word(["apple", "banana", "cherry"]))  # Output: "banana"
```


### 25: Calculate Fibonacci Number
**Problem**: Write a function that returns the nth Fibonacci number.

```python
def fibonacci(n):
    if n <= 1:
        return n
    a, b = 0, 1
    for _ in range(2, n + 1):
        a, b = b, a + b
    return b

# Example usage:
print(fibonacci(10))  # Output: 55 (The 10th Fibonacci number)
```

### 26: Count Specific Characters in String
**Problem**: Count how many times a specific character appears in a string.

```python
def count_char(s, char):
    return s.count(char)

# Example usage:
print(count_char("hello world", 'l'))  # Output: 3
```

### 27: Remove Specific Element
**Problem**: Write a function to remove all occurrences of a specific element from a list.

```python
def remove_element(arr, element):
    return [x for x in arr if x != element]

# Example usage:
print(remove_element([1, 2, 3, 2, 4, 2, 5], 2))  # Output: [1, 3, 4, 5]
```

### 28: Find Minimum and Maximum
**Problem**: Create a function that returns both the minimum and maximum number from a list.

```python
def find_min_max(arr):
    return min(arr), max(arr)

# Example usage:
print(find_min_max([3, 1, 4, 1, 5, 9, 2, 6]))  # Output: (1, 9)
```

### 29: Check for Anagrams
**Problem**: Determine if two strings are anagrams of each other.

```python
def are_anagrams(str1, str2):
    return sorted(str1) == sorted(str2)

# Example usage:
print(are_anagrams("listen", "silent"))  # Output: True
```

### 30: Merge and Square List Elements
**Problem**: Given two lists of numbers, merge them and return a new list where each element is squared.

```python
def merge_and_square(list1, list2):
    merged_list = list1 + list2
    return [x**2 for x in merged_list]

# Example usage:
print(merge_and_square([1, 2], [3, 4]))  # Output: [1, 4, 9, 16]
```

### 31: Validate IP Address
**Problem**: Write a function to validate if a given string is a valid IPv4 address.

```python
def is_valid_ip(ip):
    parts = ip.split('.')
    if len(parts) != 4:
        return False
    for part in parts:
        if not part.isdigit() or not 0 <= int(part) <= 255 or (part[0] == '0' and len(part) > 1):
            return False
    return True

# Example usage:
print(is_valid_ip("192.168.1.1"))  # Output: True
print(is_valid_ip("256.100.50.25"))  # Output: False
```


### 32: Sum of Squares
**Problem**: Given a list of integers, compute the sum of the squares of each number.

```python
def sum_of_squares(nums):
    return sum(x**2 for x in nums)

# Example usage:
print(sum_of_squares([1, 2, 3, 4]))  # Output: 30 (1 + 4 + 9 + 16)
```

### 33: Toggle Case
**Problem**: Write a function that converts all uppercase letters to lowercase and vice versa in a string.

```python
def toggle_case(s):
    return s.swapcase()

# Example usage:
print(toggle_case("Hello World"))  # Output: "hELLO wORLD"
```

### 34: List of Multiples
**Problem**: Create a list of the first n multiples of a given number x.

```python
def list_of_multiples(x, n):
    return [x * i for i in range(1, n + 1)]

# Example usage:
print(list_of_multiples(7, 5))  # Output: [7, 14, 21, 28, 35]
```

### 35: Valid Parentheses
**Problem**: Check if a string containing only '(', ')', '{', '}', '[' and ']' is valid. The string is valid if all types of brackets are closed in the correct order.

```python
def is_valid(s):
    stack = []
    mapping = {')': '(', '}': '{', ']': '['}
    for char in s:
        if char in mapping:
            top_element = stack.pop() if stack else '#'
            if mapping[char] != top_element:
                return False
        else:
            stack.append(char)
    return not stack

# Example usage:
print(is_valid("()[]{}"))  # Output: True
print(is_valid("(]"))  # Output: False
```

### 36: Filter Non-Positive Numbers
**Problem**: Given a list of integers, return a new list containing only the positive numbers.

```python
def filter_positive(nums):
    return [num for num in nums if num > 0]

# Example usage:
print(filter_positive([-1, 2, -3, 4, -5, 6]))  # Output: [2, 4, 6]
```

### 37: Convert Hex to Decimal
**Problem**: Write a function to convert a hexadecimal string to its decimal equivalent.

```python
def hex_to_decimal(hex_string):
    return int(hex_string, 16)

# Example usage:
print(hex_to_decimal("1A"))  # Output: 26
print(hex_to_decimal("FF"))  # Output: 255
```

### 38: Interleave Lists
**Problem**: Given two lists of equal length, create a new list by interleaving their elements.

```python
def interleave_lists(list1, list2):
    result = []
    for a, b in zip(list1, list2):
        result.extend([a, b])
    return result

# Example usage:
print(interleave_lists([1, 2, 3], ['a', 'b', 'c']))  # Output: [1, 'a', 2, 'b', 3, 'c']
```

These examples provide a thorough exploration of basic and intermediate programming tasks that are typically found in coding assessments. They are intended to strengthen your problem-solving skills through varied challenges, ensuring you are well-prepared for any basic coding module.