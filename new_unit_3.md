---
title: New Unit 3 - Class Creation
---

[Go back to home page](README.md)

# [previous](new_unit_2.md) <--> [next](new_unit_4.md)

# New AP CS A Unit Three: Class Creation

**Exam weight: 10%-18% of the multiple-choice section.** Small on the exam, huge in real life. This unit is the old Unit 5 renamed and slightly reworded: it is all about designing your own classes instead of just using `String` and `Math`. You get to decide what data an object holds and what it can do. With great power comes great responsibility - and ample opportunity for trash code.

**TOP TIP**: A class is a blueprint; an object is a house built from it. If your blueprint says "walls made of spaghetti," every house will be made of spaghetti. Design matters.

## 3.1 Abstraction and Program Design

### Definition
**Abstraction** is hiding unnecessary details and exposing only what matters. In object-oriented programming, a class abstracts a real-world concept into **attributes** (data) and **behaviors** (methods).

A `Student` class does not need to know the student's favorite color to compute their GPA. Leaving it out is abstraction. Including it is trash code with extra steps.

### Program design
**Program design** is deciding how to break a problem into classes and methods before writing code. Good design makes code readable, testable, and reusable. Bad design makes code that works once and then haunts you.

### Key Notes
- Identify the **nouns** in a problem to find candidate classes (Student, Course, Grade).
- Identify the **verbs** to find candidate methods (calculateGPA, enroll, getName).
- Abstraction is not omission by accident; it is omission on purpose.

### Trash Code Example - no abstraction at all
```java
public class NoAbstractionTrash {
    public static void main(String[] args) {
        // One giant method tracks two students with parallel arrays of mystery data
        String[] names = {"Alan", "Grace"};
        int[] scores = {5, 4};
        double[] gpas = {4.0, 3.8};
        // ... 200 more lines of spaghetti
        System.out.println(names[0] + " scored " + scores[0]);
    }
}
```

**Output**:
```
Alan scored 5
```

**Why It's Trash**: There is no `Student` class, no encapsulation, and three parallel arrays that must be kept in sync by sheer willpower. This is what happens when you skip abstraction and design on the fly.

## 3.2 Impact of Program Design

### Definition
The choices you make when designing a class affect:
- **Readability**: can another human understand it?
- **Maintainability**: can you fix it without breaking everything?
- **Reusability**: can you use it in another program?
- **Correctness**: does poor design make bugs more likely?

### Key Notes
- Classes with a single, clear responsibility are easier to test. This is the **Single Responsibility Principle**, stated in plain English.
- Encapsulation (private fields + public methods) protects data from being set to invalid values.
- The exam may ask you to evaluate a design: "Which change improves this class?" The answer is usually the one that hides data or decomposes a giant method.

### Common Errors
- Making every field `public` because it is "easier." It is easier right up until someone sets `gpa = 100.0`.

## 3.3 Anatomy of a Class

### Definition
A class contains **fields** (instance variables), **constructors**, and **methods**.

```java
public class Student {
    // fields (attributes) -- usually private
    private String name;
    private int apScore;

    // constructor
    public Student(String name, int apScore) {
        this.name = name;
        this.apScore = apScore;
    }

    // methods (behaviors)
    public String getName() { return name; }
    public int getApScore() { return apScore; }

    public boolean isPassing() {
        return apScore >= 3;
    }
}
```

### Key Notes
- **Instance variables** (fields) belong to each object. Every `Student` has its own `name` and `apScore`.
- **Local variables** belong to a method call and disappear when the method returns.
- A file can contain multiple classes, but only one can be `public`, and its name must match the filename.

### Common Errors
- Forgetting to initialize fields. If you do not set them in a constructor, they get default values (`0`, `0.0`, `false`, `null`), which are rarely what you want.

## 3.4 Constructors

### Definition
A **constructor** is a special method called with `new` to initialize an object. It has the same name as the class and **no return type**.

```java
public class Student {
    private String name;
    private int apScore;

    // no-arg constructor
    public Student() {
        name = "Unknown";
        apScore = 0;
    }

    // parameterized constructor
    public Student(String name, int apScore) {
        this.name = name;
        this.apScore = apScore;
    }
}
```

### Key Notes
- If you write no constructor, Java supplies a default no-arg constructor that sets fields to default values.
- If you write *any* constructor, the default one disappears. Add a no-arg constructor explicitly if you need it.
- Constructors can be **overloaded** (different parameter lists).

### Common Errors
- Adding a return type to a constructor: `public void Student(...)` makes it a regular method, not a constructor. Java will then give you a default constructor and your "constructor" will never be called by `new`.
- Forgetting to initialize all fields in every constructor.

## 3.5 Methods: How to Write Them

### Definition
A **method** is a named block of code that performs a task. It has a return type, a name, and parameters.

```java
public double calculateGrade(double exam, double homework) {
    return 0.7 * exam + 0.3 * homework;
}

public void printInfo() {
    System.out.println(name + ": " + apScore);
}
```

### Types of methods
- **Non-void (returning) methods**: return a value with `return`. The return type matches the value.
- **void methods**: perform an action and return nothing.
- **Accessor (getter)**: returns a field's value.
- **Mutator (setter)**: changes a field's value, often with validation.

```java
public void setApScore(int score) {
    if (score >= 1 && score <= 5) {
        apScore = score;
    }
}
```

### Method decomposition
**Decomposition** means breaking a big method into smaller methods that each do one thing. A method called `processEverything()` is a trash code smell; `readInput()`, `validate()`, and `computeResult()` are better.

### Common Errors
- **Missing return**: a non-void method that does not return a value on every path fails to compile.
- **Unreachable code**: statements after a `return` are a compile error.
- Returning the wrong type: `return 3.5;` from an `int` method fails.

## 3.6 Methods: Passing and Returning References of an Object

### Definition
When you pass an **object reference** to a method, you pass the address, not a copy of the object. The method can therefore modify the original object's state.

```java
public static void boostScore(Student s) {
    s.setApScore(5);          // changes the caller's object
}

public static void reassign(Student s) {
    s = new Student("New", 5); // only changes the local reference
}
```

```java
Student alice = new Student("Alice", 3);
boostScore(alice);
System.out.println(alice.getApScore());  // 5 -- the object changed
reassign(alice);
System.out.println(alice.getName());     // Alice -- the reference was not changed
```

### Key Notes
- **Primitives are passed by value**: changing the parameter inside the method does not change the caller's variable.
- **References are also passed by value** - but the value being copied is the address. So the method can mutate the object, but cannot make the caller's variable point to a different object.
- Returning a reference works the same way: you return an address, and the caller now points to that object.

### Common Errors
- Assuming `s = new Student(...)` inside a method reassigns the caller's variable. It does not. This is one of the most-tested and most-missed ideas on the exam.

### Trash Code Example - expecting pass-by-value magic
```java
public class ReferenceTrash {
    static void tryToChange(int x, Student s) {
        x = 99;                       // only changes local copy
        s.setApScore(1);              // changes the real object
        s = new Student("Ghost", 5);  // only changes local reference
    }
    public static void main(String[] args) {
        int score = 3;
        Student stu = new Student("Real", 3);
        tryToChange(score, stu);
        System.out.println(score);             // 3 -- unchanged
        System.out.println(stu.getName());     // Real -- unchanged
        System.out.println(stu.getApScore());  // 1 -- changed!
    }
}
```

**Output**:
```
3
Real
1
```

**Why It's Trash**: The method *looks* like it changes everything, but only the object mutation sticks. Trash code keeps the reader guessing about which variables survived - exactly the kind of confusion the exam loves to exploit.

## 3.7 Class Variables and Methods

### Definition
- **Instance variables / methods** belong to each object.
- **Static (class) variables / methods** belong to the class itself; there is one copy shared by all objects.

```java
public class Student {
    private static int studentCount = 0;   // shared by ALL students
    private String name;

    public Student(String name) {
        this.name = name;
        studentCount++;
    }

    public static int getStudentCount() {
        return studentCount;
    }
}
```

```java
Student a = new Student("Alan");
Student b = new Student("Grace");
System.out.println(Student.getStudentCount());  // 2
```

### Key Notes
- Static variables are initialized when the class is loaded, not when an object is created.
- Static methods cannot access instance variables directly (there is no `this`).
- Call static methods with the class name: `Student.getStudentCount()`.

### Common Errors
- Accessing a static method through an object (`a.getStudentCount()` compiles but is misleading).
- Trying to use `this` inside a static method - compile error.

## 3.8 Scope and Access

### Definition
**Scope** is the region of code where a variable is accessible. **Access modifiers** control which classes can see fields and methods.

### Scope levels
- **Local variables**: declared inside a method, visible only within that method (and nested blocks).
- **Instance variables (fields)**: declared in the class, visible to all methods of the class.
- **Block scope**: variables declared inside `{}` (loops, `if`) are limited to that block.

### Access modifiers
| Modifier | Who can access |
| --- | --- |
| `private` | Only the class itself |
| `public` | Any class |
| `protected` | Same package and subclasses (legacy/inheritance topic) |
| *(default, no keyword)* | Same package only |

### Key Notes
- Encapsulation = `private` fields + `public` accessors/mutators. This is the AP CS A ideal.
- A `public` field can be read and written by anyone, bypassing validation.

### Common Errors
- Using a local variable outside its block.
- Shadowing: declaring a local variable with the same name as a field. Use `this` to refer to the field.

## 3.9 The `this` Keyword

### Definition
`this` is a reference to the **current object**. It distinguishes instance variables from parameters with the same name and can be used to call one constructor from another.

```java
public class Student {
    private String name;

    public Student(String name) {
        this.name = name;   // this.name = field, name = parameter
    }

    public boolean hasName(String name) {
        return this.name.equals(name);
    }
}
```

### Key Notes
- `this` is only available in instance methods and constructors, not static ones.
- Constructor chaining: `this("Unknown", 0);` must be the first statement in a constructor.

### Common Errors
- Omitting `this` when a parameter shadows a field: `name = name;` assigns the parameter to itself, leaving the field unchanged. This bug is silent and devastating.

### Python aside (optional, Java stays canonical)
Python uses `self` where Java uses `this`:

```python
class Student:
    def __init__(self, name):
        self.name = name
```

Same idea, different keyword. The AP exam uses Java, where forgetting `this` is a rite of passage.

## 4. Connection to AP CS A New Unit Three

### Curriculum Context
New Unit 3 is the old [Unit 5](unit_5.md) with a few new buzzwords: "abstraction and program design" and "impact of program design." The actual content - classes, constructors, methods, static, scope, access, `this` - is the same.

### Relevance
Every data-collection algorithm in [New Unit 4](new_unit_4.md) operates on objects you design here. If your class is a mess, your collections are a mess. Trash in, trash out.

### Practice Questions
1. **Trace**: What is printed?
   ```java
   Student s = new Student("Alan", 3);
   s.setApScore(5);
   System.out.println(s.getApScore());
   ```
   **Answer**: `5`.

2. ** Identify the error**: Why does this fail?
   ```java
   public void Student() { }
   ```
   **Answer**: A constructor cannot have a return type, not even `void`. This is just a badly named method.

3. **References**: What is printed after `reassign(stu)` from the example above?
   **Answer**: The caller's `stu` still refers to the original object; reassignment inside the method does not escape.

4. **Static**: If three `Student` objects are created, how many copies of `studentCount` exist?
   **Answer**: One - static variables are shared.

5. **Coding exercise**: Design a `Course` class with private fields for name and roster size, a constructor, getters, and a method that returns whether the course is full (capacity 30). Add validation in the setter.

---
# [next](new_unit_4.md)
