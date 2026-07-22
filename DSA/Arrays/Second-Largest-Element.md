# 🔢 Second Largest Element

## 🔗 Problem Link

GeeksforGeeks: Second Largest Element

---

## 🏷️ Tags

- Array
- Traversal

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given an array of positive integers `arr[]`, return the **second largest distinct element** in the array.

If it does not exist, return `-1`.

---

## ✨ Examples

### Example 1

**Input**

```text
arr = [12,35,1,10,34,1]
```

**Output**

```text
34
```

---

### Example 2

**Input**

```text
arr = [10,5,10]
```

**Output**

```text
5
```

---

### Example 3

**Input**

```text
arr = [10,10,10]
```

**Output**

```text
-1
```

---

## 🚀 Approach

Maintain two variables:

- `max` → largest element
- `secMax` → second largest element

During traversal:

- Update both if a new maximum is found.
- Otherwise update only `secMax` if the current element is greater than it and different from `max`.

---

## 💻 Java Solution

```java
class Solution {
    public int getSecondLargest(int[] arr) {

        int max = arr[0];
        int secMax = -1;

        for (int i = 1; i < arr.length; i++) {

            if (arr[i] > max) {
                secMax = max;
                max = arr[i];
            }

            else if (arr[i] > secMax && arr[i] != max) {
                secMax = arr[i];
            }
        }

        return secMax;
    }
}
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

**Space Complexity:** `O(1)`

---

## 🔒 Constraints

- `2 ≤ arr.size() ≤ 10⁵`
- `1 ≤ arr[i] ≤ 10⁵`

---

## 🌟 Key Points

- Single-pass solution.
- No sorting.
- Handles duplicate maximum values correctly.

---

## ⚠️ Common Mistakes

- Forgetting to ignore duplicate maximum values.
- Using sorting instead of linear traversal.