# 🔄 Rotate Image

## 🔗 Problem Link

LeetCode 48: Rotate Image

---

## 🏷️ Tags

- Array
- Matrix
- Two Pointers
- In-Place
- Transpose

---

## 📊 Difficulty

Medium

---

## Problem Statement

You are given an `n × n` 2D matrix representing an image.

Rotate the image **90 degrees clockwise**.

The rotation must be done **in-place**, meaning:

- Modify the original matrix.
- Do not create another `n × n` matrix.

---

## ✨ Examples

### Example 1

**Input**

```text
matrix = [
    [1,2,3],
    [4,5,6],
    [7,8,9]
]
```

**Output**

```text
[
    [7,4,1],
    [8,5,2],
    [9,6,3]
]
```

---

### Example 2

**Input**

```text
matrix = [
    [5,1,9,11],
    [2,4,8,10],
    [13,3,6,7],
    [15,14,12,16]
]
```

**Output**

```text
[
    [15,13,2,5],
    [14,3,4,1],
    [12,6,8,9],
    [16,7,10,11]
]
```

---

# 🚀 Approach

The main trick is:

> **90° clockwise rotation = Transpose + Reverse every row**

Instead of trying to directly move every element to its final position, break the rotation into two simple operations.

---

# 1️⃣ Transpose the Matrix

Transpose means:

```text
matrix[i][j] ↔ matrix[j][i]
```

In other words:

> Convert rows into columns.

### Before

```text
1 2 3
4 5 6
7 8 9
```

### After Transpose

```text
1 4 7
2 5 8
3 6 9
```

Notice:

```text
Row 1 → Column 1
Row 2 → Column 2
Row 3 → Column 3
```

---

## How to Transpose In-Place

We only need to swap elements **above the main diagonal**.

```text
1 2 3
4 5 6
7 8 9
  ↘
main diagonal
```

Swap:

```text
matrix[0][1] ↔ matrix[1][0]
matrix[0][2] ↔ matrix[2][0]
matrix[1][2] ↔ matrix[2][1]
```

So:

```java
for (int i = 0; i < n; i++) {

    for (int j = i + 1; j < n; j++) {

        int temp = matrix[i][j];

        matrix[i][j] = matrix[j][i];

        matrix[j][i] = temp;
    }
}
```

### Why `j = i + 1`?

Because:

```text
matrix[i][j]
```

and

```text
matrix[j][i]
```

are the same pair.

If we started from `j = 0`, we would swap the same elements twice.

---

# 2️⃣ Reverse Every Row

After transpose:

```text
1 4 7
2 5 8
3 6 9
```

Reverse each row:

```text
7 4 1
8 5 2
9 6 3
```

This is exactly the required **90° clockwise rotation**.

---

# 🧠 Complete Logic

```text
Original Matrix
      ↓
   Transpose
      ↓
Rows become Columns
      ↓
Reverse Every Row
      ↓
90° Clockwise Rotation
```

### 🔑 Memory Trick

```text
Clockwise 90° = Transpose + Reverse Rows
```

---

# 💻 Java Solution

```java
class Solution {

    public void rotate(int[][] matrix) {

        int n = matrix.length;

        // Step 1: Transpose the matrix
        for (int i = 0; i < n; i++) {

            for (int j = i + 1; j < n; j++) {

                int temp = matrix[i][j];

                matrix[i][j] = matrix[j][i];

                matrix[j][i] = temp;
            }
        }

        // Step 2: Reverse every row
        for (int i = 0; i < n; i++) {

            int left = 0;
            int right = n - 1;

            while (left < right) {

                int temp = matrix[i][left];

                matrix[i][left] = matrix[i][right];

                matrix[i][right] = temp;

                left++;
                right--;
            }
        }
    }
}
```

---

# 🧪 Dry Run

Consider:

```text
1 2 3
4 5 6
7 8 9
```

## Step 1 — Transpose

Swap:

```text
2 ↔ 4
3 ↔ 7
6 ↔ 8
```

Result:

```text
1 4 7
2 5 8
3 6 9
```

---

## Step 2 — Reverse Each Row

First row:

```text
1 4 7
↓
7 4 1
```

Second row:

```text
2 5 8
↓
8 5 2
```

Third row:

```text
3 6 9
↓
9 6 3
```

Final:

```text
7 4 1
8 5 2
9 6 3
```

---

# 🆚 Alternative Approach

Another way is to directly move each element to its rotated position.

For example:

```text
matrix[i][j]
```

moves to:

```text
matrix[j][n - 1 - i]
```

However, doing this directly requires careful swapping/cycle handling.

The **Transpose + Reverse** approach is much easier to reason about.

---

# 🏆 Why Transpose + Reverse Is Preferred

### 1. Simple logic

Instead of remembering complicated index transformations:

```text
(i, j) → (j, n - 1 - i)
```

we remember:

```text
Transpose
+
Reverse rows
```

### 2. In-place

No additional matrix is created.

### 3. Constant extra space

Only a temporary variable is used for swapping.

### 4. Optimal time

Every element is processed a constant number of times.

---

# ⏱️ Complexity Analysis

**Time Complexity:** `O(n²)`

### Transpose

There are approximately:

```text
n² / 2
```

swaps.

Therefore:

```text
O(n²)
```

### Reverse Rows

There are `n` rows, each taking `O(n)`:

```text
O(n²)
```

Overall:

```text
O(n²) + O(n²)
= O(n²)
```

---

**Space Complexity:** `O(1)`

Only a temporary variable is used:

```java
int temp;
```

No additional matrix or array is created.

---

## 🌟 Key Points

- 90° clockwise rotation can be broken into two operations.
- **Step 1:** Transpose.
- **Step 2:** Reverse every row.
- Transpose swaps:

```text
matrix[i][j]
↔
matrix[j][i]
```

- During transpose, start `j` from:

```text
i + 1
```

to avoid swapping elements twice.
- Reverse each row using two pointers.
- The solution modifies the matrix **in-place**.
- Optimal complexity:

```text
Time  → O(n²)
Space → O(1)
```

---

## ⚠️ Common Mistakes

- Creating another matrix when the problem requires in-place modification.
- Transposing the matrix incorrectly.
- Starting the transpose loop with `j = 0`.
- Forgetting to reverse the rows after transposing.
- Reversing columns instead of rows.
- Confusing clockwise rotation with anticlockwise rotation.

---

## 🎯 Interview Tip

If the interviewer asks:

> "Rotate an `n × n` matrix 90° clockwise in-place."

Think immediately:

```text
90° Clockwise
      ↓
Transpose
      ↓
Reverse every row
```

### 🔑 One-line memory trick

```text
Transpose + Reverse Rows = 90° Clockwise
```

For **90° anticlockwise**:

```text
Transpose + Reverse Columns
```
