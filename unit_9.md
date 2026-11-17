---
title: AP CS A Unit 9 - Inheritance (Legacy Only)
---
[Go back to home page](README.md)
# [previous](unit_8.md)<-->[next](unit_10.md)
> **NOTE**: Inheritance was REMOVED from the AP CS A exam starting with the 2025-26 school year (new four-unit curriculum). This legacy unit is kept as enrichment only - do not study it for the current exam.

**TOP TIP**: If you are reading this for the current exam, you are studying a museum exhibit - admire the architecture, do not pack it for the trip. If you are here for enrichment (or a teacher who still teaches the old sequence), remember the one rule that matters: a reference variable is a campus map, and `new` builds the lecture hall. Polymorphism is when the map says "building" and the actual lecture hall is a specialized room that answers the same question its own way.

# AP CS A Unit Nine: Inheritance
## 1. Overview
Inheritance is a core object-oriented principle where a class (child/subclass) acquires fields and methods of another class (parent/superclass), promoting code reuse and abstraction. In AP CS A Unit Nine, the foci are single inheritance in Java, method overriding, and object interactions across an inheritance hierarchy.
## 2. Object Class Methods
### Definition
Every class in Java implicitly extends the `Object` class, which provides several important methods that can be overridden to customize behavior. In AP CS A, understanding `toString()`, `equals()`, and `hashCode()` is crucial for creating meaningful class representations and comparisons.
### Key Methods
1. **`toString()`**: Returns a string representation of the object. The default implementation returns a string containing the class name and hash code, which is often not useful.
   ```java
   public class Student {
       private String name;
       private int id;
       @Override
       public String toString() {
           return "Student[name=" + name + ", id=" + id + "]";
       }
   }
   ```
   - **Usage**: Automatically called by `System.out.println()` and string concatenation.
   - **Best Practice**: Always override `toString()` to provide meaningful information.
2. **`equals(Object obj)`**: Compares this object with another for equality. The default implementation uses `==` (reference equality).
   ```java
   @Override
   public boolean equals(Object obj) {
       if (this == obj) return true;
       if (obj == null || getClass() != obj.getClass()) return false;
       Student other = (Student) obj;
       return id == other.id && Objects.equals(name, other.name);
   }
   ```
   - **Contract**: Must be reflexive, symmetric, transitive, and consistent.
   - **Best Practice**: Override `equals()` when you need value-based equality, and always override `hashCode()` alongside it.
3. **`hashCode()`**: Returns an integer hash code for the object, used by hash-based collections like `HashMap` and `HashSet`.
   ```java
   @Override
   public int hashCode() {
       return Objects.hash(name, id);
   }
   ```
   - **Contract**: Equal objects must have equal hash codes (but not vice versa).
   - **Best Practice**: Use `Objects.hash()` to generate hash codes from relevant fields.
### Example Program
```java
import java.util.Objects;
public class APStudent {
    private String name;
    private int studentId;
    public APStudent(String name, int studentId) {
        this.name = name;
        this.studentId = studentId;
    }
    @Override
    public String toString() {
        return "APStudent[name=" + name + ", id=" + studentId + "]";
    }
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        APStudent other = (APStudent) obj;
        return studentId == other.studentId && Objects.equals(name, other.name);
    }
    @Override
    public int hashCode() {
        return Objects.hash(name, studentId);
    }
    public static void main(String[] args) {
        APStudent s1 = new APStudent("Alice", 1001);
        APStudent s2 = new APStudent("Alice", 1001);
        APStudent s3 = new APStudent("Bob", 1002);
        System.out.println("s1: " + s1); // Uses toString()
        System.out.println("s2: " + s2);
        System.out.println("s3: " + s3);
        System.out.println("s1.equals(s2): " + s1.equals(s2)); // true
        System.out.println("s1.equals(s3): " + s1.equals(s3)); // false
        System.out.println("s1 == s2: " + (s1 == s2)); // false (different objects)
        System.out.println("s1.hashCode(): " + s1.hashCode());
        System.out.println("s2.hashCode(): " + s2.hashCode());
        System.out.println("s3.hashCode(): " + s3.hashCode());
    }
}
```
**Output**:
```
s1: APStudent[name=Alice, id=1001]
s2: APStudent[name=Alice, id=1001]
s3: APStudent[name=Bob, id=1002]
s1.equals(s2): true
s1.equals(s3): false
s1 == s2: false
s1.hashCode(): 1963863037
s2.hashCode(): 1963863037
s3.hashCode(): 66965
```
### Common Errors
- **Forgetting to override `hashCode()` when overriding `equals()`**: This violates the contract and can cause issues with hash-based collections.
- **Not checking `null` and class type in `equals()`**: Can cause `ClassCastException` or incorrect comparisons.
- **Using mutable fields in `equals()` and `hashCode()`**: If fields change, the hash code changes, breaking collections.
- **Inconsistent `equals()` and `hashCode()`**: Equal objects must have equal hash codes.
### Connection to Inheritance
- When a subclass overrides `equals()`, it should also consider the superclass fields if the superclass has its own `equals()` implementation.
- The `instanceof` check in `equals()` should consider the class hierarchy if you want subclasses to be comparable with superclasses (though this is complex and often avoided in AP CS A).
---
## 3. Polymorphism
### Definition
Polymorphism allows a reference variable of a parent class type to refer to objects of child classes. The actual method invoked is determined at runtime, depending on the object's concrete class.
### Syntax and Behavior
```java
// Declaration using polymorphism
ApExamRecord record = new MultipleChoiceRecord();
```
* **Compile-time type**: `ApExamRecord` (parent)
* **Runtime type**: `MultipleChoiceRecord` (child)
When `record.calculateScore()` is called, Java invokes the lowest override in the hierarchy. If `MultipleChoiceRecord` overrides `calculateScore()`, that implementation runs; otherwise, it falls back to the parent’s version.
```java
public class ApExamRecord {
    public int calculateScore() {
        return 0; // default base behavior
    }
}
public class MultipleChoiceRecord extends ApExamRecord {
    @Override
    public int calculateScore() {
        int[] studentAnswers = {1, 3, 2, 4, 2};
        int[] correctAnswers = {1, 3, 2, 4, 2};
        int totalCorrect = 0;
        for (int i = 0; i < studentAnswers.length; i++) {
            if (studentAnswers[i] == correctAnswers[i]) {
                totalCorrect++;
            }
        }
        return totalCorrect * 2; // 2 points per question
    }
}
```
> **Key Point:** The overridden method must be declared in the parent class to be called polymorphically. New methods in the child require downcasting to invoke.
## 4. Constructors in Inheritance
### Note for Child Class Constructor
**REMEMBER:** If the parent class has a constructor requiring parameters, the first line of every child constructor must call `super(...)` with appropriate arguments before initializing child-specific fields.
```java
public class ApStudent {
    protected String studentName;

    public ApStudent(String studentName) {
        this.studentName = studentName;
    }
}
public class ChemistryStudent extends ApStudent {
    private int labScore;

    public ChemistryStudent(String studentName, int labScore) {
        super(studentName);        // call to parent constructor
        this.labScore = labScore;   // child-specific initialization
    }
}
```
Failure to call `super(...)` causes a compile-time error if no default parent constructor exists.
## 5. Upcasting and Downcasting
* **Upcasting**: Assigning a child object to a parent reference. Implicit and safe.
  ```java
  ApStudent student = new ChemistryStudent("Alex", 95);
  ```
* **Downcasting**: Converting a parent reference back to a child type. Requires an explicit cast and `instanceof` check to avoid `ClassCastException`.
  ```java
  if (student instanceof ChemistryStudent) {
      ChemistryStudent chem = (ChemistryStudent) student;
      int score = chem.getLabScore();
  }
  ```
## 6. Interfaces vs. Abstract Classes
### Abstract Classes
* Can include fields, constructors, concrete methods, and abstract methods.
* A class may extend one abstract class.
```java
public abstract class ApCourse {
    public abstract void takeExam();
    public void joinStudyGroup() {
        System.out.println("Joining study group...");
    }
}
```
### Interfaces
* Cannot have constructors or instance fields (Java 8+ allows `default` methods and `static` fields).
* A class can implement multiple interfaces.
```java
public interface GradingPolicy {
    double calculateGrade(double[] scores);
}
public class ApEnglish implements GradingPolicy {
    @Override
    public double calculateGrade(double[] scores) {
        double sum = 0;
        for (double s : scores) sum += s;
        return sum / scores.length;
    }
}
```
## 7. Inheritance Pitfalls and Best Practices
* **Fragile Base Class**: Changes in the parent can unexpectedly affect all subclasses - maintain clear documentation.
* **Use `@Override` Annotation**: Catches signature mismatches at compile time.
* **Favor Composition Over Inheritance**: Use when reuse can be achieved by containing instances rather than extending.
## 8. Composition Example
Composition involves including existing classes as fields rather than extending them, promoting loose coupling.
```java
public class ApExamReport {
    private ApStudent student;
    private ApExamRecord record;
    public ApExamReport(ApStudent student, ApExamRecord record) {
        this.student = student;
        this.record = record;
    }
    public void printReport() {
        System.out.println(student.studentName + " scored " + record.calculateScore());
    }
}
```
## 9. Extensions to Non-Curricular Topics
### 9.1 How to Use These Principles
1. **Liskov Substitution Principle (LSP)**
   * Ensure subclass methods honor the contracts of superclass methods (preconditions and postconditions).
   * Use tests that treat superclass and subclass instances interchangeably.
2. **Final Classes and Methods**
   * Mark classes/methods `final` to prevent modification or extension when stability is crucial.
   * Example: Utility classes like `java.lang.Math` are `final`.
3. **Design Patterns**
   * **Template Method**: Define a skeleton of an algorithm in an abstract class, deferring steps to subclasses.
     ```java
     public abstract class ExamGrader {
         public final void grade() {
             collectAnswers();
             int score = calculateScore();
             report(score);
         }
         protected abstract void collectAnswers();
         protected abstract int calculateScore();
         private void report(int score) {
             System.out.println("Score: " + score);
         }
     }
     ```
   * **Strategy Pattern**: Define a family of algorithms (interfaces) and make them interchangeable within a context class.
     ```java
     public interface ScoringStrategy {
         int score(int[] ans, int[] key);
     }
     public class StandardScoring implements ScoringStrategy {
         public int score(int[] a, int[] k) {
             int count = 0;
             for (int i = 0; i < a.length; i++) if (a[i] == k[i]) count++;
             return count * 1;
         }
     }
     public class EnhancedScoring implements ScoringStrategy {
         public int score(int[] a, int[] k) {
             int points = 0;
             for (int i = 0; i < a.length; i++) {
                 points += (a[i] == k[i]) ? 2 : -1;
             }
             return Math.max(points, 0);
         }
     }
     public class ExamContext {
         private ScoringStrategy strategy;
         public ExamContext(ScoringStrategy strategy) {
             this.strategy = strategy;
         }
         public int execute(int[] ans, int[] key) {
             return strategy.score(ans, key);
         }
     }
     ```
### 9.2 Examples
* **LSP in Action**:
  ```java
  public class BasePrinter {
      public void print(String text) { System.out.println(text); }
  }
  public class ColorPrinter extends BasePrinter {
      @Override
      public void print(String text) {
          System.out.println("\u001B[31m" + text + "\u001B[0m");
      }
  }
  BasePrinter p1 = new BasePrinter();
  BasePrinter p2 = new ColorPrinter();
  p1.print("Hello"); // normal
  p2.print("Hello"); // colored, still "Hello"
  ```
* **Final Method Example**:
  ```java
  public class SecureExam {
      public final void validateIdentity() {
          // fixed identity checks
      }
  }

  // Any subclass cannot override validateIdentity()
  ```
* **Strategy Pattern Use Case**:
  ```java
  int[] answers = {1,2,3};
  int[] key = {1,2,4};
  ExamContext standard = new ExamContext(new StandardScoring());
  ExamContext enhanced = new ExamContext(new EnhancedScoring());
  System.out.println(standard.execute(answers, key)); // score 2
  System.out.println(enhanced.execute(answers, key)); // score maybe higher
  ```
---
### 9.3 Additional Advanced Topics
4. **SOLID Principles**: A mnemonic for five design principles:
   * **S**ingle Responsibility Principle: A class should have one reason to change.
   * **O**pen/Closed Principle: Classes should be open for extension but closed for modification.
   * **L**iskov Substitution Principle (covered above).
   * **I**nterface Segregation Principle: Clients should not be forced to depend on unused methods - favor smaller, role-specific interfaces.
   * **D**ependency Inversion Principle: Depend upon abstractions, not concrete classes - inject dependencies via constructors or setters.
5. **Reflection and Annotations**:
   * Use the Reflection API (`java.lang.reflect`) to inspect classes, methods, and fields at runtime, enabling dynamic loading or testing frameworks.
     ```java
     Class<?> cls = Class.forName("ApStudent");
     for (Method m : cls.getMethods()) {
         System.out.println(m.getName());
     }
     ```
   * Create custom annotations to add metadata for tools or frameworks:
     ```java
     @Retention(RetentionPolicy.RUNTIME)
     @Target(ElementType.METHOD)
     public @interface TestCase {
         String description();
     }

     public class StudentTests {
         @TestCase(description = "Verify lab score calculation")
         public void testLabScore() { /* ... */ }
     }
     ```
6. **Generics and Bounded Types**:
   * Parameterize classes and methods to work with any type, improving type safety and reuse:
     ```java
     public class GradeBox<T extends Number> {
         private T grade;
         public GradeBox(T grade) { this.grade = grade; }
         public T getGrade() { return grade; }
     }
     ```
7. **Default and Static Interface Methods**:
   * Introduced in Java 8, interfaces can provide default implementations and static helper methods:
     ```java
     public interface Reportable {
         default void report() { System.out.println("Reporting..."); }
         static void log(String msg) { System.out.println("LOG: " + msg); }
     }
     ```
8. **Module System (Java 9+)**:
   * Encapsulate packages into modules using `module-info.java`, controlling visibility and dependencies:
     ```java
     module ap.course { exports com.ap.course; requires java.base; }
     ```
---
## 10. Inheritance Mechanics in Depth
### super and Constructor Chaining
Every constructor's very first statement is either `super(...)` or `this(...)`. If you write neither, Java inserts an invisible `super()` - the no-argument parent constructor. If the parent only defines a constructor with parameters, that implicit `super()` has nothing to call and the code will not compile. This is why the `ChemistryStudent` example above must call `super(studentName)` explicitly.

A chain can run several levels deep:
```java
public class Person {
    protected String name;
    public Person(String name) { this.name = name; }
}
public class Student extends Person {
    protected double gpa;
    public Student(String name, double gpa) {
        super(name);
        this.gpa = gpa;
    }
}
public class APStudent extends Student {
    private int apScore;
    public APStudent(String name, double gpa, int apScore) {
        super(name, gpa);
        this.apScore = apScore;
    }
}
```
Construct `new APStudent("Alex", 4.0, 5)` and the chain runs `Person` → `Student` → `APStudent`, one `super(...)` at a time.

### Overriding Rules
An override must match the parent method's name and parameter list exactly. The return type may be the same or a subtype (covariant return), and the override may not reduce visibility (`public` cannot become `private`). Adding `@Override` asks the compiler to verify all of this for you - which is the opposite of trash code, but a habit worth keeping.

**TOP TIP**: `static` methods are *hidden*, not overridden. Dynamic dispatch applies to instance methods only. A `static` method is chosen by the compile-time type of the reference, so it ignores polymorphism entirely.

### Trash Code Example - the missing @Override
```java
public class OverrideTrash {
    public static void main(String[] args) {
        ApExamRecord r = new MultipleChoiceRecord();
        System.out.println(r.calculateScroe()); // trash: typo, compiles fine
    }
}
class MultipleChoiceRecord extends ApExamRecord {
    public int calculateScroe() { // typo -- this is a NEW method, not an override
        return 10;
    }
}
```
**Output**:
```
0
```
**Why It's Trash**: `calculateScroe()` is misspelled, so it does not override `calculateScore()`. The parent's version runs and returns `0`, while the child's shiny new method is never reached through a parent reference. With `@Override` on the child method, the compiler would have caught the typo instantly. This is the sneakiest kind of trash code: it compiles, it runs, and it is quietly wrong.

### Common Errors
- Calling `super(...)` anywhere but the first line of a constructor - compile error.
- Calling an overridable method from a constructor: the subclass override can run before subclass fields are initialized, producing bizarre values.
- Forgetting that a private parent method is not inherited and therefore cannot be overridden (a same-named method in the child is just a new method).
- Assuming fields are polymorphic - they are not. Method calls dispatch on the runtime object; field access uses the compile-time type.
---
## 11. Polymorphism Deep Dive
### Compile-time Type vs Runtime Type
The reference's declared type decides *which methods exist* and *which overload is chosen* at compile time. The object's actual class decides *which override runs* at runtime. Get this distinction backwards and you will trace polymorphic code wrong every single time.

```java
ApStudent a = new ChemistryStudent("Alex", 95); // map says ApStudent, hall is ChemistryStudent
System.out.println(a.studentName);              // inherited field, fine
// a.getLabScore();                             // compile error: method not in ApStudent
if (a instanceof ChemistryStudent) {
    ChemistryStudent c = (ChemistryStudent) a;  // downcast after checking
    System.out.println(c.getLabScore());        // now the child-only method is legal
}
```

### Pseudocode Angle
```
DECLARE ref AS Parent
SET ref = NEW Child()
CALL ref.method()   -> runs Child's override if it exists, else Parent's
IF ref IS Child THEN
    CAST ref TO Child AND CALL childOnlyMethod()
END IF
```
Pseudocode makes dispatch look trivial. In Java the compiler still checks that `method()` exists on the *parent* before any of this runtime magic happens - a detail pseudocode glosses over and the legacy exam loved to test.

### Python aside (optional, Java stays canonical)
Python has the same idea with less ceremony:
```python
class ApExamRecord:
    def calculate_score(self):
        return 0

class MultipleChoiceRecord(ApExamRecord):
    def calculate_score(self):
        return 10

r = MultipleChoiceRecord()
print(r.calculate_score())   # 10 -- dynamic dispatch, same as Java
```
Python has no `instanceof` keyword (it uses `isinstance`) and no compile-time type checks on references. Java is stricter - and the (legacy) exam is Java.

### Common Errors
- Downcasting without an `instanceof` guard - `ClassCastException` when the object is not that subclass.
- Calling a child-only method through a parent reference - compile error until you downcast.
- Believing overriding a `private`, `static`, or `final` method works - it does not.

### Practice Questions
1. **Trace**: Given `ApExamRecord r = new MultipleChoiceRecord();` (where the child overrides `calculateScore()` to return `10`), what does `r.calculateScore()` return?
   **Answer**: `10` - runtime type picks the override.

2. **Compile or crash?**: `ApStudent s = new ChemistryStudent("Alex", 95); int x = s.getLabScore();`
   **Answer**: Compile error - `getLabScore()` is not declared in `ApStudent`. Downcast first.

3. **Constructor order**: In `new APStudent("Alex", 4.0, 5)` from section 10, which constructor body runs first?
   **Answer**: `Person`'s, then `Student`'s, then `APStudent`'s. `super(...)` always completes first.

4. **equals contract**: Why must `hashCode()` be overridden when `equals()` is?
   **Answer**: Equal objects must have equal hash codes; otherwise hash-based collections treat equal objects inconsistently.

5. **Coding Exercise**: Write a `toString()` override for a `GradeBook` class holding a `String student` and a `double gpa`. Keep the format `GradeBook[student=..., gpa=...]`.
---
## 12. Connection, Practice, and Extensions
### Connection to AP CS A Unit Nine
Inheritance was a full legacy unit and is the classic "hard" object-oriented topic: overriding, polymorphism, `super`, and `instanceof`. **It is not on the current four-unit exam** (see the banner at the top of this page); the modern path covers objects and classes in [New Unit 3](new_unit_3.md) and collections in [New Unit 4](new_unit_4.md) without a dedicated inheritance unit. Study this only for enrichment, old exams, or a teacher who still uses the ten-unit sequence - and enjoy the "trash code with a family tree" jokes while you are here.

### Best Practices
- Put `@Override` on every method you intend to override; let the compiler catch typos before the grader does.
- Keep `super(...)` as the first statement of every child constructor.
- Guard every downcast with `instanceof`.
- Override `equals()` and `hashCode()` together, and use the same fields in both.
- Prefer composition when the relationship is "has-a" rather than "is-a" - fewer fragile base classes, less trash code.

### Extensions
- **Abstract vs interface revisited**: An abstract class is a "is-a" blueprint with shared state; an interface is a "can-do" contract. Java allows one `extends` and many `implements`.
- **Template Method**: The `ExamGrader` example in section 9.1 fixes an algorithm's skeleton and lets subclasses fill in the steps - inheritance used for good, not trash.
- **Sealed classes (Java 17+)**: Restrict which classes may extend a parent, giving you control over the hierarchy. Well beyond the AP, but a natural next read if you liked this unit.
- **Records (Java 16+)**: Immutable data carriers with generated `equals`, `hashCode`, and `toString` - the modern answer to a lot of the boilerplate in section 2.

# [next](unit_10.md)
