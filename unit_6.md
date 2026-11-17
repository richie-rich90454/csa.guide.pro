---
title: AP CS A Unit 6 - Arrays
---
[Go back to home page](README.md)
# [previous](unit_5.md) <-- [next](unit_7.md)
**New curriculum equivalent**: This material now lives in [New Unit 4](new_unit_4.md).


# AP CS A Unit Six: Arrays
## 1. Arrays
### Definition
An **array** in Java is a fixed-size container that holds multiple values of the same type. Arrays are used to efficiently organize and access related data using an index-based system.
### Syntax
```java
// Declaration and instantiation
int[] apScores = new int[5];
// Declaration with initialization
int[] studentScores = {5, 4, 4, 3, 5};
```
### Accessing Elements
* Arrays use **zero-based indexing**.
* Access and assign values with index notation `array[index]`.
```java
System.out.println(studentScores[0]); // prints 5
studentScores[2] = 5; // updates third score to 5
```
### Example: Printing All Scores
```java
for (int i = 0; i < studentScores.length; i++) {
    System.out.println("Score " + (i + 1) + ": " + studentScores[i]);
}
```
---
## 2. Traversing Arrays
### Traditional For Loop
```java
for (int i = 0; i < apScores.length; i++) {
    System.out.println("AP Score: " + apScores[i]);
}
```
### Enhanced For Loop
Used for **read-only** access:
```java
for (int score : apScores) {
    System.out.println("Score: " + score);
}
```
---
## 3. Array Algorithms
### Sum and Average
```java
int total = 0;
for (int score : studentScores) {
    total += score;
}
double average = (double) total / studentScores.length;
System.out.println("Average Score: " + average);
```
### Finding the Maximum
```java
int maxScore = studentScores[0];
for (int i = 1; i < studentScores.length; i++) {
    if (studentScores[i] > maxScore) {
        maxScore = studentScores[i];
    }
}
System.out.println("Top Score: " + maxScore);
```
### Counting Occurrences
```java
int fives = 0;
for (int score : studentScores) {
    if (score == 5) {
        fives++;
    }
}
System.out.println("Number of 5s: " + fives);
```
---
## 4. Arrays and Methods
Arrays can be passed to and returned from methods:
```java
public static int sumScores(int[] scores) {
    int sum = 0;
    for (int score : scores) {
        sum += score;
    }
    return sum;
}
```
---
## 5. Common Errors and Tips
### Index Out of Bounds
Accessing an invalid index causes a runtime error:
```java
int score = apScores[5]; // Error: only indices 0-4 are valid
```
### Uninitialized Elements
Elements are automatically initialized to:
* `0` for numeric arrays
* `false` for `boolean` arrays
* `null` for object arrays
### Fixed Size
Array size cannot be changed after creation. Use `ArrayList` (in Unit 7) for dynamic resizing.
---
## 6. AP Exam Connections
Arrays appear frequently in both multiple choice and free response questions:
* **FRQs** may involve traversing arrays, computing values, or modifying elements.
* Understanding both index-based and enhanced for loops is crucial.
---
## 7. Example Program: AP Exam Analysis
```java
public class ExamStats {
    public static void main(String[] args) {
        int[] apScores = {5, 4, 3, 5, 2};
        // Print scores
        for (int i = 0; i < apScores.length; i++) {
            System.out.println("Exam " + (i + 1) + ": " + apScores[i]);
        }
        // Calculate average
        int sum = 0;
        for (int score : apScores) {
            sum += score;
        }
        double average = (double) sum / apScores.length;
        System.out.println("Average Score: " + average);
        // Find highest score
        int max = apScores[0];
        for (int i = 1; i < apScores.length; i++) {
            if (apScores[i] > max) {
                max = apScores[i];
            }
        }
        System.out.println("Top Score: " + max);
    }
}
```
**Sample Output**:
```
Exam 1: 5
Exam 2: 4
Exam 3: 3
Exam 4: 5
Exam 5: 2
Average Score: 3.8
Top Score: 5
```
---
## 8. Extensions (Beyond Scope but Useful)
### Two-Dimensional Arrays
Used for grid-based data, like a matrix of AP practice scores:
```java
int[][] studentScores = {
    {5, 4, 4},
    {3, 3, 4},
    {5, 5, 5}
};
System.out.println(studentScores[1][2]); // prints 4
```
### Array Utility Methods
* `Arrays.toString(array)` for quick printing.
```java
import java.util.Arrays;
System.out.println(Arrays.toString(apScores));
```
* `Arrays.sort(array)` to sort scores.
### Array Copying
To avoid modifying the original array:
```java
int[] copy = Arrays.copyOf(apScores, apScores.length);
```
---
## 9. Practice Questions
1. **Code Tracing**: What is the output?
   ```java
   int[] scores = {3, 4, 5};
   for (int i = scores.length - 1; i >= 0; i--) {
       System.out.print(scores[i] + " ");
   }
   ```
   **Answer**: `5 4 3`
2. **Bug Fixing**: What's wrong here?
   ```java
   int[] ap = new int[3];
   ap[3] = 5;
   ```
   **Answer**: Index `3` is out of bounds. Valid indices are `0`, `1`, and `2`.
3. **Write a Method**: Write a method that counts how many `5`s are in an array of AP scores.
4. **Challenge**: Write a method that returns the index of the lowest score.
---
## 10. More Array Algorithms

### Finding the minimum
Mirror the maximum algorithm, but start from the first element and flip the comparison:
```java
int minScore = studentScores[0];
for (int i = 1; i < studentScores.length; i++) {
    if (studentScores[i] < minScore) {
        minScore = studentScores[i];
    }
}
System.out.println("Lowest Score: " + minScore);
```

### Linear search over an array
Return the index when found, `-1` otherwise. This is the exact algorithm from [Unit 4](unit_4.md) now wearing an array costume:
```java
public static int findScore(int[] scores, int target) {
    for (int i = 0; i < scores.length; i++) {
        if (scores[i] == target) {
            return i;
        }
    }
    return -1;
}
```

### Counting values above a threshold
```java
int fives = 0;
for (int score : studentScores) {
    if (score == 5) fives++;
}
```

### Reversing in place
```java
for (int left = 0, right = apScores.length - 1; left < right; left++, right++) {
    int temp = apScores[left];
    apScores[left] = apScores[right];
    apScores[right] = temp;
}
```

### Arrays of objects
An array of `Scholar` references starts full of `null` until you fill it:
```java
Scholar[] roster = new Scholar[5];
roster[0] = new Scholar("Alan", 5);
System.out.println(roster[1]); // null -- the lecture hall is empty
```
**TOP TIP**: A `Scholar[]` is a campus map with five labeled spots. The spots exist, but until you build a `Scholar` and point a spot at it, each spot holds `null`. Calling a method on an empty spot earns you the dreaded `NullPointerException`.

### Key Notes
- Initialize a "best so far" variable to the first element, not to `0`. If every score were negative, `0` would be wrong.
- Accumulators (`sum`, `count`) start before the loop at `0` or at the first element.
- A two-pointer loop (`left`, `right`) is the standard in-place reversal.

---
## 11. Arrays Are Objects: Passing, Returning, and Aliasing

### Definition
An array variable is a **reference**, not the array itself. It is a campus map pointing to the real row of lecture halls in heap memory. Copying the map gives you two maps to the *same* campus. Change a room through one map and the other map sees it.

```java
public static void bumpFirst(int[] scores) {
    scores[0] += 1;                 // changes the caller's array
}
public static void replaceArray(int[] scores) {
    scores = new int[] {5, 5, 5};   // only reassigns the local reference
}
```
```java
int[] apScores = {3, 4, 5};
bumpFirst(apScores);      // {4, 4, 5}
replaceArray(apScores);   // still {4, 4, 5}
```

### Arrays returned from methods
```java
public static int[] doubled(int[] a) {
    int[] result = new int[a.length];
    for (int i = 0; i < a.length; i++) {
        result[i] = a[i] * 2;
    }
    return result;   // a new array; the original is untouched
}
```

### Common Errors
- Assuming `replaceArray` above changes the caller's variable. It does not; only element mutation through the reference sticks.
- **Aliasing**: `int[] copy = original;` creates a second reference to the *same* array, not a copy. Use `Arrays.copyOf(original, original.length)` for a real copy.

### Trash Code Example: the swap that does nothing
```java
public class SwapTrash {
    static void swapFirstTwo(int[] a) {
        int[] temp = a;                 // "save" the array
        a = new int[a.length];          // point a somewhere new
        int hold = a[0];                // swap inside the new array
        a[0] = a[1];
        a[1] = hold;
        a = temp;                       // restore the map
    }
    public static void main(String[] args) {
        int[] scores = {3, 5};
        swapFirstTwo(scores);
        System.out.println(java.util.Arrays.toString(scores));
    }
}
```
**Output**: `[3, 5]`

**Why It's Trash**: Three references and a brand-new array to perform a swap that should take two lines with a single `int temp`. It reassigns the parameter, builds a decoy array, swaps the decoy, then throws the decoy away; the caller's array never changes. Peak trash code: a lot of motion, zero result.

Correct version:
```java
static void swapFirstTwo(int[] a) {
    int temp = a[0];
    a[0] = a[1];
    a[1] = temp;
}
```

---
## 12. Pseudocode Angle

```
ALGORITHM ClassAverage
  SET total TO 0
  FOR EACH score IN scores
    total = total + score
  END FOR
  average = total / LENGTH(scores)
  OUTPUT average
END ALGORITHM
```
Map the pseudocode to Java: `total` is declared before the loop, `FOR EACH` becomes the enhanced `for`, and `LENGTH(scores)` is `scores.length` (a field, not a method). The `/` here is real division; in Java you must cast to `double`.

---
## 13. Python Aside (optional, Java stays canonical)
Python's `list` absorbs both the array and the ArrayList roles:
```python
scores = [5, 4, 3, 5, 2]
avg = sum(scores) / len(scores)
scores[0] = 5
```
Java makes you pick a fixed `int[]` or a growable `ArrayList<Integer>` and makes you write the loop yourself. The exam is Java, so the traversal discipline you practice here is the point.

---
## 14. Common Errors (expanded)
- **Off-by-one**: `i <= scores.length` throws `ArrayIndexOutOfBoundsException` on the last pass. Use `<`.
- **`length` vs `length()`**: arrays use the field `scores.length`; Strings use `s.length()` and ArrayLists use `list.size()`.
- **Integer division**: `total / length` truncates. Cast: `(double) total / length`.
- **Empty array**: `scores[0]` on an empty array throws. Check `scores.length > 0` first.
- **Aliasing**: `int[] b = a;` does not copy. Use `Arrays.copyOf` or a manual loop.
- **Object arrays**: elements default to `null`, not to a constructed object. Fill them before you call methods.
- **Ragged 2D arrays**: use `grid[i].length` for row `i`, not `grid[0].length`.

---
## 15. Connection to AP CS A Unit Six

### Curriculum Context
Unit Six is arrays: creation, indexing, traversal, standard algorithms, and passing arrays to methods. In the modern exam this material lives in [New Unit 4](new_unit_4.md), which folds arrays together with ArrayLists, 2D arrays, and recursion.

### Relevance
Arrays are the vocabulary of AP free-response questions. Nearly every FRQ hands you an array (or an ArrayList) and asks you to traverse it, compute a value, or modify it in place. Master the index-based loop and the enhanced loop and you master the exam's favorite shape.

### Practice Questions
1. **Trace**: What is printed?
   ```java
   int[] a = {4, 5, 3};
   for (int i = 0; i < a.length; i++) a[i] += 1;
   System.out.println(java.util.Arrays.toString(a));
   ```
   **Answer**: `[5, 6, 4]`, every element was incremented in place.
2. **Bug fix**: Why does this crash?
   ```java
   int[] a = new int[4];
   for (int i = 0; i <= a.length; i++) a[i] = i;
   ```
   **Answer**: The `<=` lets `i` reach `4`, which is out of bounds for length 4. Use `<`.
3. **Aliasing**: After `int[] b = a; b[0] = 99;`, what is `a[0]`?
   **Answer**: `99`. `b` and `a` are two maps to the same array.
4. **Average**: For `int[] s = {5, 4, 3}`, what does `(double) (s[0] + s[1] + s[2]) / s.length` return?
   **Answer**: `4.0`. Without the cast it would be the integer `4`.
5. **Write a method**: Write `countFives(int[] scores)` returning how many elements equal 5.
   ```java
   public static int countFives(int[] scores) {
       int count = 0;
       for (int score : scores) {
           if (score == 5) count++;
       }
       return count;
   }
   ```
6. **Challenge**: Write `indexOfMin(int[] a)` returning the index of the smallest element (return `-1` for an empty array).
   ```java
   public static int indexOfMin(int[] a) {
       if (a.length == 0) return -1;
       int minIndex = 0;
       for (int i = 1; i < a.length; i++) {
           if (a[i] < a[minIndex]) minIndex = i;
       }
       return minIndex;
   }
   ```

---
## 16. Best Practices
- Use `scores.length`, never a magic number like `5`.
- Prefer the index-based loop when you need the index or want to modify elements; use the enhanced loop for read-only passes.
- Initialize accumulators before the loop and "best so far" to the first element.
- Cast to `double` before dividing to avoid silent truncation.
- Copy with `Arrays.copyOf` when you need a genuinely separate array.
- Check for `null` before calling methods on elements of an object array.

---
# [next](unit_7.md)