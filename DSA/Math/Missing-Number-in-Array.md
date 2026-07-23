# 🔢 Missing Number in Array

## 🔗 Problem Link

GeeksforGeeks: Missing Number in Array

---

## 🏷️ Tags

- Array
- Math

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given an array `arr[]` of size `n - 1` containing distinct integers in the range `1` to `n`, find the missing number.

The array contains all numbers from `1` to `n` except one.

---

## ✨ Examples

### Example 1

**Input**

```text
arr = [1, 2, 3, 5]
```

**Output**

```text
4
```

**Explanation**

The numbers from `1` to `5` are present except `4`.

---

### Example 2

**Input**

```text
arr = [8, 2, 4, 5, 3, 7, 1]
```

**Output**

```text
6
```

**Explanation**

The numbers from `1` to `8` are present except `6`.

---

## 🚀 Approach

Use the mathematical formula for the sum of the first `n` natural numbers.

1. Calculate `n = arr.length + 1`.
2. Compute the expected sum using:
   ```
   n × (n + 1) / 2
   ```
3. Find the actual sum of all elements in the array.
4. The missing number is:
   ```
   expectedSum - actualSum
   ```

Using `long` prevents integer overflow for larger values of `n`.

---

## 💻 Java Solution

```java
class Solution {

    int missingNum(int arr[]) {

        long n = arr.length + 1;

        long sum = 0;

        for (int i = 0; i < arr.length; i++) {
            sum += arr[i];
        }

        long expectedSum = n * (n + 1) / 2;

        return (int)(expectedSum - sum);
    }
}
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

- The array is traversed only once.

**Space Complexity:** `O(1)`

- Only a few extra variables are used.

---

## 🔒 Constraints

- `2 ≤ n ≤ 10⁶`
- `1 ≤ arr[i] ≤ n`

---

## 🌟 Key Points

- Uses the mathematical sum formula.
- No sorting is required.
- No extra data structures are used.
- Using `long` avoids overflow.
- One of the most common approaches for this problem.

---

## ⚠️ Common Mistakes

- Using `int` instead of `long` for large inputs.
- Forgetting that the array size is `n - 1`.
- Calculating the expected sum with the wrong value of `n`.
- Making an off-by-one error while determining `n`.
