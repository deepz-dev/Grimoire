# 🔢 Rotate Array by One

## 🔗 Problem Link

GeeksforGeeks: Rotate Array by One

---

## 🏷️ Tags

- Array

---

## 📊 Difficulty

Basic

---

## Problem Statement

Given an array `arr`, rotate the array by **one position in the clockwise direction**.

After rotation, the last element becomes the first element, and all other elements are shifted one position to the right.

---

## ✨ Examples

### Example 1

**Input**

```text
arr = [1, 2, 3, 4, 5]
```

**Output**

```text
[5, 1, 2, 3, 4]
```

**Explanation**

The last element (`5`) moves to the front, and the remaining elements shift one position to the right.

---

### Example 2

**Input**

```text
arr = [9, 8, 7, 6, 4, 2, 1, 3]
```

**Output**

```text
[3, 9, 8, 7, 6, 4, 2, 1]
```

**Explanation**

The last element (`3`) becomes the first element after rotation.

---

## 🚀 Approach

To rotate the array by one position:

1. Store the last element of the array.
2. Traverse the array from the end towards the beginning.
3. Shift every element one position to the right.
4. Place the stored last element at index `0`.

This performs the rotation in-place without using any extra array.

---

## 💻 Java Solution

```java
class Solution {
    public void rotate(int[] arr) {

        int n = arr.length;
        int last = arr[n - 1];

        for (int i = n - 1; i > 0; i--) {
            arr[i] = arr[i - 1];
        }

        arr[0] = last;
    }
}
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

- Each element is shifted exactly once.

**Space Complexity:** `O(1)`

- Only one extra variable is used.

---

## 🔒 Constraints

- `1 ≤ arr.size() ≤ 10⁵`
- `0 ≤ arr[i] ≤ 10⁵`

---

## 🌟 Key Points

- Performs the rotation in-place.
- No extra array is required.
- Right shift is done from the end to avoid overwriting elements.
- Efficient linear-time solution.

---

## ⚠️ Common Mistakes

- Traversing from left to right while shifting, which overwrites values.
- Forgetting to store the last element before shifting.
- Placing the last element at the wrong index after the shift.
