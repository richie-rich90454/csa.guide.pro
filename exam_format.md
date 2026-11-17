---
title: Exam Format - Old vs New
---

[Go back to home page](README.md)

# The Exam, Before and After the Great Reorganization

So College Board looked at the AP Computer Science A exam, decided ten units were too many, squashed them into four, and changed the exam while they were at it. Here is what changed, in case you are preparing for one version while your teacher is preparing you for the other.

## 1. Side-by-side comparison

| Feature | Legacy exam (through May 2025) | New exam (May 2026 onward) |
| --- | --- | --- |
| Multiple-choice weight | 50% of exam score | **55%** of exam score |
| Number of MC questions | 40 | **42** |
| Answer choices per MC question | 5 | **4** |
| Free-response weight | 50% | **45%** |
| Number of FR questions | 4 | 4 (but **shortened**) |
| Scored FR points | 36 | **25** |
| FR Question 3 | Data analysis with ArrayList **and arrays** | Data analysis with **ArrayList only** |
| Units | 10 | **4** |
| Inheritance | Tested (Unit 9) | **Removed** |
| Text files & data sets | Not tested | **Tested** (File, Scanner, ethics) |

**TOP TIP**: Fewer answer choices means guessing is now a 25% sport instead of a 20% sport. Trash code enthusiasts rejoice - your odds of accidentally getting one right went up.

## 2. What got added

- **Text files and data sets**: reading files with `File` and `Scanner` (`nextInt()`, `nextLine()`, `hasNext()`), and thinking about the ethics of collecting data. Covered in full detail in [New Unit 4](new_unit_4.md).
- **Binary search and merge sort** are now explicitly called out as standard algorithms. Covered in [New Unit 2](new_unit_2.md) and [New Unit 4](new_unit_4.md).
- **Informal runtime analysis**: being able to say "this is slower than that" without writing a proof. Covered in [New Unit 2](new_unit_2.md).
- **APIs and libraries**, assignment statements, input, and compiler basics get their own spotlight in [New Unit 1](new_unit_1.md).

## 3. What got removed or moved

- **Inheritance, polymorphism, interfaces, abstract classes**: gone from the exam. The old [Unit 9](unit_9.md) is kept here as enrichment because deleting knowledge is itself a form of trash code.
- **Arrays in FR Question 3**: the data-analysis FRQ now focuses only on `ArrayList`.
- The ten units were consolidated: old U1+U2 → new U1; old U3+U4 → new U2; old U5 → new U3; old U6+U7+U8+U10 → new U4.

## 4. Trash Code Example - studying the wrong exam

```java
public class WrongExamPrep {
    public static void main(String[] args) {
        // Study only inheritance for the new exam because it's "classic"
        String topic = "inheritance";
        boolean onNewExam = false;
        if (topic.equals("inheritance") && !onNewExam) {
            System.out.println("Wasting time correctly!");
        }
        // Gotcha: the new exam doesn't test this at all
    }
}
```

**Output**:
```
Wasting time correctly!
```

**Why It's Trash**: It compiles, it runs, and it prepares you for a question that no longer exists. That is peak trash code. Read the [exam changes](https://apcentral.collegeboard.org/courses/ap-computer-science-a/future-revisions) instead.

## 5. Practice Questions

1. **Recall**: What percentage of the new exam is multiple-choice? **Answer**: 55%.
2. **Compare**: How many answer choices does each new MC question have? **Answer**: 4.
3. **Trace**: True or false - arrays still appear in FR Question 3 on the new exam. **Answer**: False; it is ArrayList only.

---
# [next](new_unit_1.md)
