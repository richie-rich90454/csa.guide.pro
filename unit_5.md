---
title: AP CS A Unit 5 - Crafting Classes
---
[Go back to home page](README.md)  
# [previous](unit_4.md) <-- [next](unit_6.md)  
**New curriculum equivalent**: This material now lives in [New Unit 3](new_unit_3.md).


# AP CS A Unit Five: Crafting Classes
## 1. Structure of a Class
A **class** in Java defines a custom data type, serving as a blueprint for objects by encapsulating **attributes (instance variables)** and **methods (behaviors)**. Classes model real-world entities, such as a student's academic profile, making them relatable for students.
```java
public class AcademicProfile {
    // Attributes
    private int studentID;
    // Constructor
    public AcademicProfile(int initialID) {
        studentID = initialID;
    }
    // Method
    public int getStudentID() {
        return studentID;
    }
}
```
## 2. Constructors
Constructors are special methods that initialize new objects. They share the class's name and have no return type, setting up initial attribute values critical for objects like a scholar's academic record.
* **Default constructor**: Automatically provided if no constructors are defined, initializing attributes to default values.
* **Parameterized constructor**: Accepts parameters to set specific initial values.
```java
public class Scholar {
    private String scholarName;
    private int scholarGradeLevel;
    public Scholar(String name, int gradeLevel) {
        scholarName = name;
        scholarGradeLevel = gradeLevel;
    }
}
```
## 3. Documentation with Comments
Effective documentation improves code clarity, a vital skill for AP CS A students collaborating on projects.
* **Single-line comment**: `// Tracks scholar's name`
* **Multi-line comment**:
  ```java
  /* Stores scholar's academic data
     for school records */
  ```
* **JavaDoc comment**: Generates professional documentation for classes and methods:
  ```java
  /**
   * Retrieves the scholar's grade level.
   * @return the scholar's grade level as an integer
   */
  public int getScholarGradeLevel() {
      return scholarGradeLevel;
  }
  ```
## 4. Accessor and Mutator Methods
Encapsulation, a core principle in AP CS A, protects attributes by declaring them `private` and providing controlled access through methods, ensuring data integrity.
* **Accessor (getter)**:
  ```java
  public String getScholarName() {
      return scholarName;
  }
  ```
* **Mutator (setter)**:
  ```java
  public void setScholarGradeLevel(int newGradeLevel) {
      scholarGradeLevel = newGradeLevel;
  }
  ```
## 5. Designing Methods
Methods define a class's functionality, enabling actions like checking academic status, a task relatable to students' experiences.
* Syntax:
  ```java
  public returnType methodName(parameters) {
      // Method implementation
  }
  ```
* Example:
  ```java
  public boolean isHonorRoll() {
      return scholarGradeLevel >= 90;
  }
  ```
## 5.1 Method Decomposition
### Definition
Method decomposition is the practice of breaking a complex method into smaller, more manageable methods. This improves code readability, maintainability, and reusability, key principles in AP CS A for writing clean, modular code.
### Why Decompose Methods?
1. **Readability**: Smaller methods with descriptive names are easier to understand.
2. **Reusability**: Common logic can be extracted into separate methods and reused.
3. **Maintainability**: Changes to specific functionality are isolated to a single method.
4. **Testing**: Smaller methods are easier to test individually.
### Example: Complex Method Before Decomposition
```java
public class GradeCalculator {
    public void processStudentGrades(int[] scores, String[] names) {
        // Complex method doing multiple things
        double sum = 0;
        for (int score : scores) {
            sum += score;
        }
        double average = sum / scores.length;
        System.out.println("Class Average: " + average);
        // Find highest score
        int highest = scores[0];
        String topStudent = names[0];
        for (int i = 1; i < scores.length; i++) {
            if (scores[i] > highest) {
                highest = scores[i];
                topStudent = names[i];
            }
        }
        System.out.println("Top Student: " + topStudent + " with score " + highest);
        // Determine grade distribution
        int aCount = 0, bCount = 0, cCount = 0, dCount = 0, fCount = 0;
        for (int score : scores) {
            if (score >= 90) aCount++;
            else if (score >= 80) bCount++;
            else if (score >= 70) cCount++;
            else if (score >= 60) dCount++;
            else fCount++;
        }
        System.out.println("Grade Distribution: A=" + aCount + ", B=" + bCount + ", C=" + cCount + ", D=" + dCount + ", F=" + fCount);
    }
}
```
### Example: After Decomposition
```java
public class GradeCalculator {
    public void processStudentGrades(int[] scores, String[] names) {
        double average = calculateAverage(scores);
        printAverage(average);
        String topStudent = findTopStudent(scores, names);
        printTopStudent(topStudent, scores, names);
        int[] gradeDistribution = calculateGradeDistribution(scores);
        printGradeDistribution(gradeDistribution);
    }
    private double calculateAverage(int[] scores) {
        double sum = 0;
        for (int score : scores) {
            sum += score;
        }
        return sum / scores.length;
    }
    private void printAverage(double average) {
        System.out.println("Class Average: " + average);
    }
    private String findTopStudent(int[] scores, String[] names) {
        int highest = scores[0];
        String topStudent = names[0];
        for (int i = 1; i < scores.length; i++) {
            if (scores[i] > highest) {
                highest = scores[i];
                topStudent = names[i];
            }
        }
        return topStudent;
    }
    private void printTopStudent(String topStudent, int[] scores, String[] names) {
        int highest = scores[0];
        for (int i = 1; i < scores.length; i++) {
            if (scores[i] > highest) {
                highest = scores[i];
            }
        }
        System.out.println("Top Student: " + topStudent + " with score " + highest);
    }
    private int[] calculateGradeDistribution(int[] scores) {
        int[] distribution = new int[5]; // A, B, C, D, F
        for (int score : scores) {
            if (score >= 90) distribution[0]++;
            else if (score >= 80) distribution[1]++;
            else if (score >= 70) distribution[2]++;
            else if (score >= 60) distribution[3]++;
            else distribution[4]++;
        }
        return distribution;
    }
    private void printGradeDistribution(int[] distribution) {
        System.out.println("Grade Distribution: A=" + distribution[0] + ", B=" + distribution[1] + ", C=" + distribution[2] + ", D=" + distribution[3] + ", F=" + distribution[4]);
    }
}
```
### Best Practices for Method Decomposition
1. **Single Responsibility Principle**: Each method should do one thing well.
2. **Descriptive Names**: Method names should clearly indicate their purpose.
3. **Reasonable Size**: If a method exceeds 20-30 lines, consider decomposition.
4. **Parameter Management**: Avoid passing too many parameters; consider creating helper classes.
5. **Access Modifiers**: Use `private` for helper methods that are only used within the class.
### Benefits in AP CS A
- **Easier Debugging**: Smaller methods make it easier to locate and fix errors.
- **Code Reuse**: Common operations (like calculating averages) can be reused across multiple methods.
- **Collaboration**: Team members can work on different methods simultaneously.
- **Readability**: Makes code more understandable for AP exam readers.
### Common Errors
- **Over-decomposition**: Creating too many tiny methods can make code harder to follow.
- **Poor Naming**: Vague method names like `doStuff()` reduce clarity.
- **Tight Coupling**: Decomposed methods that depend too much on each other's internal details.
---
## 6. Static Variables and Methods
Static members belong to the class, not individual objects, useful for tracking shared data like the total number of scholars in a school.
* **Static variable**:
  ```java
  private static int totalScholars = 0;
  ```
* **Static method**:
  ```java
  public static int getTotalScholars() {
      return totalScholars;
  }
  ```
## 7. Scope and Access Modifiers
Understanding scope and access is critical for AP CS A students to manage data visibility effectively.
* **`private`**: Restricts access to within the class.
* **`public`**: Allows access from any class.
* **Scope**: Determines where variables and methods are accessible (e.g., local to a method, instance-level, or class-level).
## 8. The `this` Keyword
The `this` keyword clarifies references to the current object's attributes, especially when parameter names match attribute names, addressing a common challenge for students.
```java
public void setScholarName(String scholarName) {
    this.scholarName = scholarName;
}
```
## 9. Ethical and Social Implications of Computing
This section encourages students to reflect on computing's broader impact, aligning with AP CS A's emphasis on responsible programming:
* **Data privacy**: Safeguarding scholar records.
* **Algorithmic fairness**: Ensuring unbiased grade calculations.
* **Ethical data use**: Respecting intellectual property in academic systems.
## Extensions for AP CS A Students
### Overloaded Constructors
Overloaded constructors provide flexibility by allowing multiple ways to initialize objects, such as creating a scholar with or without a grade level.
```java
public class Scholar {
    private String scholarName;
    private int scholarGradeLevel;
    // Default constructor
    public Scholar() {
        scholarName = "Unknown";
        scholarGradeLevel = 0;
    }
    // Overloaded constructor
    public Scholar(String name) {
        scholarName = name;
        scholarGradeLevel = 0;
    }
    // Overloaded constructor
    public Scholar(String name, int gradeLevel) {
        scholarName = name;
        scholarGradeLevel = gradeLevel;
    }
}
```
### Class Relationships
Explore how classes interact through **inheritance** (e.g., a `Scholar` class extending a `Person` class) and **composition** (e.g., a `Course` class containing a `Scholar` object).
* **Inheritance** example:
  ```java
  public class Person {
      private String name;
      public Person(String name) {
          this.name = name;
      }
  }
  public class Scholar extends Person {
      private int scholarGradeLevel;
      public Scholar(String name, int gradeLevel) {
          super(name);
          scholarGradeLevel = gradeLevel;
      }
  }
  ```
* **Composition** example:
  ```java
  public class Course {
      private Scholar enrolledScholar;
      public Course(Scholar scholar) {
          enrolledScholar = scholar;
      }
  }
  ```
### Generating JavaDoc Documentation
Students can use JavaDoc to create professional documentation, a practical skill for AP CS A projects.

* Command to generate JavaDoc:
  ```bash
  javadoc -d doc AcademicProfile.java
  ```
* Example JavaDoc for a method:
  ```java
  /**
   * Checks if the scholar qualifies for honor roll.
   * @return true if scholarGradeLevel is 90 or above, false otherwise
   */
  public boolean isHonorRoll() {
      return scholarGradeLevel >= 90;
  }
  ```
---
## 10. Abstraction and Program Design

### Definition
**Abstraction** is hiding the details that do not matter and exposing only what does. The site mascot, the `AcademicProfile`, does not need a student's favorite lunch to compute a GPA. Leaving it out is abstraction; including it is trash code wearing a fake moustache.

**Program design** is deciding, before you type, which classes and methods a problem needs. Nouns become classes (`Scholar`, `Course`); verbs become methods (`calculateGpa`, `enroll`). Skip this step and you get the academic version of a campus map with no lecture halls on it.

### Key Notes
- Abstraction is intentional omission, not forgetting.
- A class with one clear responsibility is easy to test. This is the Single Responsibility Principle in plain clothes.
- Encapsulation (`private` fields plus `public` methods) is abstraction enforced by the compiler.

### Trash Code Example: no abstraction, just parallel arrays
```java
public class NoAbstractionTrash {
    public static void main(String[] args) {
        String[] names = {"Alan", "Grace"};
        int[] apScores = {5, 4};
        double[] gpas = {4.0, 3.8};
        // keep three arrays in sync by sheer willpower
        System.out.println(names[0] + " scored " + apScores[0] + " with GPA " + gpas[0]);
    }
}
```
**Output**:
```
Alan scored 5 with GPA 4.0
```

**Why It's Trash**: There is no `Scholar` class. Three parallel arrays must be kept in lockstep forever, and one careless insert in the wrong array scrambles the whole grade book. This is what happens when you design on the fly instead of designing a class. Yes, this is the campus map with no lecture halls.

### Common Errors
- Making every field `public` "for convenience." It is convenient right up until someone sets `gpa = 100.0` and the dean calls.

---
## 11. Passing and Returning Object References

### Definition
When you pass an **object reference** into a method, Java copies the *address*, not the object. The method can therefore change the object's state, but it cannot make the caller's variable point somewhere else. The same rule applies to arrays, which are objects too (see [Unit 6](unit_6.md)).

```java
public static void boostScore(Scholar s) {
    s.setScholarGradeLevel(5);          // changes the caller's object
}
public static void reassign(Scholar s) {
    s = new Scholar("Transfer", 12);    // only changes the local reference
}
```

### Key Notes
- **Primitives** are passed by value: an `int` parameter inside the method is a copy.
- **References** are also passed by value, but the value copied is the address. Mutating the object sticks; reassigning the parameter does not.
- Returning a reference hands the caller an address to the same object.

### Common Errors
- Believing `s = new Scholar(...)` inside a method reassigns the caller's variable. It does not. This is one of the most-tested, most-missed ideas on the whole exam.

### Trash Code Example: reference wishful thinking
```java
public class ReferenceTrash {
    static void tryToChange(int score, Scholar s) {
        score = 99;                          // only the local copy
        s.setScholarGradeLevel(1);            // the real object changes
        s = new Scholar("Ghost", 12);         // only the local reference
    }
    public static void main(String[] args) {
        int gpaPoints = 3;
        Scholar real = new Scholar("Real", 3);
        tryToChange(gpaPoints, real);
        System.out.println(gpaPoints);                    // 3
        System.out.println(real.getScholarName());        // Real
        System.out.println(real.getScholarGradeLevel());  // 1
    }
}
```
**Output**:
```
3
Real
1
```

**Why It's Trash**: The method *looks* like it rewrites everything, but only the object mutation survives. Trash code keeps the reader guessing which variables are still real, exactly the confusion the exam is built to exploit.

### Python aside (optional, Java stays canonical)
Python passes object references the same way; it just spells the receiver `self` instead of `this`:
```python
class Scholar:
    def __init__(self, name):
        self.name = name
```
Same address-copied semantics. The exam uses Java, where forgetting `this` is a rite of passage.

---
## 12. Pseudocode Angle: Designing a Method

```
METHOD isHonorRoll(scholar)
  IF scholar.gradeLevel >= 90 THEN
    RETURN true
  ELSE
    RETURN false
  END IF
END METHOD
```
This is exactly the Java `isHonorRoll()` from Section 5 with the punctuation stripped. If you cannot say what a method does in pseudocode, you are not ready to write it in Java.

---
## 13. Connection to AP CS A Unit Five

### Curriculum Context
Unit Five is the original home of class design: fields, constructors, methods, decomposition, `static`, scope, access modifiers, and `this`. The [New Unit 3](new_unit_3.md) guide renames parts of this "abstraction and program design," but the Java is unchanged.

### Relevance
Every collection algorithm in [Unit 6](unit_6.md) and [New Unit 4](new_unit_4.md) operates on objects you design here. Bad classes make bad collections. Trash in, trash out.

### Practice Questions
1. **Trace**: What is printed?
   ```java
   Scholar s = new Scholar("Alan", 95);
   s.setScholarGradeLevel(92);
   System.out.println(s.isHonorRoll());
   ```
   **Answer**: `true` (92 is at least 90).
2. **Identify the error**: Why does this fail?
   ```java
   public void Scholar() { }
   ```
   **Answer**: A constructor cannot have a return type, not even `void`. This is just a badly named method, and Java supplies a default constructor instead.
3. **References**: After `tryToChange(gpaPoints, real)` above, what is `real.getScholarGradeLevel()`?
   **Answer**: `1`. The object was mutated; the reassignment inside the method did not escape.
4. **Static**: Three `Scholar` objects exist. How many copies of `totalScholars` are there?
   **Answer**: One. Static fields are shared by the class.
5. **Design exercise**: Design a `Course` class with private fields for name and capacity, a constructor, getters, and an `isFull()` method. Add validation in the setter so capacity cannot be negative.

---
## 14. Best Practices
- Keep fields `private`; expose them through accessors and validating mutators.
- Give each method one job. If a method needs a comment to explain what it does, decompose it.
- Initialize **every** field in **every** constructor, even the no-arg one.
- Use `this` whenever a parameter shadows a field.
- Call static members through the class name (`Scholar.getTotalScholars()`), never through an object.
- When you write a helper that mutates an object, name it as a verb (`boostScore`, not `change`).

---
# [next](unit_6.md)