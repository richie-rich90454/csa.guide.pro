---
title: New Unit 4 - Data Collections
---

[Go back to home page](README.md)

# [previous](new_unit_3.md)

# New AP CS A Unit Four: Data Collections

**Exam weight: 30%-40% of the multiple-choice section** - the heaviest unit by far. It swallows the old Units 6 (arrays), 7 (ArrayLists), 8 (2D arrays), and 10 (recursion), then adds brand-new material on data sets, text files, and the ethics of collecting data. It also makes binary search, merge sort, and recursive searching/sorting explicit exam topics. If you only study one unit, study this one. If you only study one unit and write trash code, study this one twice.

**TOP TIP**: Roughly 40% of the MC and a big chunk of the FRQ live here. Arrays, ArrayLists, 2D arrays, searching, sorting, and recursion are all fair game. Practice tracing until your brain does loop bounds in its sleep.

## 4.1 Ethical and Social Issues Around Data Collection

### Definition
Data collection is not neutral. The **ethics of data collection** asks who owns data, who benefits from it, who is harmed, and whether consent was meaningful. The new exam explicitly tests this, so it is no longer enough to write code that works - you should be able to say whether you *should*.

### Key ideas
- **Privacy**: collecting only what you need, and protecting what you collect.
- **Consent**: people should know what is being collected and agree to it.
- **Bias**: data sets can reflect historical inequalities; algorithms trained on biased data reproduce bias.
- **Transparency and accountability**: users deserve to know how decisions about them are made.
- **Security**: collected data must be protected from unauthorized access.

### Example scenario
A school app tracks every student's location to "improve campus safety," but sells the data to advertisers. The code might be flawless - correct arrays, perfect ArrayLists - but the design is trash code of the ethical variety. **Just because you can collect it does not mean you should.**

### Key Notes
- The exam may ask a multiple-choice question about the responsible use of data, often in a scenario about surveys, tracking, or personal information.
- Look for the answer that prioritizes consent, minimization, and fairness - not the one that says "collect everything, it is fine."

## 4.2 Introduction to Using Data Sets

### Definition
A **data set** is a collection of related data, often stored in a file, that you read into a program and analyze. The new exam expects you to work with data sets, including reading them from text files.

### Typical workflow
1. Open a data source (a text file).
2. Read values into an array or `ArrayList`.
3. Traverse the collection to compute statistics (average, max, count).
4. Report results.

### Example data set
```
95
88
72
100
64
```

Each line is one score. A program reads these into an `ArrayList<Integer>` and computes the average.

### Key Notes
- Real data is messy: missing values, unexpected formats, duplicates. Robust code checks before using data.
- You will usually not know the size of a data set in advance. This is why `ArrayList` (which grows) is often more convenient than a fixed-size array.

## 4.3 Array Creation and Access

### Definition
An **array** is a fixed-size, ordered collection of elements of the same type. Each element is accessed by an integer **index**, starting at 0.

### Syntax
```java
int[] scores = new int[5];              // five ints, default 0
int[] more = {95, 88, 72, 100, 64};     // inline initialization
String[] names = new String[3];         // default null
```

### Accessing and modifying
```java
scores[0] = 95;              // set first element
int first = scores[0];       // read first element
int length = scores.length;  // number of elements (not a method!)
```

### Key Notes
- Arrays are **fixed size**. `scores.length` cannot change after creation.
- Array indices run from `0` to `length - 1`.
- Array elements get default values: `0`, `0.0`, `false`, or `null`.

### Common Errors
- **ArrayIndexOutOfBoundsException**: accessing `scores[5]` when the length is 5.
- Using `scores.length()` instead of `scores.length` - compile error; `length` is a field, not a method.

## 4.4 Array Traversals

### Definition
**Traversal** means visiting every element of an array, usually with a loop.

### Index-based loop
```java
for (int i = 0; i < scores.length; i++) {
    System.out.println(scores[i]);
}
```

Use this when you need the index or want to modify elements.

### Enhanced for loop (for-each)
```java
for (int score : scores) {
    System.out.println(score);
}
```

Use this when you only need the values. It cannot modify elements or give you the index.

### Key Notes
- The most common exam bug is `i <= scores.length` (should be `<`). It causes an out-of-bounds error on the last iteration.
- To traverse backward: `for (int i = scores.length - 1; i >= 0; i--)`.

## 4.5 Implementing Array Algorithms

### Definition
Standard array algorithms appear constantly on the exam.

### Sum and average
```java
int sum = 0;
for (int score : scores) sum += score;
double avg = (double) sum / scores.length;   // cast to avoid integer division
```

### Find maximum
```java
int max = scores[0];
for (int i = 1; i < scores.length; i++) {
    if (scores[i] > max) max = scores[i];
}
```

### Count occurrences
```java
int count = 0;
for (int score : scores) {
    if (score == 5) count++;
}
```

### Key Notes
- Initialize accumulators before the loop.
- Initialize `max`/`min` to the first element, not to `0` (which fails when all values are negative).

### Trash Code Example - average with a trap
```java
public class AverageTrash {
    public static void main(String[] args) {
        int[] scores = {95, 88, 72, 100, 64};
        int sum = 0;
        for (int i = 0; i <= scores.length; i++) {   // <= : classic trash
            sum += scores[i];                        // crashes on last iteration
        }
        int avg = sum / scores.length;               // integer division too
        System.out.println("Avg: " + avg);
    }
}
```

**Why It's Trash**: It has two bugs: an off-by-one that throws `ArrayIndexOutOfBoundsException` and integer division that truncates the average. Fix them: use `<` and cast to `double`.

## 4.6 Using Text Files

### Definition
This is **new exam content**. Java reads text files with the `File` and `Scanner` classes (both require imports).

```java
import java.io.File;
import java.util.Scanner;
import java.io.IOException;

public class ReadFileDemo {
    public static void main(String[] args) throws IOException {
        File file = new File("scores.txt");
        Scanner sc = new Scanner(file);
        while (sc.hasNextInt()) {
            int score = sc.nextInt();
            System.out.println("Score: " + score);
        }
        sc.close();
    }
}
```

### Key Scanner methods for files
- `boolean hasNext()` - true if another token exists.
- `boolean hasNextInt()` - true if the next token is an int.
- `int nextInt()` - reads the next int.
- `String nextLine()` - reads the rest of the line.
- `String next()` - reads the next token.

### Key Notes
- `hasNext()` / `hasNextInt()` guard against `NoSuchElementException` at end of file.
- `File` represents a path; it does not read anything by itself. `Scanner` does the reading.
- You must handle or declare `IOException` (with `throws IOException` or a try/catch).
- Newline handling after `nextInt()` follows the same rule as keyboard input: call `nextLine()` once to consume the leftover newline before reading a full line.

### Reading a whole file into an ArrayList
```java
ArrayList<Integer> scores = new ArrayList<Integer>();
Scanner sc = new Scanner(new File("scores.txt"));
while (sc.hasNextInt()) {
    scores.add(sc.nextInt());
}
sc.close();
```

### Common Errors
- Forgetting `import java.io.File;` or `import java.util.Scanner;`.
- Forgetting to `close()` the `Scanner` (resource leak).
- Calling `nextInt()` without checking `hasNextInt()` first.

## 4.7 Wrapper Classes

### Definition
**Wrapper classes** are object versions of primitives: `Integer` (int), `Double` (double), `Boolean` (boolean), `Character` (char), `Long`, `Float`, `Short`, `Byte`. Collections like `ArrayList` can only hold objects, so wrappers are essential.

### Autoboxing and unboxing
- **Autoboxing**: primitive → wrapper. `Integer x = 5;`
- **Unboxing**: wrapper → primitive. `int y = x;`

```java
ArrayList<Integer> list = new ArrayList<Integer>();
list.add(95);            // autoboxing int -> Integer
int first = list.get(0); // unboxing Integer -> int
```

### Useful methods and constants
- `Integer.parseInt("42")` → `42`
- `Double.parseDouble("3.14")` → `3.14`
- `Integer.toString(42)` → `"42"`
- `Integer.MAX_VALUE`, `Integer.MIN_VALUE`

### Key Notes
- Java caches small `Integer` objects (−128 to 127), so `==` may appear to work for small values but fails for larger ones. **Always use `.equals()` to compare wrapper objects.**

### Common Errors
- Unboxing a `null` wrapper: `Integer x = null; int y = x;` throws `NullPointerException`.

## 4.8 ArrayList Methods

### Definition
An **ArrayList** is a resizable collection of object references from `java.util`. Unlike arrays, it can grow and shrink.

```java
import java.util.ArrayList;

ArrayList<String> names = new ArrayList<String>();
```

### Core methods
| Method | What it does |
| --- | --- |
| `boolean add(E obj)` | Appends to the end |
| `void add(int i, E obj)` | Inserts at index `i`, shifting elements |
| `E get(int i)` | Returns element at `i` |
| `E set(int i, E obj)` | Replaces element at `i`, returns old value |
| `E remove(int i)` | Removes and returns element at `i` |
| `boolean remove(E obj)` | Removes first matching object |
| `int size()` | Number of elements |
| `boolean contains(E obj)` | True if present (uses `equals`) |
| `int indexOf(E obj)` | First index, or −1 |
| `void clear()` | Removes all elements |

### Key Notes
- Use `Integer`, `Double`, etc. as the type parameter, never primitives: `ArrayList<int>` is illegal.
- `remove(int)` and `remove(Object)` are overloaded. `list.remove(2)` removes by index; `list.remove("Alan")` removes by value.
- Adding at `size()` appends; adding beyond `size()` throws `IndexOutOfBoundsException`.

### Common Errors
- Confusing `size()` (a method) with `length` (an array field).

## 4.9 ArrayList Traversals

### Definition
ArrayLists are traversed with index-based loops or for-each loops, same as arrays.

```java
for (int i = 0; i < names.size(); i++) {
    System.out.println(names.get(i));
}

for (String name : names) {
    System.out.println(name);
}
```

### Removing while traversing
Removing elements inside a for-each loop throws `ConcurrentModificationException`. Traverse backward with an index instead:

```java
for (int i = names.size() - 1; i >= 0; i--) {
    if (names.get(i).length() < 3) {
        names.remove(i);
    }
}
```

### Key Notes
- Use `size()`, not `length`.
- Backward removal avoids index-shifting problems.

## 4.10 Implementing ArrayList Algorithms

### Definition
The same standard algorithms apply, with `size()` and `get()` replacing `length` and `[i]`.

### Find maximum
```java
int max = list.get(0);
for (int i = 1; i < list.size(); i++) {
    if (list.get(i) > max) max = list.get(i);
}
```

### Count values above a threshold
```java
int count = 0;
for (int score : scores) {
    if (score >= 3) count++;
}
```

### Key Notes
- The new FRQ Question 3 focuses **only** on ArrayList (arrays were removed from that question), so be fluent with `size()`, `get()`, and `add()`.

### Python aside (optional, Java stays canonical)
Python's `list` plays the role of both array and ArrayList:

```python
scores = [95, 88, 72]
scores.append(100)          # like ArrayList.add
avg = sum(scores) / len(scores)
```

Java makes you choose between fixed arrays and growable ArrayLists; Python does not. The exam uses Java.

## 4.11 2D Array Creation and Access

### Definition
A **2D array** is an array of arrays, useful for grids, tables, and matrices.

```java
int[][] grid = new int[3][4];          // 3 rows, 4 columns
int[][] literal = { {1, 2}, {3, 4}};    // 2x2
```

### Accessing elements
```java
grid[row][col] = 5;
int value = grid[1][2];
int rows = grid.length;                // number of rows
int cols = grid[0].length;             // number of columns in row 0
```

### Ragged arrays
Rows can have different lengths:

```java
int[][] ragged = new int[3][];
ragged[0] = new int[2];
ragged[1] = new int[5];
```

### Key Notes
- `grid.length` is the number of rows; `grid[i].length` is the number of columns in row `i`.
- Java stores 2D arrays as an array of row references. That is why ragged arrays are possible.

### Common Errors
- Assuming all rows have the same length. Use `grid[i].length`, not `grid[0].length`, when rows may differ.

## 4.12 2D Array Traversals

### Definition
Traverse a 2D array with nested loops: one for rows, one for columns.

```java
for (int row = 0; row < grid.length; row++) {
    for (int col = 0; col < grid[row].length; col++) {
        System.out.print(grid[row][col] + " ");
    }
    System.out.println();
}
```

### Row-major vs column-major
- **Row-major** (outer loop = rows): visit all of row 0, then row 1. This is the usual order.
- **Column-major** (outer loop = columns): visit column 0 top to bottom, then column 1.

### Enhanced for loops
```java
for (int[] row : grid) {
    for (int value : row) {
        System.out.print(value + " ");
    }
}
```

### Common Errors
- Using `grid[0].length` for the inner bound when rows are ragged.
- Swapping row and column indices; `grid[col][row]` silently reads the wrong cell.

## 4.13 Implementing 2D Array Algorithms

### Definition
Standard 2D algorithms: sum all elements, row/column sums, find max/min, search.

### Sum of all elements
```java
int sum = 0;
for (int row = 0; row < grid.length; row++) {
    for (int col = 0; col < grid[row].length; col++) {
        sum += grid[row][col];
    }
}
```

### Row sums
```java
for (int row = 0; row < grid.length; row++) {
    int rowSum = 0;
    for (int col = 0; col < grid[row].length; col++) {
        rowSum += grid[row][col];
    }
    System.out.println("Row " + row + ": " + rowSum);
}
```

### Searching for a value
```java
public static boolean contains(int[][] grid, int target) {
    for (int[] row : grid) {
        for (int value : row) {
            if (value == target) return true;
        }
    }
    return false;
}
```

### Key Notes
- Declare the accumulator for row sums **inside** the outer loop so it resets each row. Declaring it outside gives you a running total instead.

### Trash Code Example - the wrong accumulator scope
```java
public class RowSumTrash {
    public static void main(String[] args) {
        int[][] grid = { {1, 2}, {3, 4}};
        int rowSum = 0;                       // declared outside -- bug
        for (int row = 0; row < grid.length; row++) {
            for (int col = 0; col < grid[row].length; col++) {
                rowSum += grid[row][col];
            }
            System.out.println("Row " + row + ": " + rowSum);
        }
    }
}
```

**Output**:
```
Row 0: 3
Row 1: 10
```

**Why It's Trash**: Row 1 should be `7`, not `10`. The accumulator was never reset. Trash code produces plausible-looking wrong answers, which are the hardest kind to catch.

## 4.14 Searching Algorithms

### Definition
**Searching** finds the position of a target value. Two algorithms matter.

### Linear search
Checks every element in order. Works on unsorted data. **O(n)**.

```java
public static int linearSearch(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) return i;
    }
    return -1;
}
```

### Binary search
Repeatedly halves a **sorted** array. **O(log n)**.

```java
public static int binarySearch(int[] arr, int target) {
    int low = 0, high = arr.length - 1;
    while (low <= high) {
        int mid = (low + high) / 2;
        if (arr[mid] == target) return mid;
        if (arr[mid] < target) low = mid + 1;
        else high = mid - 1;
    }
    return -1;
}
```

### Key Notes
- Binary search **requires sorted data**. Running it on unsorted data may return −1 even when the target exists.
- When `low` and `high` cross, the target is not present.
- `(low + high) / 2` can overflow for huge indices; `(low + high) >>> 1` avoids it, but the simple form is fine for AP CS A.

### Common Errors
- Using `low < high` instead of `low <= high`, which misses a one-element range.
- Forgetting `+ 1` / `− 1` and looping forever when `mid` equals `low` or `high`.

## 4.15 Sorting Algorithms

### Definition
**Sorting** arranges elements in order. The exam emphasizes selection sort, insertion sort, and merge sort.

### Selection sort
Repeatedly find the smallest element in the unsorted region and swap it into place. **O(n²)**.

```java
public static void selectionSort(int[] a) {
    for (int i = 0; i < a.length - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < a.length; j++) {
            if (a[j] < a[minIndex]) minIndex = j;
        }
        int temp = a[i];
        a[i] = a[minIndex];
        a[minIndex] = temp;
    }
}
```

### Insertion sort
Builds a sorted prefix by inserting each element into its correct position. **O(n²)** worst case, efficient for nearly sorted data.

```java
public static void insertionSort(int[] a) {
    for (int i = 1; i < a.length; i++) {
        int key = a[i];
        int j = i - 1;
        while (j >= 0 && a[j] > key) {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = key;
    }
}
```

### Merge sort
Divide-and-conquer: split the array in half, sort each half, then merge. **O(n log n)**. This is now an explicit exam topic.

```java
public static void mergeSort(int[] a) {
    if (a.length <= 1) return;
    int mid = a.length / 2;
    int[] left = new int[mid];
    int[] right = new int[a.length - mid];
    for (int i = 0; i < mid; i++) left[i] = a[i];
    for (int i = mid; i < a.length; i++) right[i - mid] = a[i];
    mergeSort(left);
    mergeSort(right);
    merge(a, left, right);
}

private static void merge(int[] a, int[] left, int[] right) {
    int i = 0, j = 0, k = 0;
    while (i < left.length && j < right.length) {
        if (left[i] <= right[j]) a[k++] = left[i++];
        else a[k++] = right[j++];
    }
    while (i < left.length) a[k++] = left[i++];
    while (j < right.length) a[k++] = right[j++];
}
```

### Key Notes
- Selection sort makes at most `n−1` swaps; insertion sort can make many shifts.
- Merge sort uses extra memory (the temporary arrays) but is much faster for large inputs.
- You should be able to trace a sort step by step and state its order of growth. More depth in [old Unit 4](unit_4.md).

### Common Errors
- Off-by-one in `selectionSort`'s outer bound (`a.length - 1` is correct; the last element is already placed).
- Forgetting to copy the remaining elements after the main merge loop.

## 4.16 Recursion

### Definition
**Recursion** is when a method calls itself. Every recursive method needs:
- A **base case**: a simple condition that stops the recursion.
- A **recursive case**: a call to itself with a smaller problem.

```java
public static int factorial(int n) {
    if (n == 0) return 1;             // base case
    return n * factorial(n - 1);      // recursive case
}
```

### Tracing factorial(4)
```
factorial(4) = 4 * factorial(3)
             = 4 * (3 * factorial(2))
             = 4 * (3 * (2 * factorial(1)))
             = 4 * (3 * (2 * (1 * factorial(0))))
             = 4 * (3 * (2 * (1 * 1))) = 24
```

### Key Notes
- Each recursive call gets its own stack frame with its own local variables.
- Without a reachable base case, you get infinite recursion → `StackOverflowError`.
- Recursion often replaces a loop, but it is not always better: it uses more memory and can be slower.

### Common Errors
- Missing base case.
- Recursive call that does not reduce the problem (`factorial(n)` calling `factorial(n)` forever).
- Redundant work, e.g. naive recursive Fibonacci recomputes the same values many times.

## 4.17 Recursive Searching and Sorting

### Definition
The new exam explicitly tests **recursive versions of searching and sorting**.

### Recursive binary search
```java
public static int recursiveBinarySearch(int[] a, int target, int low, int high) {
    if (low > high) return -1;                 // base case: not found
    int mid = (low + high) / 2;
    if (a[mid] == target) return mid;           // base case: found
    if (a[mid] < target)
        return recursiveBinarySearch(a, target, mid + 1, high);
    else
        return recursiveBinarySearch(a, target, low, mid - 1);
}
```

Call it with `recursiveBinarySearch(a, target, 0, a.length - 1)`.

### Recursive merge sort
Merge sort is naturally recursive - the version in 4.15 already calls itself. The base case is `a.length <= 1`.

### Key Notes
- Recursive binary search is still O(log n).
- Recursive merge sort is still O(n log n).
- The base case is what stops the recursion; the recursive case must move toward it.

### Trash Code Example - recursion with no plan
```java
public class RecursiveTrash {
    static int bad(int n) {
        return bad(n - 1);   // no base case!
    }
    public static void main(String[] args) {
        System.out.println(bad(5));
    }
}
```

**Why It's Trash**: There is no base case, so this recurses until the stack explodes with `StackOverflowError`. It is trash code that never even returns an answer.

### Python aside (optional, Java stays canonical)
Recursive binary search in Python:

```python
def binary_search(a, target, low, high):
    if low > high:
        return -1
    mid = (low + high) // 2
    if a[mid] == target:
        return mid
    if a[mid] < target:
        return binary_search(a, target, mid + 1, high)
    return binary_search(a, target, low, mid - 1)
```

Same algorithm, same base cases - just fewer semicolons.

## 5. Connection to AP CS A New Unit Four

### Curriculum Context
New Unit 4 combines the old [Unit 6](unit_6.md) (arrays), [Unit 7](unit_7.md) (ArrayLists), [Unit 8](unit_8.md) (2D arrays), and [Unit 10](unit_10.md) (recursion), and adds new content on ethics, data sets, and text files. It is worth 30%-40% of the MC section.

### Relevance
This unit is where most of the coding happens. The new FRQ section has four shortened questions worth 25 points total, and Data Analysis with ArrayList is a guaranteed fixture. Master traversal and you master the exam.

### Practice Questions
1. **Trace**: What is printed?
   ```java
   int[] a = {1, 2, 3, 4};
   for (int i = 0; i < a.length; i++) a[i] *= 2;
   System.out.println(a[2]);
   ```
   **Answer**: `6`.

2. **Binary search**: For `int[] a = {2, 4, 6, 8, 10}`, how many comparisons does binary search need to find `8`?
   **Answer**: 2 (check middle `6`, then middle of right half `8`).

3. **ArrayList**: What does `list.remove(2)` do when `list = ["a", "b", "c", "d"]`?
   **Answer**: Removes `"c"` (removes by index).

4. **2D array**: For `int[][] g = new int[3][5]`, what is `g.length` and `g[0].length`?
   **Answer**: `3` and `5`.

5. **Recursion**: What is the base case in `factorial`, and what happens without it?
   **Answer**: `n == 0` returns `1`; without it, infinite recursion causes `StackOverflowError`.

6. **Coding exercise**: Write a method that reads integers from `scores.txt` into an `ArrayList<Integer>` and returns the average. Guard the read with `hasNextInt()`.

---
# [next](README.md)
