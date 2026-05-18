---
layout: post
title: Input/Output
description: Notes and examples from CS 111 on input and output — reading user input, printing, and file I/O.
permalink: /cs111/input-output
---

## What is Input/Output?

I/O is how a program talks to the world. **Input** is what flows in (from the user, a file, the network). **Output** is what flows out (to the screen, a file, another program).

## Reading User Input

```python
name = input("What is your name? ")
print("Hello, " + name + "!")
```

`input()` always returns a string — convert it if you need a number.

```python
age = int(input("How old are you? "))
```

## Printing Output

```python
print("Hello")
print("x =", 5, "and y =", 10)
print(f"My name is {name}")   # f-string
```

## File I/O

```python
# Writing
with open("notes.txt", "w") as f:
    f.write("Hello, file!")

# Reading
with open("notes.txt", "r") as f:
    contents = f.read()
print(contents)
```

The `with` block automatically closes the file for you — much safer than `open()` / `close()` by hand.

## Why it matters

A program with no I/O is invisible. Input/Output is what makes a program useful to real people.
