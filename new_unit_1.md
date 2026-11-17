---
title: New Unit 1 - Using Objects and Methods
---

[Go back to home page](README.md)

# [next](new_unit_2.md)

# New AP CS A Unit One: Using Objects and Methods

**Exam weight: 15%-25% of the multiple-choice section.** This is the unit where Java stops being magic and starts being annoying. It combines the old Unit 1 (primitive types, casting) and old Unit 2 (objects, String, Math) into one giant sandbox. Everything here is the foundation for the other three units, so if you write trash code here, you will write trash code everywhere. That is the goal.

**TOP TIP**: The new exam assumes you can jump between primitives, objects, and method calls without getting a nosebleed. Practice until it is boring. Boring code is the opposite of trash code, which is why you should practice until you can *choose* to be boring.

## 1.1 Introduction to Algorithms, Programming, and Compilers

### Definition
An **algorithm** is a finite, ordered sequence of steps that solves a problem or accomplishes a task. **Programming** is expressing an algorithm in a language a computer can follow. A **compiler** translates human-readable source code (`.java` files) into **bytecode** (`.class` files) that the Java Virtual Machine (JVM) can run.

In Java the pipeline is:

```
MyProgram.java  --javac (compiler)-->  MyProgram.class  --JVM-->  program runs
```

If the compiler finds a syntax error, there is no bytecode and no program. The compiler is the world's most pedantic grammar teacher.

### Key Notes
- An algorithm must be **unambiguous**, **finite**, and **ordered**. "Sort the list, but like, vibe it" is not an algorithm.
- Java is **compiled** to bytecode, then **interpreted/JIT-compiled** by the JVM. This is why Java runs on many machines with the same `.class` file.
- Pseudocode is an informal, language-free way to sketch an algorithm before writing Java. It is the training wheels of trash code.

### Pseudocode angle
```
ALGORITHM PrintGreeting
  SET name TO "AP CS A"
  OUTPUT "Hello, " + name
END ALGORITHM
```

The same thing in Java:

```java
public class Greeting {
    public static void main(String[] args) {
        String name = "AP CS A";
        System.out.println("Hello, " + name);
    }
}
```

**Output**:
```
Hello, AP CS A
```

### Common Errors
- **Syntax errors**: missing semicolons or braces are caught by the compiler, not at runtime.
- **Logic errors**: the program compiles but does the wrong thing. These are the sneakiest and the most trash.
- **Runtime errors**: the program compiles and starts, then crashes (e.g. dividing by zero).

## 1.2 Variables and Data Types

### Definition
A **variable** is a named storage location with a type and a value. Java is **statically typed**: you must declare the type before using the variable.

### The three core primitive types
- **`int`**: 32-bit whole number, range −2,147,483,648 to 2,147,483,647 (−2³¹ to 2³¹−1). Example: `int apScore = 5;`
- **`double`**: 64-bit floating-point decimal. Example: `double gpa = 4.0;`
- **`boolean`**: `true` or `false`. Example: `boolean isEnrolled = true;`

### Other primitives you should know
- `byte` (−128 to 127), `short` (−32,768 to 32,767), `long` (about −9 quintillion to 9 quintillion), `float` (32-bit decimal), `char` (single Unicode character).

### Reference types
A **reference variable** stores the address of an object, not the object itself. `String` is the reference type you will meet first:

```java
String student = "Grace Hopper";
```

Primitives live in **stack memory**; objects live in **heap memory**, with the stack holding a reference to them.

### Key Notes
- Variable names begin with a letter, `$`, or `_`, and are case-sensitive. `apScore` and `APScore` are different variables.
- Declaring without initializing leaves a local variable unusable: `int x;` then `System.out.println(x);` fails to compile.

### Common Errors
- **Overflow**: `byte exams = 128;` will not compile because 128 is outside `byte` range.
- **Missing suffix**: `long id = 123456789012;` fails; large `long` literals need `L`. `float f = 3.85;` fails; `float` literals need `f`.

## 1.3 Expressions and Output

### Definition
An **expression** is a combination of literals, variables, operators, and method calls that produces a value. **Output** is done with `System.out.print`, `System.out.println`, and `System.out.printf`.

### Operators
- Arithmetic: `+`, `-`, `*`, `/`, `%` (remainder).
- **Integer division truncates**: `5 / 2` is `2`, not `2.5`. `5.0 / 2` is `2.5`.
- `%` returns the remainder: `5 % 2` is `1`.
- **Operator precedence**: parentheses first, then `* / %`, then `+ -`, left to right.

### String concatenation
When `+` touches a `String`, it concatenates:

```java
int score = 5;
System.out.println("AP Score: " + score);   // AP Score: 5
System.out.println("Sum: " + (3 + 4));      // Sum: 7
System.out.println("Sum: " + 3 + 4);        // Sum: 34 -- trash!
```

### Output methods
- `System.out.print(x)` - prints without a newline.
- `System.out.println(x)` - prints with a newline.
- `System.out.printf("Score: %d GPA: %.2f", score, gpa);` - formatted output (`%d` int, `%f` floating point, `%s` String, `%.2f` two decimals).

### Common Errors
- Forgetting parentheses changes concatenation order, as shown above.
- Mixing integer division with decimals: `int avg = (a + b) / 2;` truncates. Use `2.0` instead.

## 1.4 Assignment Statements and Input

### Definition
An **assignment statement** stores a value into a variable using `=`. The right side is evaluated first, then stored. `int x = 3; x = x + 1;` makes `x` equal `4`.

### Input with Scanner
The `Scanner` class (in `java.util`) reads input. The new exam tests it for both keyboard input and text files (see [New Unit 4](new_unit_4.md)).

```java
import java.util.Scanner;

public class InputDemo {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter your AP score: ");
        int score = sc.nextInt();          // reads an int
        sc.nextLine();                     // consume the leftover newline
        System.out.print("Enter your name: ");
        String name = sc.nextLine();       // reads a whole line
        System.out.println(name + " got a " + score);
        sc.close();
    }
}
```

**Sample run**:
```
Enter your AP score: 5
Enter your name: Alan
Alan got a 5
```

### Key Scanner methods
- `int nextInt()` - reads the next integer token.
- `String next()` - reads the next whitespace-delimited token.
- `String nextLine()` - reads the rest of the current line.
- `boolean hasNext()` - returns `true` if another token is available.
- `boolean hasNextInt()` - returns `true` if the next token is an integer.

### Key Notes
- Calling `nextInt()` before `nextLine()` leaves a newline behind, so `nextLine()` returns an empty string. Fix it with an extra `sc.nextLine()` to consume the newline. This bug has caused more existential crises than inheritance.

### Common Errors
- **InputMismatchException**: typing "five" when `nextInt()` expects `5`.
- **NoSuchElementException**: calling `nextInt()` when there is no more input. Guard with `hasNext()`.
- Forgetting `import java.util.Scanner;`.

## 1.5 Casting and Range of Variables

### Definition
**Casting** converts a value from one type to another.

- **Implicit (widening)**: automatic, no data loss. `int score = 5; double d = score;` gives `5.0`.
- **Explicit (narrowing)**: manual, may lose data. `double gpa = 3.95; int g = (int) gpa;` gives `3` (truncated, not rounded).

### Rounding
There is no cast that rounds. Use arithmetic or `Math.round`:

```java
double x = 3.95;
int rounded = (int)(x + 0.5);   // 4, works for positive numbers
int alsoRounded = (int)Math.round(x);  // 4, the clean way
```

For negatives, `(int)(x - 0.5)` or `Math.round` handles it correctly.

### Range and overflow
Every primitive has a fixed range. Adding 1 to `Integer.MAX_VALUE` wraps around to `Integer.MIN_VALUE` (overflow). The new exam likes asking you to predict this.

```java
int big = Integer.MAX_VALUE;
System.out.println(big + 1);   // -2147483648
```

### Common Errors
- `int gpa = 3.95;` will not compile; narrowing requires a cast.
- Casting `double` to `int` truncates toward zero, so `(int)-3.95` is `-3`.
- `boolean` cannot be cast to or from any other type.

## 1.6 Compound Assignment Operators

### Definition
Compound assignment operators combine an operation with assignment.

| Operator | Meaning | Example | Result (x = 10) |
| --- | --- | --- | --- |
| `+=` | `x = x + y` | `x += 3` | 13 |
| `-=` | `x = x - y` | `x -= 3` | 7 |
| `*=` | `x = x * y` | `x *= 3` | 30 |
| `/=` | `x = x / y` | `x /= 3` | 3 |
| `%=` | `x = x % y` | `x %= 3` | 1 |

### Increment and decrement
- `x++` / `++x` both add 1. The difference matters inside expressions:
  - `int a = 5; int b = a++;` → `a` is 6, `b` is 5 (post-increment uses old value).
  - `int a = 5; int b = ++a;` → `a` is 6, `b` is 6 (pre-increment uses new value).
- `x--` / `--x` subtract 1 similarly.

### Key Notes
- Compound assignment performs an implicit cast: `int x = 5; x += 2.5;` compiles and gives `7` - it is equivalent to `x = (int)(x + 2.5)`. Writing `x = x + 2.5;` would *not* compile. This is a classic exam trick.

### Common Errors
- Assuming `x += 2.5` and `x = x + 2.5` are the same. They are not.

## 1.7 Application Program Interface (API) and Libraries

### Definition
An **API** (Application Programming Interface) is a set of classes, methods, and constants you can call without knowing how they are implemented. Java's **standard library** is organized into packages.

- `java.lang` - automatically imported (`String`, `Math`, `Integer`, `System`).
- `java.util` - must be imported (`Scanner`, `ArrayList`, `Arrays`).
- `java.io` - must be imported (`File`).

### Importing
```java
import java.util.Scanner;      // one class
import java.util.*;            // everything in the package
```

### Why APIs matter
You are never expected to memorize every method. You are expected to know that APIs exist, how to import them, and how to look them up in documentation. Trash code ignores APIs and reinvents the wheel; we do that on purpose in the examples, but you should know the wheel already exists.

### Common Errors
- Forgetting the `import` statement for non-`java.lang` classes.
- Thinking `Math` needs an import - it does not; `java.lang` is automatic.

## 1.8 Documentation with Comments

### Definition
**Comments** are ignored by the compiler and exist to explain code to humans.

- Single-line: `// explains the next line or the rest of the line`
- Multi-line: `/* ... */`
- Javadoc: `/** ... */` placed before a class or method, used by documentation tools.

```java
/**
 * Returns the area of a circle.
 * @param radius the radius of the circle
 * @return the area as a double
 */
public static double area(double radius) {
    return Math.PI * radius * radius;   // PI * r squared
}
```

### Key Notes
- Comments should explain **why**, not **what**. `i++ // add one to i` is trash commenting; `i++ // move to the next student record` is better.
- On the AP exam, comments never affect the output. They are there for you and the grader's sanity.

### Trash Code Example - over-commenting
```java
public class CommentTrash {
    public static void main(String[] args) {
        int x = 5; // declare x and set it to five, a whole number
        x = x + 1; // add one to x, so now x is six because five plus one is six
        // print x below, which should be six because we just said it is six
        System.out.println(x); // output: 6, obviously
    }
}
```

**Output**:
```
6
```

**Why It's Trash**: The comments say the same thing as the code, in more words. It is documentation written by someone who does not trust the reader - or themselves.

## 1.9 Method Signatures

### Definition
A **method signature** is the method's name plus the ordered list of parameter **types**. The return type is *not* part of the signature.

```java
public static int area(int length, int width)   // signature: area(int, int)
public static double area(double radius)        // signature: area(double)
```

### Overloading
Methods can share a name if their signatures differ. This is **overloading**:

```java
public static int add(int a, int b) { return a + b; }
public static double add(double a, double b) { return a + b; }
```

Java picks the right one based on the argument types. You cannot overload by return type alone:

```java
// int add(int a, int b) and double add(int a, int b) -> compile error
```

### Parameters vs arguments
- **Parameters** are the variables in the method declaration (`int a`).
- **Arguments** are the actual values passed when calling (`add(3, 4)`).

### Common Errors
- Changing only the return type and expecting overloading to work.
- Passing arguments in the wrong order when parameters share a type: `substring(int start, int end)` is not the same as `substring(end, start)`.

## 1.10 Calling Class Methods

### Definition
**Class methods** (also called **static methods**) belong to the class, not to an instance. You call them with `ClassName.methodName(arguments)`.

```java
int abs = Math.abs(-5);           // 5
int max = Math.max(3, 8);         // 8
String s = Integer.toString(42);  // "42"
```

### Key Notes
- Static methods are declared with the `static` keyword.
- `main` itself is static, which is why it can be called without creating an object.
- You cannot call an instance method statically (without an object) unless it is also declared `static`.

### Common Errors
- `Math.random()` with parentheses is a call; `Math.random` without them is not. The exam will try to sneak this past you.

## 1.11 Math Class

### Definition
`Math` is a utility class in `java.lang` with static methods and constants. No import needed, no objects allowed.

### Key methods
- `double random()` - returns a value in `[0.0, 1.0)`.
- `int randomInt = (int)(Math.random() * (max - min + 1)) + min;` - random integer in `[min, max]`.
- `double abs(double x)` - absolute value.
- `double pow(double base, double exp)` - base to the power of exp.
- `double sqrt(double x)` - square root.
- `double min(double a, double b)`, `double max(double a, double b)`.
- `double PI` - approximately 3.14159.
- `long round(double x)` - rounds to the nearest whole number (returns `long`).

### Example Program
```java
public class MathDemo {
    public static void main(String[] args) {
        int die = (int)(Math.random() * 6) + 1;   // 1 to 6
        System.out.println("Die roll: " + die);
        System.out.println("Abs: " + Math.abs(-4.2));
        System.out.println("Pow: " + Math.pow(2, 10));
        System.out.println("Sqrt: " + Math.sqrt(144));
        System.out.println("Rounded: " + Math.round(3.95));
    }
}
```

**Sample output**:
```
Die roll: 4
Abs: 4.2
Pow: 1024.0
Sqrt: 12.0
Rounded: 4
```

### Common Errors
- **Off-by-one**: `(int)(Math.random() * 6)` gives 0-5, not 1-6. Add 1.
- Forgetting the cast: `int x = Math.random() * 5;` will not compile.

## 1.12 Objects: Instances of Classes

### Definition
A **class** is a blueprint; an **object** is one thing built from that blueprint. A class describes **attributes** (data) and **behaviors** (methods). An object is an **instance** of a class.

**TOP TIP**: A reference variable is not the object. It is like a campus map: it holds the address of where the object (the lecture hall) actually lives in memory.

```java
String a = new String("AP");
String b = a;         // b points to the SAME object
System.out.println(a == b);  // true -- same address
```

Objects are stored in **heap memory**; the reference variables live in **stack memory** and point to them. When no reference points to an object, it becomes eligible for **garbage collection**.

### Common Errors
- Assuming `String a = b;` copies the object. It copies the reference. Both variables now point to the same object.

## 1.13 Object Creation and Storage (Instantiation)

### Definition
**Instantiation** is creating an object with the `new` keyword, which calls a **constructor**.

```java
String empty = new String();              // no-arg constructor
String named = new String("AP CS A");     // parameterized constructor
Scanner sc = new Scanner(System.in);
```

### What `new` does
1. Allocates memory on the heap for the object.
2. Calls the constructor to initialize it.
3. Returns a reference, which is stored in the variable.

### Common Errors
- `String s; s.length();` - `s` was never initialized, so this fails to compile.
- `String s = null; s.length();` - compiles, then throws `NullPointerException`. Checking `if (s != null)` first avoids it.

## 1.14 Calling Instance Methods

### Definition
**Instance methods** require an object: `object.method(arguments)`. Unlike static methods, they act on that object's data.

```java
String name = "Grace Hopper";
System.out.println(name.length());             // 12
System.out.println(name.toUpperCase());        // GRACE HOPPER
System.out.println(name.substring(0, 5));      // Grace
System.out.println(name.indexOf("Hopper"));    // 6
```

### Key Notes
- Strings are **immutable**: methods return a new `String` instead of changing the original. `name.toUpperCase()` does not modify `name`.
- Method calls can be chained: `name.trim().toLowerCase().substring(0, 2)`.

### Common Errors
- Ignoring the return value: `name.toUpperCase();` on its own line does nothing useful because the new string is thrown away.
- Calling an instance method as if it were static: `String.length()` is wrong.

## 1.15 String Manipulation

### Definition
The `String` class represents an immutable sequence of characters. Mastering its methods is non-negotiable for the new exam.

### Essential methods
| Method | What it does |
| --- | --- |
| `int length()` | Number of characters |
| `char charAt(int i)` | Character at index `i` |
| `String substring(int start)` | From `start` to the end |
| `String substring(int start, int end)` | From `start` (inclusive) to `end` (exclusive) |
| `int indexOf(String s)` | First index of `s`, or −1 if absent |
| `boolean equals(String s)` | Content equality |
| `int compareTo(String s)` | Lexicographic comparison (negative/0/positive) |
| `String toUpperCase()`, `toLowerCase()` | Case conversion |
| `String trim()` | Removes leading/trailing whitespace |

### `==` vs `equals()`
- `==` compares references (memory addresses) for objects, values for primitives.
- `equals()` compares content for `String`.

```java
String s1 = new String("AP");
String s2 = new String("AP");
System.out.println(s1 == s2);       // false
System.out.println(s1.equals(s2));  // true
```

### Trash Code Example - the scenic route to initials
```java
public class InitialsTrash {
    public static void main(String[] args) {
        String full = "Alan Turing";
        String initials = "";
        int space = -1;
        for (int i = 0; i < full.length(); i++) {
            if (full.charAt(i) == ' ') { space = i; break; }
        }
        if (space != -1) {
            initials += full.charAt(0);
            initials += full.charAt(space + 1);
        }
        System.out.println("Initials: " + initials.toUpperCase());
    }
}
```

**Output**:
```
Initials: AT
```

**Why It's Trash**: `String initials = "" + full.charAt(0) + full.charAt(full.indexOf(' ') + 1);` does the whole job. We took the scenic route and wrote a loop that runs character by character like a tourist with a map.

### Python aside (optional, Java stays canonical)
The same String ideas in Python look like this - notice there is no `charAt`, just indexing:

```python
full = "Alan Turing"
initials = (full[0] + full[full.index(" ") + 1]).upper()
print("Initials:", initials)
```

Do not write this on the AP exam. They will be confused and so will your Java compiler.

### Common Errors
- **IndexOutOfBoundsException**: `"Hi".substring(3);` or `"Hi".charAt(5);`.
- **NullPointerException**: calling any method on a `null` String.
- Using `==` for String content comparison.
- Forgetting that `substring`'s end index is exclusive.

## 2. Connection to AP CS A New Unit One

### Curriculum Context
New Unit 1 merges the old Units 1 and 2. It introduces:
- Variables, primitive types, expressions, and assignment.
- Input via `Scanner`, casting, compound operators, comments.
- APIs/libraries, method signatures, static vs instance methods.
- Objects, instantiation, and the `String` and `Math` classes.

Deep dives for each topic also live in the legacy pages: [old Unit 1](unit_1.md) for primitives and casting, [old Unit 2](unit_2.md) for objects, String, and Math.

### Relevance
Every later unit calls methods, uses objects, and manipulates Strings. Skipping this unit is like building a house on a pile of trash - which, admittedly, is on brand, but still a bad idea.

### Practice Questions
1. **Code tracing**: What is printed?
   ```java
   int x = 5;
   x += 2.5;
   System.out.println(x);
   ```
   **Answer**: `7` (compound assignment implicitly casts).

2. **Error identification**: Why does this fail?
   ```java
   String s = null;
   System.out.println(s.length());
   ```
   **Answer**: `NullPointerException` - `s` points to no object. Check `s != null` first.

3. **Expression output**: What is printed?
   ```java
   System.out.println("Result: " + 5 / 2);
   ```
   **Answer**: `Result: 2` (integer division happens before concatenation).

4. **Method design**: Write a method signature for a method named `avg` that takes two `int`s and returns a `double`.
   **Answer**: `public static double avg(int a, int b)` - the return type is not part of the signature.

5. **Coding exercise**: Write a program that reads a radius from the user with `Scanner` and prints the area using `Math.PI`. Trash version encouraged, but the correct one is `Math.PI * r * r`.

---
# [next](new_unit_2.md)
