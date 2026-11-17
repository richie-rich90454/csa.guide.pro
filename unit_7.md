---
title: AP CS A Unit 7 - ArrayLists
---
[Go back to home page](README.md)
# [previous](unit_6.md)<-->[next](unit_8.md)
> **New curriculum equivalent**: This material now lives in [New Unit 4](new_unit_4.md) (the four-unit curriculum that launched in 2025-26). Same Java, different filing cabinet - the College Board just re-sorted the drawers.

**TOP TIP**: An `ArrayList` is a lecture hall that adds seats when you need them. A plain array is a lecture hall with a fixed number of chairs: show up with one extra student and somebody is standing in the aisle (or you get an `IndexOutOfBoundsException`). The exam lives on `size()`, `get()`, and `add()` - know them cold, or write trash code under pressure like the rest of us.

# AP CS A Unit Seven: ArrayLists
## 1. Introduction to ArrayLists
### Definition
In Java, an `ArrayList` is a dynamic, resizable data structure provided in the `java.util` package. Unlike arrays, which have a fixed size, `ArrayLists` can grow or shrink as elements are added or removed. In AP Computer Science A (AP CS A) Unit Seven, `ArrayList` is introduced as a key tool for managing collections of objects, with a focus on `ArrayList<Integer>` and `ArrayList<String>` for storing integers and strings, respectively, particularly in contexts like managing AP exam data or study groups.
### Key Characteristics
- **Dynamic Size**: `ArrayList` automatically adjusts its size, ideal for lists with varying lengths, such as a list of AP exam scores.
- **Generic Type**: Uses generics (e.g., `ArrayList<String>`) to enforce type safety, ensuring only specified types are stored.
- **Reference Types Only**: Stores objects (e.g., `Integer`, `String`), not primitives (e.g., `int`). Autoboxing/unboxing converts between primitives and wrapper classes (e.g., `int` to `Integer`).
- **AP Context**: Useful for managing dynamic data, such as lists of AP course names, exam scores, or study session hours.
### Core Methods for AP CS A
The following methods are emphasized in Unit Seven:
- `ArrayList<Type> list = new ArrayList<Type>();`: Creates a new `ArrayList`.
- `add(E element)`: Appends an element to the end of the list.
  - Example: `apCourses.add("AP Calculus");`
- `add(int index, E element)`: Inserts an element at the specified index.
  - Example: `apCourses.add(0, "AP Physics");`
- `get(int index)`: Returns the element at the specified index.
  - Example: `String course = apCourses.get(0); // Returns "AP Physics"`
- `set(int index, E element)`: Replaces the element at the specified index.
  - Example: `apCourses.set(0, "AP Chemistry");`
- `remove(int index)`: Removes the element at the specified index, shifting subsequent elements.
  - Example: `apCourses.remove(0);`
- `size()`: Returns the number of elements in the list.
  - Example: `int courseCount = apCourses.size();`
- `clear()`: Removes all elements from the list.
  - Example: `apCourses.clear();`
### Key Notes
- **Import**: Requires `import java.util.ArrayList;` at the top of the file.
- **Indexing**: Like arrays, `ArrayList` uses zero-based indexing.
- **Autoboxing**: Adding an `int` to an `ArrayList<Integer>` automatically wraps it as an `Integer`.
- **Performance**: Adding/removing elements at the end is efficient, but inserting/removing at the beginning or middle is slower due to shifting elements.
- **AP Use**: `ArrayList` is ideal for managing dynamic lists, such as tracking AP exam scores or hours spent studying.
### Example Program
```java
import java.util.ArrayList;
public class APStudyTracker {
    public static void main(String[] args) {
        // Create ArrayList for AP courses
        ArrayList<String> apCourses = new ArrayList<String>();
        // Add courses
        apCourses.add("AP Calculus"); // Index 0
        apCourses.add("AP Biology"); // Index 1
        apCourses.add(1, "AP Physics"); // Inserts at index 1
        // Modify and retrieve
        apCourses.set(0, "AP Chemistry"); // Replaces "AP Calculus"
        String firstCourse = apCourses.get(0); // Retrieves "AP Chemistry"
        // Remove and size
        apCourses.remove(1); // Removes "AP Physics"
        int courseCount = apCourses.size(); // Returns 2
        // Print courses
        System.out.println("AP Courses:");
        for (int i = 0; i < apCourses.size(); i++) {
            System.out.println("Course " + (i + 1) + ": " + apCourses.get(i));
        }
        System.out.println("Total Courses: " + courseCount);
        // AP exam scores
        ArrayList<Integer> apScores = new ArrayList<Integer>();
        apScores.add(5); // Score for exam 1
        apScores.add(5); // Score for exam 2
        System.out.println("AP Exam Scores: " + apScores);
    }
}
```
**Output**:
```
AP Courses:
Course 1: AP Chemistry
Course 2: AP Biology
Total Courses: 2
AP Exam Scores: [5, 5]
```
### Common Errors
- **IndexOutOfBoundsException**: Accessing an invalid index, e.g., `apCourses.get(apCourses.size())`.
- **Missing Import**: Forgetting `import java.util.ArrayList;` causes compilation errors.
- **Type Mismatch**: Adding a non-matching type to a generic `ArrayList`, e.g., `ArrayList<Integer> list; list.add("String");` fails.
---
## 2. ArrayList Operations and Loops
### Definition
`ArrayList` operations involve manipulating elements using loops and methods to process dynamic data, such as sorting AP course lists or calculating total study hours. Unit Seven emphasizes iterating over `ArrayList` using `for` loops and enhanced `for` loops.
### Loop Types
1. **Standard For Loop**:
   - Uses an index to access elements, allowing modifications during iteration.
   - Example:
     ```java
     ArrayList<String> apCourses = new ArrayList<String>();
     apCourses.add("AP Chemistry");
     apCourses.add("AP Biology");
     for (int i = 0; i < apCourses.size(); i++) {
         System.out.println(apCourses.get(i));
     }
     ```
2. **Enhanced For Loop**:
   - Simplifies iteration for read-only access, ideal for printing or summing.
   - Example:
     ```java
     ArrayList<Integer> studyHours = new ArrayList<Integer>();
     studyHours.add(10);
     studyHours.add(15);
     int total = 0;
     for (Integer hour : studyHours) {
         total += hour; // Autounboxing to int
     }
     System.out.println("Total Study Hours: " + total);
     ```
### Key Operations
- **Searching**: Check if an element exists using `contains(E element)` or linear search.
  - Example: `if (apCourses.contains("AP Chemistry")) { ... }`
- **Summing**: Calculate totals, e.g., total study hours.
  - Example: Sum hours in an `ArrayList<Integer>` using a loop.
- **Modifying During Iteration**: Use a standard `for` loop to modify elements, as enhanced `for` loops cannot modify the list structure (e.g., adding/removing).
### Example Program
```java
import java.util.ArrayList;
public class APStudyManager {
    public static void main(String[] args) {
        // Initialize ArrayList
        ArrayList<String> apCourses = new ArrayList<String>();
        apCourses.add("AP Chemistry");
        apCourses.add("AP Biology");
        apCourses.add("AP Physics");
        // Search for a course
        String searchCourse = "AP Biology";
        boolean found = apCourses.contains(searchCourse);
        System.out.println(searchCourse + " found: " + found);
        // Calculate total study hours
        ArrayList<Integer> studyHours = new ArrayList<Integer>();
        studyHours.add(10);
        studyHours.add(15);
        studyHours.add(5);
        int totalHours = 0;
        for (Integer hour : studyHours) {
            totalHours += hour;
        }
        System.out.println("Total Study Hours: " + totalHours);
        // Modify list: Remove courses with "AP" in name
        for (int i = apCourses.size() - 1; i >= 0; i--) {
            if (apCourses.get(i).contains("AP")) {
                apCourses.remove(i);
            }
        }
        System.out.println("Courses after removal: " + apCourses);
    }
}
```
**Output**:
```
AP Biology found: true
Total Study Hours: 30
Courses after removal: []
```
### Common Errors
- **ConcurrentModificationException**: Modifying an `ArrayList` (e.g., removing elements) during an enhanced `for` loop causes this error. Use a standard `for` loop instead.
- **Off-by-One Errors**: Incorrect loop bounds, e.g., `i <= list.size()` instead of `i < list.size()`.
- **Null Elements**: Adding `null` to an `ArrayList` can cause `NullPointerException` during operations like `contains`.
---
## 3. Connection to AP CS A Unit Seven
### Curriculum Context
Unit Seven builds on arrays (Unit Six) by introducing `ArrayList` as a more flexible data structure. Key concepts include:
- **Dynamic Lists**: Managing collections with varying sizes, like AP exam scores.
- **Iteration**: Using loops to process `ArrayList` elements.
- **Methods**: Applying `add`, `remove`, `get`, `set`, and `size` for list manipulation.
- **Wrapper Classes**: Understanding autoboxing/unboxing with `Integer` and `Double`.
### Relevance to AP Studies
- `ArrayList` simplifies managing dynamic data, such as adding new AP courses or tracking study hours.
- Loops enable processing lists, e.g., calculating total hours or filtering enrolled courses.
- Methods like `contains` support searching for specific courses, enhancing functionality in AP-related applications.
### Practice Questions
1. **Code Tracing**: What is the output of this code?
   ```java
   ArrayList<Integer> studyHours = new ArrayList<Integer>();
   studyHours.add(10);
   studyHours.add(20);
   int sum = 0;
   for (Integer h : studyHours) {
       sum += h;
   }
   System.out.println(sum);
   ```
   **Answer**: `30`
2. **Error Identification**: Why does this code fail?
   ```java
   ArrayList<String> apCourses = new ArrayList<String>();
   apCourses.add("AP Chemistry");
   for (String course : apCourses) {
       apCourses.remove(0);
   }
   ```
   **Answer**: It throws a `ConcurrentModificationException` because the `ArrayList` is modified during an enhanced `for` loop. Use a standard `for` loop instead.
3. **Coding Exercise**: Write a program that stores AP exam scores in an `ArrayList<Integer>` and calculates the average score, handling empty lists.
---
## 4. Additional Notes
### Best Practices
- Use generics (e.g., `ArrayList<String>`) to ensure type safety.
- Check `size()` before accessing elements to avoid `IndexOutOfBoundsException`.
- Use meaningful names (e.g., `apCourses` instead of `list`) for clarity.
- Comment complex operations, like removing elements during iteration.
### Additional ArrayList Information
- **Additional Methods**:
  - `indexOf(E element)`: Returns the index of the first occurrence of the element, or `-1` if not found.
    - Example: `int index = apCourses.indexOf("AP Chemistry");`
  - `lastIndexOf(E element)`: Returns the index of the last occurrence of the element.
    - Example: `int last = apCourses.lastIndexOf("AP Physics");`
  - `isEmpty()`: Returns `true` if the list is empty.
    - Example: `boolean empty = apCourses.isEmpty();`
  - `toArray()`: Converts the `ArrayList` to an array (advanced, less common in AP CS A).
    - Example: `Object[] courseArray = apCourses.toArray();`
- **Other Characteristics**:
  - **Initial Capacity**: `ArrayList` starts with a default capacity (typically 10) and doubles when needed, improving performance for large lists.
  - **Null Elements**: `ArrayList` allows `null` elements, unlike some other collections.
  - **Thread Safety**: `ArrayList` is not thread-safe; for concurrent access, use `Collections.synchronizedList` (beyond AP CS A scope).
  - **Memory Usage**: Stores references to objects in the heap, with resizing impacting memory efficiency compared to arrays.
- **Sorting**: Use `Collections.sort(list)` (requires `import java.util.Collections;`) to sort elements.
  - Example: `Collections.sort(apCourses);` sorts courses alphabetically.
- **Comparison to Arrays**: Arrays are faster for fixed-size data but lack flexibility; `ArrayList` is preferred for dynamic data in AP applications.
---
## 5. ArrayList Methods in Depth
### Definition
The `ArrayList` class exposes more than `add`, `get`, `set`, `remove`, and `size`. The AP CS A subset also includes `indexOf`, `lastIndexOf`, `isEmpty`, `clear`, and `contains`. Knowing the exact return types and overloads is what separates a 5 from a "close enough" 3 - and, importantly, what lets you write *precise* trash code instead of accidental trash code.

### Method Reference Table
| Method | Return type | What it does |
| --- | --- | --- |
| `boolean add(E obj)` | `boolean` | Appends to the end (always returns `true`) |
| `void add(int i, E obj)` | `void` | Inserts at index `i`, shifting later elements right |
| `E get(int i)` | `E` | Returns the element at `i` |
| `E set(int i, E obj)` | `E` | Replaces element at `i`, returns the old value |
| `E remove(int i)` | `E` | Removes and returns the element at index `i` |
| `boolean remove(E obj)` | `boolean` | Removes the first element equal to `obj` |
| `int size()` | `int` | Number of elements |
| `boolean contains(E obj)` | `boolean` | `true` if some element `.equals(obj)` |
| `int indexOf(E obj)` | `int` | First index where `.equals(obj)`, or `-1` |
| `int lastIndexOf(E obj)` | `int` | Last index where `.equals(obj)`, or `-1` |
| `boolean isEmpty()` | `boolean` | `true` when `size() == 0` |
| `void clear()` | `void` | Removes every element |

### The Two Overloads That Bite Everyone
`remove(int)` and `remove(Object)` are overloaded. With `ArrayList<String>`, `list.remove(2)` removes by index while `list.remove("AP Physics")` removes by value. With `ArrayList<Integer>`, the distinction is a genuine trap: `list.remove(2)` removes the element at **index** 2, not the **value** `2`. To remove the value `2`, write `list.remove(Integer.valueOf(2))`.

### Trash Code Example - the Integer removal trap
```java
import java.util.ArrayList;
public class RemoveTrash {
    public static void main(String[] args) {
        ArrayList<Integer> apScores = new ArrayList<Integer>();
        apScores.add(5);
        apScores.add(4);
        apScores.add(3);
        apScores.remove(2);          // trash: removes index 2 (the 3), not the value 2
        System.out.println(apScores); // [5, 4] -- "wait, where did the 3 go?"
        apScores.remove(5);          // trash again: index 5 is out of bounds
        System.out.println(apScores); // never reached -- crash
    }
}
```
**Output** (up to the crash):
```
[5, 4]
```
**Why It's Trash**: `remove(2)` on an `ArrayList<Integer>` removes by index, not by value - a classic trash-code surprise. Then `remove(5)` throws `IndexOutOfBoundsException` because there is no index 5. If you meant to delete the score `5`, write `apScores.remove(Integer.valueOf(5))`. That `Integer.valueOf(...)` is the non-obvious why: it forces Java to pick the `remove(Object)` overload instead of `remove(int)`.

### Common Errors
- Assuming `remove(x)` removes the *value* `x` when the list holds `Integer` - it removes the element at *index* `x`.
- Calling `set(i, value)` on an empty list - no index `0` exists; use `add` instead.
- Confusing `size()` (a method) with `length` (an array field).
- Expecting `indexOf` to return `0` when the item is missing - it returns `-1`.
---
## 6. Wrapper Classes, Autoboxing, and Unboxing
### Definition
`ArrayList` can only hold objects, never primitives. Java silently converts between `int` and `Integer` through **autoboxing** and **unboxing**. This is convenient, and also a reliable source of trash code - the kind that compiles cleanly and fails at runtime, which is the exam's favorite flavor.

### The Wrapper Classes
| Primitive | Wrapper |
| --- | --- |
| `int` | `Integer` |
| `double` | `Double` |
| `boolean` | `Boolean` |
| `char` | `Character` |
| `long` | `Long` |
| `float` | `Float` |
| `short` | `Short` |
| `byte` | `Byte` |

- **Autoboxing**: `int gpa = 5; list.add(gpa);` wraps `5` as an `Integer`.
- **Unboxing**: `int first = list.get(0);` unwraps the `Integer` back to `int`.
- Constants: `Integer.MAX_VALUE`, `Integer.MIN_VALUE`.
- Parsing: `Integer.parseInt("42")` returns `42`; `Integer.toString(42)` returns `"42"`.

### TOP TIP
Java caches `Integer` objects for values `-128` to `127`. So `Integer a = 5; Integer b = 5; a == b` is `true` - but for `1000` it is `false`. **Always compare wrapper objects with `.equals()`, never `==`.** The cache is a trick question waiting to happen, and "it worked for small numbers" is the worst kind of evidence.

### Common Errors
- Unboxing `null`: `Integer x = null; int y = x;` throws `NullPointerException`.
- Writing `ArrayList<int>` - does not compile; use `ArrayList<Integer>`.
- Comparing wrapper objects with `==` and getting results that change depending on the value's size.

### Python aside (optional, Java stays canonical)
Python's `list` holds any object with no wrappers needed:
```python
scores = [5, 4, 3]      # plain ints, no Integer wrapper
scores.append(2)
avg = sum(scores) / len(scores)
```
Java forces the wrapper choice on you; the AP exam is in Java, so keep the wrappers straight. Python is the easy mode you are not allowed to play on test day.
---
## 7. Passing ArrayLists to Methods
### Definition
An `ArrayList` is an object, so passing it to a method passes a *reference*. Mutations inside the method affect the original list. This is the campus map / lecture hall idea again: the parameter holds the address of the same lecture hall, not a photocopy of the building. Hand the map to a friend and they can rearrange the chairs - you will see the change when you arrive.

### Example
```java
import java.util.ArrayList;
public class ArrayListMethods {
    public static void addBonus(ArrayList<Integer> scores) {
        for (int i = 0; i < scores.size(); i++) {
            scores.set(i, scores.get(i) + 1); // mutate in place
        }
    }
    public static ArrayList<Integer> copyOf(ArrayList<Integer> scores) {
        ArrayList<Integer> copy = new ArrayList<Integer>();
        for (Integer s : scores) {
            copy.add(s);
        }
        return copy; // a new lecture hall, same students
    }
    public static void main(String[] args) {
        ArrayList<Integer> apScores = new ArrayList<Integer>();
        apScores.add(4);
        apScores.add(3);
        addBonus(apScores);
        System.out.println(apScores);        // [5, 4] -- original changed
        ArrayList<Integer> copy = copyOf(apScores);
        copy.clear();
        System.out.println(apScores);        // [5, 4] -- original survived
        System.out.println(copy);            // []
    }
}
```
**Output**:
```
[5, 4]
[5, 4]
[]
```

### Pseudocode Angle
```
FUNCTION addBonus(list):
    FOR i FROM 0 TO list.size() - 1:
        list.set(i, list.get(i) + 1)
    END FOR
END FUNCTION
```
Pseudocode hides the reference subtlety - in Java, whether a method mutates the original depends on whether you mutate the object or replace the reference. That distinction is pure Java, and the exam tests it relentlessly.

### Common Errors
- Expecting a method to leave the list unchanged when it calls `set`, `add`, or `remove`.
- Reassigning the parameter (`scores = new ArrayList<Integer>();`) and thinking the caller's list changed - it did not. You only redirected the local campus map; the original lecture hall is untouched.
---
## 8. More Trash Code Examples
### Trash Code Example - the off-by-one average
```java
import java.util.ArrayList;
public class AverageTrash7 {
    public static void main(String[] args) {
        ArrayList<Integer> studyHours = new ArrayList<Integer>();
        studyHours.add(10);
        studyHours.add(15);
        studyHours.add(5);
        int total = 0;
        for (int i = 0; i <= studyHours.size(); i++) { // trash: <= walks one too far
            total += studyHours.get(i);               // crashes at i == size()
        }
        System.out.println("Average: " + total / studyHours.size()); // integer division too
    }
}
```
**Why It's Trash**: Two trash-code classics in one loop. `i <= studyHours.size()` walks one index too far and throws `IndexOutOfBoundsException`; even if it survived, `total / size()` uses integer division and truncates the GPA-style average. Fix: use `<` and cast to `double`. This is the exact bug the exam hides in plain sight, and the one you will write at 2 a.m. if you are not careful.

### Trash Code Example - four nested loops to find one score
```java
import java.util.ArrayList;
public class NestedTrash7 {
    public static void main(String[] args) {
        ArrayList<Integer> apScores = new ArrayList<Integer>();
        apScores.add(5);
        apScores.add(4);
        apScores.add(3);
        boolean hasFive = false;
        for (int i = 0; i < 1; i++) {                  // trash: loop that runs once
            for (int j = 0; j < apScores.size(); j++) {
                for (int k = 0; k < 1; k++) {
                    for (int m = 0; m < 1; m++) {
                        if (apScores.get(j) == 5) hasFive = true;
                    }
                }
            }
        }
        System.out.println("Has a 5: " + hasFive);
    }
}
```
**Why It's Trash**: Four nested loops to do the work of `apScores.contains(5)`. The three single-iteration loops are pure scaffolding - a Rube Goldberg machine made of trash code. Correct output, maximum confusion, zero GPA points for style.
---
## 9. Connection, Practice, and Extensions
### Connection to AP CS A Unit Seven
Unit Seven converts the fixed-size arrays of [Unit Six](unit_6.md) into a resizable collection. The legacy exam tested `ArrayList` heavily in multiple choice and in the free-response questions that asked you to build or filter a list. In the current four-unit curriculum the same Java lives in [New Unit 4](new_unit_4.md), where it is worth a large slice of the MC and the entire ArrayList FRQ. Nothing about the syntax changed - only the chapter number. The trash code, unfortunately, is backward compatible.

### Practice Questions
1. **Code Tracing**: What is printed?
   ```java
   ArrayList<Integer> scores = new ArrayList<Integer>();
   scores.add(3);
   scores.add(4);
   scores.add(3);
   System.out.println(scores.indexOf(3));
   System.out.println(scores.lastIndexOf(3));
   System.out.println(scores.remove(Integer.valueOf(3)));
   System.out.println(scores);
   ```
   **Answer**: `0`, then `2`, then `true`, then `[4, 3]`. The first `3` (index 0) is removed by value because of `Integer.valueOf(3)`.

2. **Error Identification**: Why does this crash?
   ```java
   ArrayList<Integer> list = new ArrayList<Integer>();
   list.add(10);
   for (Integer x : list) {
       list.remove(0);
   }
   ```
   **Answer**: Removing during an enhanced `for` loop throws `ConcurrentModificationException`. Traverse backward with an index loop instead: `for (int i = list.size() - 1; i >= 0; i--) list.remove(i);`.

3. **Method Writing**: Write `public static int maxScore(ArrayList<Integer> scores)` returning the largest score, or `Integer.MIN_VALUE` for an empty list.
   **Answer sketch**: Initialize `int max = Integer.MIN_VALUE;`, loop with `for (Integer s : scores) if (s > max) max = s;`, return `max`. Initializing `max` to `0` would be trash code when every score is negative - but AP scores are 1–5, so you can get away with it here. Do not get cocky.

4. **Output Prediction**: Given `ArrayList<String> courses`, what does `courses.add(0, "AP CS A")` do if the list is empty?
   **Answer**: It adds `"AP CS A"` at index 0, which is also `size()` - perfectly legal. Inserting at any index greater than `size()` throws `IndexOutOfBoundsException`.

5. **Reference Semantics**: A method does `list.clear()` on a parameter. Does the caller's list change?
   **Answer**: Yes. The parameter is a campus map to the same lecture hall; `clear()` empties the original.

6. **Coding Exercise**: Read AP scores 1–5 into an `ArrayList<Integer>`, drop every score below 3 with a backward index loop, and print the average of what remains. Guard against an empty list so you do not divide by zero - that is the "handling empty lists" trap from question 3 of the earlier Practice block.

### Extensions
- **Sorting**: `Collections.sort(list)` sorts an `ArrayList<String>` alphabetically or an `ArrayList<Integer>` numerically (import `java.util.Collections`). This is `O(n log n)` and beats any trash-code bubble sort you write by hand.
- **`ArrayList` of `ArrayList`**: `ArrayList<ArrayList<Integer>>` models a gradebook with a list per student. Access with `gradebook.get(row).get(col)` - twice the index arithmetic, twice the chance of a trash-code off-by-one.
- **Arrays vs `ArrayList`**: Arrays are faster and hold primitives; `ArrayList` resizes and holds objects. When the size is unknown (most real data), `ArrayList` wins.
- **Capacity**: `new ArrayList<Integer>(100)` preallocates room for 100 elements, avoiding repeated resizing. Micro-optimization, but it is the kind of detail that makes code look like you know what you are doing.

### Best Practices
- Use generics (`ArrayList<String>`) so the compiler catches type errors before the exam proctor catches you.
- Check `size()` before `get()`/`set()`/`remove(int)` to avoid `IndexOutOfBoundsException`.
- Remove elements with a backward index loop, never an enhanced `for` loop.
- Use `.equals()` for wrapper/String comparison; reserve `==` for primitives and for comparing an object to `null`.
- Return a defensive copy (`copyOf`) when a method must not let the caller's list be mutated - a real lecture hall you can lock.
- Name lists by content (`apScores`, not `list`) - your future self grading your own trash code will thank you.

# [next](unit_8.md)
