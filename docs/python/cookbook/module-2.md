
# Data Manipulation

Here are comprehensive reference examples that encompass the key skills and techniques you are expected to demonstrate. These examples will cover the operations on numbers, strings, and arrays as specified in the module details.

### 1: Manipulating Strings and Numbers
**Task**: Write a function that takes a string representing a long number and reverses the digits of the number in each comma-separated segment.

**Python Code**:
```python
def reverse_segments(number_str):
    segments = number_str.split(',')
    reversed_segments = [segment[::-1] for segment in segments]
    return ','.join(reversed_segments)

# Example usage:
input_str = "12345,67890"
print(reverse_segments(input_str))  # Outputs: "54321,09876"
```

### 2: Array Manipulation
**Task**: Write a function that accepts an array of integers and modifies each element by adding its index value, then reverses the array.

**Python Code**:
```python
def modify_and_reverse_array(arr):
    modified_array = [arr[i] + i for i in range(len(arr))]
    return modified_array[::-1]

# Example usage:
arr = [10, 20, 30, 40, 50]
print(modify_and_reverse_array(arr))  # Outputs: [54, 43, 32, 21, 10]
```

### 3: Combining String and Array Operations
**Task**: Write a function that takes a sentence, splits it into words, reverses each word, and concatenates them into a new string with spaces in between.

**Python Code**:
```python
def reverse_words(sentence):
    words = sentence.split()
    reversed_words = [word[::-1] for word in words]
    return ' '.join(reversed_words)

# Example usage:
sentence = "hello world"
print(reverse_words(sentence))  # Outputs: "olleh dlrow"
```

### 4: Nested Loop Array Manipulation
**Task**: Write a function that takes an array of non-negative integers, where each integer is less than 10, and converts it into a single integer where each array element contributes a digit.

**Python Code**:
```python
def array_to_number(digits):
    number = 0
    for digit in digits:
        number = number * 10 + digit
    return number

# Example usage:
digits = [1, 2, 3, 4, 5]
print(array_to_number(digits))  # Outputs: 12345
```

### 5: Complex Data Manipulation with Nested Loops
**Task**: Write a function that takes a list of strings and finds the string which, when reversed, is lexicographically smallest.

**Python Code**:
```python
def find_min_reversed_lex(strings):
    reversed_strings = [s[::-1] for s in strings]
    return min(reversed_strings)

# Example usage:
strings = ["banana", "apple", "orange"]
print(find_min_reversed_lex(strings))  # Outputs: "elppa"
```




### 6:  **Splitting Numbers into Digits and Basic Operations:**
```python
# Example 1: Splitting numbers into digits and performing basic operations
number = 12345
digits = [int(digit) for digit in str(number)]
sum_of_digits = sum(digits)
product_of_digits = 1
for digit in digits:
    product_of_digits *= digit
```

### 7:  **Basic String Manipulation:**
```python
# Example 2: Basic string manipulation - splitting a string into substrings
text = "hello world"
words = text.split()  # Split the string into individual words
# Comparing strings
if "hello" == words[0]:
    print("The first word is 'hello'.")
```

### 8:  **Modifying Elements of a String:**
```python
# Example 3: Modifying elements of a string
string = "python"
# Concatenating strings
new_string = string + " is fun"
# Reversing strings
reversed_string = string[::-1]
```

### 9:  **Basic Array Manipulation:**
```python
# Example 4: Basic array manipulation
numbers = [1, 2, 3, 4, 5]
# Iterating over an array
for num in numbers:
    print(num)
# Modifying elements of an array
squared_numbers = [num ** 2 for num in numbers]
# Reversing an array
reversed_numbers = numbers[::-1]
# Concatenating two arrays
combined_array = numbers + squared_numbers
```

### 10:  **Combination of Basic Concepts:**
```python
# Example 5: Combination of basic concepts
sentence = "hello world"
# Splitting a string into substrings, modifying each substring, and comparing
words = sentence.split()
modified_words = [word.upper() for word in words]
if modified_words[0] == "HELLO":
    print("The first word is 'HELLO'.")
```

### 11:  **Combination of Basic Concepts with Nested Loops:**
```python
# Example 6: Combination of basic concepts with nested loops
text = "abc def"
# Splitting a string into substrings and modifying each substring
modified_text = ""
for char in text:
    if char.isalpha():
        modified_text += char.upper()
    else:
        modified_text += char
# Comparing each modified substring with other substrings
for i in range(len(modified_text)):
    for j in range(i + 1, len(modified_text)):
        if modified_text[i] == modified_text[j]:
            print(f"The character '{modified_text[i]}' appears more than once.")
```

### 12:  **Iterating over an Array and Modifying Elements:**
```python
# Example 7: Iterating over an array to split into two arrays, modifying the second array, and appending it to the first array
original_array = [1, 2, 3, 4, 5]
# Splitting an array into two arrays
first_half = original_array[:len(original_array) // 2]
second_half = original_array[len(original_array) // 2:]
# Modifying the second array
modified_second_half = [num * 2 for num in second_half]
# Appending the modified second array to the first array
combined_array = first_half + modified_second_half
```


## 13: **Combination of Basic Concepts with String Comparison:**
```python
# Example 8: Combination of basic concepts with string comparison
text = "hello world"
# Splitting a string into substrings, modifying each substring, and comparing with other substrings
words = text.split()
for i in range(len(words)):
    modified_word = words[i].upper()
    for j in range(len(words)):
        if i != j and modified_word == words[j].upper():
            print(f"The word '{modified_word}' appears more than once.")
```

## 14:  **Iterating over an Array, Modifying Elements, and Reversing:**
```python
# Example 9: Iterating over an array, modifying elements, and reversing the array
numbers = [1, 2, 3, 4, 5]
# Iterating over an array and modifying elements
modified_numbers = [num + 10 for num in numbers]
# Reversing the modified array
reversed_modified_numbers = modified_numbers[::-1]
```

## 15:  **Combination of String and Array Manipulation:**
```python
# Example 10: Combination of string and array manipulation
sentence = "hello world"
# Splitting a string into substrings and modifying each substring
words = sentence.split()
# Modifying each word and concatenating into a new sentence
new_sentence = " ".join([word.upper() for word in words])
```


## 16:  **Combination of Basic Concepts with String Concatenation:**
```python
# Example 11: Combination of basic concepts with string concatenation
string1 = "hello"
string2 = "world"
# Concatenating strings and modifying the result
concatenated_string = string1 + string2
modified_string = concatenated_string.upper()
```

## 17:  **Iterating over an Array, Reversing, and Concatenating:**
```python
# Example 12: Iterating over an array, reversing, and concatenating arrays
original_array = [1, 2, 3, 4, 5]
# Iterating over an array and modifying elements
squared_numbers = [num ** 2 for num in original_array]
# Reversing the modified array
reversed_squared_numbers = squared_numbers[::-1]
# Concatenating the original and reversed arrays
combined_array = original_array + reversed_squared_numbers
```

## 18:  **Combination of String and Array Manipulation with Nested Loops:**
```python
# Example 13: Combination of string and array manipulation with nested loops
text = "hello world"
numbers = [1, 2, 3, 4, 5]
# Splitting a string into substrings and modifying each substring
words = text.split()
# Iterating over an array and modifying elements, then concatenating with each word
modified_text = ""
for word in words:
    for num in numbers:
        modified_text += word + str(num)
```

## 19:  **Combination of String and Array Manipulation with Comparison:**
```python
# Example 14: Combination of string and array manipulation with comparison
text = "python is awesome"
vowels = "aeiou"
# Splitting a string into substrings and modifying each substring
words = text.split()
# Counting vowels in each word and comparing with a threshold
for word in words:
    vowel_count = sum(1 for char in word if char in vowels)
    if vowel_count > len(word) // 2:
        print(f"The word '{word}' has more vowels than consonants.")
```

## 20:  **Advanced Array Manipulation with List Comprehensions:**
```python
# Example 15: Advanced array manipulation with list comprehensions
numbers = [1, 2, 3, 4, 5]
# Generating a new array by performing operations on each element
modified_numbers = [num * 2 if num % 2 == 0 else num for num in numbers]
```

## 21:  **Combination of String and Array Manipulation with Reversing:**
```python
# Example 16: Combination of string and array manipulation with reversing
text = "hello world"
# Splitting a string into substrings and modifying each substring
words = text.split()
# Reversing each word and concatenating into a new string
reversed_text = " ".join(word[::-1] for word in words)
```

These examples offer additional scenarios for practicing data manipulation techniques, combining multiple concepts, and solving problems efficiently within the constraints specified for Module 2 of the assessment.

Each of these examples tackles key concepts listed in the module specifications, such as working with basic data operations, using loops effectively, and handling string and array manipulations without resorting to advanced algorithms or optimizations. These tasks are designed to be solved within the time constraints provided, focusing on clarity and efficiency in implementation.
