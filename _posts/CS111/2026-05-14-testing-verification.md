---
layout: post
title: Testing & Verification
description: Notes and examples from CS 111 on testing and verification — unit tests, edge cases, and checking correctness.
permalink: /cs111/testing
---

## What is Testing?

Testing is how you prove your code does what it's supposed to do — not just on the happy path, but also when things get weird.

## Manual vs. Automated

- **Manual testing** — you run the program and try things by hand. Fine for tiny projects.
- **Automated testing** — you write code that tests your code. Scales much better.

## A Simple Unit Test

```python
def add(a, b):
    return a + b

def test_add():
    assert add(2, 3) == 5
    assert add(-1, 1) == 0
    assert add(0, 0) == 0

test_add()
print("All tests passed!")
```

If any `assert` is false, the program raises an error and you know exactly which case broke.

## Think About Edge Cases

When writing tests, ask:
- What's the smallest input? An empty one?
- What's the biggest input?
- What if the input is negative, zero, or a different type?
- What if a file is missing?

## Verification vs. Validation

- **Verification:** "Did we build the thing right?" (No bugs.)
- **Validation:** "Did we build the right thing?" (Solves the user's actual problem.)

You need both.

## Why it matters

Tests give you confidence to change code without breaking it. Without tests, every edit is a gamble. With tests, you know within seconds if you broke something.
