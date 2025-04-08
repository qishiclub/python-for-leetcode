# Python Beginner/Intermediate Guide to Functions, DS, & Techniques

# Techniques

## list/dict/set... comprehensions

```python
nums = [1, 2, 3, 4, 5]
new_nums = [num for num in nums if num >= 3]
```

```python
dict = {'a': 1, 'b': 2, 'c': 3}
new_dict = {key: value * 2 if value >= 2 else value  for key, value in dict.items() }

# values = [(expression_one) if (boolean) else (expression_two) for (item) in (iterable)]
```

## using booleans as values

Since python does not have strict types, you can use booleans as values in dictionaries or lists.

```python
# s1 = "abcdef"
# s2 = "abc123"

num_in_common = 0
for i in range(len(s1)):
    if s1[i] == s2[i]:
        num_in_common += 1
print(num_in_common)  # 3

# or using `s1[i] == s2[i]` as a boolean value
num_in_common = 0
for i in range(len(s1)):
    num_in_common += s1[i] == s2[i]
print(num_in_common)  # 3
```

## lambda functions

lambda function is a small anonymous function. It can take any number of arguments, but can only have one expression.

```python
def double(num):
    return num * 2
print(double(5))  # 10

# or using a lambda function
double = lambda num: num * 2

print(double(5))  # 10
```

or using lambda function in sorting for point(x, y)

```python
points = [(1, 2), (3, 6), (5, 6), (3, 5), (7, 8)]
points.sort(key=lambda point: (-point[0], point[1])) # sort by x desc, y asc
print(points)  # [(7, 8), (5, 6), (3, 5), (3, 6), (1, 2)]
```

 Other examples of functions which could take in a key argument include
 `max`, `min`, many [heapq](https://docs.python.org/3/library/heapq.html) methods,
 [bisect](https://docs.python.org/3/library/bisect.html) methods, etc.

# Functions

## `enumerate`

```python
for i in range(len(nums)):
    print(f"{i}: {nums[i]}")

# or using enumerate
for i, num in enumerate(nums):
    print(f"{i}: {num}")
```

## `zip`

`zip` is a built-in function that takes iterables (can be zero or more), aggregates them in a tuple, and returns it.

```python
list1 = [1, 2, 3, 4]
list2 = [4, 5, 6]

# using min length
for i in range(min(len(list1), len(list2))):
    print(f"{list1[i]}: {list2[i]}") # 1: 4, 2: 5, 3: 6

# or using zip
for num1, num2 in zip(list1, list2):
    print(f"{num1}: {num2}") # 1: 4, 2: 5, 3: 6
```

## `all`

all returns True if all elements of the iterable are true (or if the iterable is empty).

```python
# using all
for num in nums:
    if num >= value:
        return False
return True

# or using all
return all(num < value for num in nums)
```

## `any`

any returns True if any element of the iterable is true. If the iterable is empty, return False.

```python
# using any
for num in nums:
    if num >= value:
        return True
return False

# or using any
return any(num >= value for num in nums)
```

## `sorted`

## `bin`

## `map`

## `reduce`

## `filter`

## `reversed`

# Data Structures

## dictionary

## counter

## set

## deque

# Packages

## bisect

## heapq

# Miscellaneous

## `If (not) ___`

## Multiplying `strings`/`lists`

## In-line If/Else statements

## `@cache`, `@lru_cache`
