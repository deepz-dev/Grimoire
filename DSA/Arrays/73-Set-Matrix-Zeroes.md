# 0️⃣ Set Matrix Zeroes

## 🔗 Problem Link

LeetCode 73: Set Matrix Zeroes

---

## 🏷️ Tags

- Array
- Matrix
- In-Place
- Two Pass

---

## 📊 Difficulty

Medium

---

## Problem Statement

Given an `m x n` integer matrix, if an element is `0`, set its **entire row and column** to `0`.

The modification must be done **in-place**.

---

## ✨ Examples

### Example 1

**Input**

```text
matrix = [
  [1,1,1],
  [1,0,1],
  [1,1,1]
]
```

**Output**

```text
[
  [1,0,1],
  [0,0,0],
  [1,0,1]
]
```

---

### Example 2

**Input**

```text
matrix = [
  [0,1,2,0],
  [3,4,5,2],
  [1,3,1,5]
]
```

**Output**

```text
[
  [0,0,0,0],
  [0,4,5,0],
  [0,3,1,0]
]
```

---

# 🚀 Approach

The important problem is:

> If we immediately convert a row/column to `0`, how do we know whether that `0` was originally present?

For example:

```text
1  1  1
1  0  1
1  1  1
```

If we start modifying while traversing, the newly-created zeros can be mistaken for original zeros.

So we use **two passes**.

---

## Step 1 — Mark Zero Rows and Columns

Create two arrays:

```text
row[m]
col[n]
```

If:

```text
matrix[i][j] == 0
```

mark:

```text
row[i] = true
col[j] = true
```

Example:

```text
1 1 1
1 0 1
1 1 1
```

Markers become:

```text
row = [false, true, false]

col = [false, true, false]
```

---

## Step 2 — Set Cells to Zero

Traverse the matrix again.

If:

```text
row[i] == true
OR
col[j] == true
```

then:

```text
matrix[i][j] = 0
```

---

## 🧠 Algorithm

```text
1. Create row[] and col[] markers.

2. Traverse the matrix.
   If matrix[i][j] == 0:
       row[i] = true
       col[j] = true

3. Traverse the matrix again.
   If row[i] == true OR col[j] == true:
       matrix[i][j] = 0

4. Done.
```

---

## 💻 Java Solution

```java
class Solution {

    public void setZeroes(int[][] matrix) {

        // Number of rows
        int m = matrix.length;

        // Number of columns
        int n = matrix[0].length;

        // Mark rows containing zero
        boolean[] row = new boolean[m];

        // Mark columns containing zero
        boolean[] col = new boolean[n];

        // First pass:
        // Find all original zeroes
        for (int i = 0; i < m; i++) {

            for (int j = 0; j < n; j++) {

                if (matrix[i][j] == 0) {

                    row[i] = true;
                    col[j] = true;
                }
            }
        }

        // Second pass:
        // Set marked rows and columns to zero
        for (int i = 0; i < m; i++) {

            for (int j = 0; j < n; j++) {

                if (row[i] || col[j]) {

                    matrix[i][j] = 0;
                }
            }
        }
    }
}
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(m × n)`

- First traversal checks every matrix element.
- Second traversal checks every matrix element.

```text
O(m × n) + O(m × n)
= O(m × n)
```

---

**Space Complexity:** `O(m + n)`

We use:

```text
row[m]
col[n]
```

to store which rows and columns contain zeroes.

---

# 🔥 Optimal Approach

The above solution is good, but it does **not** use constant extra space.

We can use the **first row and first column of the matrix itself as markers**.

Instead of:

```text
boolean[] row
boolean[] col
```

we store the information inside:

```text
matrix[0][j]
matrix[i][0]
```

This reduces the extra space to:

```text
O(1)
```

---

## 🧠 Optimal Idea

Suppose:

```text
1 1 1
1 0 1
1 1 1
```

The zero at:

```text
matrix[1][1]
```

means:

```text
row 1 → zero
col 1 → zero
```

We can mark this using:

```text
matrix[1][0] = 0
matrix[0][1] = 0
```

So the matrix itself stores the markers.

---

## ⚠️ Important Problem

The first row and first column are being used as marker storage.

Therefore, we must separately remember whether the **original first row** and **original first column** contained zero.

Use:

```text
boolean firstRowZero
boolean firstColZero
```

---

## 🚀 Optimal Algorithm

### 1. Check first row

```text
firstRowZero = true
```

if any element in the first row is `0`.

### 2. Check first column

```text
firstColZero = true
```

if any element in the first column is `0`.

### 3. Use first row and first column as markers

For every remaining cell:

```text
if matrix[i][j] == 0

    matrix[i][0] = 0
    matrix[0][j] = 0
```

### 4. Zero marked rows and columns

For:

```text
i = 1 → m-1
j = 1 → n-1
```

if:

```text
matrix[i][0] == 0
OR
matrix[0][j] == 0
```

set:

```text
matrix[i][j] = 0
```

### 5. Finally handle first row and first column

Use the saved:

```text
firstRowZero
firstColZero
```

values.

---

## 💻 Optimal Java Solution

```java
class Solution {

    public void setZeroes(int[][] matrix) {

        int m = matrix.length;
        int n = matrix[0].length;

        boolean firstRowZero = false;
        boolean firstColZero = false;

        // Check first row
        for (int j = 0; j < n; j++) {

            if (matrix[0][j] == 0) {
                firstRowZero = true;
                break;
            }
        }

        // Check first column
        for (int i = 0; i < m; i++) {

            if (matrix[i][0] == 0) {
                firstColZero = true;
                break;
            }
        }

        // Use first row and first column as markers
        for (int i = 1; i < m; i++) {

            for (int j = 1; j < n; j++) {

                if (matrix[i][j] == 0) {

                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }

        // Set marked rows to zero
        for (int i = 1; i < m; i++) {

            if (matrix[i][0] == 0) {

                for (int j = 1; j < n; j++) {
                    matrix[i][j] = 0;
                }
            }
        }

        // Set marked columns to zero
        for (int j = 1; j < n; j++) {

            if (matrix[0][j] == 0) {

                for (int i = 1; i < m; i++) {
                    matrix[i][j] = 0;
                }
            }
        }

        // Handle first row
        if (firstRowZero) {

            for (int j = 0; j < n; j++) {
                matrix[0][j] = 0;
            }
        }

        // Handle first column
        if (firstColZero) {

            for (int i = 0; i < m; i++) {
                matrix[i][0] = 0;
            }
        }
    }
}
```

---

# 🆚 Solutions

| Approach | Extra Space | Time | Idea |
|---|---:|---:|---|
| Row + Column Arrays | `O(m+n)` | `O(m×n)` | Store markers separately |
| First Row + Column | `O(1)` | `O(m×n)` | Use matrix itself as markers |

### 🏆 Which is better?

**Optimal → First Row + First Column**

Why?

Both solutions take:

```text
O(m × n)
```

time.

But:

```text
Solution 1 → O(m + n) space
Solution 2 → O(1) space
```

So the second approach is better when the interviewer asks for **constant extra space**.

---

## 🌟 Key Points

- Do not immediately convert cells to zero while detecting zeroes.
- First **mark**, then **modify**.
- Simple solution uses separate row/column arrays.
- Optimal solution uses the matrix's first row and first column as markers.
- Remember the original state of the first row and first column.
- Optimal complexity:

```text
Time  → O(m × n)
Space → O(1)
```

---

## ⚠️ Common Mistakes

- Modifying the matrix while detecting zeroes.
- Forgetting that newly-created zeroes can affect later cells.
- Forgetting to separately track the first row.
- Forgetting to separately track the first column.
- Using extra `O(m × n)` space unnecessarily.
- Overwriting marker information before using it.

---

## 🎯 Interview Tip

If asked:

> "Can you do it without extra space?"

Think:

```text
Use first row + first column as markers
```

The key trick is:

```text
matrix[i][0] → tells whether row i should become 0

matrix[0][j] → tells whether column j should become 0
```

And separately remember:

```text
firstRowZero
firstColZero
```

That's the main idea behind the **O(1) space solution**.
