---
layout: post
title: "Python: List Comprehensions"
date: 2026-01-09
categories: [python]
tags: [fundamentals, syntax]
---

## Overview

List comprehensions provide a concise way to create lists in Python. They're more readable and often faster than traditional for loops for simple transformations and filtering operations.

## Basic Syntax

```python
# Traditional approach
squares = []
for i in range(10):
    squares.append(i**2)

# List comprehension
squares = [i**2 for i in range(10)]
```

## Key Points

- **More Pythonic**: Considered idiomatic Python code
- **More efficient**: Often faster than equivalent for loops
- **Readable**: Intent is clear for simple operations
- **Single expression**: The entire comprehension returns a new list

## Common Use Cases

### Transforming Data
```python
# Convert to uppercase
names = ['alice', 'bob', 'charlie']
upper_names = [name.upper() for name in names]
# Result: ['ALICE', 'BOB', 'CHARLIE']
```

### Filtering
```python
# Get even numbers
numbers = [1, 2, 3, 4, 5, 6]
evens = [n for n in numbers if n % 2 == 0]
# Result: [2, 4, 6]
```

### Combining Transform + Filter
```python
# Square of even numbers only
numbers = [1, 2, 3, 4, 5, 6]
even_squares = [n**2 for n in numbers if n % 2 == 0]
# Result: [4, 16, 36]
```

### Nested Comprehensions
```python
# Flatten a 2D matrix
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flat = [num for row in matrix for num in row]
# Result: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## Gotchas & Best Practices

**Watch out for:**
- **Complexity**: Don't sacrifice readability for brevity. If it's complex, use a regular loop
- **Side effects**: List comprehensions are for creating lists, not executing side effects
- **Nested comprehensions**: More than 2 levels becomes hard to read

**Best practices:**
- Keep it simple - if you need more than one `if` or complex logic, use a function
- Use parentheses for clarity when needed
- Consider generator expressions for large datasets (use `()` instead of `[]`)

## Practical Example

Real-world scenario: Processing user data

```python
# Extract valid email addresses from user data
users = [
    {'name': 'Alice', 'email': 'alice@example.com', 'active': True},
    {'name': 'Bob', 'email': None, 'active': False},
    {'name': 'Charlie', 'email': 'charlie@example.com', 'active': True},
]

# Get emails of active users
active_emails = [
    user['email']
    for user in users
    if user['active'] and user['email']
]
# Result: ['alice@example.com', 'charlie@example.com']
```

## Related Concepts

- **Dictionary comprehensions**: `{k: v for k, v in items}`
- **Set comprehensions**: `{x for x in list}`
- **Generator expressions**: `(x for x in list)` - lazy evaluation
- **Filter/Map functions**: Functional programming alternatives

## References

- [Python Docs - List Comprehensions](https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions)
- [PEP 202 - List Comprehensions](https://www.python.org/dev/peps/pep-0202/)
