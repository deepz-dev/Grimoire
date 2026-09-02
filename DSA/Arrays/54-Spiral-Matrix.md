# 🌀 Spiral Matrix

## 🔗 Problem Link : https://leetcode.com/problems/spiral-matrix/description/

LeetCode 54: Spiral Matrix


---

## 🏷️ Tags

- Array
- Matrix
- Simulation
- Boundary Traversal

---

## 📊 Difficulty

Medium

---

## Problem Statement

Given an `m × n` matrix, return all elements of the matrix in **spiral order**.

Spiral order means:

```text
→ Right
↓ Down
← Left
↑ Up
```

and then continue moving inward until all elements are visited.

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
[1,2,3,6,9,8,7,4,5]
```

---

### Example 2

**Input**

```text
matrix = [
    [1,2,3,4],
    [5,6,7,8],
    [9,10,11,12]
]
```

**Output**

```text
[1,2,3,4,8,12,11,10,9,5,6,7]
```

---

# 🚀 Approach

Use **Boundary Traversal**.

Instead of thinking about individual elements, maintain four boundaries:

```text
top
bottom
left
right
```

These boundaries represent the current outer layer of the matrix.

---

## 🧠 The 4 Steps

For every layer, traverse in this order:

### 1️⃣ Traverse Top Row

Move:

```text
left → right
```

Then:

```text
top++
```

because the top row has been completely processed.

---

### 2️⃣ Traverse Right Column

Move:

```text
top → bottom
```

Then:

```text
right--
```

because the right column has been completely processed.

---

### 3️⃣ Traverse Bottom Row

Move:

```text
right → left
```

Then:

```text
bottom--
```

because the bottom row has been completely processed.

But this should only happen if:

```text
top <= bottom
```

This prevents processing the same row twice.

---

### 4️⃣ Traverse Left Column

Move:

```text
bottom → top
```

Then:

```text
left++
```

But this should only happen if:

```text
left <= right
```

This prevents processing the same column twice.

---

# 🔑 Boundary Visualization

For:

```text
1  2  3
4  5  6
7  8  9
```

Initially:

```text
top = 0
bottom = 2
left = 0
right = 2
```

### Step 1 — Top

```text
1 → 2 → 3
```

Then:

```text
top++
```

---

### Step 2 — Right

```text
6
↓
9
```

Then:

```text
right--
```

---

### Step 3 — Bottom

```text
8 ← 7
```

Then:

```text
bottom--
```

---

### Step 4 — Left

```text
4
↑
```

Then:

```text
left++
```

Remaining:

```text
5
```

Final:

```text
[1,2,3,6,9,8,7,4,5]
```

---

# 🧠 Why Do We Need the Boundary Checks?

Consider:

```text
1 2 3
4 5 6
```

After processing the top row and right column:

```text
1 2 3
4 5 6
```

When processing the bottom row, we get:

```text
6 ← 5 ← 4
```

Now there is no remaining left column to process.

So we check:

```java
if (top <= bottom)
```

Similarly, for a matrix with only one remaining column, we must check:

```java
if (left <= right)
```

These conditions prevent **duplicate elements**.

---

# 💻 Java Solution

```java
class Solution {

    public List<Integer> spiralOrder(int[][] matrix) {

        List<Integer> result = new ArrayList<>();

        int top = 0;
        int bottom = matrix.length - 1;
        int left = 0;
        int right = matrix[0].length - 1;

        while (top <= bottom && left <= right) {

            // Traverse top row: left → right
            for (int i = left; i <= right; i++) {
                result.add(matrix[top][i]);
            }
            top++;

            // Traverse right column: top → bottom
            for (int i = top; i <= bottom; i++) {
                result.add(matrix[i][right]);
            }
            right--;

            // Traverse bottom row: right → left
            if (top <= bottom) {

                for (int i = right; i >= left; i--) {
                    result.add(matrix[bottom][i]);
                }

                bottom--;
            }

            // Traverse left column: bottom → top
            if (left <= right) {

                for (int i = bottom; i >= top; i--) {
                    result.add(matrix[i][left]);
                }

                left++;
            }
        }

        return result;
    }
}
```

---

# 🧪 Dry Run

For:

```text
1 2 3
4 5 6
7 8 9
```

Initial:

```text
top = 0
bottom = 2
left = 0
right = 2
```

### Round 1

**Top row**

```text
1 2 3
```

Result:

```text
[1,2,3]
```

Update:

```text
top = 1
```

---

**Right column**

```text
6
9
```

Result:

```text
[1,2,3,6,9]
```

Update:

```text
right = 1
```

---

**Bottom row**

```text
8 7
```

Result:

```text
[1,2,3,6,9,8,7]
```

Update:

```text
bottom = 1
```

---

**Left column**

```text
4
```

Result:

```text
[1,2,3,6,9,8,7,4]
```

Update:

```text
left = 1
```

---

### Round 2

Remaining:

```text
5
```

Add:

```text
5
```

Final:

```text
[1,2,3,6,9,8,7,4,5]
```

---

# ⏱️ Complexity Analysis

Let the matrix contain `m × n` elements.

**Time Complexity:** `O(m × n)`

- Every matrix element is visited exactly once.

**Space Complexity:** `O(m × n)`

- The returned `result` list contains all `m × n` elements.
- Apart from the output list, only a few variables are used:

```text
O(1) auxiliary space
```

---

## 🌟 Key Points

- Use **four boundaries**:

```text
top
bottom
left
right
```

- Traverse in four directions:

```text
→ Top row
↓ Right column
← Bottom row
↑ Left column
```

- Move the corresponding boundary after each traversal.
- Use boundary checks before traversing the bottom row and left column.
- Every element is visited exactly once.
- This is the standard **Boundary Traversal** approach.

---

## ⚠️ Common Mistakes

- Forgetting to update a boundary after traversal.
- Traversing the bottom row without checking:

```java
if (top <= bottom)
```

- Traversing the left column without checking:

```java
if (left <= right)
```

- Mixing up the four directions.
- Using `i < right` instead of `i <= right`.
- Forgetting that the matrix can have only one row or one column.

---

## 🎯 Interview Tip

When you see:

> **"Return the matrix in spiral order."**

Immediately think:

```text
4 Boundaries
    ↓
top, bottom, left, right
    ↓
→ ↓ ← ↑
    ↓
Shrink boundaries
    ↓
Repeat
```

### 🔑 One-line memory trick

```text
Top → Right → Bottom → Left → Shrink → Repeat
```
