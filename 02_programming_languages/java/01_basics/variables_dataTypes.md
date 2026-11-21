# ${\color{#7C4DFF}\textsf{Java Variables and Data Types}}$

## ${\color{#7C4DFF}\textsf{Theory}}$

### ${\color{#7C4DFF}\textsf{Definition and Purpose}}$

A **variable** holds a value that a program can read and, where allowed, replace. Its **type** determines which values it can hold, which operations can use it, and how Java interprets those operations. Java is statically typed. The compiler knows the type of each variable and expression, including variables declared with `var`.

| Kind | What the variable holds | Typical uses |
|---|---|---|
| Primitive | A primitive value, such as an integer, a logical value, or a UTF-16 code unit | A loop counter, a test score, a flag, or a grade letter |
| Reference | A reference to an object, or `null` | A `String`, an array, a list, or an instance of a class |

A **declaration** introduces a variable. An **initializer** supplies its starting value as part of that declaration. An **assignment** stores a value in an existing variable. A **literal** writes a value directly in the source, such as `42` or `"Sam"`. A **scope** is the region of source code where a declared name is available.

### ${\color{#7C4DFF}\textsf{Syntax}}$

#### ${\color{#7C4DFF}\textsf{Declarations, initializers, and assignments}}$

| Written form | How to read it |
|---|---|
| `Type name;` | Declare `name` with the given `Type`. Use this form for a field or when a local value will be assigned before its first read. |
| `Type name = expression;` | Declare and initialize `name`. The expression must be compatible with `Type`. |
| `name = expression;` | Assign to a variable that is already in scope. |
| `final Type name = expression;` | Declare a variable whose stored value can be assigned only once. |
| `private static final Type NAME = expression;` | Declare a class member that is shared and assigned once. Use an uppercase name with underscores for a named constant. |
| `var name = expression;` | Let the compiler infer a local variable's type from the initializer. Requires JDK 10 or later. |
| `Type[] name = new Type[length];` | Declare an array reference and allocate an array with the given number of components. |
| `Type[] name = { expression, expression };` | Declare an array reference with an initializer list. The list determines the length. |
| `(TargetType) expression` | Cast the expression's value to the target type where Java permits that conversion. |

Replace `Type`, `TargetType`, `name`, `NAME`, `expression`, and `length` with the type, identifier, or expression your code needs. Separate unrelated declarations to make each variable's purpose and initializer clear. Ordinary variable and field names usually use `lowerCamelCase`, such as `totalScore` or `isReady`.

#### ${\color{#7C4DFF}\textsf{Where declarations go}}$

| Location | Declaration form | What it declares |
|---|---|---|
| Within a method or a block | `Type name = expression;` | A local variable |
| In an entry-point or ordinary method signature | `Type name` in the parameter list | A method parameter |
| In a constructor signature | `Type name` in the parameter list | A constructor parameter |
| At class-member level | `Type name;` | An instance field |
| At class-member level with `static` | `static Type name;` | A class field |

| Form | Java Classic — Class-Based | Java 25 — Compact Source File |
|---|---|---|
| Program structure | Write members inside an explicit class. A conventional entry point is `public static void main(String[] args)`. | Write members directly in the file. Java declares their enclosing class implicitly. A compact entry point can be `void main()` and has JDK 25 support without preview flags. |
| Field and local placement | A declaration in the class body is a field. A declaration inside `main` is local. The static `main` can access static fields directly. | A declaration at the member level of the file is a field of the implicit class. A declaration inside `main` is local. An instance `main` can access instance and static fields. |
| Standard-library imports | `java.lang` types are available by default. Import a type such as `java.util.Scanner` or qualify its name. | Public top-level types in exported packages of `java.base` are implicitly available on demand. This includes `Scanner`, `ArrayList`, and `Locale`. |
| Package | An explicit class can be placed in a named package. | A compact source file belongs to the unnamed package. |

**Java Classic** here names the class-based entry-point style. A class-based program can target JDK 25 and use its APIs and language features. The Classic program under **Implementation** uses Java 8-compatible syntax and APIs.

#### ${\color{#7C4DFF}\textsf{Literal notation}}$

| Form | Type or meaning |
|---|---|
| `42`, `1_000_000` | Decimal `int` literals. Underscores between digits are separators. |
| `42L` | `long` literal. Uppercase `L` is easier to distinguish from `1`. |
| `0b1010`, `0xFF`, `012` | Binary, hexadecimal, and octal integer literals. Their decimal values are 10, 255, and 10. |
| `3.14`, `3.14d`, `2e2` | `double` literals. The exponent in `2e2` means `2 × 10²`. |
| `3.14f` | `float` literal. The `f` or `F` suffix selects `float`. |
| `'A'`, `'\n'`, `'\u0041'` | `char` literals for the letter A, a newline, and the Unicode escape for A. |
| `"A"`, `""`, `"Hi\nSam"` | `String` literals. The empty string has zero code units. |
| `"""` | Opening and closing delimiter for a text block, a multiline `String` literal form available from JDK 15. The opening delimiter is followed by a line terminator, with optional intervening whitespace. |
| `true`, `false` | The two `boolean` literals. |
| `null` | The null literal. It has the null type and can be assigned to a reference variable. |

#### ${\color{#7C4DFF}\textsf{Input and output}}$

| Operation | Class-based example on JDK 8 | Compact example on JDK 25 |
|---|---|---|
| Read a line of input | `input.nextLine()`, where `input` is a `Scanner` reading `System.in`. | `IO.readln()`, which reads from `System.in` and returns `null` at end-of-input when no characters remain. |
| Convert integer text | `Integer.parseInt(text)` | `Integer.parseInt(text)` |
| Print a line | `System.out.println(value)` | `IO.println(value)` or `System.out.println(value)` |
| Print a formatted decimal | `System.out.printf(Locale.ROOT, "%.2f%n", value)` | The same `printf` call. `Locale` is available through the compact file's implicit imports. |

`Scanner` is available in both styles. `java.lang.IO` is available in both styles when targeting JDK 25. Use the `IO.` qualifier unless the method is explicitly statically imported.

### ${\color{#7C4DFF}\textsf{Behavior}}$

#### ${\color{#7C4DFF}\textsf{The eight primitive types}}$

| Type | Representation | Range or values | Default for fields and array components |
|---|---|---|---|
| `byte` | 8-bit signed integer | −128 through 127 | `0` |
| `short` | 16-bit signed integer | −32,768 through 32,767 | `0` |
| `int` | 32-bit signed integer | −2,147,483,648 through 2,147,483,647 | `0` |
| `long` | 64-bit signed integer | −9,223,372,036,854,775,808 through 9,223,372,036,854,775,807 | `0L` |
| `float` | 32-bit IEEE 754 binary floating point | Finite magnitudes up to about 3.4028235 × 10³⁸ | `0.0f` |
| `double` | 64-bit IEEE 754 binary floating point | Finite magnitudes up to about 1.7976931348623157 × 10³⁰⁸ | `0.0d` |
| `char` | 16-bit unsigned UTF-16 code unit | 0 through 65,535 | `'\u0000'` |
| `boolean` | Two logical values | `true` or `false` | `false` |

The signed range for `n` bits is `−2^(n−1)` through `2^(n−1) − 1`. The language specifies the two `boolean` values and leaves the storage width of a variable to the implementation. Both floating-point types also support signed zero, infinities, and `NaN`.

`float` has 24 bits of significand precision and `double` has 53. Multiplying each by `log₁₀(2)` gives roughly 7 and 16 significant decimal digits, respectively. Many decimal fractions, including `0.1`, have an approximate binary representation. `Float.MIN_VALUE` and `Double.MIN_VALUE` are the smallest positive nonzero values of their types. For the most negative finite values, use `-Float.MAX_VALUE` and `-Double.MAX_VALUE`.

`char` holds one code unit. `String.length()` counts code units, and `String.codePointCount(begin, end)` counts code points in that range. A supplementary Unicode code point requires two UTF-16 code units.

#### ${\color{#7C4DFF}\textsf{Reference values and copying}}$

Class types such as `String` and `Integer`, interface types such as `List<String>`, array types such as `int[]`, and type variables such as `T` are reference types. Enums and records are kinds of classes. A variable's **declared type** determines which members the compiler allows through that variable. The referenced object's **runtime class** may be a compatible subtype.

Assignment copies the stored value. Copying a primitive value gives a second variable its own copy. Copying a reference can give two variables access to the same object. This is called **aliasing**. A method also receives a copy of each argument value, so it can modify a shared mutable object through a copied reference. Reassigning its parameter changes only that parameter.

A `String` is immutable. A call that transforms text returns a result while the original string's contents stay the same. An array is mutable. For a one-dimensional primitive array, `clone()` copies the components into a separate array. For an object array or nested array, `clone()` copies the component references, so the referenced objects may still be shared.

#### ${\color{#7C4DFF}\textsf{Numeric conversions}}$

A **widening primitive conversion** can occur implicitly in a compatible assignment.

| Source | Widens to |
|---|---|
| `byte` | `short`, `int`, `long`, `float`, `double` |
| `short` | `int`, `long`, `float`, `double` |
| `char` | `int`, `long`, `float`, `double` |
| `int` | `long`, `float`, `double` |
| `long` | `float`, `double` |
| `float` | `double` |

Widening from `int` to `double` preserves every `int` value. Widening from `int` to `float`, or from `long` to `float` or `double`, can round large integers.

A **narrowing primitive conversion** generally needs an explicit cast. The cast converts the expression's value for that use. The original variable retains its type.

| Conversion | Result or possible loss |
|---|---|
| Floating point to `int` or `long` | Discards a fractional part toward zero. `NaN` becomes zero. A value beyond the range becomes the corresponding minimum or maximum. |
| Floating point to `byte`, `short`, or `char` | First converts to `int`, then narrows to the destination type. |
| Integer to a narrower integer type | Keeps the destination width's low-order bits. A signed result can change sign. |
| `double` to `float` | Can lose precision, overflow to infinity, or underflow toward zero. |
| Numeric primitive to `boolean`, or the reverse | Java rejects the conversion. Use a comparison such as `count != 0` when a condition is needed. |

Use `Math.round(value)` when you need rounding. It returns `int` for a `float` argument and `long` for a `double` argument, with ties toward positive infinity. Use `Math.toIntExact(value)` for a checked `long` to `int` conversion that throws `ArithmeticException` for an out-of-range value.

#### ${\color{#7C4DFF}\textsf{Operators and result types}}$

For binary arithmetic, Java first promotes the numeric operands. It chooses the first applicable type from `double`, `float`, `long`, and `int`. In particular, arithmetic with `byte`, `short`, or `char` operands usually produces `int` when both operands are these small integral types.

| Operation | Effect |
|---|---|
| `+`, `-`, `*`, `/`, `%` | Arithmetic on promoted operands. Integer division truncates toward zero. A nonzero integer remainder has the dividend's sign. |
| `+` with a `String` operand | Concatenates text. Group arithmetic in parentheses when it should take place before concatenation. |
| `==`, `!=`, `<`, `<=`, `>`, `>=` | Compare values where the operand types support the operator and produce a `boolean`. |
| `&&`, `\|\|`, `!` | Short-circuit AND, short-circuit OR, and logical negation. The short-circuit forms evaluate the right operand only when needed. |
| `&`, `\|`, `^` | Bitwise operations with integral operands, or logical operations with boolean operands. Both operands of the boolean forms are evaluated. |
| `~`, `<<`, `>>`, `>>>` | Bit complement, left shift, sign-extending right shift, and zero-fill right shift. |
| `+=`, `-=`, `*=`, `/=`, `%=` | Performs the operation and assigns the result, with conversion back to the destination type. |
| `++`, `--` | Increments or decrements a variable. Prefix yields the updated value, and postfix yields the previous value. |
| `condition ? whenTrue : whenFalse` | Evaluates the condition and then evaluates only the selected result expression. |

Precedence determines how operators group. Parentheses can change that grouping. For a positive divisor, `Math.floorMod` gives a nonnegative modulus. Use `Math.pow(base, exponent)` for floating-point exponentiation. The `^` operator performs XOR.

#### ${\color{#7C4DFF}\textsf{Boxing, unboxing, and parsing}}$

| Primitive | Wrapper | Primitive | Wrapper |
|---|---|---|---|
| `byte` | `Byte` | `short` | `Short` |
| `int` | `Integer` | `long` | `Long` |
| `float` | `Float` | `double` | `Double` |
| `char` | `Character` | `boolean` | `Boolean` |

**Boxing** produces a wrapper reference from a primitive value. **Unboxing** takes the primitive value from a wrapper reference. For instance, a collection declared as `ArrayList<Integer>` can accept an `int` through boxing and produce an `int` through unboxing on assignment.

**Parsing** interprets text as a value. `Integer.parseInt` and `Long.parseLong` read integer text. `Double.parseDouble` reads floating-point text. `Boolean.parseBoolean` returns `true` when the input equals `"true"` ignoring case, and `false` for other input, including `null`. `String.valueOf(value)` provides the corresponding text conversion for many kinds of values. Formatting such as `%.2f` changes the displayed text and leaves the stored number intact. `%n` emits the platform's line separator.

### ${\color{#7C4DFF}\textsf{Rules and Boundaries}}$

#### ${\color{#7C4DFF}\textsf{Names, scope, and initialization}}$

- A Java identifier can begin with a permitted Java letter, including many Unicode letters, `_`, or `$`. A digit may follow a permitted starting character. Names are case-sensitive. A leading digit, a space, or a hyphen makes a proposed name invalid. Reserved spellings such as `class`, `int`, `true`, and `null` are unavailable as names. A single `_` is a reserved keyword in modern Java, with specific unnamed declaration uses from JDK 22.
- A local name declared in a block is only in scope through the rest of its enclosing block, including its initializer. An attempt to read its own value in that initializer fails definite assignment. A variable declared in a basic `for` header is available within its scope in the header and body. A local variable or parameter can shadow a field. In an instance method, `this.fieldName` selects the current object's field.
- A local variable needs a definitely assigned value on every possible execution path that reaches a read. Declaring `int total;` inside a method leaves it unassigned until an initializer or later assignment supplies a value. A method or constructor parameter receives the corresponding argument value on entry.
- A class field, instance field, or array component starts with its type's default. Primitive defaults are in the primitive table and reference defaults are `null`. An instance field is associated with one object, while a static field belongs to its class. Java applies field initializers and initialization code where applicable. Blank `final` fields have additional definite-assignment rules.

#### ${\color{#7C4DFF}\textsf{Literal types and assignment compatibility}}$

- Java determines the type of a literal before applying assignment conversions. An unsuffixed decimal integer literal too large for `int` cannot be rescued by assignment to `long`. Write `3_000_000_000L`. The minus sign is a unary operator. Java has special literal rules for writing the decimal minimum values `-2147483648` and `-9223372036854775808L`.
- A floating-point literal such as `1.5` has type `double`. To initialize a `float` directly with that literal, use `1.5f` or an explicit `(float)` cast.
- A representable constant expression of type `byte`, `short`, `char`, or `int` can be assigned directly to `byte`, `short`, or `char`. Thus `byte limit = 100;` is valid. With an ordinary `int` variable holding 100, a `byte` assignment needs a cast. Regular method arguments follow invocation conversion rules and do not get this constant narrowing allowance.
- `void` indicates that a method returns no value. It cannot be used as a variable type.

#### ${\color{#7C4DFF}\textsf{Final variables and constants}}$

A `final` variable can be assigned once. A **blank final** starts with no initializer in its declaration and must be assigned at the required point. For example, a constructor can assign a blank final instance field. If the variable holds a reference, `final` prevents replacing that reference. The object's type still determines whether its contents can change.

A **constant variable** is a `final` primitive or `String` variable initialized with a constant expression. A `static final Integer` field and a primitive field initialized with `Integer.parseInt(...)` fall outside this definition. An **effectively final** local variable or parameter is a candidate for capture by a lambda because it satisfies the compiler's rules for being left unchanged after initialization.

#### ${\color{#7C4DFF}\textsf{Type inference and version-specific declarations}}$

**Local inference with `var`.** JDK 8 requires an explicit local type, as in `int score = 42;`. JDK 10 and later, including JDK 25, can also use `var score = 42;` in the class-based or compact style. In that example the compiler infers `int`. The type stays fixed. For `var` in an ordinary local declaration, write one declarator and supply an initializer with a type that can be inferred. A bare `null`, an array initializer such as `{84, 91}`, or a lambda without a target type causes a compile-time error. `var item = (String) null;` and `var scores = new int[] {84, 91};` supply types. The form `var list = new ArrayList<>();` infers `ArrayList<Object>` in this context. Use `new ArrayList<String>()` when the intended element type is `String`.

**Other `var` positions.** Supported local positions include enhanced `for` variables and suitable try-with-resources declarations. Fields, ordinary method parameters, and return types require explicit types. JDK 11 introduced `var` in implicitly typed lambda parameters, where the target functional interface supplies the parameter types.

| Declaration or type test | Classic example on JDK 8 | Available on JDK 25 |
|---|---|---|
| Reference type pattern | Test `value instanceof String`, then declare a local with `String name = (String) value;` on the matching path. | `value instanceof String name` declares `name` where the compiler knows the pattern matched. This form became permanent in JDK 16. |
| Intentionally unused exception variable | Write a named parameter, such as `catch (NumberFormatException ignored)`. | `catch (NumberFormatException _)` leaves the parameter unnamed. This form became permanent in JDK 22. The handling code cannot read the discarded parameter. |
| Exact test before narrowing a primitive | For an `int`, check `Byte.MIN_VALUE` through `Byte.MAX_VALUE` before casting to `byte`. | `number instanceof byte narrowed` tests whether the value is exactly representable as a `byte` and binds the converted value on success. This extension is a third preview in JDK 25 and requires preview to be enabled. It also extends primitive support in `switch`. |

#### ${\color{#7C4DFF}\textsf{Runtime boundaries}}$

| Condition | Consequence |
|---|---|
| Dereferencing `null` or unboxing a null wrapper | `NullPointerException` |
| Casting a reference whose object has an incompatible runtime type | `ClassCastException` |
| Integer division or remainder by zero | `ArithmeticException` |
| Floating-point division by zero | An appropriately signed infinity for a finite nonzero dividend, or `NaN` for zero divided by zero |
| An integer arithmetic result outside its type's range | Ordinary `int` and `long` operations wrap. `Math.addExact` and `Math.multiplyExact` throw `ArithmeticException` on overflow. |
| Trying to use a primitive as a generic type argument | Compile-time error. Use `ArrayList<Integer>` for boxed integer elements. |
| Malformed or out-of-range integer text passed to `Integer.parseInt` or `Long.parseLong` | `NumberFormatException` |
| Using `Scanner.nextLine()` right after a token read at the end of a line | It consumes the current line's remainder, which may be empty. |
| Reusing `System.in` directly after an `IO.readln()` call | The `IO` API leaves the subsequent use unspecified. |

A destination type cannot retroactively change an expression's result. For example, assigning an integer quotient to `double` only widens the already truncated result. Likewise, an `int` product can overflow before assignment to `long`. Make an operand `double` for floating-point division or `long` for a product that needs the wider integer range.

### ${\color{#7C4DFF}\textsf{Related Forms}}$

#### ${\color{#7C4DFF}\textsf{Choosing a type}}$

| Need | Use | Practical distinction |
|---|---|---|
| Counts and ordinary whole-number arithmetic | `int` | Use `long` if either the values or the intermediate calculations exceed the `int` range. |
| Small signed integer values | `byte` or `short` | Useful when a field, array, or API expects that width. Arithmetic still commonly promotes the operands to `int`. |
| Integers beyond `long` | `BigInteger` | Arbitrary-precision integer arithmetic through methods such as `add` and `multiply`. |
| Approximate fractional calculations | `double` | Use `float` when a format or API requires single precision or when its trade-offs fit the data. |
| Exact decimal values | `BigDecimal` | Construct from text such as `"0.10"` to preserve the intended decimal value. Use an explicit rounding policy when the operation needs one. |
| One UTF-16 unit or text | `char` or `String` | `'A'` holds one code unit. `"A"` is a string. A supplementary code point may need a pair of code units in a string. |
| Identifiers with meaningful formatting | `String` | Values such as `"00042"` keep their leading zeros. |
| A true/false condition | `boolean` | Use a wrapper when a compatible generic collection or a nullable reference is needed. |

#### ${\color{#7C4DFF}\textsf{Comparing values}}$

| Form | What it checks |
|---|---|
| `left == right` with primitive numeric or boolean operands | Numeric or logical equality as allowed by the operand types. For floating point, `NaN` compares unequal to every value, including itself. Use `Double.isNaN(value)` or `Float.isNaN(value)` to detect it. |
| `left == right` with compatible reference operands | The same referenced object, or two null references. This also applies when both operands are compatible wrapper references. |
| `left.equals(right)` for a non-null `String` receiver | Equal string contents. `""` is an empty string object and `null` has no referenced object. |
| `Objects.equals(left, right)` | Null-safe equality. It returns true for two nulls and delegates to the first object's `equals` method when that object is non-null. |
| `Arrays.equals(left, right)` | One-dimensional array equality using the applicable array overload. |
| `boxed == 42` for an `Integer` variable | Unboxes the wrapper and compares numerically. A null wrapper causes `NullPointerException`. |


## ${\color{#276BD1}\textsf{Code Example}}$

### ${\color{#276BD1}\textsf{Example Setup}}$

The two complete programs below expect two valid integers on separate lines. Use `84` and `91`. The odd total, `175`, makes the difference between integer and floating-point division visible. Both programs also read a static `int` field declared without an initializer to show its default value.

The shared snippets each belong inside a separate `main` body in either style. They show how copying a value differs from copying a reference, what happens during numeric conversions, and what a string's length measures.

### ${\color{#276BD1}\textsf{Implementation}}$

#### ${\color{#276BD1}\textsf{Java Classic — Class-Based}}$

Save as `ClassicVariables.java`. This complete program uses the conventional class-based entry point and targets JDK 8 or later. Compile with `javac ClassicVariables.java`, then run `java ClassicVariables`.

```java
import java.util.Scanner;

public class ClassicVariables {
    private static final int SCORE_COUNT = 2;
    private static int recordedAttempts;

    public static void main(String[] args) {
        try (Scanner input = new Scanner(System.in)) {
            int firstScore = Integer.parseInt(input.nextLine().trim());
            int secondScore = Integer.parseInt(input.nextLine().trim());
            int total = firstScore + secondScore;

            double widenedQuotient = total / SCORE_COUNT;
            double fractionalMean = (double) total / SCORE_COUNT;

            System.out.println("Recorded attempts = " + recordedAttempts);
            System.out.println("Widened quotient = " + widenedQuotient);
            System.out.println("Fractional mean = " + fractionalMean);
        }
    }
}
```

#### ${\color{#276BD1}\textsf{Java 25 — Compact Source File}}$

Save as `CompactVariables.java` and run `java CompactVariables.java` using JDK 25. This complete program uses an instance `main` method, `IO` for line input and output, and `var` for the local total.

```java
private static final int SCORE_COUNT = 2;
private static int recordedAttempts;

void main() {
    int firstScore = Integer.parseInt(IO.readln().trim());
    int secondScore = Integer.parseInt(IO.readln().trim());
    var total = firstScore + secondScore;

    double widenedQuotient = total / SCORE_COUNT;
    double fractionalMean = (double) total / SCORE_COUNT;

    IO.println("Recorded attempts = " + recordedAttempts);
    IO.println("Widened quotient = " + widenedQuotient);
    IO.println("Fractional mean = " + fractionalMean);
}
```

#### ${\color{#276BD1}\textsf{Shared Snippet — Copying Values and References}}$

```java
int score = 84;
int copiedScore = score;
copiedScore = 90;

final int[] scores = {84, 91};
int[] alias = scores;
alias[0] = 90;

int[] independentCopy = scores.clone();
independentCopy[0] = 77;

Integer boxed = scores[0];
int unboxed = boxed;

System.out.println(score);
System.out.println(scores[0]);
System.out.println(independentCopy[0]);
System.out.println(unboxed);
```

#### ${\color{#276BD1}\textsf{Shared Snippet — Numeric Conversion and Promotion}}$

```java
byte limit = 100;
short offset = 20;
int sum = limit + offset;

int largeInteger = 16_777_217;
float approximate = largeInteger;

int truncated = (int) -9.78;
byte lowBits = (byte) 130;

int side = 50_000;
long widenedProduct = side * side;
long longProduct = (long) side * side;

System.out.println(sum);
System.out.println((int) approximate);
System.out.println(truncated);
System.out.println(lowBits);
System.out.println(widenedProduct);
System.out.println(longProduct);
```

#### ${\color{#276BD1}\textsf{Shared Snippet — Code Units and Text}}$

```java
char grade = 'A';
String text = "😀";

System.out.println((int) grade);
System.out.println(text.length());
System.out.println(text.codePointCount(0, text.length()));
```

### ${\color{#276BD1}\textsf{Result and Walkthrough}}$

#### ${\color{#276BD1}\textsf{Complete Programs}}$

**Result** for the class-based program and **expected result** for the Java 25 compact program with input `84` followed by `91`.

```text
Recorded attempts = 0
Widened quotient = 87.0
Fractional mean = 87.5
```

1. `recordedAttempts` is a class field. Java initializes it to zero before the entry point reads it.
2. Both inputs parse as `int`. Adding the two `int` operands produces an `int` result of `175`, so the compact program infers `int` for `var total`.
3. `175 / 2` first yields the integer `87`. The assignment converts that value to `87.0`.
4. `(double) total / SCORE_COUNT` divides `175.0` by `2.0` after numeric promotion. This gives `87.5`.

#### ${\color{#276BD1}\textsf{Copying Values and References}}$

```text
84
90
77
90
```

`copiedScore` holds a separate primitive value, so changing it leaves `score` at `84`. `alias` and `scores` hold references to the same array. Through `alias`, the code changes the first component to `90`. The `final` declaration fixes the reference in `scores` while allowing component updates. `clone()` creates an independent primitive array, so `77` appears only in the copy. Boxing and unboxing preserve the integer `90`.

#### ${\color{#276BD1}\textsf{Numeric Conversion and Promotion}}$

```text
120
16777216
-9
-126
-1794967296
2500000000
```

- Java promotes `limit` and `offset` to `int` before adding them, yielding `120`.
- `16,777,217` is `2²⁴ + 1`. The `float` conversion rounds it to `16,777,216`. Casting that rounded value to `int` displays the precision loss.
- Casting `-9.78` to `int` discards the fraction toward zero. Casting `130` to `byte` retains the eight-bit pattern for unsigned `130`, which represents `130 − 256 = −126` in a signed byte.
- `50,000 × 50,000` is `2,500,000,000`. The `int` product wraps by `2³²` to `-1,794,967,296` before widening. Casting an operand to `long` makes the multiplication itself use `long`, so the second calculation preserves `2,500,000,000`.

#### ${\color{#276BD1}\textsf{Code Units and Text}}$

```text
65
2
1
```

`(int) grade` gives the numeric code-unit value of `'A'`. The string contains one supplementary Unicode code point encoded as two UTF-16 code units, so the two counting methods return different values.

