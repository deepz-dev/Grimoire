# 🔺 Right Angle Triangle 2

## 🔗 Problem Link

GeeksforGeeks: Right Angle Triangle 2

---

## 🏷️ Tags

- Pattern Printing
- Nested Loops

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given an integer `n`, print a hollow right-angled triangle where the perpendicular and base have length `n`.

---

## ✨ Examples

### Example 1

**Input**

```text
n = 4
```

**Output**

```text
*
* *
*  *
* * * *
```

---

## 🚀 Approach

Use nested loops.

- Outer loop prints rows.
- Inner loop prints columns.
- Print `*` when:
  - first column
  - diagonal
  - last row
- Otherwise print spaces.

---

## 💻 Java Solution

```java
class Solution {

    public void printPattern(int n) {

        for (int i = 1; i <= n; i++) {

            for (int j = 1; j <= i; j++) {

                if (i == n || j == 1 || i == j)
                    System.out.print("* ");
                else
                    System.out.print("  ");
            }

            System.out.println();
        }
    }
}
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n²)`

**Space Complexity:** `O(1)`

---

## 🔒 Constraints

- `1 ≤ n ≤ 12`

---

## 🌟 Key Points

- Uses nested loops.
- Prints only the boundary.
- Last row is completely filled.

---

## ⚠️ Common Mistakes

- Forgetting the last row condition.
- Printing incorrect spaces leading to misaligned output.