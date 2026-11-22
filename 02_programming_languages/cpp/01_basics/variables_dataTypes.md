# ${\color{#7C4DFF}\textsf{C++ Variables, Data Types, Operators, Input and Output}}$

The examples use **C++17**.

## ${\color{#7C4DFF}\textsf{Theory}}$

### ${\color{#7C4DFF}\textsf{Definition and Purpose}}$

| Concept | What it does |
|---|---|
| **Variable** | Gives a name to an object that holds a value, such as a student's age or a running total. |
| **Data type** | Determines what values an object can represent and which operations are available. |
| **Operator** | Performs an operation on one or more operands. In `a + b`, `+` is the operator and `a` and `b` are the operands. |
| **Standard input** | Supplies data to the program through `cin`, for example from a keyboard or an online judge's test data. |
| **Standard output** | Receives the text the program writes through `cout`, for example a result displayed in a terminal or checked by a judge. |

### ${\color{#7C4DFF}\textsf{Syntax}}$

#### ${\color{#7C4DFF}\textsf{Variable declarations and data types}}$

```cpp
int count;              // Declaration without an initializer
int total = 0;          // Declaration with an initializer
const int passMark = 5; // Initialized const variable

total = 12;             // Assignment to an existing variable
```

In `int total = 0;`, `int` is the type, `total` is the variable name, and `0` is the initializer. The `=` in a declaration gives the variable its first value. In `total = 12;`, `=` assigns a new value to an existing variable. `const` prevents later assignment to `passMark`.

| Type | Use | Example declaration |
|---|---|---|
| `short` | Signed whole numbers with a guaranteed minimum width of 16 bits | `short day = 25;` |
| `int` | Whole-number counts, indices, and small arithmetic | `int age = 19;` |
| `long` | Signed whole numbers with a guaranteed minimum width of 32 bits | `long distance = 120000L;` |
| `long long` | Large whole numbers with a guaranteed minimum width of 64 bits | `long long total = 3'000'000'000LL;` |
| `unsigned int` | Nonnegative integer values, such as bit masks | `unsigned int mask = 5u;` |
| `float` | Floating-point values when `float` precision is sufficient | `float ratio = 0.5f;` |
| `double` | Floating-point values such as decimal scores and averages | `double score = 7.25;` |
| `long double` | Floating-point values with at least the precision of `double` | `long double pi = 3.14159L;` |
| `char` | A single ordinary character such as a grade letter | `char grade = 'A';` |
| `bool` | A truth value | `bool passed = true;` |
| `string` | Text such as a full name. Include `<string>`. | `string name = "Alex Morgan";` |

A **literal** writes a value directly in source code. `'A'` is a character literal, while `"A"` is a string literal that can initialize a `string`. `7.25` and `4e3` are `double` literals, and `4e3` represents `4 × 10³ = 4000`. The suffix `f` makes a floating-point literal a `float`. The suffix `LL` selects `long long` for the decimal integer literal shown above.

#### ${\color{#7C4DFF}\textsf{Operator groups}}$

| Group | Operator names and symbols | How to read an expression |
|---|---|---|
| **Arithmetic operators** | Addition `+`, subtraction `-`, multiplication `*`, division `/`, remainder `%`, unary plus `+`, unary minus `-` | `a % b` yields the remainder. `-a` negates one operand. |
| **Assignment operators** | Simple assignment `=`, compound assignment `+=`, `-=`, `*=`, `/=`, `%=` | `a += b` adds `b` to `a` and stores the result in `a`. |
| **Increment and decrement operators** | Prefix `++a`, `--a` and postfix `a++`, `a--` | Each changes the variable by one. The position controls which value the expression supplies. |
| **Comparison operators** | Equality `==`, inequality `!=`, less/greater than `<` and `>`, less/greater than or equal to `<=` and `>=` | `a == b` tests equality and yields a `bool`. |
| **Logical operators** | AND `&&`, OR `\|\|`, NOT `!` | `valid && ready` is true when both conditions are true. |
| **Conditional operator (ternary)** | `condition ? valueIfTrue : valueIfFalse` | `passed ? "Pass" : "Retry"` selects one result. |
| **Bitwise operators** | AND `&`, OR `\|`, XOR `^`, complement `~`, left shift `<<`, right shift `>>` | `a & b` preserves bits set in both integer operands. |
| **Stream operators** | Extraction `>>`, insertion `<<` | `cin >> value` reads into a variable. `cout << value` writes a value. |

#### ${\color{#7C4DFF}\textsf{Standard input}}$

Include `<iostream>` for `cin` and `cout`. The examples put `using namespace std;` after the `#include` directives and before `main()` so standard-library names such as `cin`, `cout`, `string`, and `getline` can be used directly. To read one integer inside `main()`, first declare a destination variable, then extract the input value into it.

```cpp
int age = 0;  // 1. Create an int variable to receive the value
cin >> age;   // 2. Read the next integer into age
```

| Input needed | Declare the destination, then read |
|---|---|
| One large integer | `long long population = 0; cin >> population;` |
| Two integers | `int a = 0, b = 0; cin >> a >> b;` |
| Two decimal numbers | `double x = 0.0, y = 0.0; cin >> x >> y;` |
| One non-whitespace character | `char grade = '\0'; cin >> grade;` |
| One word | `string word = ""; cin >> word;` |
| One full line | `string line = ""; getline(cin, line);` |

Include `<string>` for `string` and the `getline` overload shown here. In `getline(cin, line)`, `cin` supplies the characters and `line` receives them.

#### ${\color{#7C4DFF}\textsf{Standard output}}$

Include `<iostream>` to use `cout`. Each `<<` inserts the following value. Put separators and line breaks into the chain wherever the output format needs them.

```cpp
cout << value << '\n';
cout << a << " + " << b << " = " << (a + b) << '\n';
cout << fixed << setprecision(2) << result << '\n';
```

The last form needs `<iomanip>` for `setprecision`. `result` is a floating-point value and `2` is the number of digits to display after the decimal point when `fixed` is active.

### ${\color{#7C4DFF}\textsf{Behavior}}$

#### ${\color{#7C4DFF}\textsf{Arithmetic and state changes}}$

- **Integer division** truncates toward zero. A floating-point operand such as `9.0` gives floating-point division with ordinary numeric operands. With `double result = a / b;`, two `int` operands still perform integer division first. To keep the fractional part, convert an operand before dividing, as in `static_cast<double>(a) / b`.
- **Remainder** satisfies `(a / b) * b + a % b == a` when the integer quotient is representable and `b` is nonzero. For a nonnegative integer `n`, `n % 10` gets the last decimal digit and `n / 10` drops it.
- **Compound assignment** updates the left-hand object. For an ordinary variable, `a += b` has the same effect as `a = a + b`. **Prefix** increment or decrement supplies the updated value, while **postfix** supplies the previous value and still updates the variable.
- **Logical operators** `&&` and `||` short-circuit. Built-in `&&` skips the right operand when the left is false, and built-in `||` skips it when the left is true. The **ternary operator** evaluates the condition and then only the selected branch.

#### ${\color{#7C4DFF}\textsf{Reading and writing values}}$

- By default, formatted extraction skips leading whitespace such as spaces, tabs, and newlines. `cin >> a >> b` therefore reads values in the same order whether they appear on one line or two. Reading into a `string` with `>>` stops at the next whitespace.
- `getline` reads through the end of a line by default. It consumes the newline and stores the preceding characters, including spaces.
- `cout` writes the supplied values without adding automatic spaces or line breaks. `fixed` and `setprecision` change how floating-point values are displayed on that stream. The settings persist until changed, and the stored number keeps its value.

### ${\color{#7C4DFF}\textsf{Rules and Boundaries}}$

| Rule | Practical consequence |
|---|---|
| Use letters, digits, or underscores for ordinary ASCII variable names. Choose a letter as the first character for names such as `yearOfBirth` or `year_of_birth`. | `1stYear`, `my age`, `this-year`, and the keyword `int` are invalid variable names. A leading underscore can be valid, and some underscore-prefixed names are reserved. `age` and `Age` are distinct. |
| A local variable declared inside a block can be referenced after its declaration up to the end of the block, unless a nested declaration hides the name. Initialize local scalar variables before reading them. | In C++17, reading an uninitialized local `int` has undefined behavior. `int count = 0;` gives it a known starting value. |
| Choose a type that can represent the value you need. | `double score = 7.9;` retains the fractional part, while `int n = 7.9;` converts the value to `7`. Use `static_cast<int>(score)` when you intend to discard the fractional part and the whole-number result fits in `int`. |
| Match the type to the range of both the inputs and intermediate results. | Signed arithmetic overflow has undefined behavior. Floating-point representations can round decimal values. Check the implementation limits below when choosing a type. |
| Use integral operands with `%`, and check that the divisor is nonzero before integer `/` or `%`. | `7.5 % 2` is a compile-time error. Integer division or remainder by zero has undefined behavior. |
| Precedence controls expression grouping. Use parentheses when mixing stream insertion with comparisons or ternary expressions. | `cout << (a < b);` prints the comparison result. `*`, `/`, and `%` bind more tightly than binary `+` and `-`. |
| Check whether extraction succeeded before using user-provided values. | `if (!(cin >> value)) { return 1; }` exits `main()` before calculation when the requested input could not be read, for example when the next token is `abc` and `value` is an `int`. A stream in a failed state also blocks later extractions until handled. |
| Plan the transition from `>>` to `getline`. | If the last extraction leaves a newline next in the stream, a plain `getline` reads an empty line. `getline(cin >> ws, name)` skips pending whitespace before reading a name. It also skips blank lines and leading spaces. |
| Follow the output format in an online judge problem. | If the judge asks for only a number, print the number and the required line break. A prompt such as `"Enter a number: "` adds text to the answer. |

#### ${\color{#7C4DFF}\textsf{Typical numeric ranges}}$

The table shows one common layout with approximate floating-point limits. With `N` bits, a two's-complement signed integer in this layout spans `-2^(N-1)` through `2^(N-1) - 1`.

| Type | Example size | What the range describes |
|---|---:|---|
| `short` | 2 bytes | `-32,768` through `32,767` |
| `int`, `long` | 4 bytes each | `-2,147,483,648` through `2,147,483,647` |
| `long long` | 8 bytes | `-9,223,372,036,854,775,808` through `9,223,372,036,854,775,807` |
| `float` | 4 bytes | Smallest positive subnormal ≈ `1.40e-45`. Largest finite value ≈ `3.40e38`. |
| `double` | 8 bytes | Smallest positive subnormal ≈ `4.94e-324`. Largest finite value ≈ `1.80e308`. |

The floating-point types in the table can also represent negative values and zero. Exact sizes and limits depend on the implementation. For example, `long` is 8 bytes on common 64-bit Unix-like systems that use LP64. Use `sizeof(T)` for object size in bytes and `numeric_limits<T>::lowest()` and `numeric_limits<T>::max()` from `<limits>` for the lowest and highest finite values.

### ${\color{#7C4DFF}\textsf{Related Forms}}$

| Forms | When to use each |
|---|---|
| `=` and `==` | Use `=` to assign a value and `==` to test equality. |
| `>>` and `getline` | Use formatted extraction for individual numbers, characters, or words. Use `getline` for a line that may contain spaces. |
| `ws` and `ignore` before `getline` | Use `ws` when leading whitespace is disposable. To discard only the rest of the current input line and preserve spaces or a blank line on the next one, use `cin.ignore(numeric_limits<streamsize>::max(), '\n');` after successful extraction, then call `getline(cin, line);`. Include `<limits>`. |
| `'\n'` and `endl` | Use `'\n'` for an ordinary line break. `endl` adds a line break and explicitly flushes the output stream. |
| Bit shifts and stream insertion/extraction | `mask << 1` shifts the bits of an integer operand. `cout << mask` writes the value to standard output. The operands determine which operation applies. |

## ${\color{#276BD1}\textsf{Code Example}}$

### ${\color{#276BD1}\textsf{Example Setup}}$

Each example is a complete C++17 program. Save each block in the file named below it. To try the first example with GCC, compile with `g++ -std=c++17 read_integer.cpp -o read_integer` and run `./read_integer` in a Unix-style shell. In PowerShell, use `-o read_integer.exe` when compiling and run `.\read_integer.exe`.

| Program | Input | What to check |
|---|---|---|
| `read_integer.cpp` | `19` | Declare an `int`, read into it, and print the result. |
| `integer_report.cpp` | `9 2`, or `9` and `2` on separate lines | Both layouts give the same output. Integer division and floating-point division give different results. |
| `score_report.cpp` | Two scores, a group letter, a course code, and a full name | Read numbers and words with `>>`, read a full name with `getline`, and control decimal display. |
| `operators.cpp` | No input. Starts with `count = 7`. | Trace assignment, prefix/postfix increments and decrements, comparisons, and bit operations. |

### ${\color{#276BD1}\textsf{Implementation}}$

#### ${\color{#276BD1}\textsf{Read one integer}}$

Save as `read_integer.cpp`. Type `19` and press Enter when running interactively.

```cpp
#include <iostream>

using namespace std;

int main() {
    int age = 0;

    if (!(cin >> age)) {
        return 1;
    }

    cout << "Age: " << age << '\n';
    return 0;
}
```

#### ${\color{#276BD1}\textsf{Read two integers and compare division results}}$

Save as `integer_report.cpp`. This example assumes both inputs are within `[-1'000'000'000, 1'000'000'000]` so the sum fits in `long long`. The divisor must be nonzero.

```cpp
#include <iomanip>
#include <iostream>

using namespace std;

int main() {
    long long a = 0;
    long long b = 0;

    if (!(cin >> a >> b) || b == 0) {
        return 1;
    }

    const long long sum = a + b;
    const long long quotient = a / b;
    const double decimalQuotient = static_cast<double>(a) / b;
    const long long remainder = a % b;

    cout << a << " + " << b << " = " << sum << '\n';
    cout << "Integer quotient: " << quotient << '\n';
    cout << "Decimal quotient: "
              << fixed << setprecision(2) << decimalQuotient << '\n';
    cout << "Remainder: " << remainder << '\n';
    return 0;
}
```

#### ${\color{#276BD1}\textsf{Read numbers, a character, a word, and a full line}}$

Save as `score_report.cpp`. The program uses `5.0` as the sample passing average.

```text
7.1 8.2
A CPP101
Alex Morgan
```

```cpp
#include <iomanip>
#include <iostream>
#include <string>

using namespace std;

int main() {
    double firstScore = 0.0;
    double secondScore = 0.0;
    char group = '\0';
    string courseCode = "";
    string fullName = "";

    if (!(cin >> firstScore >> secondScore >> group >> courseCode)) {
        return 1;
    }
    if (!getline(cin >> ws, fullName)) {
        return 1;
    }

    const double total = firstScore + secondScore;
    const double average = total / 2.0;
    const bool passed = average >= 5.0;

    cout << "Student: " << fullName << '\n';
    cout << "Course: " << courseCode << " (group " << group << ")\n";
    cout << fixed << setprecision(1) << "Total: " << total << '\n';
    cout << setprecision(2) << "Average: " << average << '\n';
    cout << "Result: " << (passed ? "Pass" : "Retry") << '\n';
    return 0;
}
```

#### ${\color{#276BD1}\textsf{Trace operators}}$

Save as `operators.cpp`.

```cpp
#include <iostream>

using namespace std;

int main() {
    int count = 7;
    count += 2;
    const int beforeIncrement = count++;
    const int afterIncrement = ++count;
    const int beforeDecrement = count--;
    const int afterDecrement = --count;
    const bool inRange = count >= 5 && count <= 10;

    cout << "Increment values: " << beforeIncrement << ' ' << afterIncrement << '\n';
    cout << "Decrement values: " << beforeDecrement << ' ' << afterDecrement << '\n';
    cout << "Count: " << count << '\n';
    cout << "Range: " << (inRange ? "Inside" : "Outside") << '\n';
    cout << "Negative division: " << (-9 / 2) << '\n';
    cout << "Negative remainder: " << (-9 % 2) << '\n';

    const unsigned int firstMask = 5u;  // Low bits: 101
    const unsigned int secondMask = 3u;  // Low bits: 011
    cout << "AND, OR, XOR: " << (firstMask & secondMask) << ' '
              << (firstMask | secondMask) << ' ' << (firstMask ^ secondMask) << '\n';
    cout << "Left shift: " << (firstMask << 1) << '\n';
    return 0;
}
```

### ${\color{#276BD1}\textsf{Result and Walkthrough}}$

#### ${\color{#276BD1}\textsf{Read one integer}}$

```text
Age: 19
```

`int age = 0;` creates the destination with an initial value of `0`. The successful `cin >> age` replaces it with `19`. The output chain writes the label, the stored number, and a newline. With input `abc`, the read fails and the program exits with status `1` before printing anything.

#### ${\color{#276BD1}\textsf{Read two integers and compare division results}}$

For both `9 2` and `9` followed by `2` on the next line, the program prints

```text
9 + 2 = 11
Integer quotient: 4
Decimal quotient: 4.50
Remainder: 1
```

- `cin >> a >> b` stores `9` in `a` and `2` in `b`. `a + b` gives `11`.
- `a / b` keeps the integer quotient `4`. Converting `a` to `double` before division yields `4.5`, displayed as `4.50` by the output formatting.
- `a % b` gives `1` because `9 = 4 × 2 + 1`.

#### ${\color{#276BD1}\textsf{Read numbers, a character, a word, and a full line}}$

```text
Student: Alex Morgan
Course: CPP101 (group A)
Total: 15.3
Average: 7.65
Result: Pass
```

- The chained extractions read `7.1`, `8.2`, `A`, and `CPP101` in that order. `ws` consumes the pending newline, then `getline` reads the full name, including its internal spaces.
- The displayed total rounds `7.1 + 8.2` to one decimal place. Dividing the computed total by `2.0` gives the displayed average `7.65` at two decimal places.
- The average meets the example's `5.0` threshold, so the ternary expression supplies `"Pass"`.

#### ${\color{#276BD1}\textsf{Trace operators}}$

```text
Increment values: 9 11
Decrement values: 11 9
Count: 9
Range: Inside
Negative division: -4
Negative remainder: -1
AND, OR, XOR: 1 7 6
Left shift: 10
```

| Operation | Value supplied | `count` afterward |
|---|---|---|
| `count += 2` | `9` | `9` |
| `count++` | `9` | `10` |
| `++count` | `11` | `11` |
| `count--` | `11` | `10` |
| `--count` | `9` | `9` |

- `9` satisfies both comparisons in `count >= 5 && count <= 10`, so the ternary expression supplies `"Inside"`.
- `-9 / 2` truncates toward zero to `-4`. The remainder is `-1` because `-9 = (-4 × 2) + (-1)`.
- In binary, `101` and `011` give `001` for AND, `111` for OR, and `110` for XOR. Those are `1`, `7`, and `6` in decimal. Shifting `101` left by one gives `1010`, or `10`.
