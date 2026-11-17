---
title: AP CS A Unit 1 - Primitive Data Types and Casting
---
[Go back to home page](README.md)
# [next](unit_2.md)

Looking for the new four-unit curriculum? See [New Unit 1](new_unit_1.md).

# AP CS A Unit One: Primitive Data Types and Casting
## 1. Primitive Data Types
### Definition
Primitive data types in Java are fundamental data types that store simple values directly in memory. Unlike objects, they lack methods or properties and represent raw data. In AP Computer Science A (AP CS A) Unit One, the primary focus is on `int`, `double`, and `boolean`, though other primitive types exist in Java.
### Core Types for AP CS A
- **`int`**: A 32-bit integer representing whole numbers, with a range of -2,147,483,648 to 2,147,483,647 ($$-2^{31}$$ to $$2^{31}-1$$). Suitable for discrete values like AP scores.
  - Example: `int apScore = 5;`
- **`double`**: A 64-bit floating-point number for decimal values, ideal for precise calculations such as grade point averages (GPAs).
  - Example: `double gpa = 4.0;`
- **`boolean`**: A logical type with values `true` or `false`, used for conditions like enrollment status.
  - Example: `boolean isEnrolled = true;`
### Extended Primitive Types
Beyond AP CS A’s core types, Java includes additional primitive types useful for specific scenarios:
- **`byte`**: An 8-bit integer with a range of -128 to 127. Useful for small counts, such as the number of AP exams taken.
  - Example: `byte apExamsTaken = 3;`
- **`short`**: A 16-bit integer with a range of -32,768 to 32,767. Suitable for intermediate counts, like total students in a school.
  - Example: `short totalStudents = 1500;`
- **`char`**: A 16-bit Unicode character representing a single character, such as a letter grade.
  - Example: `char gradeLetter = 'A';`
- **`long`**: A 64-bit integer with a range of approximately -9 quintillion to 9 quintillion ($$-2^{63}$$ to $$2^{63}-1$$). Used for large values, like a cumulative academic record ID.
  - Example: `long studentId = 123456789012L;` (Note the `L` suffix for `long` literals.)
- **`float`**: A 32-bit floating-point number for decimals with less precision than `double`. Useful for less critical decimal calculations, like temporary GPA estimates.
  - Example: `float tempGpa = 3.85f;` (Note the `f` suffix for `float` literals.)
### Key Notes
- Primitive types are stored in stack memory, ensuring efficiency for simple operations compared to reference types (e.g., `String`), which store references in the stack and data in the heap.
- Variables must be declared with their type before use, e.g., `int apScore = 5;`.
- AP CS A emphasizes `int`, `double`, and `boolean`, but understanding other types enhances versatility in programming.
### Example Program
```java
public class AcademicProfile {
    public static void main(String[] args) {
        // Core AP CS A types
        int apScore = 5; // AP exam score
        double gpa = 4.0; // Grade point average
        boolean isEnrolled = true; // Enrollment status
        // Extended types
        byte apExamsTaken = 3; // Number of AP exams
        short totalStudents = 1500; // Total students in school
        char gradeLetter = 'A'; // Letter grade
        long studentId = 123456789012L; // Unique student ID
        float tempGpa = 3.85f; // Temporary GPA estimate
        System.out.println("Student Profile:");
        System.out.println("AP Score: " + apScore);
        System.out.println("GPA: " + gpa);
        System.out.println("Enrolled: " + isEnrolled);
        System.out.println("Exams Taken: " + apExamsTaken);
        System.out.println("Total Students: " + totalStudents);
        System.out.println("Grade: " + gradeLetter);
        System.out.println("Student ID: " + studentId);
        System.out.println("Temporary GPA: " + tempGpa);
    }
}
```
**Output**:
```
Student Profile:
AP Score: 5
GPA: 4.0
Enrolled: true
Exams Taken: 3
Total Students: 1500
Grade: A
Student ID: 123456789012
Temporary GPA: 3.85
```
### Common Errors
- **Overflow**: Assigning a value beyond a type’s range causes errors. Example: `byte apExams = 128;` exceeds `byte`’s range.
- **Incorrect Type Assignment**: Assigning a `double` to an `int` without casting fails. Example: `int gpa = 4.0;` requires `(int)`.
- **Missing Suffix**: Omitting `L` for `long` or `f` for `float` literals causes compilation errors. Example: `float tempGpa = 3.85;` needs `f`.
---
## 2. Data Type Casting
### Definition
Type casting converts a value from one primitive data type to another. In AP CS A, casting is essential when mixing types in calculations or formatting outputs, such as converting a `double` GPA to an `int` score.
### Types of Casting
1. **Implicit Casting (Widening Conversion)**:
   - Automatically converts a smaller or less precise type to a larger or more precise type (e.g., `int` to `double`).
   - No data loss occurs.
   - Example:
     ```java
     int apScore = 5;
     double scoreAsDouble = apScore; // Implicitly converts to 5.0
     System.out.println(scoreAsDouble); // Output: 5.0
     ```
2. **Explicit Casting (Narrowing Conversion)**:
   - Manually converts a larger or more precise type to a smaller or less precise type (e.g., `double` to `int`).
   - Uses the cast operator, e.g., `(int)`.
   - May cause data loss, such as truncating decimals.
   - Examples:
     ```java
     double gpa = 3.95;
     int truncatedGpa = (int) gpa; // Truncates to 3
     System.out.println(truncatedGpa); // Output: 3
     ```
     ```java
     int exams = 3;
     float examsAsFloat = (float) exams; // Converts to 3.0f
     System.out.println(examsAsFloat); // Output: 3.0
     ```
### Key Rules
- **Syntax**: Use `(targetType)` before the value, e.g., `(int)(gpa)`.
- **Truncation**: Casting `double` or `float` to `int` discards decimals (e.g., `(int) 3.95` yields `3`).
- **No `boolean` Casting**: `boolean` cannot be cast to or from other types.
- **Extended Types**: Casting applies to all primitives (e.g., `long` to `int`, `float` to `double`), but narrowing conversions risk data loss.
### Rounding Doubles to Nearest Integer
To round a `double` to the nearest integer (instead of truncating):
- **Positive Numbers**: `(int)(x + 0.5)`
  - Example: `(int)(3.95 + 0.5)` → `(int)(4.45)` → `4`
- **Negative Numbers**: `(int)(x - 0.5)`
  - Example: `(int)(-3.95 - 0.5)` → `(int)(-4.45)` → `-4`
### Example Program
```java
public class AcademicCasting {
    public static void main(String[] args) {
        // Core type casting
        double gpa = 3.95;
        int truncatedGpa = (int) gpa; // Truncates to 3
        int roundedGpa = (int)(gpa + 0.5); // Rounds to 4
        int apScore = 5;
        double scoreAsDouble = apScore; // Implicitly 5.0
        // Extended type casting
        long studentId = 123456789012L;
        int shortId = (int) studentId; // Narrows, may lose data
        float tempGpa = 3.85f;
        double preciseGpa = tempGpa; // Widens to double
        System.out.println("Truncated GPA: " + truncatedGpa);
        System.out.println("Rounded GPA: " + roundedGpa);
        System.out.println("AP Score as Double: " + scoreAsDouble);
        System.out.println("Shortened Student ID: " + shortId);
        System.out.println("Precise GPA: " + preciseGpa);
    }
}
```
**Output**:
```
Truncated GPA: 3
Rounded GPA: 4
AP Score as Double: 5.0
Shortened Student ID: 1665732
Precise GPA: 3.8499999046325684
```
### Common Errors
- **Missing Cast**: Narrowing conversions require explicit casting. Example: `int gpa = 3.95;` fails without `(int)`.
- **Rounding Errors**: Using the positive rounding formula for negative numbers yields incorrect results. Example: `(int)(-3.95 + 0.5)` → `-3` (should be `-4`).
- **Overflow in Narrowing**: Casting a `long` to `int` may produce unexpected results if the value exceeds `int`’s range.
---
## 3. Connection to AP CS A Unit One
### Curriculum Context
AP CS A Unit One introduces Java programming fundamentals, including:
- **Variables and Data Types**: Declaring and using `int`, `double`, and `boolean` to represent academic data like scores and GPAs.
- **Basic Operations**: Arithmetic operations (`+`, `-`, `*`, `/`, `%`) often require casting for mixed types (e.g., averaging `int` scores as a `double`).
- **Input/Output**: Using `System.out.println` to display results, sometimes requiring casting for formatting.
- **Program Structure**: Writing `main` methods and simple programs to process academic data.
### Relevance of Casting
- Casting is critical for calculations involving mixed types, such as computing a GPA from integer scores.
- It facilitates formatting output (e.g., truncating a `double` GPA for display).
- Rounding techniques are practical for real-world applications, like converting GPAs to integer scales.
### Practice Questions
1. **Code Tracing**: What is the output of this code?
   ```java
   double gpa = 4.45;
   int roundedGpa = (int)(gpa + 0.5);
   System.out.println(roundedGpa);
   ```
   **Answer**: `4`
2. **Error Identification**: Why does this code fail?
   ```java
   float tempGpa = 3.85;
   int gpa = tempGpa;
   ```
   **Answer**: A `float` cannot be assigned to an `int` without explicit casting. Correct: `int$gpa = (int) tempGpa;`.
3. **Coding Exercise**: Write a program that takes a `double` GPA and rounds it to the nearest integer, handling positive and negative inputs correctly.
---
## 4. Additional Notes
### Best Practices
- Use meaningful variable names (e.g., `apScore` instead of `x`) to enhance readability.
- Comment complex casting or rounding logic for clarity.
- Test edge cases (e.g., `0.5`, `-0.5`, large `long` values) to ensure robustness.
### Extensions
- The `Math` class provides methods like `Math.round`, `Math.floor`, and `Math.ceil` for advanced rounding, introduced later in AP CS A.
- Casting affects arithmetic: `(double) 5 / 2` yields `2.5`, while `5 / 2` yields `2`.
- Extended types like `char` can be used for letter grades, and `long` for unique identifiers, expanding the scope of academic applications.

---

## 5. Variables, Declaration, and Constants
### Definition
A **variable** is a named location in memory that holds a value of a specific type. Declaring a variable tells the compiler its type and name; initializing it gives it a first value. In trash-code tradition the two are constantly conflated, but the compiler is not fooled.
### Declaration and Initialization
- Declaration: `int apScore;` reserves a slot for an `int`.
- Initialization: `apScore = 5;` stores a value in that slot.
- Combined: `int apScore = 5;` does both, and is what you should write essentially every time.
- Multiple declarations: `int a = 1, b = 2;` is legal but considered trashy because it hides types on a shared line.
### Constants
A variable declared `final` cannot be reassigned after initialization. Constants are conventionally written in `ALL_CAPS`.
```java
final int MAX_AP_SCORE = 5;
final double WEIGHT_OF_EXAM = 0.40;
// MAX_AP_SCORE = 4; // compile-time error: cannot assign to a final variable
```
**TOP TIP**: A `final` *reference* still points to a mutable object; it is the address that is frozen, not the object itself. That delicious distinction becomes very important in [Unit 2](unit_2.md).
### Example Program: Academic Constants
```java
public class AcademicConstants {
    public static void main(String[] args) {
        final int MAX_SCORE = 5;
        final double PASSING_GPA = 2.0;
        int apScore = 5;
        double gpa = 3.7;
        boolean onHonorRoll = gpa >= PASSING_GPA && apScore <= MAX_SCORE;
        System.out.println("Score: " + apScore);
        System.out.println("GPA: " + gpa);
        System.out.println("Honor roll eligible: " + onHonorRoll);
    }
}
```
**Output**:
```
Score: 5
GPA: 3.7
Honor roll eligible: true
```
### Common Errors
- **Uninitialized local variable**: `int x; System.out.println(x);` fails because local variables have no default value.
- **Reassigning a `final`**: `final int X = 1; X = 2;` will not compile.
- **Name collisions**: Declaring `int apScore` twice in the same scope fails; a local variable cannot be redeclared.

## 6. Arithmetic Operators and Expressions
### Definition
Java supports the usual arithmetic operators on numeric primitives: `+`, `-`, `*`, `/`, and `%`. Knowing exactly how they behave on `int` versus `double` is the difference between a 5 and a "why is my average 3 instead of 3.5".
### The Operators
- `+` addition (also string concatenation when either operand is a `String`).
- `-` subtraction.
- `*` multiplication.
- `/` division: **integer division truncates** when both operands are integers; if either operand is a `double`, the result is a `double`.
- `%` remainder (modulus): returns the remainder of division, e.g. `7 % 3` is `1`. It works on `double`s too, but AP CS A focuses on integers.
### Integer Division and Modulus in Action
```java
int a = 7;
int b = 3;
System.out.println(a / b);          // 2  (truncated, not 2.333...)
System.out.println(a % b);          // 1
System.out.println((double) a / b); // 2.3333333333333335
System.out.println(5 / 2);          // 2
System.out.println(5.0 / 2);        // 2.5
```
### Operator Precedence and Associativity
- Parentheses `()` bind first.
- Multiplication, division, and remainder `*` `/` `%` bind before addition and subtraction `+` `-`.
- Operators of equal precedence evaluate **left to right**.
- `2 + 3 * 4` is `14`, not `20`; `(2 + 3) * 4` is `20`.
### Compound Assignment and Increment/Decrement
- `x += 5` is shorthand for `x = x + 5`, and it performs an implicit cast. That is why `int x = 5; x += 2.5;` actually compiles and yields `7`.
- `-=`, `*=`, `/=`, `%=` behave the same way.
- `++` and `--` add or subtract one. Prefix `++x` increments before use; postfix `x++` uses the old value first.
```java
int score = 5;
System.out.println(score++); // prints 5, score becomes 6
System.out.println(++score); // score becomes 7, prints 7
score += 3;                  // score is 10
```
### Common Errors
- **Forgetting integer division**: `double avg = (a + b) / 2;` with `int a, b` still performs integer division before widening. Cast first: `(double)(a + b) / 2`.
- **Modulus by zero**: `int x = 5 % 0;` throws `ArithmeticException` at runtime.
- **Prefix/postfix confusion**: `int y = x++ + ++x;` is legal but a trash-code classic; never write it.

## 7. Trash Code Example: The GPA Averaging Ceremony
### Trash Code Example
Behold a program that averages three `int` exam scores into a `double` GPA, but refuses to simply add three numbers.
```java
public class TrashyAverage {
    public static void main(String[] args) {
        int s1 = 95, s2 = 88, s3 = 91;
        double total = 0.0;
        // Step 1: convert each score to a double the hard way
        double d1 = s1 + 0.0;
        double d2 = s2 + 0.0;
        double d3 = s3 + 0.0;
        // Step 2: add them one at a time with pointless intermediate variables
        double sum1 = d1 + d2;
        double sum2 = sum1 + d3;
        double sum3 = sum2 + 0;
        // Step 3: divide by a double stored in a variable named after a building
        double lectureHall = 3.0;
        double average = sum3 / lectureHall;
        // Step 4: round to two decimals with a bizarre truncation trick
        average = (int)(average * 100 + 0.5) / 100.0;
        System.out.println("Average: " + average);
    }
}
```
**Output**:
```
Average: 91.33
```
**Why It's Trash**: The entire ceremony collapses to `double average = (s1 + s2 + s3) / 3.0;`. Every intermediate variable is a costume; `d1`, `sum2`, and `lectureHall` exist only to pad the lecture-hall analogy. The "round to two decimals" step uses integer truncation in a trench coat instead of just printing with `printf`. It is correct, technically, which is exactly what makes it perfect trash code.

## 8. Practice Questions with Answers
### Practice Questions
1. **Evaluate the expression**: What are the values of `7 / 2`, `7 % 2`, and `7.0 / 2`?
   **Answer**: `3`, `1`, and `3.5`. The first two are integer operations; the last uses a `double` operand.
2. **Code tracing**: What is printed?
   ```java
   int x = 3;
   x += 2;
   x++;
   System.out.println(x);
   ```
   **Answer**: `6`.
3. **Casting**: What is the value of `(int)(3.7 + 0.5)`?
   **Answer**: `4`. `3.7 + 0.5` is `4.2`, and the cast truncates to `4`.
4. **Boolean from primitives**: Is `boolean b = (5 / 2 == 2);` valid, and what is `b`?
   **Answer**: Yes. `5 / 2` is `2`, so the comparison is `true`.
5. **Error identification**: Why does `int gpa = 3.95;` fail, and what are two ways to fix it?
   **Answer**: Narrowing a `double` to an `int` requires an explicit cast. Use `int gpa = (int) 3.95;` (yields `3`) or change the variable to `double gpa = 3.95;`.
6. **Coding exercise**: Write a single expression that computes the average of `int` variables `a`, `b`, `c` as a `double`, then state what breaks if you omit the cast.
   **Answer**: `(double)(a + b + c) / 3`. Without the cast, `a + b + c` is an `int`, so dividing by `3` truncates before widening; e.g. `(1 + 1 + 2) / 3` gives `1.0` instead of `1.333...`.

## 9. Multiple Angles: Pseudocode and a Python Aside
### Pseudocode Angle
Rounding a positive `double` to the nearest integer, in language-agnostic form:
```
IF x >= 0 THEN
    result <- FLOOR(x + 0.5)
ELSE
    result <- CEILING(x - 0.5)
END IF
```
That is exactly what `(int)(x + 0.5)` and `(int)(x - 0.5)` implement in Java, using truncation as a stand-in for floor/ceiling.
### Python Aside (optional, Java stays canonical)
Python has no primitive casts; `int(x)` truncates toward zero just like Java's `(int)`, but `int` and `float` are objects and arithmetic between them promotes automatically. Python's `/` always returns a float (no integer-division surprise); `//` is the truncating operator. The Java lesson about which operand's type decides the result is identical.
```python
# Python aside: same idea, different syntax
gpa = 3.95
truncated = int(gpa)          # 3, like (int) gpa in Java
rounded = int(gpa + 0.5)      # 4
average = (95 + 88 + 91) / 3  # 91.333..., no cast needed in Python
```
Java remains canonical on this site; the aside exists only to show that the *concept* is portable while the *syntax* is not. In Java you must still write `(double)` to avoid integer division.

## 10. Connection to AP CS A Unit Two
### Connection to AP CS A Unit Two
The primitives here are the raw material for everything in [Unit 2](unit_2.md):
- `String` concatenation (`"Score: " + apScore`) widens an `int` into text without any explicit cast.
- `Math` methods take and return `double`s, so `(int)` often appears immediately after `Math.random()` or `Math.sqrt()`.
- Wrapper classes wrap these primitives so they can live inside `ArrayList`s.
- `boolean` expressions here become the conditions that drive `if` statements in [Unit 3](unit_3.md).
Master the casts now; the objects in Unit 2 will not cast for you.

---
# [next](unit_2.md)
