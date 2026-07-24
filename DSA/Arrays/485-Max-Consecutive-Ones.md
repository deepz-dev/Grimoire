# 🔢 Max Consecutive Ones

## 🔗 Problem Link

LeetCode 485: Max Consecutive Ones

---

## 🏷️ Tags

- Array

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given a binary array `nums`, return the maximum number of consecutive `1`s in the array.

---

## ✨ Examples

### Example 1

**Input**

```text
nums = [1,1,0,1,1,1]
```

**Output**

```text
3
```

**Explanation**

The first sequence contains two consecutive `1`s, while the second sequence contains three consecutive `1`s. Hence, the answer is `3`.

---

### Example 2

**Input**

```text
nums = [1,0,1,1,0,1]
```

**Output**

```text
2
```

---

## 🚀 Approach

Traverse the array while keeping track of the current streak of consecutive `1`s.

1. Initialize two variables:
   - `count` to store the current streak.
   - `max` to store the maximum streak found so far.
2. Traverse the array.
3. If the current element is `1`, increment `count`.
4. Otherwise, reset `count` to `0`.
5. Update `max` after each iteration.
6. Return `max`.

---

## 💻 Java Solution

```java
class Solution {

    public int findMaxConsecutiveOnes(int[] nums) {

        int count = 0;
        int max = 0;

        for (int i = 0; i < nums.length; i++) {

            if (nums[i] == 1) {
                count++;
            } else {
                count = 0;
            }

            max = Math.max(count, max);
        }

        return max;
    }
}
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

- The array is traversed exactly once.

**Space Complexity:** `O(1)`

- Only two integer variables are used.

---

## 🔒 Constraints

- `1 ≤ nums.length ≤ 10⁵`
- `nums[i]` is either `0` or `1`

---

## 🌟 Key Points

- Uses a single traversal.
- No extra data structures are required.
- Resets the counter whenever a `0` is encountered.
- Updates the maximum streak after processing each element.

---

## ⚠️ Common Mistakes

- Forgetting to reset the counter when encountering `0`.
- Updating the maximum only after the loop instead of during traversal.
- Using nested loops, resulting in unnecessary `O(n²)` complexity.
