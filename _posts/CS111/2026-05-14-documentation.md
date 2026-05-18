---
layout: post
title: Documentation
description: Notes and examples from CS 111 on documentation — comments, docstrings, READMEs, and naming.
permalink: /cs111/documentation
---

## What is Documentation?

Documentation is everything that explains your code to other people — including future you. Good code without documentation is still hard to use; documented code is reusable.

## Comments

Use comments to explain **why**, not what. The code already shows what.

```python
# Use binary search since the list is huge and sorted
index = binary_search(items, target)
```

## Docstrings

A docstring is a description right inside a function.

```python
def add(a, b):
    """Return the sum of a and b."""
    return a + b
```

Tools like `help(add)` will print the docstring back out.

## README Files

A README is a project's front door. A good one answers:
- What does this project do?
- How do I install and run it?
- How do I use it (with an example)?
- Who built it and how do I get help?

## Naming as Documentation

Clear names reduce the need for comments:

```python
# bad
x = u * 0.15

# good
tip = bill_total * tip_rate
```

## Why it matters

You will forget how your own code works within a few weeks. Documentation is a note to your future self — and a gift to anyone else who reads your work.
