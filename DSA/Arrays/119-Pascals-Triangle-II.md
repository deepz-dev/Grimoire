# 🔺 Pascal's Triangle II

## 🔗 Problem Link

<a href="https://leetcode.com/problems/pascals-triangle-ii/description/" target="_blank">LeetCode 119: Pascal's Triangle II</a>

## 🏷️ Tags

- Array
- Dynamic Programming
- Math

## 📊 Difficulty

Easy

## Problem Statement

Given an integer `rowIndex`, return the `rowIndex`th (0-indexed) row of Pascal's Triangle.

In Pascal's Triangle, each number is the sum of the two numbers directly above it. The first and last elements of every row are always `1`.

---

## ✨ Examples

### Example 1

```text
Input:  rowIndex = 3
Output: [1,3,3,1]
```

### Example 2

```text
Input:  rowIndex = 0
Output: [1]
```

### Example 3

```text
Input:  rowIndex = 1
Output: [1,1]
```

---

## 🚀 Approach

### Build Each Row Using the Previous Row

The main idea is:

> Start with `[1]` and construct each next row using the previous row.

### Step 1: Initialize the First Row

```java
List<Integer> row = new ArrayList<>();
row.add(1);
```

The first row is always `[1]`.

### Step 2: Build Each New Row

Loop from `i = 1` to `rowIndex`.

For every iteration:

- Create a new list called `newRow`.
- Add `1` at the beginning.
- Calculate the middle elements using the previous row.
- Add `1` at the end.

### Step 3: Calculate Middle Elements

Each middle element is the sum of two adjacent elements from the previous row.

```java
newRow.add(row.get(j - 1) + row.get(j));
```

For example:

```text
Previous row: [1, 2, 1]

New row:      [1, 3, 3, 1]
                  ↑  ↑
                1+2 2+1
```

### Step 4: Update the Row

After constructing the new row:

```java
row = newRow;
```

The newly generated row becomes the previous row for the next iteration.

### Step 5: Return the Required Row

Once the loop finishes, return `row`.

---

## 💻 Java Solution

```java
class Solution {
    public List<Integer> getRow(int rowIndex) {

        List<Integer> row = new ArrayList<>();
        row.add(1);

        for (int i = 1; i <= rowIndex; i++) {

            List<Integer> newRow = new ArrayList<>();
            newRow.add(1);

            for (int j = 1; j < i; j++) {
                newRow.add(row.get(j - 1) + row.get(j));
            }

            newRow.add(1);
            row = newRow;
        }

        return row;
    }
}
```

---

## ⏱️ Complexity Analysis

### Time Complexity

`O(rowIndex²)`

Each new row is constructed by processing its middle elements. The total work is proportional to:

`1 + 2 + 3 + ... + rowIndex`

### Space Complexity

`O(rowIndex)`

Only the previous row and the newly generated row are stored at a time. Each row contains at most `rowIndex + 1` elements.

---

## 🔒 Constraints

- `0 <= rowIndex <= 33`

---

## 🌟 Key Points

- Pascal's Triangle is **0-indexed** in this problem.
- The first and last elements of every row are `1`.
- Middle elements are calculated by adding adjacent elements from the previous row.
- `row = newRow` updates the current row for the next iteration.
- Only two rows are needed at a time.
- Time complexity is `O(rowIndex²)`.
- Space complexity is `O(rowIndex)`.

## ⚠️ Common Mistakes

- Treating `rowIndex` as a 1-based index.
- Forgetting to add the first or last `1`.
- Using an incorrect inner-loop boundary.
- Trying to calculate middle elements without using the previous row.
- Forgetting to update `row` after creating `newRow`.

## 🎯 Interview Tip

Remember:

> **Pascal's Triangle II = Previous Row + Adjacent Sum + Boundary Ones.**

Unlike generating the entire triangle, this solution builds only the rows required to reach the target row.

## 📝 Commit Message

```text
feat(array): add Pascal's Triangle II solution
```
