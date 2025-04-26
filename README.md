# python-for-leetcode

## type hints

Evolution of Python Typing

- Python 3.5 (2015): Introduced type hints via `typing` module [PEP 484].
- Python 3.9 (2020): Added native type hints for collections (e.g., `list[str]`) [PEP 585].
- Python 3.10 (2021): Added writing union types as `X | Y` [PEP 604].
- Python 3.11 (2022): Added `Self` [PEP 673] and `TypeVarTuple` [PEP 646].
- Python 3.12 (2023): Introduced Override Decorator [PEP 698].
- Python 3.13 (2024): Introduced annotating type forms `TypeForm` [PEP 747]

Since python 3.9:

- List -> list
- Dict -> dict
- Tuple -> tuple
- Set -> set
- Deque -> collections.deque
- DefaultDict -> collections.defaultdict
- Optional[T] -> T | None

## flatten 2D array

```python
a = [
  [1,2,3],
  [4,5,6],
  [7,8,9]
]

flattened = [item for sublist in a for item in sublist]
print(flattened)  # [1, 2, 3, 4, 5, 6, 7, 8, 9]

# or
print(sum(a, []))  # [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## Reverse a string

```python
s = "hello"

# Method 1: Using slicing
reversed_s = s[::-1]
print(reversed_s)  # "olleh"

# Method 2: Using the `reversed()` function
reversed_s = ''.join(reversed(s)) # NOTE `reversed()` returns an iterator
print(reversed_s)  # "olleh"
```

## Reverse a list or string

```python
str = "abcde"
print(str[::-1])

list = [1, 2, 3, 4, 5]
print(list[::-1])
```

## Array index trick (e.g. Palindrome checking)

```python
str = "abcba"
n = len(str)
print(all(str[i] == str[n-i-1] for i in range(n)))

str = "abcba"
print(all(str[i] == str[~i] for i in range(len(str)))) # ~i is -i-1, ~ is bitwise not
```

## Tuple unpacking

```python
point = (1, 2)
x, y = point
print(f"x: {x}, y: {y}")  # x: 1, y: 2
```

or

```python
point = (3, 4)
def distance(x, y):
    return (x**2 + y**2)**0.5
print(distance(*point))  # 5.0
```

### use `_` to ignore values

```python
point = (1, 2, 3)
x, _, z = point
print(f"x: {x}, z: {z}")  # x: 1, z: 3
```

## Boolean as int

```python
nums = [4, 6, 8, 3, 5, 7]

count = sum(n > 5 for n in nums)  # count of numbers greater than 5
print(count)  # 3
```

## map

```python
nums = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, nums)) # NOTE: map returns an iterator, need to use list() to convert it to a list
print(squared)  # [1, 4, 9, 16, 25]
```

## reduce

```python
from functools import reduce
from operator import add
nums = [1, 2, 3, 4, 5]
sum = reduce(add, nums)  # sum of all numbers
print(sum)  # 15

# or using lambda

sum = reduce(lambda x, y: x + y, nums)  # sum of all numbers
print(sum)  # 15
```

## defaultdict

```python
from collections import defaultdict

d = defaultdict(int)  # default value is 0
d['a'] += 1
print(d['a'])  # 1

# you dont need `setdefault`, which is working with regular `{}`
```

## swap variables

```python
a, b = b, a

# or using `^`
a = a ^ b
b = a ^ b
a = a ^ b
```

## chained boolean comparisons

```python
if 'a' < 'b' < 'c':

if 1 < 2 < 3:

# tuple comparison
if ('a', 3) < ('b', 2) < ('c', 1):
```

## Multiple assignment

When assign multiple variables to the same value, you can do it in one line:

```python
a = b = c = 0
```

## `match` syntax

Since python 3.10, you can use `match` syntax to match patterns in data structures (this is what is used in `match` in other languages):

```python
def process(data):
    match data:
        case int(value):
            print(f"Integer: {value}")
        case str(value):
            print(f"String: {value}")
        case list():
            print("List: {data}")
        case dict():
            print("Dictionary: {data}")
        case _:
            print("Unknown type")
process(42)  # Integer: 42
process("hello")  # String: hello
process([1, 2, 3])  # List: [1, 2, 3]
process({"key": "value"})  # Dictionary: {'key': 'value'}
process({1, 2, 3})  # Unknown type
process(None)  # Unknown type
```

Or you can match exact values:

```python
def process(data):
    match data:
        case 1:
            print("One")
        case 2:
            print("Two")
        case _:
            print("Other")
process(1)  # One
process(2)  # Two
process(3)  # Other
```
