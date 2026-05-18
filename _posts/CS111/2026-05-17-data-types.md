---
layout: post
title: Data Types
description: Notes and examples from CS 111 on data types — strings, numbers, booleans, lists, and dictionaries.
permalink: /cs111/data-types
---

## What are Data Types?

A data type tells the computer what kind of value a variable holds and what you can do with it. Picking the right type makes code clearer and prevents bugs.

## Primitive Types

| Type | Example | Description |
|------|---------|-------------|
| `int` | `42` | Whole numbers |
| `float` | `3.14` | Decimal numbers |
| `str` | `"hello"` | Text |
| `bool` | `True` / `False` | Yes/no values |

## Collection Types

```python
# List — ordered, changeable
grades = [85, 92, 78]

# Tuple — ordered, locked
point = (3, 4)

# Dictionary — key/value pairs
student = {"name": "Aashi", "grade": "A"}

# Set — unique items only
unique_scores = {85, 92, 85, 78}  # becomes {85, 92, 78}
```

## Type Conversion

```python
age = int("21")     # string to int
price = float("9.99")
text = str(100)
```

## Why it matters

The wrong type causes a lot of beginner bugs — like adding `"5" + 3` and getting an error. Knowing types up front saves debugging time later.
