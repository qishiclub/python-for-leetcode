# String

## Chain string operations

```python
info = "  John Doe, 30, New York  "
formatted_info = info.strip()
formatted_info = formatted_info.upper()
formatted_info = formatted_info.split(',')
print(formatted_info)  # ['JOHN DOE', ' 30', ' NEW YORK']

# chained operations
formatted_info = info.strip().upper().split(",")
print(formatted_info)  # ['JOHN DOE', ' 30', ' NEW YORK']
```

## `''.join()` when creating a single string for `list` elements

```python
list_of_strings = ['Hello', 'World']
joined_string = ''.join(list_of_strings)

# vs
res = ''
for string in list_of_strings:
    res += string
```

## Case Conversion

- `lower()`, `'HELLO WORLD'.lower()  # 'hello world'`
- `upper()`, `'hello world'.upper()  # 'HELLO WORLD'`
- `title()`, `'hello world'.title()  # 'Hello World'`
- `capitalize()`, `'hello world'.capitalize()  # 'Hello world'`
- `swapcase()`, `'HeLLo'.swapcase()  # 'hEllO'`

## Searching and Counting

### `.find(sub[, start[, end]])`

```python
'hello world'.find('world')  # 6
```

### `.rfind(sub[, start[, end]])`

```python
'hello world world'.rfind('world')  # 12
```

### `.count(sub[, start[, end]])`

```python
'hello world'.count('o')  # 2
```

## Trimming and Padding

### `.strip([chars])`

```python
'  hello world  '.strip()  # 'hello world'
```

### `.lstrip([chars])`

```python
'  hello world  '.lstrip()  # 'hello world  '
```

lstrip `-`

```python
'-42'.lstrip('-')  # '42'
```

### `.rstrip([chars])`

```python
'  hello world  '.rstrip()  # '  hello world'
```

### `.ljust(width[, fillchar])`

```python
'hello'.ljust(10, '-')  # 'hello-----'
```

### `.rjust(width[, fillchar])`

```python
'hello'.rjust(10, '-')  # '-----hello'
```

### `.zfill(width[, fillchar])`

```python
'42'.zfill(5)  # '00042'
```

## Replacement

### `.replace(old, new[, count])`

```python
'hello world'.replace('world', 'Python')  # 'hello Python'
```

## Splitting and Joining

### `.split([sep[, maxsplit]])`

```python
'hello world'.split()  # ['hello', 'world']
```

### `.rsplit([sep[, maxsplit]])`

```python
'one,two,three'.rsplit(',', 1)  # ['one,two', 'three']
```

### `join(iterable)`

```python
'-'.join(['hello', 'world'])  # 'hello-world'
```

## Testing and Validation

### `.startswith(prefix[, start[, end]])`

```python
'hello world'.startswith('hello')  # True
```

### `.endswith(suffix[, start[, end]])`

```python
'hello world'.endswith('world')  # True
```

### `.isalnum()`

```python
'hello123'.isalnum()  # True
```

### `.isalpha()`

```python
'hello'.isalpha()  # True
```

### `.isdigit()`

```python
'123'.isdigit()  # True
```

### `.isnumeric()`

```python
'⅕'.isnumeric()  # True
```

### `.isspace()`

```python
'   '.isspace()  # True
```

## MIscellaneous

### `len(str)`

```python
len('hello')  # 5
```

### `ord(char)` and `chr(codepoint)`

```python
ord('A')  # 65
chr(65)  # 'A'
```

### `eval()`

eval() evaluates a string as a Python expression and returns the result. It can be dangerous if used with untrusted input.

```python
result = eval('2 + 3 * 4')  # 14
result = eval('x + y', {'x': 1, 'y': 2})  # 3
result = eval('x + 2'.replace('x', '2'))  # 4
```
