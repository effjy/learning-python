<div align="center">
<a href="https://github.com/effjy/learning-python/"><img src="titles/learning-python-title.svg" height="52" alt="Learning Python"></a>
</div>

# Learning to Code in Python — A Complete Beginner's Guide

Welcome! This document is a hands-on, from-scratch introduction to the **Python programming language**. It assumes you have *never written a line of Python* before. By the end you will understand what a program is, how to write and run one, how Python differs from lower-level languages, and you will have solved **5 exercises** that grow in difficulty.

Read it top to bottom the first time. Later you can jump back to any section as a reference.

> Coming from the C guide in this folder? Great — you will spot many shared ideas (variables, loops, functions). Python keeps the concepts but removes the ceremony: no compiler step, no semicolons, no manual memory management.

---

## Table of Contents

1. [What is Python and why learn it?](#1-what-is-python-and-why-learn-it)
2. [How Python runs your code (interpreting, not compiling)](#2-how-python-runs-your-code-interpreting-not-compiling)
3. [Setting up your tools](#3-setting-up-your-tools)
4. [Your first program, line by line](#4-your-first-program-line-by-line)
5. [Variables and data types](#5-variables-and-data-types)
6. [Operators and expressions](#6-operators-and-expressions)
7. [Input and output](#7-input-and-output)
8. [Control flow: if, elif, else](#8-control-flow-if-elif-else)
9. [Loops: while and for](#9-loops-while-and-for)
10. [Functions](#10-functions)
11. [Lists, tuples, dictionaries, and sets](#11-lists-tuples-dictionaries-and-sets)
12. [Strings in depth](#12-strings-in-depth)
13. [Errors and exceptions](#13-errors-and-exceptions)
14. [Files and modules](#14-files-and-modules)
15. [Coding style and indentation (PEP 8)](#15-coding-style-and-indentation-pep-8)
16. [The 5 Exercises](#16-the-5-exercises)
17. [Where to go next](#17-where-to-go-next)

---

## 1. What is Python and why learn it?

**Python** is a programming language created by Guido van Rossum and first released in 1991. It was designed around one big idea: **code should be easy for humans to read and write**. (The name comes from the British comedy troupe *Monty Python*, not the snake.)

Why it is one of the most popular languages in the world:

- **It reads almost like English.** Python deliberately avoids punctuation clutter. There are no curly braces and no semicolons; structure is shown with indentation. Beginners become productive in days, not weeks.
- **It is general-purpose.** Web sites (Instagram, YouTube backends), data science and machine learning (the entire AI field runs on Python), automation and scripting, scientific computing, finance, and education all rely on it heavily.
- **"Batteries included."** Python ships with a huge standard library, and the community has published hundreds of thousands of free packages (via `pip`) for almost any task imaginable.
- **It handles the tedious parts for you.** Unlike C, Python manages memory automatically, checks array bounds, and gives clear error messages instead of crashing silently.

The trade-off: that convenience has a cost. Python is generally **slower** than C and uses more memory, because the language does so much for you behind the scenes. For most tasks this does not matter — your time is more valuable than the computer's. When speed is critical, performance-sensitive parts are often written in C and called from Python (the best of both worlds).

> **Mental model:** If C hands you the keys to every room in the building, Python gives you a helpful concierge. You ask for what you want in plain terms, and it handles the details. You trade some control for a great deal of speed *in writing code*.

---

## 2. How Python runs your code (interpreting, not compiling)

This is the biggest practical difference from C, so we go slowly.

In C, you write source code, then a **compiler** translates the whole file into machine code *ahead of time*, producing an executable you run later. Python works differently: it is **interpreted**.

An **interpreter** is a program that reads your code and executes it **directly, line by line, as it goes** — no separate "build" step, no executable file to manage. You just run the source file.

```
your_code.py
     │
     ▼  python reads the file
The Python interpreter executes each statement, top to bottom
     │
     ▼
Output appears immediately
```

Under the hood Python does a quick internal step (it compiles your code to **bytecode** — a compact intermediate form stored in `.pyc` files — which the Python Virtual Machine then runs), but **you never have to think about this**. From your point of view there is exactly one command: run the file.

Two consequences that make Python beginner-friendly:

1. **Edit and run instantly.** Change your `.py` file, run it again, see the result. There is no compile-link cycle to forget. (Contrast with C, where forgetting to recompile is a classic confusion.)
2. **Interactive mode (the REPL).** Because Python executes statements one at a time, you can type code into a live prompt and see results immediately. This **REPL** (Read–Eval–Print Loop) is a fantastic learning playground — we use it in Section 3.

The trade-off, mentioned in Section 1: interpreting line by line is slower than running pre-compiled machine code. For learning and for the vast majority of real programs, you will never notice.

---

## 3. Setting up your tools

You need two things: **Python itself** (the interpreter) and a **text editor**.

### Installing Python

**On macOS / Linux:** Python is often pre-installed, but it may be an old version. Get the current one:
- **Linux (Debian/Ubuntu):** `sudo apt update && sudo apt install python3 python3-pip`
- **macOS:** install [Homebrew](https://brew.sh), then `brew install python`

**On Windows:** download the installer from [python.org/downloads](https://www.python.org/downloads/). **Important:** on the first screen, tick the box **"Add Python to PATH"** before clicking Install — this lets you run `python` from any terminal.

> Many systems have both Python 2 (ancient, retired in 2020) and Python 3. **Always use Python 3.** On Linux/macOS the command is often `python3` to be explicit.

### Verify it works

Open a terminal and type:
```bash
python3 --version
```
If you see something like `Python 3.12.1` rather than "command not found", you are ready. (On Windows it may simply be `python --version`.)

### The interactive interpreter (REPL)

Type `python3` with no filename and press Enter. You will get a `>>>` prompt where you can run code live:
```python
>>> 2 + 3
5
>>> print("Hello!")
Hello!
>>> name = "Sam"
>>> name
'Sam'
```
This is the perfect scratchpad for experimenting. Type `exit()` or press `Ctrl+D` (Linux/macOS) / `Ctrl+Z` then Enter (Windows) to leave.

### A text editor

Anything that saves plain text: **VS Code** (with the official Python extension) is the most popular and friendliest choice. Others: PyCharm, Sublime Text, Vim, Emacs. Avoid word processors — they add invisible formatting that breaks code.

### The run cycle

Save your code in a file ending in `.py`, then run it:
```bash
python3 hello.py
```
Breaking this down:
- `python3` — invoke the interpreter.
- `hello.py` — your source file. The interpreter reads and executes it top to bottom.

That is the entire cycle. No `-o`, no separate executable, no linking. Edit, save, re-run.

### Installing extra packages with `pip`

Python's package installer is `pip`. To add a third-party library:
```bash
pip3 install requests
```
This downloads and installs the `requests` package so you can `import` it in your code. (You will not need this for the exercises, but it is good to know it exists — it is one of Python's superpowers.)

> **Good habit (for later):** real projects use a **virtual environment** (`python3 -m venv venv`) to keep each project's packages separate. You do not need it now, but remember the term.

---

## 4. Your first program, line by line

Create a file called `hello.py` and type this in:

```python
print("Hello, world!")
```

Run it:
```bash
python3 hello.py
```
You should see:
```
Hello, world!
```

That is it — **one line**. Compare this to the C version, which needed `#include`, a `main` function, braces, and `return 0`. Python needs none of that ceremony. Let us understand exactly what this line does, then explore a slightly bigger version.

### `print("Hello, world!")`
- `print` is a **built-in function** — a ready-made command that comes with Python. It writes text to the screen.
- The **parentheses** `( )` *call* the function. Whatever you put inside is given to it as input (an **argument**).
- `"Hello, world!"` is a **string** — text wrapped in quotes. You can use double quotes `"..."` or single quotes `'...'`; both work identically in Python.
- There is **no semicolon** at the end. In Python, the end of a line *is* the end of a statement. (You may add a `;` but it is considered un-Pythonic and almost nobody does.)
- `print` automatically adds a newline at the end, so the cursor moves to the next line — no `\n` needed like in C (though `\n` still works inside strings if you want extra line breaks).

### A slightly bigger first program

```python
# This program greets the user by name.
name = input("What is your name? ")
print("Hello, " + name + "! Welcome to Python.")
```
Line by line:
- `# This program greets the user by name.` — a **comment**. Everything after `#` on a line is ignored by Python; it is a note for humans. (Python uses `#`, not C's `//` or `/* */`.)
- `name = input("What is your name? ")` — `input()` is a built-in that prints its prompt, waits for the user to type something and press Enter, and hands back what they typed as a **string**. The `=` stores that string in a variable named `name`.
- `print("Hello, " + name + "! Welcome to Python.")` — the `+` between strings **joins** (concatenates) them into one. So if the user typed `Sam`, this prints `Hello, Sam! Welcome to Python.`

### The most important rule in Python: indentation is meaningful

In C, indentation is just for looks — the compiler ignores it. **In Python, indentation is part of the syntax.** It is how Python knows which lines belong to a block. We will see this in every loop, `if`, and function from Section 8 onward. For now, just know: leading spaces are not decoration in Python — they have meaning.

---

## 5. Variables and data types

A **variable** is a name that refers to a value. Creating one is simple — just assign with `=`:
```python
age = 30
```
Read this as: "let the name `age` refer to the value `30`." Notice what is **missing** compared to C: you do **not** declare a type. Python figures out the type from the value automatically. This is called **dynamic typing**.

```python
age = 30          # Python sees an integer
age = "thirty"    # the SAME name can later refer to a string — perfectly legal
```
The name `age` is just a label; you can re-point it at any kind of value at any time. (This flexibility is powerful but means *you* must keep track of what a variable holds.)

### Checking a type
```python
x = 42
print(type(x))     # <class 'int'>
```
`type()` tells you what kind of value something is — handy when debugging.

### The core built-in types

| Type | What it stores | Example |
|------|----------------|---------|
| `int` | Whole numbers (no size limit!) | `-42`, `0`, `1000000000000` |
| `float` | Decimal numbers | `3.14`, `-0.5`, `2.0` |
| `str` | Text ("string") | `"hello"`, `'A'` |
| `bool` | True or false | `True`, `False` |
| `NoneType` | "nothing" / absence of a value | `None` |
| `list` | An ordered, changeable collection | `[1, 2, 3]` |
| `tuple` | An ordered, **un**changeable collection | `(1, 2, 3)` |
| `dict` | Key→value pairs | `{"name": "Sam", "age": 30}` |
| `set` | An unordered collection of unique items | `{1, 2, 3}` |

Notes:
- **`int` has no fixed size.** Unlike C's 4-byte `int`, a Python integer can be astronomically large — Python grows it automatically. `2 ** 1000` (2 to the power 1000) just works.
- **There is no separate `char` type.** A single character is simply a string of length 1.
- **`bool` values are capitalized:** `True` and `False` (not `true`/`false`).
- **`None`** is Python's "no value" placeholder, used when something is deliberately empty or not yet set. It is *not* the same as `0` or `""`.
- Collections (`list`, `dict`, etc.) get their own sections later — they are central to Python.

### Constants
Python has no true "constant" keyword. By **convention**, a name written in `ALL_CAPS` signals "do not change this":
```python
PI = 3.14159
MAX_USERS = 100
```
Nothing stops you from reassigning it, but other programmers will understand your intent.

### Naming rules
- Names may contain letters, digits, and underscores, but may **not start with a digit**.
- Names are **case-sensitive**: `age`, `Age`, and `AGE` are different.
- The Python convention is `lower_case_with_underscores` (called **snake_case**) for variables — e.g., `student_count`, not `studentCount`.
- Choose descriptive names. Clear code beats clever code.

---

## 6. Operators and expressions

An **operator** combines values to produce a new value. A combination of values and operators is an **expression** (e.g., `2 + 3` evaluates to `5`).

### Arithmetic operators
```python
a = 7
b = 2
a + b    # 9    addition
a - b    # 5    subtraction
a * b    # 14   multiplication
a / b    # 3.5  division — ALWAYS gives a float in Python 3
a // b   # 3    floor division — discards the fractional part
a % b    # 1    modulo: the remainder of a / b
a ** b   # 49   exponentiation: a to the power b
```
**Key difference from C:** in Python, `/` always produces a `float`. `7 / 2` is `3.5`, *not* `3`. If you want the C-style "throw away the decimals" behaviour, use the **floor division** operator `//`: `7 // 2` is `3`. This is a common source of confusion for people coming from other languages — Python split division into two clear operators.

### Assignment shortcuts
```python
x = 10
x += 5    # x = x + 5   → 15
x -= 3    # x = x - 3   → 12
x *= 2    # x = x * 2   → 24
x //= 5   # x = x // 5  → 4
x **= 2   # x = x ** 2  → 16
```
> Python has **no** `++` or `--` operators. Use `x += 1` to increment.

### Comparison operators (result is `True` or `False`)
```python
a == b    # equal to       (double equals)
a != b    # not equal to
a <  b    # less than
a >  b    # greater than
a <= b    # less than or equal
a >= b    # greater than or equal
```
As in C, a single `=` *assigns* and a double `==` *compares*. Happily, Python makes the `if (x = 5)` mistake impossible — it raises an error rather than silently assigning, so this whole class of bug disappears.

A Python nicety: you can **chain** comparisons just like maths:
```python
if 0 < age < 120:        # means (0 < age) AND (age < 120)
    print("plausible age")
```

### Logical operators
Python spells them out as English words (not C's `&&`, `||`, `!`):
```python
(a > 0) and (b > 0)    # True only if BOTH are true
(a > 0) or  (b > 0)    # True if EITHER is true
not (a > 0)            # flips True/False
```

### String operators
The arithmetic symbols do friendly things with strings:
```python
"foo" + "bar"     # 'foobar'   — + joins (concatenates) strings
"ab" * 3          # 'ababab'   — * repeats a string
```

### Operator precedence
As in maths, `**` happens first, then `*` `/` `//` `%`, then `+` `-`. When in doubt, **use parentheses** for clarity:
```python
2 + 3 * 4        # 14, because * goes first
(2 + 3) * 4      # 20, parentheses force the addition first
```

---

## 7. Input and output

### Output with `print`
You already met `print`. It is more capable than C's `printf` and far simpler — no format specifiers required:
```python
name = "Sam"
age = 30
print("Hello")                      # Hello
print(name, age)                    # Sam 30   (comma adds a space between items)
print("Age:", age)                  # Age: 30
```
`print` accepts any number of arguments separated by commas and prints them with a space in between, then a newline.

Useful options:
```python
print("no newline at end", end="")  # end="" suppresses the trailing newline
print("a", "b", "c", sep="-")       # a-b-c    (sep sets the separator)
```

### f-strings: the modern way to build text
The cleanest way to insert variables into text is an **f-string** — a string prefixed with the letter `f`. Put any variable or expression inside `{ }` and Python substitutes its value:
```python
name = "Sam"
age = 30
print(f"{name} is {age} years old.")        # Sam is 30 years old.
print(f"Next year: {age + 1}")              # Next year: 31
print(f"Pi is about {3.14159:.2f}")         # Pi is about 3.14   (.2f = 2 decimals)
```
This is the recommended approach in modern Python — readable and concise. The `:.2f` inside the braces is an optional **format specifier** (here: a float with 2 decimal places), echoing C's `%.2f` but tucked right next to the value.

### Input with `input`
`input()` reads a line the user types and returns it **as a string**:
```python
name = input("What is your name? ")
print(f"Hello, {name}!")
```

### The crucial gotcha: `input` always returns a string
Even if the user types digits, `input` gives you **text**, not a number. To do maths you must **convert** it with `int()` or `float()`:
```python
age_text = input("Enter your age: ")   # e.g. the string "30"
age = int(age_text)                    # convert to the integer 30
print(f"Next year you will be {age + 1}.")
```
If you skip the conversion, `age_text + 1` raises an error (you cannot add a number to text). You can also convert in one step:
```python
age = int(input("Enter your age: "))
```
- `int("30")` → `30`
- `float("3.5")` → `3.5`
- `str(30)` → `"30"` (the reverse: number to text)

> If the user types something that is not a number (like `"hello"`), `int()` raises a `ValueError`. Section 13 shows how to handle that gracefully.

---

## 8. Control flow: if, elif, else

By default, statements run top to bottom. **Control flow** lets your program make decisions.

This is where Python's **indentation rule** becomes concrete, so read carefully.

### `if`
```python
temperature = 30

if temperature > 25:
    print("It is hot.")
```
Several things to notice, all different from C:
- The condition needs **no parentheses** (though `if (temperature > 25):` also works, it is not the convention).
- The line **ends with a colon** `:`. The colon introduces a block.
- The body is marked by **indentation**, not braces `{ }`. Everything indented under the `if` belongs to it. When the indentation stops, the block is over.
- The standard indent is **4 spaces**. Be consistent — mixing tabs and spaces causes errors.

### `if` / `else`
```python
if temperature > 25:
    print("It is hot.")
else:
    print("It is not hot.")
```
`else` lines up with `if` (same indentation) and also ends with a colon. Exactly one block runs.

### `if` / `elif` / `else` chains
Python's keyword for "else if" is **`elif`** (one word):
```python
if score >= 90:
    print("Grade A")
elif score >= 80:
    print("Grade B")
elif score >= 70:
    print("Grade C")
else:
    print("Fail")
```
Conditions are checked **top to bottom**; the first true one runs and the rest are skipped. Order matters — checking `>= 70` first would mislabel an A student.

### What counts as true? "Truthiness"
A condition does not have to be a comparison. Python treats many values as true or false in a boolean context:
- **Falsy** (treated as false): `False`, `0`, `0.0`, `""` (empty string), `[]` (empty list), `{}` (empty dict), `None`.
- **Truthy** (treated as true): basically everything else — any non-zero number, any non-empty string or collection.

This enables clean idioms:
```python
name = input("Name: ")
if name:                       # true when name is not empty
    print(f"Hi {name}")
else:
    print("You entered nothing.")
```

### There is no `switch` (well, almost)
Older Python has no `switch` statement — you use `if`/`elif` chains. (Python 3.10+ added a `match` statement for advanced pattern matching, but `if`/`elif` is what you will use 95% of the time, so master that first.)

---

## 9. Loops: while and for

A **loop** repeats a block of code. Python has two: `while` and `for`. (There is no C-style `do-while`.)

### `while` — "repeat as long as a condition holds"
```python
i = 1
while i <= 5:
    print(i, end=" ")
    i += 1               # CRUCIAL: move toward ending the loop
# prints: 1 2 3 4 5
```
- The condition is checked before each pass; the indented body runs while it is true.
- **You must change something** inside the loop so the condition eventually becomes false, or you get an **infinite loop**. (Press `Ctrl+C` to stop a runaway program.)

### `for` — Python's loop is different (and better)
In C, `for` counts with an index. In Python, **`for` iterates directly over the items of a collection**. This is one of Python's most loved features:
```python
for fruit in ["apple", "banana", "cherry"]:
    print(fruit)
# prints each fruit on its own line
```
Read it as plain English: "for each fruit in this list, do the following." No index, no bounds, no off-by-one errors. You get the items themselves.

### Counting with `range`
When you *do* want to count, use `range`:
```python
for i in range(5):
    print(i, end=" ")
# prints: 0 1 2 3 4
```
`range(5)` produces the numbers `0, 1, 2, 3, 4` — **it starts at 0 and stops *before* the end value**. Other forms:
```python
range(2, 6)      # 2 3 4 5         (start, stop)
range(0, 10, 2)  # 0 2 4 6 8       (start, stop, step)
range(5, 0, -1)  # 5 4 3 2 1       (counting down)
```

### Looping with the index *and* the item: `enumerate`
When you need both the position and the value, `enumerate` gives you both:
```python
for index, fruit in enumerate(["apple", "banana"]):
    print(index, fruit)
# 0 apple
# 1 banana
```

### Controlling loops: `break` and `continue`
Same meaning as in C:
```python
for i in range(10):
    if i == 5:
        break        # leave the loop entirely
    if i % 2 == 0:
        continue     # skip to the next iteration
    print(i, end=" ")
# prints: 1 3
```
- `break` exits the loop immediately.
- `continue` skips the rest of this pass and starts the next one.

### Nested loops
Loops can contain loops, with each level indented further:
```python
for row in range(1, 4):
    for col in range(1, 4):
        print(f"({row},{col})", end=" ")
    print()          # newline after each row
```

---

## 10. Functions

A **function** is a reusable, named block of code. You have used `print`, `input`, `int`, `range`. Now you write your own. Functions let you **avoid repetition** and **break a big problem into small, named pieces**.

### Defining a function
```python
def add(a, b):
    result = a + b
    return result
```
- `def` is the keyword that **def**ines a function.
- `add` is the **name** you choose.
- `(a, b)` are the **parameters** — inputs the function receives. Notice: **no types are written** (Python is dynamically typed).
- The line ends with a **colon** `:`, and the body is **indented** — exactly like `if` and loops.
- `return result` hands a value back to whoever called the function and ends it.

### Calling a function
```python
total = add(3, 4)        # total becomes 7
print(total)
```
`add(3, 4)` runs the function with `a = 3` and `b = 4`; the whole expression evaluates to the returned value, `7`.

### Functions that return nothing
If you omit `return` (or write a bare `return`), the function gives back `None` automatically:
```python
def greet(name):
    print(f"Hello, {name}!")
    # no return → returns None
```

### Default parameter values
You can give a parameter a default, used when the caller omits it:
```python
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Sam")                  # Hello, Sam!
greet("Sam", "Welcome")       # Welcome, Sam!
```

### Keyword arguments
You can pass arguments by name, in any order, which makes calls self-documenting:
```python
greet(greeting="Hi", name="Sam")     # Hi, Sam!
```

### Returning multiple values
Unlike C, a Python function can easily return several values at once (as a tuple):
```python
def min_and_max(numbers):
    return min(numbers), max(numbers)

low, high = min_and_max([4, 1, 9, 2])    # low=1, high=9
```
The `low, high = ...` part is called **unpacking** — it spreads the returned pair into two variables.

### A note on order
Unlike C, Python does not need function "prototypes." A function just needs to be **defined before it is called at runtime**. The common pattern is to define your functions, then have the code that uses them at the bottom — often inside a `main()` function guarded by:
```python
def main():
    print(add(2, 5))

if __name__ == "__main__":
    main()
```
That last line means "only run `main()` if this file is being run directly" (not when it is imported by another file). It is a standard, professional Python idiom — you will see it everywhere.

### A quick word on scope
Variables created **inside** a function are **local** — they exist only while the function runs and are invisible outside it. This keeps functions self-contained and is generally what you want.

---

## 11. Lists, tuples, dictionaries, and sets

These four **collection types** are the heart of practical Python. Where C makes you manage fixed-size arrays by hand, Python gives you flexible, powerful containers that grow and shrink automatically.

### Lists — ordered, changeable sequences
A **list** holds an ordered series of items. Items can be of any type, and you can add or remove them freely.
```python
fruits = ["apple", "banana", "cherry"]

fruits[0]            # 'apple'    — indexing starts at 0
fruits[-1]           # 'cherry'   — negative indexes count from the end!
len(fruits)          # 3          — number of items

fruits.append("date")        # add to the end
fruits.remove("banana")      # remove by value
fruits[0] = "apricot"        # change an item in place
```
- **Indexing starts at 0**, like C. But Python adds **negative indexing**: `-1` is the last item, `-2` the second-to-last. Very handy.
- Unlike C arrays, **Python checks bounds**: `fruits[99]` raises a clear `IndexError` instead of corrupting memory. This safety is a big reason Python is beginner-friendly.

**Slicing** extracts a sub-section with `[start:stop]` (stop is excluded):
```python
nums = [10, 20, 30, 40, 50]
nums[1:3]     # [20, 30]
nums[:2]      # [10, 20]      (from the start)
nums[2:]      # [30, 40, 50]  (to the end)
```

**Looping over a list** (from Section 9):
```python
for fruit in fruits:
    print(fruit)
```

**List comprehensions** — a concise, very Pythonic way to build a list:
```python
squares = [n * n for n in range(5)]      # [0, 1, 4, 9, 16]
evens = [n for n in range(10) if n % 2 == 0]   # [0, 2, 4, 6, 8]
```
Read it as "give me `n * n` for each `n` in range(5)." It replaces a whole loop with one readable line.

### Tuples — ordered, *un*changeable sequences
A **tuple** is like a list but **immutable**: once created, it cannot be changed. Use round brackets:
```python
point = (3, 7)
point[0]          # 3
# point[0] = 5    # ERROR — tuples cannot be modified
```
Use a tuple for a fixed group of related values (like coordinates) that should not change. (Remember Section 10's multiple return values? Those come back as a tuple.)

### Dictionaries — key→value lookups
A **dictionary** (`dict`) stores pairs: each **key** maps to a **value**. It is perfect for labelled data and for fast lookups by name.
```python
person = {"name": "Sam", "age": 30}

person["name"]              # 'Sam'      — look up by key
person["age"] = 31          # change a value
person["city"] = "Paris"    # add a new key→value pair
"name" in person            # True       — test for a key

for key, value in person.items():
    print(key, "->", value)
```
Think of it as a real-world dictionary: you look up a word (key) to get its definition (value). Keys are usually strings; values can be anything.

### Sets — unordered collections of unique items
A **set** stores items with **no duplicates** and no defined order. Great for membership tests and removing duplicates:
```python
numbers = {1, 2, 2, 3, 3, 3}    # becomes {1, 2, 3} — duplicates dropped
3 in numbers                    # True
numbers.add(4)

# a classic use: remove duplicates from a list
unique = list(set([1, 1, 2, 3, 3]))   # [1, 2, 3]
```

### Quick comparison

| Type | Brackets | Ordered? | Changeable? | Duplicates? |
|------|----------|----------|-------------|-------------|
| `list` | `[ ]` | Yes | Yes | Yes |
| `tuple` | `( )` | Yes | No | Yes |
| `dict` | `{key: val}` | Yes (insertion) | Yes | Keys unique |
| `set` | `{ }` | No | Yes | No |

---

## 12. Strings in depth

A **string** is text. You met the basics in Section 4; here is the fuller picture, because strings are everywhere.

### Creating strings
```python
a = "double quotes"
b = 'single quotes'           # identical to double
c = """a string that spans
multiple lines"""             # triple quotes for multi-line text
```

### Strings are sequences
A string behaves much like a list of characters. You can index, slice, and loop over it:
```python
word = "Python"
word[0]        # 'P'
word[-1]       # 'n'
word[0:3]      # 'Pyt'   (slicing, just like lists)
len(word)      # 6
for letter in word:
    print(letter)
```
> **Strings are immutable.** Like tuples, you cannot change a character in place (`word[0] = "J"` is an error). Instead you build a new string.

### Handy string methods
Methods are functions attached to a value, called with a dot:
```python
text = "  Hello, World  "
text.lower()           # '  hello, world  '
text.upper()           # '  HELLO, WORLD  '
text.strip()           # 'Hello, World'   — removes surrounding whitespace
text.replace("l", "L") # '  HeLLo, WorLd  '
"a,b,c".split(",")     # ['a', 'b', 'c']   — split into a list
"-".join(["a", "b"])   # 'a-b'             — join a list into a string
"World" in text        # True              — substring test
text.strip().startswith("Hello")   # True
```
> Because strings are immutable, these methods **return a new string** — they do not modify the original. `text.lower()` gives you a lowercase copy; `text` itself is unchanged unless you reassign it.

### Building strings from values
Use f-strings (Section 7) — the cleanest way:
```python
name = "Sam"
score = 95.5
print(f"{name} scored {score:.1f}%")     # Sam scored 95.5%
```

### Converting between strings and numbers
```python
int("42")        # 42      — string to int
float("3.14")    # 3.14    — string to float
str(42)          # '42'    — number to string
```
This connects back to Section 7's input gotcha: `input()` always gives a string, so wrap it in `int()` or `float()` to do maths.

---

## 13. Errors and exceptions

When something goes wrong, Python **raises an exception** — it stops and reports the problem with a helpful message rather than crashing silently (a huge improvement over C's segfaults). Learning to read and handle these is essential.

### Reading an error message
```python
print(int("hello"))
```
produces:
```
Traceback (most recent call last):
  File "test.py", line 1, in <module>
    print(int("hello"))
ValueError: invalid literal for int() with base 10: 'hello'
```
Read it **bottom to top**: the last line names the **error type** (`ValueError`) and **what went wrong** (can't turn `"hello"` into an int). The lines above show **where** it happened (file and line number). This "traceback" is your best debugging friend — read it, do not panic.

### Common exception types
- `ValueError` — right type, wrong value (e.g., `int("hello")`).
- `TypeError` — wrong type (e.g., `"2" + 2`, adding text to a number).
- `NameError` — using a variable that does not exist (often a typo).
- `IndexError` — a list index out of range.
- `KeyError` — a dictionary key that does not exist.
- `ZeroDivisionError` — dividing by zero.
- `FileNotFoundError` — opening a file that is not there.

### Handling exceptions with `try` / `except`
Wrap risky code in `try`; handle problems in `except`:
```python
try:
    age = int(input("Enter your age: "))
    print(f"Next year you will be {age + 1}.")
except ValueError:
    print("That was not a valid whole number.")
```
- The `try` block runs normally.
- If an exception of the named type occurs, Python **jumps** to the matching `except` block instead of crashing.
- If no error occurs, the `except` block is skipped.

### The fuller form: `else` and `finally`
```python
try:
    number = int(input("Number: "))
except ValueError:
    print("Not a number.")
else:
    print(f"You entered {number}.")   # runs only if NO error happened
finally:
    print("Done.")                    # ALWAYS runs, error or not
```
- `else` runs only when the `try` succeeded.
- `finally` runs no matter what — useful for cleanup (like closing a file).

> **Good practice:** catch *specific* exceptions (`except ValueError:`), not a bare `except:` that hides every problem including your own typos. Specific handling keeps real bugs visible.

---

## 14. Files and modules

### Reading and writing files
Python makes file handling clean with the `with` statement, which **automatically closes the file** for you when the block ends — even if an error occurs.

**Writing to a file:**
```python
with open("notes.txt", "w") as f:      # "w" = write (overwrites!)
    f.write("First line\n")
    f.write("Second line\n")
```
**Reading from a file:**
```python
with open("notes.txt", "r") as f:      # "r" = read (the default)
    content = f.read()                 # whole file as one string
    print(content)
```
**Reading line by line** (memory-friendly for big files):
```python
with open("notes.txt", "r") as f:
    for line in f:                     # iterate one line at a time
        print(line.strip())            # strip() removes the trailing newline
```
The **mode** in `open` controls what you can do:
- `"r"` — read (file must exist). The default.
- `"w"` — write, **erasing any existing content**. Creates the file if needed.
- `"a"` — append: add to the end without erasing.

> The `with open(...) as f:` form is the standard, safe way. It guarantees the file is closed properly — no manual cleanup, unlike C's `fopen`/`fclose` pairing you must remember.

### Modules — using code from elsewhere
A **module** is a file of Python code you can reuse. The standard library has hundreds. Bring one in with `import`:
```python
import math
print(math.sqrt(16))      # 4.0
print(math.pi)            # 3.141592653589793

import random
print(random.randint(1, 6))    # a random integer from 1 to 6

from datetime import datetime
print(datetime.now())     # the current date and time
```
- `import math` loads the whole module; you then prefix its tools with `math.`.
- `from datetime import datetime` pulls one specific name in so you can use it directly.

A few standard modules worth knowing: `math` (maths functions), `random` (randomness), `datetime` (dates and times), `os` (operating-system tasks), `json` (read/write JSON data), `sys` (interpreter and command-line access).

> Beyond the standard library, `pip install` (Section 3) gives you the vast third-party ecosystem — `requests` for web, `numpy`/`pandas` for data, `flask`/`django` for web apps, and far more.

---

## 15. Coding style and indentation (PEP 8)

Python's official style guide is called **PEP 8**. Following it makes your code instantly familiar to every other Python programmer. Crucially, in Python **indentation is not optional styling — it is part of the language**, so getting it right is mandatory, not merely polite.

### Indentation is syntax
In C, bad indentation is ugly but compiles. **In Python, wrong indentation is a syntax error** or, worse, silently changes meaning. The block structure *is* the indentation.
```python
# This loop prints 0,1,2 then "Done" once:
for i in range(3):
    print(i)
print("Done")          # OUTSIDE the loop (not indented)

# Move "Done" inside and it prints three times:
for i in range(3):
    print(i)
    print("Done")      # INSIDE the loop (indented)
```
The only difference is four spaces — and it changes the program's behaviour. Indentation carries meaning in Python.

### The PEP 8 essentials
- **Indent with 4 spaces per level.** Never use tabs, and **never mix tabs and spaces** — Python will reject it. (Configure your editor to insert 4 spaces when you press Tab.)
- **`snake_case`** for variables and functions: `student_count`, `calculate_total`.
- **`ALL_CAPS`** for constants: `MAX_SIZE`.
- **Spaces around operators:** `x = a + b`, not `x=a+b`.
- **A space after commas:** `func(a, b, c)`, not `func(a,b,c)`.
- **Two blank lines** between top-level functions; keep lines reasonably short (PEP 8 suggests ≤ 79 characters).
- **Comment the *why*, not the obvious *what*.** Good names reduce the need for comments.

### Docstrings
Document what a function does with a **docstring** — a string on the first line of the body:
```python
def area(radius):
    """Return the area of a circle with the given radius."""
    return 3.14159 * radius ** 2
```
Tools and editors display docstrings as help text.

### Automatic formatters and linters
Let tools enforce style so you can focus on logic:
- **`black`** — reformats your code to a consistent style instantly: `black myfile.py`
- **`flake8`** or **`ruff`** — *linters* that flag style issues and likely bugs.

Install with `pip install black ruff` and run them on your files. Professional teams do this automatically.

---

## 16. The 5 Exercises

Work through these in order — each uses ideas from the one before. **Try to solve each yourself first.** A full worked solution follows every problem, but you learn by struggling, not by reading.

For each exercise: create a `.py` file and run it with `python3 file.py`.

---

### Exercise 1 — Hello, *you* (variables + output)

**Goal:** Print a personalized greeting using variables and an f-string.

**Task:** Create a variable for your name and one for your age. Print a sentence like: `Hi, my name is Alex and I am 25 years old.`

**Concepts:** variables (Section 5), f-strings (Section 7).

<details>
<summary>Show solution</summary>

```python
name = "Alex"
age = 25

print(f"Hi, my name is {name} and I am {age} years old.")
```
**Why it works:** Inside the f-string, `{name}` and `{age}` are replaced by the variables' values. No type declarations, no format specifiers — Python figures it out. Compare this to the C version, which needed `%s` and `%d` lined up with separate arguments.
</details>

---

### Exercise 2 — Even or odd (input + conditionals)

**Goal:** Read a number and decide whether it is even or odd.

**Task:** Ask the user for an integer with `input`, convert it with `int`, use the modulo operator `%`, and print `"even"` or `"odd"`.

**Concepts:** `input` and `int()` conversion (Section 7), `if`/`else` (Section 8), `%` (Section 6).

<details>
<summary>Show solution</summary>

```python
number = int(input("Enter an integer: "))   # convert text to a number!

if number % 2 == 0:                          # remainder 0 → divisible by 2
    print(f"{number} is even.")
else:
    print(f"{number} is odd.")
```
**Why it works:** `input()` returns a string, so we wrap it in `int()` to get a number we can do maths on (the #1 beginner gotcha). `number % 2` is the remainder after dividing by 2 — `0` for even, `1` for odd. Note `==` (compare), not `=` (assign).
</details>

---

### Exercise 3 — Sum and average of a list (loops + lists)

**Goal:** Read several numbers into a list, then report their sum and average.

**Task:** Ask the user how many numbers they have. Use a loop to read that many numbers into a **list**. Compute and print the sum and the average.

**Concepts:** lists and `append` (Section 11), `for`/`range` loops (Section 9), built-in `sum` and `len`.

<details>
<summary>Show solution</summary>

```python
count = int(input("How many numbers? "))
numbers = []                               # start with an empty list

for i in range(count):
    value = float(input(f"Number {i + 1}: "))
    numbers.append(value)                  # grow the list as we go

total = sum(numbers)                       # built-in: adds all items
average = total / len(numbers)             # len gives the count

print(f"Sum: {total}")
print(f"Average: {average:.2f}")
```
**Why it works:** A list starts empty and grows with `.append()` — no fixed size to declare (unlike a C array). `range(count)` runs the loop `count` times. The built-in `sum()` adds every item, and `len()` counts them, so the average is just `total / len(numbers)`. Because Python's `/` always gives a float, the average is a true decimal automatically — no casting needed. `:.2f` formats it to two decimal places.

*Bonus — the whole input loop as a one-line comprehension:*
```python
numbers = [float(input(f"Number {i + 1}: ")) for i in range(count)]
```
</details>

---

### Exercise 4 — A reusable function: is it prime? (functions + loops)

**Goal:** Write a function that tests whether a number is prime, and use it.

**Task:** Write `is_prime(n)` that returns `True` if `n` is prime and `False` otherwise. Then print all primes from 2 to 50 using it.

**Concepts:** functions (Section 10), returning booleans, loops (Section 9), `range`.

<details>
<summary>Show solution</summary>

```python
def is_prime(n):
    """Return True if n is a prime number, False otherwise."""
    if n < 2:
        return False                  # 0 and 1 are not prime
    for divisor in range(2, int(n ** 0.5) + 1):
        if n % divisor == 0:          # found a factor → not prime
            return False
    return True                       # no factors found → prime


primes = [n for n in range(2, 51) if is_prime(n)]
print("Primes from 2 to 50:")
print(primes)
```
**Why it works:** A prime has no divisors other than 1 and itself. We only need to test divisors up to the square root of `n` — `n ** 0.5` is the square root, and `range(2, int(n ** 0.5) + 1)` covers `2` up to that. The moment we find any factor, we `return False` early. If the loop finishes with none, the number is prime, so we `return True`. The list comprehension then keeps every `n` from 2 to 50 for which `is_prime(n)` is true — a whole filtering loop in one readable line.
</details>

---

### Exercise 5 — A to-do list saved to a file (dicts + files + exceptions)

**Goal:** Combine everything: manage a list of tasks (stored as dictionaries), let the user add tasks in a loop, and save them to a file.

**Task:** Repeatedly ask the user to enter a task (an empty line stops). Store each task as a dictionary with a `description` and a `done` flag in a list. Print the list, then save it to `todo.txt`. Handle the case where the user types nothing gracefully.

**Concepts:** lists + dictionaries (Section 11), `while` loops (Section 9), files (Section 14), f-strings, truthiness (Section 8).

<details>
<summary>Show solution</summary>

```python
def main():
    tasks = []                                  # a list of dicts

    print("Enter your tasks. Press Enter on an empty line to finish.")
    while True:                                 # loop until we break
        description = input("Task: ").strip()
        if not description:                     # empty string is "falsy"
            break                               # stop collecting
        tasks.append({"description": description, "done": False})

    if not tasks:                               # nothing was entered
        print("No tasks added. Goodbye!")
        return

    # Show the list on screen.
    print("\nYour to-do list:")
    for i, task in enumerate(tasks, start=1):   # number from 1
        mark = "x" if task["done"] else " "
        print(f"  {i}. [{mark}] {task['description']}")

    # Save it to a file.
    with open("todo.txt", "w") as f:
        for task in tasks:
            mark = "x" if task["done"] else " "
            f.write(f"[{mark}] {task['description']}\n")

    print(f"\nSaved {len(tasks)} task(s) to todo.txt")


if __name__ == "__main__":
    main()
```
**Why it works, piece by piece:**
- `tasks = []` is a list that will hold **dictionaries**, each bundling a description with a done-flag — Python's flexible answer to C's `struct`.
- `while True:` loops forever until an explicit `break`. We break when the user enters an empty line: `if not description` is true for the empty string (recall "truthiness" — `""` is falsy).
- `.strip()` removes stray spaces so a line of only spaces also counts as empty.
- `tasks.append({...})` adds a new dictionary to the list each time.
- `enumerate(tasks, start=1)` gives us both a counter (starting at 1) and each task, so we can print a numbered list.
- `"x" if task["done"] else " "` is Python's **conditional expression** (the ternary): `value_if_true if condition else value_if_false`.
- `with open("todo.txt", "w") as f:` opens the file for writing and **closes it automatically** when the block ends — no manual cleanup. We write one line per task.
- The `if __name__ == "__main__": main()` guard runs `main()` only when the file is executed directly (Section 10).

*Run it, then look at the created `todo.txt` — your tasks are saved on disk!*
</details>

---

## 17. Where to go next

You now know the core of Python: types, operators, I/O, control flow, loops, functions, the four collection types, strings, exceptions, files, and modules. That is genuinely enough to write real, useful programs. Mastery comes from *practice*, not from collecting more features.

Suggested next steps:
- **Build small programs:** a number-guessing game, a unit converter, a quiz, a simple budget tracker that saves to a file.
- **Learn `classes` and object-oriented programming** — the next big concept (`class`, `self`, methods). Python's collections and many libraries are built on it.
- **Explore the standard library:** `random`, `datetime`, `json`, `os`, `collections`. Skim the docs at [docs.python.org](https://docs.python.org/3/).
- **Try a third-party package:** `requests` to fetch web pages, or `pandas` if you are curious about data.
- **Use the tools:** format with `black`, lint with `ruff`, and debug by reading tracebacks carefully (Section 13).
- **Read:** the official [Python Tutorial](https://docs.python.org/3/tutorial/) and *Automate the Boring Stuff with Python* (free online) are excellent, beginner-friendly next reads.

**The single most important habit:** experiment constantly. Open the REPL (`python3`), try things, and read the error messages when they appear — Python's errors are written to help you. The language rewards curiosity.

Happy coding! 🐍
