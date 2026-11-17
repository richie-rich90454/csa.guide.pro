---
title: AP CS A Unit 10 - Recursion
---
[Go back to home page](README.md)
# [previous](unit_9.md)<-->[next](README.md)
> **New curriculum equivalent**: This material now lives in [New Unit 4](new_unit_4.md) (the four-unit curriculum that launched in 2025-26). Same Java, different filing cabinet - the College Board just re-sorted the drawers.

**TOP TIP**: Recursion is the campus map that points to another campus map that points to another lecture hall - until one map finally says "you are here" (the base case). Forget that final sign and you wander the same hallway until the `StackOverflowError` bounces you out. The new exam is explicit about **recursive searching and sorting**, so binary search and merge sort are no longer "nice to know" - they are fair game.

# AP CS A Unit Ten: Recursion
You either get it or you don't, try harder
# Recursion, Seriously
## 1. Introduction to Recursion
### Definition
Recursion is a programming technique where a method calls itself to solve a problem by breaking it down into smaller, similar subproblems. In AP Computer Science A (AP CS A) Unit Ten, recursion is introduced as an alternative to iterative approaches, emphasizing its elegance for problems that naturally exhibit self-similarity, such as computing factorials, traversing hierarchical data, or solving mathematical sequences.
### Core Concepts
- **Recursive Method**: A method that calls itself, either directly or indirectly.
- **Base Case**: The condition that stops the recursion, preventing infinite calls and stack overflow.
- **Recursive Case**: The part where the method calls itself with modified parameters, moving toward the base case.
- **Call Stack**: The memory structure that tracks recursive calls, with each call creating a new stack frame.
### Key Notes
- Recursion can simplify code for problems with recursive definitions (e.g., tree traversal, divide-and-conquer algorithms).
- Every recursive method must have at least one base case and a recursive case that progresses toward it.
- Recursion may be less efficient than iteration due to overhead from multiple method calls but offers clearer logic for certain problems.
- AP CS A focuses on understanding recursion through classic examples like factorial and Fibonacci.
### Example: Factorial
The factorial of a non-negative integer \( n \) (denoted \( n! \)) is defined recursively:
- Base case: \( 0! = 1 \)
- Recursive case: \( n! = n \times (n-1)! \) for \( n > 0 \)
```java
public class FactorialExample {
    public static int factorial(int n) {
        if (n == 0) { // Base case
            return 1;
        }
        else { // Recursive case
            return n * factorial(n - 1);
        }
    }
    public static void main(String[] args) {
        int result = factorial(5);
        System.out.println("5! = " + result);
    }
}
```
**Output**:
```
5! = 120
```
### Common Errors
- **Missing Base Case**: Leads to infinite recursion and `StackOverflowError`.
- **Incorrect Recursive Step**: Failing to progress toward the base case causes infinite recursion.
- **Stack Overflow**: Deep recursion with large inputs may exceed the call stack limit.
- **Inefficiency**: Redundant calculations (e.g., naive Fibonacci recursion) can be extremely slow.
---
## 2. Base Cases and Recursive Cases
### Definition
The success of recursion hinges on properly defining base cases and recursive cases. The **base case** provides a direct answer for the simplest instance of the problem, while the **recursive case** reduces the problem to a smaller version, eventually reaching a base case.
### Designing Recursive Solutions
1. **Identify the Base Case(s)**: Determine the simplest scenario that can be solved without further recursion.
2. **Define the Recursive Case**: Express the problem in terms of a smaller or simpler version of itself.
3. **Ensure Progress**: Each recursive call must move closer to a base case.
### Example: Fibonacci Sequence
The Fibonacci sequence is defined recursively:
- Base cases: \( F(0) = 0 \), \( F(1) = 1 \)
- Recursive case: \( F(n) = F(n-1) + F(n-2) \) for \( n > 1 \)
```java
public class FibonacciExample {
    public static int fibonacci(int n) {
        if (n == 0) { // Base case 1
            return 0;
        }
        else if (n == 1) { // Base case 2
            return 1;
        }
        else { // Recursive case
            return fibonacci(n - 1) + fibonacci(n - 2);
        }
    }
    public static void main(String[] args) {
        for (int i = 0; i <= 5; i++) {
            System.out.println("F(" + i + ") = " + fibonacci(i));
        }
    }
}
```
**Output**:
```
F(0) = 0
F(1) = 1
F(2) = 1
F(3) = 2
F(4) = 3
F(5) = 5
```
### Key Notes
- Multiple base cases may be needed (e.g., Fibonacci requires two).
- The recursive case should simplify the problem (e.g., reducing \( n \) by 1 or dividing the problem size).
- Visualizing the recursion tree helps understand the flow and identify inefficiencies.
### Common Errors
- **Insufficient Base Cases**: Missing a base case for all terminal conditions.
- **Non-Terminating Recursion**: The recursive case doesn't approach a base case (e.g., `factorial(n)` calling `factorial(n)`).
- **Overcomplication**: Adding unnecessary complexity instead of leveraging the natural recursive structure.
---
## 3. Recursive vs. Iterative Approaches
### Definition
Many recursive problems can also be solved iteratively using loops. Choosing between recursion and iteration depends on factors like readability, performance, and problem nature.
### Comparison
| Aspect | Recursion | Iteration |
|--------|-----------|-----------|
| **Readability** | Often more intuitive for recursive problems (e.g., tree traversal). | Can be clearer for simple linear processes. |
| **Performance** | Overhead from method calls may cause stack overflow or slower execution. | Generally faster with less memory overhead. |
| **Memory Usage** | Uses call stack, potentially leading to stack overflow for deep recursion. | Uses constant or heap memory, more scalable. |
| **Code Length** | Can be shorter and more elegant for self-similar problems. | May require more code to manage state manually. |
### Example: Factorial Iterative vs. Recursive
```java
public class FactorialComparison {
    // Recursive version
    public static int factorialRecursive(int n) {
        if (n == 0) return 1;
        return n * factorialRecursive(n - 1);
    }
    // Iterative version
    public static int factorialIterative(int n) {
        int result = 1;
        for (int i = 1; i <= n; i++) {
            result *= i;
        }
        return result;
    }
    public static void main(String[] args) {
        int n = 5;
        System.out.println("Recursive: " + factorialRecursive(n));
        System.out.println("Iterative: " + factorialIterative(n));
    }
}
```
**Output**:
```
Recursive: 120
Iterative: 120
```
### When to Use Recursion
- **Natural Recursion**: Problems with recursive definitions (e.g., mathematical sequences, tree structures).
- **Divide and Conquer**: Algorithms like merge sort or binary search (though often implemented iteratively in AP CS A).
- **Backtracking**: Problems requiring exploration of multiple paths (e.g., maze solving, permutations).
### When to Use Iteration
- **Simple Loops**: Straightforward counting or processing.
- **Performance-Critical Code**: Avoiding call overhead and stack limits.
- **Tail Recursion**: Can be optimized by compilers, but Java doesn't guarantee tail-call optimization.
### Key Notes
- AP CS A expects understanding of both approaches and ability to convert between them.
- Recursion is a foundational concept for advanced topics like dynamic programming and graph algorithms.
- Practice tracing recursive calls to build intuition.
---
## 4. Example Program: Recursive Sum of Array
This program demonstrates recursion by summing the elements of an array, showcasing divide-and-conquer thinking.
```java
public class ArraySumRecursive {
    // Recursive method to sum array elements from index start to end
    public static int sumArray(int[] arr, int start, int end) {
        if (start > end) { // Base case: empty range
            return 0;
        }
        else if (start == end) { // Base case: single element
            return arr[start];
        }
        else { // Recursive case: divide range and conquer
            int mid = (start + end) / 2;
            int leftSum = sumArray(arr, start, mid);
            int rightSum = sumArray(arr, mid + 1, end);
            return leftSum + rightSum;
        }
    }
    public static void main(String[] args) {
        int[] grades = {90, 85, 88, 92, 87};
        int total = sumArray(grades, 0, grades.length - 1);
        System.out.println("Sum of grades: " + total);
        System.out.println("Average: " + (double) total / grades.length);
    }
}
```
**Output**:
```
Sum of grades: 442
Average: 88.4
```
### Explanation
- **Base Cases**: Handle empty range (return 0) and single element (return the element).
- **Recursive Case**: Split the array into two halves, sum each recursively, and combine results.
- **Divide and Conquer**: This approach mirrors merge sort's logic, illustrating recursion's power for splitting problems.
### Common Errors
- **Incorrect Index Handling**: Off-by-one errors in start/end indices can cause infinite recursion or incorrect sums.
- **Missing Base Case**: Forgetting the empty range case may lead to infinite recursion for zero-length arrays.
- **Inefficient Splitting**: For linear problems like summing, simple iteration is more efficient; this example is for educational purposes.
---
## 5. Recursive Algorithms in AP CS A
### Curriculum Context
AP CS A Unit Ten introduces recursion as a problem-solving technique, covering:
- **Mathematical Recursion**: Implementing sequences like factorial and Fibonacci.
- **Array Processing**: Applying recursion to arrays (e.g., searching, summing).
- **String Manipulation**: Recursive string reversal or palindrome checking.
- **Simple Divide and Conquer**: Understanding the concept through examples like binary search (though often taught iteratively).
### Key Topics
- **Tracing Recursive Calls**: Step-by-step execution to understand stack behavior.
- **Writing Recursive Methods**: Designing methods with proper base cases and recursive steps.
- **Comparing Efficiency**: Analyzing time and space complexity of recursive vs. iterative solutions.
- **Debugging Recursion**: Identifying common pitfalls like stack overflow.
### Example: Recursive Binary Search
Binary search naturally fits recursion, though AP CS A typically uses iteration.
```java
public class RecursiveBinarySearch {
    public static int binarySearch(int[] arr, int target, int left, int right) {
        if (left > right) { // Base case: target not found
            return -1;
        }
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) { // Base case: target found
            return mid;
        }
        else if (arr[mid] < target) { // Recursive case: search right half
            return binarySearch(arr, target, mid + 1, right);
        }
        else { // Recursive case: search left half
            return binarySearch(arr, target, left, mid - 1);
        }
    }
    public static void main(String[] args) {
        int[] sortedGrades = {85, 87, 88, 90, 92};
        int index = binarySearch(sortedGrades, 90, 0, sortedGrades.length - 1);
        System.out.println("Index of 90: " + index);
    }
}
```
**Output**:
```
Index of 90: 3
```
### Relevance
- Recursion is a stepping stone to advanced algorithms (e.g., tree traversal, dynamic programming).
- It reinforces understanding of method calls and the call stack.
- AP exam questions may ask to trace or write simple recursive methods.
---
## 6. Common Errors and Debugging
### Stack Overflow
- **Cause**: Deep recursion without a base case or with very large input.
- **Symptoms**: `StackOverflowError` at runtime.
- **Prevention**: Ensure base cases are reachable and consider iterative alternatives for deep recursion.
### Infinite Recursion
- **Cause**: Recursive case doesn't progress toward base case (e.g., `factorial(n)` calling `factorial(n)`).
- **Symptoms**: Program hangs or crashes with stack overflow.
- **Debugging**: Add print statements to trace parameter values and check progression.
### Redundant Calculations
- **Example**: Naive Fibonacci recursion recalculates the same values many times.
- **Impact**: Exponential time complexity (\(O(2^n)\)) for Fibonacci.
- **Solution**: Use memoization (caching results) or iteration.
### Example: Debugging with Print Statements
```java
public class DebugRecursion {
    public static int factorial(int n) {
        System.out.println("Calling factorial(" + n + ")");
        if (n == 0) {
            System.out.println("Base case reached, returning 1");
            return 1;
        }
        int result = n * factorial(n - 1);
        System.out.println("Returning " + result + " from factorial(" + n + ")");
        return result;
    }
    public static void main(String[] args) {
        factorial(3);
    }
}
```
**Output**:
```
Calling factorial(3)
Calling factorial(2)
Calling factorial(1)
Calling factorial(0)
Base case reached, returning 1
Returning 1 from factorial(1)
Returning 2 from factorial(2)
Returning 6 from factorial(3)
```
### Best Practices
- **Test with Small Inputs**: Verify correctness before scaling up.
- **Visualize the Call Stack**: Draw recursion trees for complex methods.
- **Consider Edge Cases**: Empty inputs, negative numbers, or large values.
- **Use Helper Methods**: For cleaner recursion with additional parameters (e.g., start/end indices).
---
## 7. Connection to AP CS A Unit Ten
### Curriculum Context
AP CS A Unit Ten builds on previous units by introducing:
- **Recursive Thinking**: Breaking problems into self-similar subproblems.
- **Method Design**: Writing methods that call themselves with proper termination.
- **Algorithm Analysis**: Comparing recursive and iterative solutions for efficiency.
- **Problem Solving**: Applying recursion to classic AP problems (e.g., string processing, array algorithms).
### Relevance
- Recursion appears in AP exam questions, often as code tracing or writing simple recursive methods.
- It connects to real-world applications like file system traversal, parsing expressions, or game AI.
- Understanding recursion prepares students for college-level computer science topics.
### Practice Questions
1. **Code Tracing**: What is the output of this recursive method for `mystery(4)`?
   ```java
   public static int mystery(int n) {
       if (n <= 1) return 1;
       return n + mystery(n - 2);
   }
   ```
   **Answer**: `4 + mystery(2)` → `4 + (2 + mystery(0))` → `4 + (2 + 1)` = `7`
2. **Error Identification**: Why does this method fail for `countDown(5)`?
   ```java
   public static void countDown(int n) {
       System.out.println(n);
       countDown(n - 1);
   }
   ```
   **Answer**: Missing base case causes infinite recursion and stack overflow.
3. **Coding Exercise**: Write a recursive method `reverseString(String s)` that returns the reverse of `s`. Base case: empty string returns itself.
---
## 8. Additional Notes
### Best Practices
- **Keep It Simple**: Start with clear base cases and a straightforward recursive step.
- **Document Assumptions**: Comment on expected input ranges and base case logic.
- **Test Thoroughly**: Use small, medium, and edge-case inputs.
- **Consider Iteration**: If recursion adds complexity without benefit, use a loop.
### Extensions
The following advanced concepts extend recursion beyond AP CS A, offering deeper insights for motivated learners.
#### 8.1 Tail Recursion
- **Definition**: A recursive call is the last operation in the method. Some languages optimize tail recursion to reuse stack frames (tail-call optimization).
- **Java Consideration**: Java doesn't guarantee tail-call optimization, but recognizing tail recursion aids in converting to iteration.
- **Example**: Tail-recursive factorial with an accumulator.
  ```java
  public static int factorialTail(int n, int acc) {
      if (n == 0) return acc;
      return factorialTail(n - 1, n * acc);
  }
  // Call: factorialTail(5, 1) returns 120
  ```
#### 8.2 Memoization
- **Definition**: Caching results of expensive recursive calls to avoid redundant calculations.
- **Application**: Drastically improves performance for problems like Fibonacci.
- **Example**: Fibonacci with memoization.
  ```java
  import java.util.HashMap;
  public class FibonacciMemo {
      private static HashMap<Integer, Integer> memo = new HashMap<>();
      public static int fib(int n) {
          if (n <= 1) return n;
          if (memo.containsKey(n)) return memo.get(n);
          int result = fib(n - 1) + fib(n - 2);
          memo.put(n, result);
          return result;
      }
  }
  ```
#### 8.3 Recursive Data Structures
- **Linked Lists**: Can be traversed recursively.
  ```java
  class Node {
      int data;
      Node next;
  }
  public static int sumList(Node head) {
      if (head == null) return 0;
      return head.data + sumList(head.next);
  }
  ```
- **Binary Trees**: Naturally recursive structure.
  ```java
  class TreeNode {
      int value;
      TreeNode left, right;
  }
  public static int sumTree(TreeNode root) {
      if (root == null) return 0;
      return root.value + sumTree(root.left) + sumTree(root.right);
  }
  ```
#### 8.4 Divide and Conquer Algorithms
- **Merge Sort**: Recursively splits and merges arrays (see Unit Four).
- **Quick Sort**: Chooses a pivot and recursively sorts partitions.
- **Binary Search**: Recursively halves search space (shown earlier).
#### 8.5 Backtracking
- **Concept**: Recursively explore possibilities, undoing (backtracking) when a path fails.
- **Example**: Generating all permutations of a string.
  ```java
  import java.util.ArrayList;
  import java.util.List;
  public class Permutations {
      public static List<String> generatePermutations(String str) {
          List<String> result = new ArrayList<>();
          permute("", str, result);
          return result;
      }
      private static void permute(String prefix, String remaining, List<String> result) {
          if (remaining.length() == 0) {
              result.add(prefix); // Base case: no characters left to permute
          } else {
              for (int i = 0; i < remaining.length(); i++) {
                  // Choose character at position i
                  String newPrefix = prefix + remaining.charAt(i);
                  String newRemaining = remaining.substring(0, i) + remaining.substring(i + 1);
                  // Recursively permute the remaining characters
                  permute(newPrefix, newRemaining, result);
                  // Backtracking is implicit: loop continues with next character
              }
          }
      }
      public static void main(String[] args) {
          List<String> perms = generatePermutations("ABC");
          System.out.println("Permutations of 'ABC': " + perms);
      }
  }
  ```
  **Output**:
  ```
  Permutations of 'ABC': [ABC, ACB, BAC, BCA, CAB, CBA]
  ```
---
## 9. Recursive Searching in Depth
### Definition
The current exam calls out **recursive searching** explicitly. The classic is recursive binary search: because each step halves the remaining range, it is \(O(\log n)\) whether you write it with a loop or with recursion. The recursion just replaces the `while` loop with a call that carries the new bounds.

### Recursive Binary Search, Fully Correct
```java
public static int binarySearch(int[] a, int target, int low, int high) {
    if (low > high) return -1;                       // base case: not found
    int mid = low + (high - low) / 2;                 // avoids overflow for huge indices
    if (a[mid] == target) return mid;                 // base case: found
    if (a[mid] < target)
        return binarySearch(a, target, mid + 1, high); // search right half
    else
        return binarySearch(a, target, low, mid - 1);  // search left half
}
```
Call it as `binarySearch(a, target, 0, a.length - 1)`. Two base cases: the bound-crossing case (not found) and the exact-match case (found). Every recursive call strictly shrinks the range, so termination is guaranteed.

### Tracing a Search
For `int[] a = {2, 4, 6, 8, 10}` and `target = 8`:
1. `low=0, high=4, mid=2` → `a[2]=6 < 8` → recurse on `low=3, high=4`.
2. `low=3, high=4, mid=3` → `a[3]=8` → return `3`.

Two comparisons. That is the whole point of halving.

### Recursive Linear Search (the \(O(n)\) cousin)
```java
public static int linearSearch(int[] a, int target, int i) {
    if (i >= a.length) return -1;              // base case: ran off the end
    if (a[i] == target) return i;              // base case: found
    return linearSearch(a, target, i + 1);     // recursive case: next index
}
```
Call it with `linearSearch(a, target, 0)`. Works on unsorted data, but visits elements one at a time - trash-code slow compared to binary search on sorted input.

### Trash Code Example - the broken binary search
```java
public class SearchTrash {
    public static int bad(int[] a, int target, int low, int high) {
        int mid = (low + high) / 2;
        if (a[mid] == target) return mid;
        if (a[mid] < target)
            return bad(a, target, mid, high);   // trash: passes mid, not mid + 1
        return bad(a, target, low, mid);         // trash: passes mid, not mid - 1
    }
    public static void main(String[] args) {
        int[] a = {2, 4, 6};
        System.out.println(bad(a, 5, 0, 2));     // target not present
    }
}
```
**Why It's Trash**: There is no `low > high` base case, and the recursive calls reuse `mid` instead of `mid + 1` / `mid - 1`. With no progress and no exit, the method recurses forever until `StackOverflowError` - or reads an out-of-range index first. Trash code that never returns an answer is still trash code.

### Common Errors
- Forgetting the `low > high` base case - searching for a missing target loops forever.
- Passing `mid` instead of `mid + 1` / `mid - 1` - the range never shrinks.
- Running binary search on unsorted data - may return `-1` even when the target exists.
---
## 10. Recursive Sorting in Depth
### Definition
**Recursive merge sort** is the poster child for divide-and-conquer: split the array into halves, recursively sort each half, then merge the sorted halves. Its recurrence is \(T(n) = 2T(n/2) + O(n)\), which solves to \(O(n \log n)\) - faster than selection sort or insertion sort (\(O(n^2)\)) on large inputs.

### Recursive Merge Sort
```java
public static void mergeSort(int[] a) {
    if (a.length <= 1) return;                       // base case: already sorted
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
The base case `a.length <= 1` is what stops the recursion. The two `while` loops after the main loop copy any leftover elements - forget them and your sorted array ends in a trail of zeros.

### Recursive Quick Sort
```java
public static void quickSort(int[] a, int low, int high) {
    if (low >= high) return;                 // base case: 0 or 1 element
    int p = partition(a, low, high);
    quickSort(a, low, p - 1);
    quickSort(a, p + 1, high);
}

private static int partition(int[] a, int low, int high) {
    int pivot = a[high];
    int i = low - 1;
    for (int j = low; j < high; j++) {
        if (a[j] <= pivot) {
            i++;
            int temp = a[i]; a[i] = a[j]; a[j] = temp;
        }
    }
    int temp = a[i + 1]; a[i + 1] = a[high]; a[high] = temp;
    return i + 1;
}
```
Call with `quickSort(a, 0, a.length - 1)`. Average case \(O(n \log n)\); worst case \(O(n^2)\) when the pivot is consistently poor (e.g., already-sorted data with the last element as pivot).

### Tracing Merge Sort
For `a = {3, 1, 2}`:
1. Split into `{3}` and `{1, 2}`.
2. Split `{1, 2}` into `{1}` and `{2}`.
3. Merge `{1}` and `{2}` → `{1, 2}`.
4. Merge `{3}` and `{1, 2}` → `{1, 2, 3}`.

Each level of the recursion tree doubles the number of subproblems and halves the work per subproblem - that is where \(\log n\) levels come from.

### Pseudocode Angle
```
FUNCTION mergeSort(a):
    IF length(a) <= 1: RETURN a
    left = mergeSort(first half of a)
    right = mergeSort(second half of a)
    RETURN merge(left, right)
END FUNCTION
```
The recursive structure is obvious in pseudocode; the subtle parts in Java are the index arithmetic and the leftover-copy loops in `merge`.

### Python aside (optional, Java stays canonical)
```python
def merge_sort(a):
    if len(a) <= 1:
        return a
    mid = len(a) // 2
    left = merge_sort(a[:mid])
    right = merge_sort(a[mid:])
    return merge(left, right)
```
Python's slicing hides the index bookkeeping Java makes you write. Same algorithm, same base case - the exam is still Java.

### Common Errors
- Base case `a.length == 1` instead of `<= 1` - an empty array sneaks through and crashes.
- Forgetting to copy leftover elements after the main merge loop.
- Recursing on `mid` instead of `mid + 1` in quick sort, creating overlapping partitions.
- Confusing the recursive merge sort's \(O(n \log n)\) with selection sort's \(O(n^2)\).
---
## 11. Connection, Practice, and Extensions
### Connection to AP CS A Unit Ten
Unit Ten's recursion now sits inside [New Unit 4](new_unit_4.md) on the current exam, where recursive searching and sorting are named topics alongside iterative binary search and merge sort. The Java is identical - base case, recursive case, progress toward termination. The campus map is the same; only the syllabus changed.

### Practice Questions
1. **Trace**: For `binarySearch(a, 8, 0, 4)` on `a = {2,4,6,8,10}`, how many recursive calls (including the first) occur before returning `3`?
   **Answer**: 2 - the first call finds `6` and recurses; the second finds `8`.

2. **Base cases**: What are the two base cases of recursive binary search?
   **Answer**: `low > high` (not found, return `-1`) and `a[mid] == target` (found, return `mid`).

3. **Complexity**: State the average time complexity of merge sort and of selection sort.
   **Answer**: Merge sort \(O(n \log n)\); selection sort \(O(n^2)\).

4. **Bug Fix**: A student writes `if (a.length == 1) return;` in `mergeSort`. What input breaks it?
   **Answer**: An empty array (`length == 0`) - no base case matches, so it recurses on empty halves forever. Use `<= 1`.

5. **Write**: Implement `public static int recSum(int[] a, int i)` returning the sum of `a[i..end]`, with base case `i == a.length`.
   **Answer sketch**: `if (i == a.length) return 0; return a[i] + recSum(a, i + 1);`

6. **Coding Exercise**: Write recursive binary search for an `ArrayList<Integer>` (use `size()` and `get()`), then state why the array version is simpler.

### Extensions
- **Recurrence relations**: Merge sort's \(T(n) = 2T(n/2) + O(n)\) is the formal reason it is \(O(n \log n)\) - a first taste of the Master Theorem.
- **Recursion vs stack depth**: Each call adds a stack frame; recursive merge sort uses \(O(\log n)\) depth, while recursive linear search uses \(O(n)\).
- **Memoization**: The `FibonacciMemo` example in section 8.2 turns exponential recursion into linear time - the bridge to dynamic programming.
- **Tail recursion**: Java does not optimize it (see section 8.1), so deep tail-recursive code can still overflow - a good reason to prefer iteration in production.

### Best Practices
- Name the base case first in your head, then write the recursive case - if you cannot name it, do not write the method.
- Guarantee progress: each call must strictly reduce the problem (`mid + 1`/`mid - 1`, `n - 1`, `i + 1`).
- Use a helper method with extra parameters (`low`, `high`) to hide implementation details from the caller.
- Add a temporary `System.out.println` trace while debugging recursion; remove it before submission (trash code has no place on an exam).
- Prefer iteration for simple linear work; reserve recursion for genuinely self-similar problems like searching, sorting, and trees.

# [next](README.md)
