---
title: AP CS A Unit 2 - Objects, Strings, and Math
---
[Go back to home page](README.md)
# [previous](unit_1.md) <--> [next](unit_3.md)

Looking for the new four-unit curriculum? See [New Unit 1](new_unit_1.md).

# AP CS A Unit Two: Objects, Strings, and Math
The basics of trash code: long and unwinded code that does nothing.
## 1. Objects and Reference Variables
### Definition
An **object** is a composite entity in Java, bundling data and behaviors (methods) into a single unit. Objects are instances of **classes**, and **reference variables** store memory addresses pointing to these objects, not the objects themselves. When no reference variables point to an object, it becomes inaccessible and is eligible for **garbage collection**.
**TOP TIP**: Reference variables are *not* objects! They're like campus maps, holding the address of where the object (the lecture hall) resides in memory. Each reference variable has a specific class type it refers to, like `String` or `Math`.
### Key Notes
- Objects are stored in **heap memory**, with reference variables in **stack memory** pointing to them.
- Assigning one reference variable to another copies the address, not the object, so both point to the same object.
- AP CS A Unit Two introduces objects through the `String` and `Math` classes, laying the foundation for object-oriented programming.
### Example Program
```java
public class AcademicObjectQuest {
    public static void main(String[] args) {
        String studentName = new String("@drasimov"); // Reference to a String object
        String alias = studentName; // Points to the same object
        System.out.println("Student: " + studentName);
        System.out.println("Alias: " + alias);
        studentName = null; // Object still exists via alias
        System.out.println("Alias after nulling: " + alias);
        alias = null; // Object now eligible for garbage collection
        // System.out.println(studentName.toUpperCase()); // NullPointerException!
    }
}
```
**Output**:
```
Student: @drasimov
Alias: @drasimov
Alias after nulling: @drasimov
```
### Common Errors
- **NullPointerException**: Accessing methods on a `null` reference. Example: `String name = null; name.length();`.
- **Misunderstanding References**: Assuming assigning a reference copies the object. Example: `String a = b;` makes `a` and `b` point to the same object.
---
## 2. String Class
### Definition
The `String` class represents immutable sequences of characters. Strings are objects, created using literals (e.g., `"Hello"`) or the `new` keyword. Their immutability means operations like concatenation create new `String` objects rather than modifying existing ones.
### Common Methods
- `int length()`: Returns the number of characters.
- `String substring(int start, int end)`: Returns a substring from `start` (inclusive) to `end` (exclusive).
- `String substring(int start)`: Returns a substring from `start` to the end.
- `int indexOf(String str)`: Returns the first index of `str`, or -1 if not found.
- `String toUpperCase()`, `String toLowerCase()`: Converts to upper or lower case.
- `char charAt(int index)`: Returns the character at `index`.
- `int compareTo(String other)`: Compares strings lexicographically (returns negative, zero, or positive).
### Key Notes
- Strings are immutable, so methods return new strings rather than modifying the original.
- Concatenation with `+` creates new `String` objects, which can be inefficient in loops.
- String literals are stored in the **string pool** for efficiency.
### Trash Code Example
Here's some *epic trash code* that overcomplicates extracting a student's initials:
```java
public class EpicInitialsExtractor {
    public static void main(String[] args) {
        String fullName = "Alan Turing"; // The genius of CS
        String initials = ""; // Prepare for the ultimate initial quest
        int spaceIndex = -1; // Where's that space hiding?
        for (int i = 0; i < fullName.length(); i++) { // Super slow space hunt
            if (fullName.charAt(i) == ' ') {
                spaceIndex = i;
                break; // Gotcha!
            }
        }
        if (spaceIndex != -1) { // Only if we found a space
            initials = initials + fullName.charAt(0); // First initial
            initials = initials + fullName.charAt(spaceIndex + 1); // Last initial
        }
        else {
            initials = fullName.charAt(0) + ""; // Fallback for single names
        }
        System.out.println("Super Complex Initials: " + initials.toUpperCase());
        // Easter Egg: Congrats, you survived the trash code maze!
    }
}
```
**Output**:
```
Super Complex Initials: AT
```
**Why It's Trash**: A simple `initials = "" + fullName.charAt(0) + fullName.charAt(fullName.indexOf(" ") + 1);` would suffice, but we took the scenic route!
### Common Errors
- **IndexOutOfBoundsException**: Accessing invalid indices. Example: `"Hi".substring(3);`.
- **NullPointerException**: Calling methods on a `null` String. Example: `String s = null; s.length();`.
- **Inefficient Concatenation**: Using `+` in loops creates multiple `String` objects.
---
### 2.5 Comparing Objects: equals() vs ==
#### Definition
When comparing objects in Java, it's crucial to understand the difference between the `equals()` method and the `==` operator. This distinction is fundamental in AP CS A for correctly comparing `String` objects and other reference types.
- **`==` Operator**: Compares **references** (memory addresses). Returns `true` only if both references point to the exact same object in memory.
- **`equals()` Method**: Compares **content** or values. For `String` objects, it returns `true` if the sequences of characters are identical.
#### Key Concepts
- **`==` with Primitives**: For primitive types (`int`, `double`, `boolean`), `==` compares values directly.
- **`==` with Objects**: For reference types (`String`, `Integer`, etc.), `==` compares memory addresses, not content.
- **`equals()` Method**: Defined in the `Object` class and overridden by many classes (like `String`) to compare meaningful equality.
- **String Literals vs. `new String()`**: String literals are pooled, so `"hello" == "hello"` may be `true`, but `new String("hello") == "hello"` is `false`.
#### Examples
```java
// Example 1: String literals (may be pooled)
String s1 = "AP";
String s2 = "AP";
System.out.println(s1 == s2);           // true (same object in pool)
System.out.println(s1.equals(s2));      // true (same content)
// Example 2: Explicit new String objects
String s3 = new String("CS");
String s4 = new String("CS");
System.out.println(s3 == s4);           // false (different objects)
System.out.println(s3.equals(s4));      // true (same content)
// Example 3: Mixed literal and new
String s5 = "A";
String s6 = new String("A");
System.out.println(s5 == s6);           // false (different objects)
System.out.println(s5.equals(s6));      // true (same content)
// Example 4: Primitives vs Wrappers
Integer a = 5;
Integer b = 5;
System.out.println(a == b);             // true (autoboxing may cache small values)
Integer c = 500;
Integer d = 500;
System.out.println(c == d);             // false (different objects)
System.out.println(c.equals(d));        // true (same value)
```
#### Best Practices for AP CS A
1. **Always use `equals()` for comparing `String` content**.
   - Correct: `if (str1.equals(str2))`
   - Incorrect: `if (str1 == str2)` (unless intentionally checking same object)
2. **For other objects, check if the class overrides `equals()`**.
   - `Integer`, `Double`, `Boolean` override `equals()` to compare values.
   - Custom classes may need to override `equals()` (covered in Unit 9).
3. **Use `==` for primitives and null checks**.
   - `if (x == 5)` for `int x`
   - `if (obj == null)` to check for null references
#### Common Errors
- **Using `==` to compare strings**: Leads to logical bugs when strings are created differently.
- **NullPointerException with `equals()`**: Calling `str1.equals(str2)` when `str1` is `null`. Use `"constant".equals(variable)` or check for null first.
- **Assuming `==` works for wrapper objects**: For `Integer`, `Double`, etc., `==` may work for small cached values (-128 to 127) but not for larger values.
#### Example Program
```java
public class StringComparisonDemo {
    public static void main(String[] args) {
        String correctPassword = "APCS2025";
        String userInput1 = "APCS2025";
        String userInput2 = new String("APCS2025");
        System.out.println("Testing password validation:");
        System.out.println("correctPassword == userInput1: " + (correctPassword == userInput1));
        System.out.println("correctPassword.equals(userInput1): " + correctPassword.equals(userInput1));
        System.out.println("correctPassword == userInput2: " + (correctPassword == userInput2));
        System.out.println("correctPassword.equals(userInput2): " + correctPassword.equals(userInput2));
        // Safe comparison practice
        boolean isValid = correctPassword.equals(userInput2);
        System.out.println("Password valid? " + isValid);
        // Null-safe comparison
        String maybeNull = null;
        System.out.println("Null-safe check: " + "APCS2025".equals(maybeNull));
    }
}
```
**Output**:
```
Testing password validation:
correctPassword == userInput1: true
correctPassword.equals(userInput1): true
correctPassword == userInput2: false
correctPassword.equals(userInput2): true
Password valid? true
Null-safe check: false
```
---
## 3. Math Class
### Definition
The `Math` class provides static methods and constants for mathematical operations. It's a utility class, not instantiated, and is crucial for calculations in AP CS A.
### Key Methods and Constants
- `double random()`: Returns a random `double` in [0.0, 1.0).
- Random integer in range `[min, max]`: `(int)(Math.random() * (max - min + 1)) + min`.
- `double abs(double x)`: Returns the absolute value.
- `double pow(double base, double exponent)`: Returns `base` raised to `exponent`.
- `double sqrt(double x)`: Returns the square root.
- `double min(double a, double b)`, `double max(double a, double b)`: Returns the minimum or maximum.
- `double PI`: Constant for π (approximately 3.14159).
### Extended Methods
- `double sin(double radians)`, `double cos(double radians)`: Trigonometric functions.
- `double log(double x)`: Natural logarithm.
- `double exp(double x)`: Returns `e^x`.
### Key Notes
- All `Math` methods are `static`, called as `Math.methodName()`.
- `Math.random()` is pseudo-random, sufficient for AP CS A applications.
- Extended methods are useful for advanced calculations, though less common in Unit Two.
### Trash Code Example
Here's a *ridiculously verbose* way to generate a random AP score (1 to 5):
```java
public class RandomAPScoreGenerator {
    public static void main(String[] args) {
        double randomValue = Math.random(); // The magic number
        double scaledValue = randomValue * (5 - 1 + 1); // Scale to 1-5
        double shiftedValue = scaledValue + 1; // Shift to start at 1
        int apScore = (int) shiftedValue; // Truncate to int
        String scoreMessage = ""; // Build the ultimate message
        for (int i = 0; i < 1; i++) { // Why loop? Because trash!
            scoreMessage = "Your randomly generated AP score is: " + apScore;
        }
        System.out.println(scoreMessage);
        // Easter Egg: Did you just roll a 5? GPA vibes!
    }
}
```
**Output**:
```
Your randomly generated AP score is: 3
```
**Why It's Trash**: A single line `(int)(Math.random() * 5 + 1)` would do, but we savored every unnecessary step!
### Common Errors
- **Off-by-One Errors**: Incorrect range in random number generation. Example: `(int)(Math.random() * 5)` gives 0 to 4.
- **Casting Oversight**: Forgetting to cast `Math.random()`'s `double` to `int`. Example: `int score = Math.random() * 5;`.
---
## 4. Methods
### Definition
A **method** is a reusable block of code that performs a specific task, often taking **parameters** (inputs) and returning a value (or `void` if no return). In Unit Two, methods are introduced via `String` and `Math` class methods and basic user-defined methods.
### Key Concepts
- **Declaration**: `returnType methodName(parameterType param) { ... }`.
- **Return Types**: `int`, `double`, `String`, etc., or `void` for no return.
- **Parameters**: Variables passed to the method, e.g., `substring(int start)`.
- **Calling Methods**: Use `object.methodName(args)` for instance methods (e.g., `String`) or `Class.methodName(args)` for static methods (e.g., `Math`).
### Example Program
```java
public class GPACalculator {
    public static double boostGPA(double currentGpa, double bonus) {
        return currentGpa + bonus; // Simple GPA boost
    }
    public static void main(String[] args) {
        double gpa = 3.5;
        double boostedGpa = boostGPA(gpa, 0.5); // Call our method
        System.out.println("Original GPA: " + gpa);
        System.out.println("Boosted GPA: " + boostedGpa);
        // Easter Egg: Max GPA achieved? You're an AP legend!
    }
}
```
**Output**:
```
Original GPA: 3.5
Boosted GPA: 4.0
```
### Common Errors
- **Incorrect Return Type**: Returning a `double` from an `int` method. Example: `int method() { return 3.5; }`.
- **Missing Return**: Omitting a return statement in a non-`void` method.
- **Parameter Mismatch**: Passing wrong types or number of arguments.
---
## 5. Scope and Null References
### Scope
- **Local Variables**: Declared inside a method, accessible only within it.
- **Instance Variables**: Declared in a class, accessible to all methods (introduced later in AP CS A).
- **Block Scope**: Variables in `{}` blocks (e.g., loops) are limited to that block.
### Null References
- A reference variable set to `null` points to no object.
- Accessing methods on a `null` reference causes a `NullPointerException`.
- Use `if (variable != null)` to check before accessing.
### Example Program
```java
public class StudentRecord {
    public static void main(String[] args) {
        String studentName = "Grace Hopper";
        if (studentName != null) { // Safe check
            String scopeDemo = studentName.toUpperCase(); // Local variable
            System.out.println("Name: " + scopeDemo);
        }
        // System.out.println(scopeDemo); // Error: scopeDemo out of scope
        studentName = null;
        // studentName.length(); // NullPointerException!
        System.out.println("Record cleared.");
        // Easter Egg: Null? Like forgetting your AP exam date!
    }
}
```
**Output**:
```
Name: GRACE HOPPER
Record cleared.
```
### Common Errors
- **Scope Violation**: Accessing a variable outside its scope. Example: Using a loop variable after the loop.
- **NullPointerException**: Not checking for `null` before method calls.
---
## 6. Connection to AP CS A Unit Two
### Curriculum Context
AP CS A Unit Two builds on Unit 1 by introducing:
- **Objects**: Using `String` and `Math` to explore reference variables and methods.
- **String Manipulation**: Processing text for academic applications (e.g., formatting names).
- **Math Operations**: Performing calculations like random score generation.
- **Methods**: Calling and defining simple methods for reusable logic.
- **Scope and Null**: Understanding variable accessibility and safe object handling.
### Relevance
- `String` methods are essential for text processing in AP problems (e.g., parsing input).
- `Math` methods support calculations like averages or random selections.
- Understanding references and scope prevents common errors like `NullPointerException`.
### Practice Questions
1. **Code Tracing**: What is the output?
   ```java
   String name = "AP CS A";
   System.out.println(name.substring(0, 2));
   ```
   **Answer**: `AP`
2. **Error Identification**: Why does this fail?
   ```java
   String s = null;
   System.out.println(s.length());
   ```
   **Answer**: `NullPointerException` because `s` is `null`. Check with `if (s != null)`.
3. **Coding Exercise**: Write a method that takes a `String` name and returns its first three characters, or the full name if shorter.
---
## 7. Additional Notes
### Best Practices
- Use meaningful variable names (e.g., `studentName` instead of `s`) for clarity.
- Check for `null` before calling object methods.
- Avoid excessive string concatenation in loops; consider `StringBuilder` (see extensions).
- Comment trash code to explain its glorious inefficiency.
### 7.1 Wrapper Classes and Autoboxing
#### Definition
Wrapper classes are object representations of primitive data types, allowing primitives to be used in contexts that require objects (e.g., collections like `ArrayList`). In AP CS A, the most commonly used wrapper classes are `Integer`, `Double`, and `Boolean`, corresponding to `int`, `double`, and `boolean` primitives.
#### Key Concepts
- **Autoboxing**: Automatic conversion of a primitive to its corresponding wrapper object.
  ```java
  Integer wrappedScore = 5; // Autoboxing: int 5 becomes Integer object
  ```
- **Unboxing**: Automatic conversion of a wrapper object to its primitive value.
  ```java
  int primitiveScore = wrappedScore; // Unboxing: Integer object becomes int
  ```
- **Common Wrapper Classes**:
  - `Integer` for `int`
  - `Double` for `double`
  - `Boolean` for `boolean`
  - `Character` for `char`
  - `Byte` for `byte`
  - `Short` for `short`
  - `Long` for `long`
  - `Float` for `float`
#### Why Use Wrapper Classes?
1. **Collections Requirement**: `ArrayList` and other Java collections can only store objects, not primitives.
   ```java
   ArrayList<Integer> scores = new ArrayList<Integer>();
   scores.add(95); // Autoboxing: int 95 → Integer
   int first = scores.get(0); // Unboxing: Integer → int
   ```
2. **Object Methods**: Wrapper classes provide useful methods like `Integer.parseInt()` or `Double.isNaN()`.
3. **Nullability**: Wrapper objects can be `null`, representing the absence of a value (primitives cannot be `null`).
#### Important Methods
- **`Integer.parseInt(String s)`**: Converts a `String` to an `int`.
  ```java
  String input = "42";
  int value = Integer.parseInt(input); // value = 42
  ```
- **`Double.parseDouble(String s)`**: Converts a `String` to a `double`.
- **`Integer.toString(int i)`**: Converts an `int` to a `String`.
- **`Integer.MAX_VALUE`, `Integer.MIN_VALUE`**: Constants for maximum and minimum `int` values.
- **`Double.NaN`, `Double.POSITIVE_INFINITY`**: Special double values.
#### Autoboxing/Unboxing Examples
```java
// Autoboxing examples
Integer a = 10; // Primitive int 10 autoboxed to Integer
Double b = 3.14; // Primitive double 3.14 autoboxed to Double
Boolean c = true; // Primitive boolean true autoboxed to Boolean
// Unboxing examples
int x = a; // Integer a unboxed to int
double y = b; // Double b unboxed to double
boolean z = c; // Boolean c unboxed to boolean
// Mixed operations (autoboxing/unboxing happens automatically)
Integer sum = a + 5; // a unboxed to int, addition performed, result autoboxed to Integer
```
#### Caching and Performance
- Java caches wrapper objects for small values (e.g., `Integer` values from -128 to 127) for performance.
- This can lead to surprising results with `==` comparison:
  ```java
  Integer i1 = 127;
  Integer i2 = 127;
  System.out.println(i1 == i2); // true (same cached object)
  Integer i3 = 128;
  Integer i4 = 128;
  System.out.println(i3 == i4); // false (different objects)
  ```
- **Always use `equals()` to compare wrapper objects for value equality**.
#### Common Errors
- **NullPointerException when Unboxing**: Unboxing a `null` wrapper causes `NullPointerException`.
  ```java
  Integer score = null;
  int s = score; // NullPointerException!
  ```
- **Performance Overhead**: Excessive autoboxing/unboxing in loops can impact performance.
- **Incorrect Method Overloading**: Methods overloaded for primitive and wrapper types may behave unexpectedly.
#### Example Program
```java
public class WrapperDemo {
    public static void main(String[] args) {
        // Autoboxing in ArrayList
        ArrayList<Integer> apScores = new ArrayList<Integer>();
        apScores.add(5); // Autoboxing
        apScores.add(4);
        apScores.add(3);
        // Unboxing for calculation
        int total = 0;
        for (Integer score : apScores) {
            total += score; // Unboxing in each iteration
        }
        double average = (double) total / apScores.size();
        System.out.println("Average AP Score: " + average);
        // String conversion
        String input = "95";
        int grade = Integer.parseInt(input);
        System.out.println("Parsed grade: " + grade);
        // Null safety check
        Integer possibleNull = null;
        if (possibleNull != null) {
            int safeValue = possibleNull; // Would throw NPE without check
        }
    }
}
```
### Extensions
- **StringBuilder**: A mutable alternative to `String` for efficient concatenation.
  ```java
  StringBuilder sb = new StringBuilder();
  sb.append("AP").append("CS").append("A");
  String result = sb.toString(); // "APCSA"
  ```
- **Advanced Math**: Use `Math.sin()`, `Math.cos()`, `Math.log()`, `Math.exp()` for scientific calculations.
  ```java
  double angle = Math.PI / 2;
  System.out.println(Math.sin(angle)); // 1.0
  ```

---

## 8. The Rest of the String Toolkit
### Definition
The `String` class has more methods than the core six. AP CS A free-response questions love the small ones (`contains`, `startsWith`, `substring`, `indexOf`) because chaining them character-by-character is the classic trash-code move.
### More Common Methods
- `boolean equalsIgnoreCase(String other)`: Content comparison ignoring case.
- `boolean contains(String str)`: True if `str` appears anywhere inside this string.
- `boolean startsWith(String prefix)`, `boolean endsWith(String suffix)`: Prefix/suffix checks.
- `String replace(char oldChar, char newChar)`, `String replace(String target, String replacement)`.
- `String trim()`: Removes leading and trailing whitespace.
- `boolean isEmpty()`: True when `length() == 0`.
- `static String valueOf(x)`: Converts almost anything to a `String` (e.g. `String.valueOf(5)` is `"5"`).
- `int compareTo(String other)`: Negative if this string comes first lexicographically, positive if it comes after, zero if equal.
### Example Program
```java
public class StringToolkit {
    public static void main(String[] args) {
        String course = "  AP Computer Science A  ";
        String trimmed = course.trim();
        System.out.println("Trimmed: [" + trimmed + "]");
        System.out.println("Starts with AP? " + trimmed.startsWith("AP"));
        System.out.println("Contains 'Science'? " + trimmed.contains("Science"));
        System.out.println("Ends with 'A'? " + trimmed.endsWith("A"));
        System.out.println("IgnoreCase match? " + trimmed.equalsIgnoreCase("ap computer science a"));
        System.out.println("Replaced: " + trimmed.replace('A', 'X'));
        System.out.println("Length: " + trimmed.length());
        System.out.println("As text: " + String.valueOf(5));
    }
}
```
**Output**:
```
Trimmed: [AP Computer Science A]
Starts with AP? true
Contains 'Science'? true
Ends with 'A'? true
IgnoreCase match? true
Replaced: XP Computer Science X
Length: 23
As text: 5
```
### Common Errors
- **Forgetting `trim()`**: Input with leading spaces makes `startsWith("AP")` false even when it looks true.
- **Confusing `replace` overloads**: `replace(char, char)` and `replace(String, String)` are different methods.
- **`compareTo` direction**: `"A".compareTo("B")` is negative; students routinely flip the sign in their heads.

## 9. More Math: round, floor, and ceil
### Definition
`Math.round`, `Math.floor`, and `Math.ceil` round or clamp `double`s. They are the respectable alternative to the `(int)(x + 0.5)` trick from [Unit 1](unit_1.md), and the exam does test the return types.
### Methods and Return Types
- `long Math.round(double x)`: Returns a **`long`**, not an `int`. `Math.round(float x)` returns an `int`.
- `double Math.floor(double x)`: Largest integer `double` less than or equal to `x`.
- `double Math.ceil(double x)`: Smallest integer `double` greater than or equal to `x`.
- `int Math.abs(int x)` and `double Math.abs(double x)`: Overloaded absolute value.
### Example Program
```java
public class MathRounding {
    public static void main(String[] args) {
        double gpa = 3.6;
        System.out.println("Round: " + Math.round(gpa));        // 4 (a long)
        System.out.println("Floor: " + Math.floor(gpa));        // 3.0
        System.out.println("Ceil:  " + Math.ceil(gpa));         // 4.0
        System.out.println("Round negative: " + Math.round(-3.6)); // -4
        int dice = (int)(Math.random() * 6) + 1; // 1..6 inclusive
        System.out.println("Die roll: " + dice);
    }
}
```
**Output** (die roll varies):
```
Round: 4
Floor: 3.0
Ceil:  4.0
Round negative: -4
Die roll: 4
```
### Common Errors
- **Assigning `Math.round` to `int` without a cast**: `int x = Math.round(3.6);` fails because the result is a `long`. Use `(int) Math.round(3.6)` or declare `long`.
- **Off-by-one in random ranges**: `(int)(Math.random() * 6)` gives 0-5; add 1 for 1-6.
- **Forgetting both operands**: `(int)(Math.random() * (max - min + 1)) + min` is the full formula for `[min, max]`.

## 10. Methods in Depth: Parameters, Overloading, and Pass-by-Value
### Definition
Java passes arguments **by value**: the method receives a copy. For primitives the copy is the value; for references the copy is the address. A method can never reassign the caller's variable, but it *can* mutate the object that a copied reference points to. This is the single most misunderstood fact in the unit.
### Key Concepts
- **Pass-by-value with primitives**: `void f(int x) { x = 99; }` does not change the caller's variable.
- **Pass-by-value with references**: `void f(String s) { s = "x"; }` does not change the caller's reference, but `StringBuilder` mutation *does* show up.
- **Method overloading**: Same name, different parameter lists (type or count). Return type alone does not distinguish overloads.
- **Static vs. instance**: `static` methods belong to the class (`Math.abs`); instance methods belong to an object (`s.length()`).
### Example Program
```java
public class PassByValueDemo {
    public static void tryToChange(int x) {
        x = 99; // only changes the local copy
    }
    public static void tryToChange(StringBuilder sb) {
        sb.append(" changed"); // mutates the shared object
    }
    public static int bigger(int a, int b) { return a > b ? a : b; }
    public static double bigger(double a, double b) { return a > b ? a : b; }
    public static void main(String[] args) {
        int score = 5;
        tryToChange(score);
        System.out.println("score is still " + score); // 5
        StringBuilder name = new StringBuilder("Grace");
        tryToChange(name);
        System.out.println(name); // Grace changed
        System.out.println(bigger(3, 7));     // 7 (int overload)
        System.out.println(bigger(3.0, 7.5)); // 7.5 (double overload)
    }
}
```
**Output**:
```
score is still 5
Grace changed
7
7.5
```
**TOP TIP**: Think of passing a reference like handing out a photocopy of a campus map. Scribbling a new route on your copy does not change the original map, but walking over to the lecture hall and repainting its door *does* change what everyone sees.
### Common Errors
- **Expecting primitives to change**: Assuming `tryToChange(score)` mutates `score`.
- **Overloading by return type only**: `int f()` and `double f()` do not compile together.
- **Calling a static method through an object**: `Math m = new Math();` is pointless; just use `Math.abs`.

## 11. Trash Code Example: The Name Formatter
### Trash Code Example
A program that formats a first and last name into "Last, First", with a heroic amount of ceremony.
```java
public class TrashyNameFormatter {
    public static void main(String[] args) {
        String fullName = "Grace Hopper";
        String result = "";
        // Step 1: find the space, like no one has ever found a space before
        int space = fullName.indexOf(" ");
        // Step 2: pull out the first name with substring arithmetic
        String first = fullName.substring(0, space);
        // Step 3: pull out the last name with MORE substring arithmetic
        String last = fullName.substring(space + 1, fullName.length());
        // Step 4: uppercase the last name one character at a time
        String upperLast = "";
        for (int i = 0; i < last.length(); i++) {
            upperLast = upperLast + Character.toUpperCase(last.charAt(i));
        }
        // Step 5: assemble with a loop that runs exactly once
        for (int pass = 0; pass < 1; pass++) {
            result = upperLast + ", " + first;
        }
        System.out.println("Formatted: " + result);
        // Easter Egg: you just reimplemented toUpperCase() badly. Proud? You should be.
    }
}
```
**Output**:
```
Formatted: HOPPER, Grace
```
**Why It's Trash**: `last.toUpperCase() + ", " + first` does the whole job. The character-by-character uppercase loop rebuilds a `String` on every iteration (immutability strikes again), and the one-iteration assembly loop is pure theater. Correct output, maximum fuss, the house style.

## 12. Practice Questions with Answers
### Practice Questions
1. **Code tracing**: What is printed?
   ```java
   String s = "APCSA";
   System.out.println(s.substring(1, 4) + s.charAt(0));
   ```
   **Answer**: `PCSA` (`substring(1, 4)` is `"PCS"`, then `'A'`).
2. **equals vs ==**: What is the value of `new String("A").equals("A")` and `new String("A") == "A"`?
   **Answer**: `true` and `false`. `equals` compares content; `==` compares references.
3. **Null safety**: Which is safer when `s` might be `null`: `s.equals("AP")` or `"AP".equals(s)`?
   **Answer**: `"AP".equals(s)`. Calling a method on `null` throws `NullPointerException`.
4. **Math rounding**: What is the declared type of `Math.round(3.6)` and what value does it hold?
   **Answer**: `long`, value `4`. Assigning to `int` requires a cast.
5. **Random range**: Write an expression for a random integer in `[10, 20]`.
   **Answer**: `(int)(Math.random() * 11) + 10`.
6. **Pass-by-value**: What is printed?
   ```java
   static void f(int x) { x = 10; }
   public static void main(String[] a) { int n = 5; f(n); System.out.println(n); }
   ```
   **Answer**: `5`. Primitives are passed by value.

## 13. Multiple Angles: Pseudocode and a Python Aside
### Pseudocode Angle
Generating a random integer in `[min, max]`, in language-agnostic form:
```
r <- a pseudo-random real in [0, 1)
scaled <- r * (max - min + 1)
result <- FLOOR(scaled) + min
```
`String` algorithms follow the same "walk the indices" pattern:
```
FOR i FROM 0 TO length(s) - 1
    IF character at i is a delimiter THEN record i
END FOR
```
### Python Aside (optional, Java stays canonical)
Python hides most of this: `str` is immutable like Java `String`, `==` compares *content* (so the `equals` vs `==` trap simply does not exist), and `random.randint(min, max)` already includes both endpoints. The Java lesson about reference identity and explicit casts is exactly what Python saves you from, which is why you must still know it for the exam.
```python
# Python aside: same ideas, different syntax
s = "APCSA"
print(s[1:4] + s[0])          # PCSA, like substring + charAt
print(s.upper())              # immutable: returns a new string
from random import randint
print(randint(1, 5))          # inclusive, no * (max-min+1) formula
```
Java remains canonical here; the aside only shows that the concepts are portable while the syntax and pitfalls are Java-specific.

## 14. Connection to AP CS A Unit Three
### Connection to AP CS A Unit Three
Everything here feeds directly into [Unit 3](unit_3.md):
- `String.equals()` returns a `boolean` used in `if` conditions.
- `Math.random()` results are compared with relational operators to build ranges.
- Wrapper `Boolean` values and comparison results become the conditions that control selection.
- The methods you wrote become the boolean-returning helpers used in compound conditions.
You cannot write a correct `if` statement until you can produce a trustworthy `boolean`, and that is this unit's job.

---
# [next](unit_3.md)
