# 🔢 Largest Element in Array

## 🔗 Problem Link

GeeksforGeeks: Largest in Array

---

## 🏷️ Tags

- Array
- Traversal

---

## 📊 Difficulty

Basic

---

## Problem Statement

Given an array `arr[]`, the task is to find and return the **largest element** in the array.

---

## ✨ Examples

### Example 1

**Input**

```text
arr = [1, 8, 7, 56, 90]
```

**Output**

```text
90
```

**Explanation**

The largest element in the array is `90`.

---

### Example 2

**Input**

```text
arr = [5, 5, 5, 5]
```

**Output**

```text
5
```

**Explanation**

All elements are the same, so the largest element is `5`.

---

### Example 3

**Input**

```text
arr = [10]
```

**Output**

```text
10
```

**Explanation**

There is only one element, so it is the largest.

---

## 🚀 Approach

Traverse the array while maintaining a variable `max` to store the largest element seen so far.

1. Initialize `max`.
2. Compare every element with `max`.
3. Update `max` whenever a larger element is found.
4. Return `max`.

---

## 💻 Java Solution

```java
class Solution {
    public static int largest(int[] arr) {

        int max = 0;

        for (int i = 0; i < arr.length; i++) {
            if (arr[i] > max)
                max = arr[i];
        }

        return max;
    }
}
```

> **Note:** Initializing `max = 0` works because the constraints guarantee non-negative values. If negative values are allowed, initialize `max = arr[0]`.

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

**Space Complexity:** `O(1)`

---

## 🔒 Constraints

- `1 ≤ arr.size() ≤ 10⁶`
- `0 ≤ arr[i] ≤ 10⁶`

---

## 🌟 Key Points

- Single traversal.
- No sorting required.
- Optimal solution.

---

## ⚠️ Common Mistakes

- Sorting the array unnecessarily.
- Initializing `max` incorrectly for negative numbers.