# 🔺 Pascal's Triangle

## 🔗 Problem Link

**LeetCode 118: Pascal's Triangle**

---

## 🏷️ Tags

- Array
- Dynamic Programming
- Recursion
- Simulation

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given an integer `numRows`, return the first `numRows` of **Pascal's Triangle**.

In Pascal's Triangle:

- The first and last element of every row is `1`.
- Every other element is the sum of the two elements directly above it.

---

## ✨ Examples

### Example 1

**Input**

```text
numRows = 5
```

**Output**

```text
[
 [1],
 [1,1],
 [1,2,1],
 [1,3,3,1],
 [1,4,6,4,1]
]
```

---

### Example 2

**Input**

```text
numRows = 1
```

**Output**

```text
[
 [1]
]
```

---

## 🚀 Approach (Recursion)

The given solution uses **Recursion** to generate Pascal's Triangle.

### Algorithm

1. If `numRows == 0`, return an empty list.
2. If `numRows == 1`, return `[[1]]`.
3. Recursively generate the first `numRows - 1` rows.
4. Create a new row of size `numRows` and fill it with `1`s.
5. Calculate the middle elements using the previous row:
   - `newRow[i] = previousRow[i-1] + previousRow[i]`
6. Add the new row to the result.
7. Return the completed triangle.

---

## 💻 Java Solution

```java
class Solution {

    public List<List<Integer>> generate(int numRows) {

        if (numRows == 0)
            return new ArrayList<>();

        if (numRows == 1) {
            List<List<Integer>> result = new ArrayList<>();
            result.add(Arrays.asList(1));
            return result;
        }

        List<List<Integer>> prevRows = generate(numRows - 1);

        List<Integer> newRow = new ArrayList<>();

        for (int i = 0; i < numRows; i++) {
            newRow.add(1);
        }

        for (int i = 1; i < numRows - 1; i++) {
            newRow.set(i,
                prevRows.get(numRows - 2).get(i - 1)
                + prevRows.get(numRows - 2).get(i));
        }

        prevRows.add(newRow);

        return prevRows;
    }
}
```

---

## ⏱️ Complexity Analysis

### Time Complexity: `O(n²)`

- There are `n` recursive calls.
- Across all calls, a total of

```
1 + 2 + 3 + ... + n
= n(n + 1) / 2
```

elements are generated.

Therefore,

```
O(n²)
```

---

### Space Complexity: `O(n²)`

- The output stores all rows of Pascal's Triangle.

Output size:

```
1 + 2 + 3 + ... + n
= n(n + 1) / 2
```

- Recursive call stack requires `O(n)` space.

Overall Space Complexity:

```
O(n²)
```

---

## 🔒 Constraints

- `1 ≤ numRows ≤ 30`

---

## 🌟 Key Points

- Uses Recursion.
- Handles base cases separately.
- First and last element of every row is `1`.
- Middle elements are calculated from the previous row.
- Builds one row at a time.
- Returns the complete Pascal's Triangle.

---

## ⭐ Alternative Solution (Iterative)

Generate each row using loops instead of recursion.

For every row:

- First and last elements are `1`.
- Middle elements are obtained by adding the two elements above.

---

### 💻 Java Solution

```java
class Solution {

    public List<List<Integer>> generate(int numRows) {

        List<List<Integer>> result = new ArrayList<>();

        for (int i = 0; i < numRows; i++) {

            List<Integer> row = new ArrayList<>();

            for (int j = 0; j <= i; j++) {

                if (j == 0 || j == i)
                    row.add(1);
                else
                    row.add(result.get(i - 1).get(j - 1)
                            + result.get(i - 1).get(j));
            }

            result.add(row);
        }

        return result;
    }
}
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n²)`

- Every element is generated exactly once.

**Space Complexity:** `O(n²)`

- Stores the complete Pascal's Triangle.

---

## 💡 Why Does This Approach Work?

Each element (except the first and last) is obtained by adding the two elements directly above it.

```
Current Element = Upper Left + Upper Right
```

Example:

```
        1
      1   1
    1   2   1
  1   3   3   1
1   4   6   4   1
```

For example:

```
2 = 1 + 1
3 = 1 + 2
6 = 3 + 3
```

The recursive solution first generates all previous rows and then constructs the current row using this rule.

---

## ⚠️ Common Mistakes

- Forgetting the base cases (`0` and `1` rows).
- Accessing the wrong previous row.
- Forgetting that the first and last element must always be `1`.
- Using incorrect loop boundaries for the middle elements.
- Not adding the newly created row before returning.
- Forgetting that recursion adds an extra call stack of `O(n)`.