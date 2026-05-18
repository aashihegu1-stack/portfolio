---
layout: post
title: Debugging
description: Notes and examples from CS 111 on debugging — reading errors, using print statements, and using a debugger.
permalink: /cs111/debugging
---

## What is Debugging?

Debugging is the process of finding and fixing problems in code. Every programmer spends a huge chunk of their time debugging — it's a skill, not a sign you did something wrong.

## Types of Bugs

- **Syntax errors** — the code won't even run (e.g., missing parenthesis).
- **Runtime errors** — the code runs, then crashes (e.g., dividing by zero).
- **Logic errors** — the code runs and finishes, but gives the wrong answer.

## Reading Error Messages

Always read the **last line** of an error first — it tells you what went wrong. Then read the traceback bottom-up to find the line in your code.

```
Traceback (most recent call last):
  File "main.py", line 4, in <module>
    print(10 / 0)
ZeroDivisionError: division by zero
```

## Print Debugging

The simplest debugger is `print()`.

```python
def average(nums):
    print("nums:", nums)        # check the input
    total = sum(nums)
    print("total:", total)      # check the math
    return total / len(nums)
```

## Using a Debugger

VS Code and most IDEs let you set **breakpoints** — the program pauses there so you can inspect every variable. Once you learn this, you'll wonder how you lived without it.

## A Strategy

1. Reproduce the bug reliably.
2. Narrow down where it happens.
3. Form a guess about why.
4. Test the guess.
5. Fix it — and make sure nothing else broke.

## Why it matters

Bugs are not failures, they're information. Good debugging skills make you faster, calmer, and a better problem-solver overall.
