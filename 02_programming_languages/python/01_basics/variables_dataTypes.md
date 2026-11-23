# ${\color{#7C4DFF}\textsf{Python Variables, Data Types, Operators, Input and Output}}$

## ${\color{#7C4DFF}\textsf{Theory}}$

### ${\color{#7C4DFF}\textsf{Definition and Purpose}}$

- A **variable** is a name bound to an object. A name lets you reuse a value, such as a birth year or a calculated score. An object's **data type** determines the operations the object supports.
- An **operator** acts on one or more operands. In `a + b`, `+` is the operator and `a` and `b` are the operands.
- A console program can **read** data with `input()`, **process** it with expressions, and **write** the result with `print()`. Both functions are built in and are available without imports. A script can call them directly at the top level.

### ${\color{#7C4DFF}\textsf{Syntax}}$

#### ${\color{#7C4DFF}\textsf{Variables and Assignment}}$

| Form | How to read it |
|---|---|
| `name = expression` | Evaluate `expression` and bind its result to `name`. The same form creates a binding or updates an existing one. |
| `first, second = expression1, expression2` | Evaluate the right-hand expressions and assign their results to the targets in order. An iterable such as a list can also supply the values. |
| `first = second = expression` | Evaluate the expression once and bind both names to the resulting object. |
| `name += expression` | Apply addition and assign the result back to the target. This is one form of **augmented assignment**. |
| `name: int = expression` | Add a type annotation to the assignment. A normal Python assignment does not enforce that annotation. |

#### ${\color{#7C4DFF}\textsf{Data Types and Literals}}$

A **literal** writes a value directly in source code. `type(value)` returns the object's type.

| Type | Purpose | Example |
|---|---|---|
| `int` | Whole numbers, including zero and negative values | `42`, `0`, `-5` |
| `float` | Floating-point numbers | `3.14`, `-0.5`, `2e2` (200.0), `4E3` (4000.0) |
| `str` | Unicode text, including a single character or an empty string | `"Hello, World!!!"`, `'A'`, `""` |
| `bool` | Truth values | `True`, `False` |
| `NoneType` | A placeholder for the absence of a value | `None` |
| `complex` | Numbers with real and imaginary parts | `2 + 3j` |
| `list` | An ordered, mutable collection | `[7, 8]` |
| `tuple` | An ordered, immutable sequence | `(7, 8)` |
| `dict` | A mapping from keys to values | `{"math": 7.5}` |
| `set` | A collection of distinct elements | `{7, 8}` |

#### ${\color{#7C4DFF}\textsf{Operators}}$

| Group | Operators or form | Purpose |
|---|---|---|
| Arithmetic operators | `+`, `-`, `*`, `/`, `//`, `%`, `**` | Add, subtract, multiply, divide, floor-divide, take the remainder, or raise to a power. Unary `+x` and `-x` apply a sign to one operand. |
| Assignment and augmented assignment | `=`, `+=`, `-=`, `*=`, `/=`, `//=`, `%=`, `**=` | Bind a value or update a target with the result of an operation. `=` is assignment statement syntax. |
| Comparison operators | `==`, `!=`, `<`, `<=`, `>`, `>=` | Compare equality or order. `==` tests equality. |
| Logical operators | `and`, `or`, `not` | Combine or negate truth tests. |
| Membership operators | `in`, `not in` | Check whether an element belongs to a container or a substring occurs in a string. |
| Identity operators | `is`, `is not` | Check whether two references point to the same object. Use `value is None` to test for `None`. |
| Bitwise operators | `&`, `\|`, `^`, `~`, `<<`, `>>` | On integers, apply bitwise AND, OR, XOR, complement, left shift, or right shift. |
| Conditional expression (ternary operator) | `value_if_true if condition else value_if_false` | Choose one of two values according to the condition. |

`&=`, `|=`, `^=`, `<<=`, and `>>=` are bitwise augmented assignment forms. `@` and `@=` are for operand types that implement matrix multiplication. An **assignment expression**, such as `(name := expression)`, both binds a name and yields the assigned value.

#### ${\color{#7C4DFF}\textsf{Console Input and Output}}$

| Form | Use |
|---|---|
| `text = input()` | Read one line of text. |
| `text = input(prompt)` | Display `prompt`, then read one line of text. |
| `number = int(input())` | Read one line and convert it to an integer. |
| `number = float(input())` | Read one line and convert it to a floating-point number. |
| `first, second = map(int, input().split())` | Read two integers from a single whitespace-separated line. Use `float` in place of `int` for decimal input. |
| `numbers = list(map(int, input().split()))` | Read a whitespace-separated line into a list of integers. |
| `print(value1, value2, sep=" ", end="\n")` | Write values with the given separator and ending. Each value is a separate argument. `sep` and `end` have the defaults shown. |
| `print(f"{value:.2f}")` | Format a value inside an f-string. `:.2f` specifies fixed-point output with two digits after the decimal point. |
| `print("{0:.2f}".format(value))` | Apply the same format through `str.format()`. `0` identifies the first argument. |

### ${\color{#7C4DFF}\textsf{Behavior}}$

#### ${\color{#7C4DFF}\textsf{Name Binding and Conversion}}$

- Python is **dynamically typed**. A name can refer to an `int` after one assignment and a `str` after the next. For a numeric variable, `count += 1` has the same effect as `count = count + 1`. Rebinding one name leaves other names pointing to their existing objects. Two names that share a mutable object can both observe a change made to that object. For example, `items += [8]` updates a built-in list in place.
- `int("42")` parses an integer. `int(-3.9)` converts a float by truncating toward zero, producing `-3`. `float("3.14")` parses a decimal as a float, and `str(42)` creates the string `"42"`. `bool(value)` tests truthiness. `None`, numeric zero, and empty strings and collections are false in a truth test. A nonempty string such as `"False"` is true.

#### ${\color{#7C4DFF}\textsf{Arithmetic and Evaluation Order}}$

| Expression | Result | Why |
|---|---|---|
| `9 + 2`, `9 - 2`, `9 * 2` | `11`, `7`, `18` | Addition, subtraction, and multiplication of integers. |
| `9 / 2` | `4.5` | True division of two integers returns a `float`. |
| `9 // 2`, `9.0 // 2.0` | `4`, `4.0` | Floor division rounds the quotient down. A floating-point operand gives a floating-point result. |
| `-9 // 2`, `int(-9 / 2)` | `-5`, `-4` | The floor of `-4.5` is `-5`. Truncation toward zero gives `-4`. |
| `9 % 2`, `9.0 % 2.0`, `-9 % 2` | `1`, `1.0`, `1` | The modulo result is zero or has the divisor's sign. For integers, `a == (a // b) * b + (a % b)` when `b` is nonzero. |
| `9 ** 2`, `2 ** 3 ** 2` | `81`, `512` | Powers group from right to left. `2 ** (3 ** 2)` is `2 ** 9`. |
| `-2 ** 2`, `(-2) ** 2`, `2 ** -2` | `-4`, `4`, `0.25` | A leading unary minus applies after a power. The exponent may itself be negative. |
| `10 * (2 + 3) - 3` | `47` | Grouped addition happens first, followed by multiplication and subtraction. |

From higher to lower precedence, the main groups here are `**`, unary `+`/`-`/`~`, `*`/`@`/`/`/`//`/`%`, `+`/`-`, shifts, `&`, `^`, `|`, comparisons (including membership and identity), `not`, `and`, `or`, and the conditional expression. Parentheses explicitly group an expression. Power has the unary-operator behavior shown above. Comparisons can chain. `0 <= score < 10` checks both inequalities with `score` evaluated once.

`and` and `or` **short-circuit**. `a and b` returns `a` if it is falsey and otherwise evaluates and returns `b`. `a or b` returns `a` if it is truthy and otherwise evaluates and returns `b`. `not` returns a `bool`. A conditional expression evaluates only the branch it selects.

#### ${\color{#7C4DFF}\textsf{Reading and Printing a Line}}$

- `input()` reads one line from standard input and returns a `str` with its trailing newline removed. For input `7 8`, `.split()` produces `["7", "8"]`. `map(int, ...)` converts each token as it is consumed. Unpacking binds the resulting `7` and `8` to the two names. With no delimiter, `split()` treats runs of whitespace as one separator and ignores leading or trailing whitespace.
- `print()` writes text to standard output by default. It converts each argument to text, inserts `sep` between arguments, and appends `end`. `print()` with no values writes just the ending. An f-string or `str.format()` builds a string before `print()` writes it. Formatting a float to one or two decimal places changes its display, while the stored value is available for later calculations.

### ${\color{#7C4DFF}\textsf{Rules and Boundaries}}$

| Area | Rule and consequence |
|---|---|
| Identifier spelling | An ASCII identifier starts with a letter or `_`, followed by letters, digits, or `_`. Python also accepts permitted Unicode identifier characters. Names are case-sensitive. Keywords, spaces, leading digits, and hyphens are invalid in variable names. Assignments such as `1st_year = 2020` and `birth-year = 2020` raise `SyntaxError`. PEP 8 recommends `snake_case`, such as `birth_year`. |
| Reading a name | A name must be bound in an accessible scope before it is read. An unresolved name raises `NameError`. Reading a function-local name before it has been assigned raises `UnboundLocalError`. Using names such as `input`, `print`, or `int` for your own values can hide the built-ins. |
| Numeric representation | `int` uses arbitrary precision, subject to resources such as available memory. `float` has finite range and precision, so values such as `0.1` are typically approximations and results such as `0.1 + 0.2` can display as `0.30000000000000004`. Check `sys.float_info` for the interpreter's limits. |
| Operand types | With built-in numeric operands, `int + float` produces a float. `str + str` concatenates and `str * int` repeats. `"7" + 8` raises `TypeError`. Convert the text with `int()` for arithmetic. For built-in integers or floats, `/`, `//`, and `%` raise `ZeroDivisionError` when the divisor is zero. |
| Incrementing and decrementing | Write `count += 1` or `count -= 1`. The C++ and Java postfix forms `count++` and `count--` are invalid Python syntax. |
| Input errors | `input()` raises `EOFError` if no line remains. `int("7.1")` and `float("abc")` raise `ValueError`. When unpacking into `a, b`, Python expects exactly two values, so one or three valid numbers on the line also raise `ValueError`. |
| Online judge output | Read the line layout given in the problem's **Input** section. Match the **Output** section's required text, spacing, line breaks, and decimal precision. Use prompt-free `input()` in a submission that expects only the result. |

### ${\color{#7C4DFF}\textsf{Related Forms}}$

| If you need to… | Use this form |
|---|---|
| Read a name, a sentence, or a code with leading zeros | `input()` keeps the line as text. |
| Read numbers on separate lines | Use one call per line, such as `a = int(input())` followed by `b = int(input())`. Use `float` for decimal input. |
| Read a fixed number of values from one line | Unpack `map(int, input().split())` or `map(float, input().split())` into the expected number of variables. |
| Print values with one repeated separator | Pass each value to `print()` and set `sep` if needed. |
| Build an equation, a label, or a number with fixed decimal places | Use an f-string such as `f"{value:.1f}"`. Use `str.format()` with `{0}`, `{1}`, and `{2}` when working with a format string that receives arguments by position. |

## ${\color{#276BD1}\textsf{Code Example}}$

### ${\color{#276BD1}\textsf{Example Setup}}$

Each implementation is a complete Python 3.12 program. Save each block to the indicated `.py` file and run it with `python filename.py` or `python3 filename.py`, depending on your Python installation. The input blocks below contain the lines to enter, in order.

| Program | Starting values or input | Demonstrates |
|---|---|---|
| `variables.py` | Enter `1998` | A variable first holds input text, then an integer. Computing `2018 - birth_year` gives the age reached in 2018. |
| `operators.py` | No input | Arithmetic, negative floor division, augmented assignment, and the other operator groups. |
| `read_numbers.py` | Enter two integer lines, two decimal lines, one integer pair, then one decimal pair | The four numeric input layouts from the lecture. |
| `format_output.py` | No input | Hello World, printing numbers, custom separators and line endings, and formatted output. |
| `total_candy.py` | Enter `7 8` | Read two integers from one line and print their sum. |
| `total_score.py` | Enter `7.5 8.0 9.0` on one line | Read three scores and print their sum with one digit after the decimal point. This example chooses a single-line input layout. |
| `digit_score.py` | Enter `52794` | Extract five decimal digits and compute the last digit of their sum. |

### ${\color{#276BD1}\textsf{Implementation}}$

#### ${\color{#276BD1}\textsf{Variables and Types}}$

```python
# variables.py
birth_year = input()
print(type(birth_year).__name__)

birth_year = int(birth_year)
print(type(birth_year).__name__)

reference_year = 2018
age_that_year = reference_year - birth_year
print(age_that_year)
```

#### ${\color{#276BD1}\textsf{Operators}}$

```python
# operators.py
print(9 + 2, 9 - 2, 9 * 2, 9 / 2, 9 % 2, 9 ** 2, 9 // 2)
print(9.0 % 2.0, 9.0 // 2.0)
print(-9 // 2, -9 % 2, int(-9 / 2))
print(10 * (2 + 3) - 3)

value = 10
value += 2
value -= 2
value *= 2
value /= 2
print(value, type(value).__name__)

value **= 2
value //= 2
value %= 2
print(value, type(value).__name__)

score = 7
print(0 <= score < 10, score > 0 and score != 7, "Py" in "Python")
print(5 & 3, "pass" if score >= 5 else "retry")

first = [7]
second = [7]
print(first == second, first is second)
```

#### ${\color{#276BD1}\textsf{Reading Integers and Decimals}}$

```python
# read_numbers.py
first_int = int(input())
second_int = int(input())

first_float = float(input())
second_float = float(input())

left_int, right_int = map(int, input().split())
left_float, right_float = map(float, input().split())

print(first_int, second_int)
print(first_float, second_float)
print(left_int, right_int)
print(left_float, right_float)
```

#### ${\color{#276BD1}\textsf{Formatting Output}}$

```python
# format_output.py
print("Hello, World!!!")
print(3, 3.14, 4E3)

a, b = 5, 7
total = a + b
print("{0} + {1} = {2}".format(a, b, total))
print(f"{a} + {b} = {total}")

pi_sample = 3.141592653589793
print("{0:.2f}".format(pi_sample))
print(f"{pi_sample:.2f}")

print("A", "B", sep="-", end=" | ")
print("C")
```

#### ${\color{#276BD1}\textsf{Candy Total}}$

```python
# total_candy.py
upan, ipan = map(int, input().split())
total = upan + ipan
print(total)
```

#### ${\color{#276BD1}\textsf{Exam Score Total}}$

```python
# total_score.py
math, science, english = map(float, input().split())
total = math + science + english
print(f"{total:.1f}")
```

#### ${\color{#276BD1}\textsf{Five-Digit Score}}$

```python
# digit_score.py
number = int(input())

digit1 = number % 10
number //= 10
digit2 = number % 10
number //= 10
digit3 = number % 10
number //= 10
digit4 = number % 10
number //= 10
digit5 = number % 10

digit_sum = digit1 + digit2 + digit3 + digit4 + digit5
print(digit_sum % 10)
```

### ${\color{#276BD1}\textsf{Result and Walkthrough}}$

#### ${\color{#276BD1}\textsf{Variables and Types}}$

Input

```text
1998
```

Output

```text
str
int
20
```

`input()` returns `"1998"`. `int(birth_year)` produces the integer `1998`, and the assignment binds the same name to that integer. The subtraction is `2018 - 1998 = 20`. A birth year alone gives the age reached in 2018. Checking someone's age on a particular date would also require their birth month and day.

#### ${\color{#276BD1}\textsf{Operators}}$

```text
11 7 18 4.5 1 81 4
1.0 4.0
-5 1 -4
47
10.0 float
0.0 float
True False True
1 pass
True False
```

The negative quotient line shows the floor of `-4.5`, the remainder from `-9 = (-5 * 2) + 1`, and the result of truncation. `value` goes through `12`, `10`, `20`, and `10.0`. Then it goes through `100.0`, `50.0`, and `0.0`. With `score = 7`, the range check passes, the `and` expression fails because `7 != 7` is false, and the conditional expression selects `"pass"`. `5 & 3` produces `1` from the shared low bit of binary `101` and `011`. The two list literals make distinct objects with equal contents, so the final line prints `True False`.

#### ${\color{#276BD1}\textsf{Reading Integers and Decimals}}$

Input

```text
7
8
7.1
8.2
7 8
7.1 8.2
```

Output

```text
7 8
7.1 8.2
7 8
7.1 8.2
```

The first four calls read separate lines. Each of the last two calls reads one full line. For `7 8`, the steps are `input()` → `"7 8"`, `.split()` → `["7", "8"]`, and conversion and unpacking → `left_int = 7`, `right_int = 8`. The decimal pair follows the same steps with `float`.

#### ${\color{#276BD1}\textsf{Formatting Output}}$

```text
Hello, World!!!
3 3.14 4000.0
5 + 7 = 12
5 + 7 = 12
3.14
3.14
A-B | C
```

The `.format()` call fills positions `0`, `1`, and `2` using the three arguments. The f-string evaluates the expressions inside its braces. Both precision examples display two decimal places. In the last line, `sep="-"` produces `A-B`, and `end=" | "` leaves the next `print()` on the same line.

#### ${\color{#276BD1}\textsf{Candy Total and Exam Score Total}}$

| Program | Input | Output | Calculation |
|---|---|---|---|
| `total_candy.py` | `7 8` | `15` | `7 + 8 = 15`. |
| `total_score.py` | `7.5 8.0 9.0` | `24.5` | `7.5 + 8.0 + 9.0 = 24.5`. `:.1f` fixes the display to one decimal place. |

#### ${\color{#276BD1}\textsf{Five-Digit Score}}$

Input

```text
52794
```

Output

```text
7
```

`% 10` gives the last digit of the current positive integer. `//= 10` removes that digit and keeps the remaining value an integer. The extracted digits are `4`, `9`, `7`, `2`, and `5`. Their sum is `27`, so `27 % 10` gives `7`.
