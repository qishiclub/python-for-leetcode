# Python Beginner/Intermediate Guide to Functions, DS, & Techniques

## Techniques

### list/dict/set... comprehensions

```python
nums = [1, 2, 3, 4, 5]
new_nums = [num for num in nums if num >= 3]
```

```python
dict = {'a': 1, 'b': 2, 'c': 3}
new_dict = {key: value * 2 if value >= 2 else value  for key, value in dict.items() }

# values = [(expression_one) if (boolean) else (expression_two) for (item) in (iterable)]
```

### using booleans as values

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

### lambda functions

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

## Functions

### `enumerate`

```python
for i in range(len(nums)):
    print(f"{i}: {nums[i]}")

# or using enumerate
for i, num in enumerate(nums):
    print(f"{i}: {num}")
```

### `zip`

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

### `all`

`all` returns True if all elements of the iterable are true (or if the iterable is empty).

```python
# using all
for num in nums:
    if num >= value:
        return False
return True

# or using all
return all(num < value for num in nums)
```

### `any`

`any` returns True if any element of the iterable is true. If the iterable is empty, return False.

```python
# using any
for num in nums:
    if num >= value:
        return True
return False

# or using any
return any(num >= value for num in nums)
```

### `sorted`

`sorted` is a built-in function that returns a new sorted list from the elements of any iterable.

```python
nums = [5, 2, 3, 1, 4]
# using sorted
sorted_nums = sorted(nums)  # [1, 2, 3, 4, 5]
# or using sort
nums.sort()  # [1, 2, 3, 4, 5]
```

The difference between `sorted(iterable)` and `sort()` is that `sorted()` returns a new list,
while `sort()` modifies the list in place and returns `None`.

### `bin`

`bin` converts an integer number to a binary string prefixed with "0b".

```python
num = 5
print(bin(num))  # 0b101

# and converts it back to an integer using `int`
print(int(bin(num), 2))  # 5
```

### `map`

`map(function, iterable)` applies the function to all items in the iterable and returns a map object (which is an iterator).

```python
nums = [1, 2, 3, 4, 5]
# using map
squared_nums = list(map(lambda x: x ** 2, nums))  # [1, 4, 9, 16, 25]
```

### `reduce`

`reduce(function, iterable)` applies the function cumulatively to the items of the iterable, from left to right, so as to reduce the iterable to a single value.

```python
from functools import reduce

def add(x, y):
    return x + y
reduce (add, [1, 2, 3, 4, 5])  # 15
# which calcuates as (((1 + 2) + 3) + 4) + 5
```

### `filter`

`filter(function, iterable)` constructs an iterator from those elements of iterable for which function returns true.

```python
nums = [1, 2, 3, 4, 5]
# using filter
even_nums = list(filter(lambda x: x % 2 == 0, nums))  # [2, 4]
```

### `reversed`

`reversed` returns a reverse iterator. The original iterable is not modified.

```python
nums = [1, 2, 3, 4, 5]
# using reversed
reversed_nums = list(reversed(nums))  # [5, 4, 3, 2, 1]

# or using sort
nums.sort(reverse=True)  # [5, 4, 3, 2, 1]
```

## Data Structures

### dictionary

### counter

```python
from collections import Counter

nums = [1, 2, 3, 4, 5, 1, 2, 3]
counter = Counter(nums)
print(counter)  # Counter({1: 2, 2: 2, 3: 2, 4: 1, 5: 1})
```

### set

```python
nums = [1, 2, 3, 4, 5]

# using set
unique_nums = set(nums)  # {1, 2, 3, 4, 5}

# or using list(dict.fromkeys)
unique_nums = list(dict.fromkeys(nums))  # [1, 2, 3, 4, 5]
```

### deque

## Packages

### bisect

The module provides support for maintaining a list in sorted order without having to sort the list after each insertion.

There are two main functions in the bisect module:
- `bisect_left`: Find the index where to insert an element to keep the list sorted.
- `bisect_right`: Find the index where to insert an element to keep the list sorted, but if the element is already present, it will be inserted to the right of the existing elements.

### heapq

The module provides an implementation of the heap queue algorithm, also known as the priority queue algorithm.
- `heapify`: Transform a list into a heap, in-place, in linear time.
- `heappush`: Push the value item onto the heap, maintaining the heap invariant.
- `heappop`: Pop and return the smallest item from the heap, maintaining the heap invariant.

## Miscellaneous

### `If (not) _`

```python
# check if list is empty
if len(nums) == 0:
    print("List is empty")

# or
if not nums:
    print("List is empty")
```

### Multiplying `strings`/`lists`

### In-line If/Else statements

### `@lru_cache`, `@cache`

`@lru_cache` caches the result of function calls up to a certain size (`maxsize`).
When the cache reaches this limit, the least recently used entries are discarded.
Setting `maxisize=None` makes the cache unbounded.

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(10))  # 55
```

With python 3.9+, you can use `@cache` instead of `@lru_cache(maxsize=None)`.

```python
from functools import cache
@cache
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(10))  # 55
```

### `float('inf')`, `math.inf`

`float('inf')` is the same as `math.inf`, meaning positive infinity.
`float('-inf')` is the same as `-math.inf`, meaning negative infinity.
