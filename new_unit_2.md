---
title: New Unit 2 - Selection and Iteration
---

[Go back to home page](README.md)

# [previous](new_unit_1.md) <--> [next](new_unit_3.md)

# New AP CS A Unit Two: Selection and Iteration

**Exam weight: 25%-35% of the multiple-choice section** - the second-heaviest unit, so treat it with the respect due to something that can ruin your score. This unit merges the old Unit 3 (Boolean expressions and conditionals) with the old Unit 4 (loops, searching, sorting). It is all about making decisions and doing things repeatedly, which is basically what every program ever written does.

**TOP TIP**: Almost every AP free-response question is a loop with an `if` inside it. If you can trace one of those on paper without running the code, you are already halfway to a 5.

## 2.1 Algorithms with Selection and Repetition

### Definition
Algorithms are built from three control structures:
- **Sequencing**: statements execute in order.
- **Selection**: choosing whether to execute a statement, using `if` / `else`.
- **Iteration**: repeating statements, using `for` / `while`.

### Pseudocode angle
```
ALGORITHM CountPassingScores
  SET count TO 0
  FOR EACH score IN scores
    IF score >= 3 THEN
      count = count + 1
    END IF
  END FOR
  OUTPUT count
END ALGORITHM
```

That is selection (the `IF`) living inside iteration (the `FOR`). Get used to this shape - it is the bread and butter of the exam.

### Key Notes
- New Unit 1 covered **sequencing**. This unit adds the other two.
- Every loop should have a clear termination condition. "Loop until you feel done" is not a condition, though it is how many trash programs feel.

## 2.2 Boolean Expressions

### Definition
A **Boolean expression** evaluates to `true` or `false`. It is built from relational and logical operators.

### Relational operators
| Operator | Meaning | Example (x = 5) |
| --- | --- | --- |
| `<` | less than | `x < 10` → true |
| `>` | greater than | `x > 10` → false |
| `<=` | less than or equal | `x <= 5` → true |
| `>=` | greater than or equal | `x >= 5` → true |
| `==` | equal to | `x == 5` → true |
| `!=` | not equal to | `x != 5` → false |

### Logical operators
- `&&` - AND (both must be true)
- `||` - OR (at least one true)
- `!` - NOT (flips the value)

### Short-circuit evaluation
- With `&&`, if the left side is false, the right side is **not evaluated**.
- With `||`, if the left side is true, the right side is **not evaluated**.

```java
int x = 0;
if (x != 0 && 10 / x > 1) {   // safe: 10/x never runs
    System.out.println("never");
}
```

This is not just trivia. Short-circuiting prevents `NullPointerException` and division by zero in guards.

### Common Errors
- `=` versus `==`: `if (x = 5)` is an assignment and will not compile inside an `if` condition (unless `x` is a boolean, in which case it compiles and does something you did not mean).
- Applying `&&` / `||` to non-boolean values: `if (5 && 3)` is illegal in Java.

## 2.3 if Statements

### Definition
An `if` statement executes a block only when its condition is true.

```java
int score = 4;
if (score >= 3) {
    System.out.println("Passing!");
}
```

### Forms
```java
if (condition) {
    // do this
}

if (condition) {
    // do this
} else {
    // do that
}

if (condition) {
    // ...
} else if (otherCondition) {
    // ...
} else {
    // fallback
}
```

### Key Notes
- An `else` binds to the **nearest unmatched `if`**. Braces make this unambiguous and are strongly recommended, even for one-line bodies.
- The condition must be a `boolean` expression, not a number.

### Common Errors
- Dangling-else bugs from omitting braces. Add the braces. Future you will send present you a thank-you note.

## 2.4 Nested if Statements

### Definition
An `if` inside another `if` is **nested**. It lets you check a second condition only after the first passes.

```java
int score = 4;
boolean studied = true;
if (score >= 3) {
    if (studied) {
        System.out.println("Deserved it!");
    } else {
        System.out.println("Lucky!");
    }
}
```

### Key Notes
- Deep nesting gets hard to read. Flatten with `&&` when possible: `if (score >= 3 && studied)`.
- The exam loves nested `if` tracing. Write down the value of every variable at every level.

### Trash Code Example - needless nesting
```java
public class NestedTrash {
    public static void main(String[] args) {
        int score = 5;
        if (score >= 3) {
            if (score >= 4) {
                if (score == 5) {
                    if (true) {
                        System.out.println("A perfect score!");
                    }
                }
            }
        }
    }
}
```

**Output**:
```
A perfect score!
```

**Why It's Trash**: Four levels of nesting to express `if (score == 5)`. It is a staircase to nowhere, built entirely out of trash code and poor decisions.

## 2.5 Compound Boolean Expressions

### Definition
**Compound Boolean expressions** join multiple conditions with `&&`, `||`, and `!`.

```java
boolean pass = (score >= 3) && (attendance >= 0.8);
boolean honors = (score == 5) || (gpa >= 3.8);
boolean notFail = !(score < 3);   // same as score >= 3
```

### Truth tables
**AND (`&&`)**

| A | B | A && B |
| --- | --- | --- |
| true | true | true |
| true | false | false |
| false | true | false |
| false | false | false |

**OR (`||`)**

| A | B | A \|\| B |
| --- | --- | --- |
| true | true | true |
| true | false | true |
| false | true | true |
| false | false | false |

### Common Errors
- Confusing `&&` with `&` (bitwise AND) or `||` with `|` (bitwise OR). The single-character versions do not short-circuit and operate on bits.

## 2.6 Comparing Boolean Expressions (De Morgan's Laws)

### Definition
**De Morgan's Laws** let you rewrite compound Boolean expressions into equivalent forms:

- `!(A && B)` is equivalent to `!A || !B`
- `!(A || B)` is equivalent to `!A && !B`

### Examples
```java
// Original: NOT (score >= 3 AND attendance >= 0.8)
boolean a = !(score >= 3 && attendance >= 0.8);
// Equivalent:
boolean b = (score < 3) || (attendance < 0.8);
```

```java
// Original: NOT (name.equals("Alan") OR name.equals("Grace"))
boolean c = !(name.equals("Alan") || name.equals("Grace"));
// Equivalent:
boolean d = !name.equals("Alan") && !name.equals("Grace");
```

### Why the exam cares
A multiple-choice question may show two expressions and ask whether they are equivalent. Memorize the two laws and, when in doubt, make a truth table.

### Common Errors
- Negating only part of the expression: `!(A && B)` is not `!A && !B`. The `&&` must flip to `||`.

## 2.7 while Loops

### Definition
A `while` loop repeats a block **while** a condition is true. The condition is checked before each iteration, so the body may never run.

```java
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;                    // must change the condition variable
}
```

**Output**:
```
0
1
2
3
4
```

### Key Notes
- A loop needs three things: initialization (`int i = 0`), a condition (`i < 5`), and an update (`i++`). Forget the update and you have written an **infinite loop**, the king of trash code.
- Use `while` when you do not know in advance how many iterations you need (e.g. reading until input ends).

### Common Errors
- **Infinite loop**: the condition never becomes false. Your program hangs, your laptop fan screams, your roommate considers moving out.
- **Off-by-one**: using `i <= 5` when you meant `i < 5`.

## 2.8 for Loops

### Definition
A `for` loop packs initialization, condition, and update into one header. Use it when the number of iterations is known.

```java
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

### Syntax
```java
for (initialization; condition; update) {
    // body
}
```

### Enhanced for loop (for-each)
Iterates over every element of an array or `ArrayList`:

```java
int[] scores = {5, 4, 3};
for (int score : scores) {
    System.out.println(score);
}
```

Limitations: you cannot use the for-each loop to modify array elements (it gives you a copy of each value), and you do not have an index variable.

### for vs while
- `for` - you know how many times (array of length 10, count 1 to 100).
- `while` - you know when to stop, not how many steps (read until end of file, keep going until found).

### Common Errors
- Declaring the loop variable with `int i` and then trying to use `i` after the loop - `i` is out of scope.

## 2.9 Implementing Selection and Iteration Algorithms

### Definition
Standard algorithms combine loops and conditionals. The new exam expects you to recognize and write them:

- **Sum / average**: loop, add to an accumulator.
- **Count occurrences**: loop, increment a counter when a condition holds.
- **Find max / min**: loop, keep the best-so-far.
- **Linear search**: loop through elements, return the index when found, return −1 otherwise.

```java
public static int linearSearch(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) {
            return i;             // found
        }
    }
    return -1;                    // not found
}
```

### Key Notes
- Initialize accumulators before the loop (`int sum = 0;`) and best-so-far to the first element or an extreme value.
- Binary search and merge sort are now explicit topics; their full treatment is in [New Unit 4](new_unit_4.md), with extra depth in [old Unit 4](unit_4.md).

### Trash Code Example - summing with a while loop and a side quest
```java
public class SumTrash {
    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 4, 5};
        int sum = 0;
        int i = 0;
        boolean done = false;
        while (!done) {
            if (i < nums.length) {
                sum = sum + nums[i];
                i++;
            } else {
                done = true;
            }
        }
        System.out.println("Sum: " + sum);
    }
}
```

**Output**:
```
Sum: 15
```

**Why It's Trash**: A single `for` loop does this in three lines. Here we invented a boolean flag, a manual index, and a `while` wrapping an `if` - a Rube Goldberg machine made of trash code.

## 2.10 Implementing String Algorithms

### Definition
String algorithms process text character by character, using `length()`, `charAt()`, `substring()`, and `indexOf()` inside loops. You met the methods in [New Unit 1](new_unit_1.md); here they go to work.

### Common patterns

**Count vowels:**
```java
public static int countVowels(String s) {
    int count = 0;
    String lower = s.toLowerCase();
    for (int i = 0; i < lower.length(); i++) {
        char c = lower.charAt(i);
        if (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u') {
            count++;
        }
    }
    return count;
}
```

**Reverse a string:**
```java
public static String reverse(String s) {
    String result = "";
    for (int i = s.length() - 1; i >= 0; i--) {
        result += s.charAt(i);
    }
    return result;
}
```

**Check for a palindrome:**
```java
public static boolean isPalindrome(String s) {
    String clean = s.toLowerCase();
    int left = 0, right = clean.length() - 1;
    while (left < right) {
        if (clean.charAt(left) != clean.charAt(right)) return false;
        left++;
        right--;
    }
    return true;
}
```

### Key Notes
- Use `i < s.length()` as the loop bound. Off-by-one here causes `StringIndexOutOfBoundsException`.
- Strings are immutable, so build a new `String` with `+=` (fine for exam-sized inputs) or `StringBuilder` for large ones.

### Common Errors
- Comparing characters with `==` is fine (they are primitives); comparing Strings with `==` is not.

## 2.11 Nested Iteration

### Definition
A loop inside another loop is **nested iteration**. The inner loop runs fully for each iteration of the outer loop.

```java
for (int row = 1; row <= 3; row++) {
    for (int col = 1; col <= 3; col++) {
        System.out.print(row + "," + col + " ");
    }
    System.out.println();
}
```

**Output**:
```
1,1 1,2 1,3
2,1 2,2 2,3
3,1 3,2 3,3
```

### Key Notes
- If the outer loop runs `n` times and the inner runs `m` times, the body executes `n × m` times.
- Nested loops are how you traverse 2D arrays (see [New Unit 4](new_unit_4.md) and [old Unit 8](unit_8.md)).
- Use different variable names (`row`, `col`) to avoid accidentally resetting the inner counter.

### Common Errors
- Reusing the same loop variable name in nested loops causes logic errors or compile errors, depending on scope.

## 2.12 Informal Run-Time Analysis

### Definition
**Informal runtime analysis** means describing how an algorithm's work grows with the input size `n`, without formal proofs. This is a new explicit topic on the exam.

### Common complexities
| Complexity | Example | Grows like |
| --- | --- | --- |
| **O(1)** | Access `arr[0]` | constant |
| **O(n)** | Linear search, single loop over `n` items | linear |
| **O(n²)** | Nested loops over `n` items | quadratic |
| **O(log n)** | Binary search | logarithmic |

### How to reason
- One loop over `n` items → O(n).
- Two nested loops each over `n` items → O(n²).
- Halving the search space each step → O(log n).
- Sequential loops (one after another) → add them, but keep only the largest term: O(n) + O(n) = O(n).

### Key Notes
- The exam asks "which is faster" or "what is the order of growth," not for Big-O proofs.
- An O(log n) algorithm crushes an O(n) algorithm for large inputs. Binary search on a million sorted items takes about 20 comparisons; linear search takes up to a million.

### Trash Code Example - accidental O(n²)
```java
public static boolean hasDuplicate(int[] arr) {
    for (int i = 0; i < arr.length; i++) {
        for (int j = 0; j < arr.length; j++) {   // starts at 0 again -- wasteful
            if (i != j && arr[i] == arr[j]) {
                return true;
            }
        }
    }
    return false;
}
```

**Output**: `true` or `false` depending on the array.

**Why It's Trash**: Starting `j` at `i + 1` avoids redundant comparisons and roughly halves the work. As written, it compares every pair twice and compares elements with themselves. It is quadratic trash code - correct output, needless work.

### Python aside (optional, Java stays canonical)
The palindrome logic from above in Python, just to prove the idea is language-independent:

```python
def is_palindrome(s):
    s = s.lower()
    return s == s[::-1]
```

Java has no `[::-1]`, which is why the Java version needs the two-pointer loop. Different language, same algorithm.

## 3. Connection to AP CS A New Unit Two

### Curriculum Context
New Unit 2 combines the old [Unit 3](unit_3.md) (Boolean expressions, conditionals, De Morgan) and the old [Unit 4](unit_4.md) (loops, searching, sorting, binary search, merge sort). It is worth 25%-35% of the MC section - the biggest single chunk after Data Collections.

### Relevance
Selection and iteration appear in essentially every free-response question. If you master tracing loops and `if` statements, the FRQ section stops being scary and starts being tedious, which is a much better problem to have.

### Practice Questions
1. **Trace**: What is printed?
   ```java
   for (int i = 1; i <= 4; i++) {
       if (i % 2 == 0) System.out.print(i + " ");
   }
   ```
   **Answer**: `2 4`

2. **Equivalence**: Which is equivalent to `!(x > 5 && y < 3)`?
   **Answer**: `x <= 5 || y >= 3` (De Morgan).

3. **Short-circuit**: What is the value of `result`?
   ```java
   int x = 0;
   boolean result = (x != 0) && (10 / x > 1);
   ```
   **Answer**: `false`, and no division-by-zero occurs because `&&` short-circuits.

4. **Runtime**: What is the order of growth of nested loops that each run `n` times?
   **Answer**: O(n²).

5. **Coding exercise**: Write a method `countMultiples(int[] a, int k)` that returns how many elements are divisible by `k`. Hint: `a[i] % k == 0`, and watch out for `k == 0`.

---
# [next](new_unit_3.md)
