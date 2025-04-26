# Special Notes

## Python variable scope

`nonlocal` and `global` keywords are used to declare variables in a different scope.

- `nonlocal` is used to declare a variable in the nearest enclosing scope that is not global.
- `global` is used to declare a variable in the global scope.

### Example of `nonlocal` keyword

```python
def outer_function():
    x = 10  # Enclosing scope variable

    def inner_function():
        nonlocal x  # Declare x as nonlocal
        x += 5
        print("Inner function:", x)

    inner_function()
    print("Outer function:", x)
outer_function()
```
Output:
```
Inner function: 15
Outer function: 15
```

### Example of `global` keyword

```python
x = 10  # Global variable
def my_function():
    global x  # Declare x as global
    x += 5
    print("Inside function:", x)
my_function()
print("Outside function:", x)
```
Output:
```
Inside function: 15
Outside function: 15
```

## Shallow copy vs Deep copy

- **Shallow copy**: Creates a new object, but inserts references into it to the objects found in the original. Changes made to mutable objects in the shallow copy will affect the original object.
- **Deep copy**: Creates a new object and recursively adds copies of nested objects found in the original. Changes made to mutable objects in the deep copy will not affect the original object.
- Use `copy.copy()` for shallow copy and `copy.deepcopy()` for deep copy.

```python
import copy

original = [1, 2, [3, 4]]
shallow_copied = copy.copy(original)  # this is the same as shallow_copied = original[:] or shallow_copied = original.copy()
deep_copied = copy.deepcopy(original)

shallow_copied[2][0] = 99
deep_copied[2][0] = 88

print(original)  # [1, 2, [99, 4]]
print(shallow_copied)  # [1, 2, [99, 4]]
print(deep_copied)  # [1, 2, [88, 4]]
```

## Default Arguments

- Default arguments are evaluated once when the function is defined, not each time the function is called.
- If you use mutable default arguments (like lists or dictionaries), they will retain changes across function calls.
- To avoid this, use `None` as the default value and initialize the mutable object inside the function.

```python
def append_to_list(value, my_list=None):
    if my_list is None:
        my_list = []
    my_list.append(value)
    return my_list
print(append_to_list(1))  # [1]
print(append_to_list(2))  # [2]
print(append_to_list(3, [4, 5]))  # [4, 5, 3]
```

```python
def append_to_list(value, my_list=[]):
    my_list.append(value)
    return my_list
print(append_to_list(1))  # [1]
print(append_to_list(2))  # [1, 2]
print(append_to_list(3, [4, 5]))  # [4, 5, 3]
```

## Sorting

- Python's built-in sorting (sorted() and list.sort()) is a stable sort, and sorts lexicographically by default.
- For tuple sorting, the first element is compared first, then the second, and so on.

```python
# Sorting a list of tuples
data = [(1, 'apple'), (2, 'banana'), (1, 'orange')]
sorted_data = sorted(data, key=lambda x: (x[0], x[1]))
print(sorted_data)  # [(1, 'apple'), (1, 'orange'), (2, 'banana')]
```

## Tuple vs List in leetcode

Tuples:

- Immutable, cannot be changed after creation.
- Hashable, can be used as dictionary keys.
- Faster than lists for iteration and access.
- Typically represent fixed collections of heterogeneous data or pairs, coordinates, etc.

Lists:

- Mutable, can be changed after creation.
- Not hashable, cannot be used as dictionary keys.
- Slower than tuples for iteration and access.
- Suitable for homogeneous sequences, dynamic-length collections, or when frequent modifications are needed.

| Use Tuple                            | Use List                                |
| ------------------------------------ | --------------------------------------- |
| Coordinate, (row, col) pairs         | When frequent insertion/deletion needed |
| Keys in dicts/sets                   | Temporary collections, stacks, queues   |
| Fixed-size states (memoization keys) | Mutable states, paths, results          |

## `*args` and `**kwargs`

- `*args` allows you to pass a variable number of non-keyword arguments to a function.
- `**kwargs` allows you to pass a variable number of keyword arguments to a function.
- They are often used in function definitions to allow for flexible argument passing.

```python
def my_function(*args, **kwargs):
    print("Positional arguments:", args)
    print("Keyword arguments:", kwargs)
my_function(1, 2, 3, a=4, b=5)

# Output:
# Positional arguments: (1, 2, 3)
# Keyword arguments: {'a': 4, 'b': 5}
```

```python
def my_function(a, b, *args, **kwargs):
    print("a:", a)
    print("b:", b)
    print("Positional arguments:", args)
    print("Keyword arguments:", kwargs)
my_function(1, 2, 3, 4, 5, x=6, y=7)

# Output:
# a: 1
# b: 2
# Positional arguments: (3, 4, 5)
# Keyword arguments: {'x': 6, 'y': 7}
```
