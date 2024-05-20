# Sum of Two Numbers

#### Problem Statement

You are given two integers, `a` and `b`. Your task is to implement a function that returns their sum.

#### Function Signature

```python
def sum_two_numbers(a: int, b: int) -> int:
    pass
```

#### Input

- `a` and `b` (−10^3 ≤ a, b ≤ 10^3): Two integers.

#### Output

- Return the sum of `a` and `b`.

#### Example

```python
a = 3
b = 5
result = sum_two_numbers(a, b)
# result should be: 8

a = -3
b = 2
result = sum_two_numbers(a, b)
# result should be: -1
```

#### Constraints

- Both integers will be within the range \([-1000, 1000]\).

### Reference Solution

```python
def sum_two_numbers(a: int, b: int) -> int:
    return a + b

# Example usage
a = 3
b = 5
print(sum_two_numbers(a, b))  # Output: 8

a = -3
b = 2
print(sum_two_numbers(a, b))  # Output: -1
```

#### Explanation

1. **Function Definition**: Define the function `sum_two_numbers` that takes two integers `a` and `b` as arguments.
2. **Return Sum**: Return the sum of `a` and `b`.

This is a straightforward problem designed to test basic understanding of function implementation and arithmetic operations in Python.