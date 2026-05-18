---
layout: post
title: Control Structures
description: Notes and examples from CS 111 on control structures — conditionals, loops, and branching logic.
permalink: /cs111/control-structures
---

## What are Control Structures?

Control structures decide **what code runs** and **how many times** it runs. They are the building blocks for any kind of decision-making or repetition in a program.

## Conditional Statements

`if`, `elif`, and `else` let your program react to different situations.

```python
score = 85
if score >= 90:
    print("A")
elif score >= 80:
    print("B")
else:
    print("Keep practicing!")
```

## Loops

- **`for` loops** repeat once for each item in a collection.
- **`while` loops** repeat as long as a condition is true.

```python
for i in range(5):
    print(i)

count = 0
while count < 3:
    print("Hello")
    count += 1
```

## Why it matters

Without control structures, code just runs top to bottom. With them, programs can respond to input, repeat tasks, and handle different cases — which is what makes software actually useful.
