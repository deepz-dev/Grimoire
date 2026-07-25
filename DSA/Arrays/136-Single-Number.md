# 🔢 Single Number

## 🔗 Problem Link

LeetCode 136: Single Number

---

## 🏷️ Tags

- Array
- Bit Manipulation

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given a **non-empty** integer array `nums`, every element appears **twice** except for one. Find and return that single element.

You must implement a solution with **linear runtime complexity** and use only **constant extra space**.

---

## ✨ Examples

### Example 1

**Input**

```text
nums = [2,2,1]
```

**Output**

```text
1
```

---

### Example 2

**Input**

```text
nums = [4,1,2,1,2]
```

**Output**

```text
4
```

---

### Example 3

**Input**

```text
nums = [1]
```

**Output**

```text
1
```

---

## 🚀 Approach

Use the **XOR** operation.

Properties of XOR:

- `a ^ a = 0`
- `a ^ 0 = a`
- XOR is commutative and associative.

Steps:

1. Initialize `res = 0`.
2. Traverse the array.
3. XOR every element with `res`.
4. Duplicate elements cancel each other out.
5. The remaining value is the element that appears only once.

---

## 💻 Java Solution

```java
class Solution {

    public int singleNumber(int[] nums) {

        int res = 0;

        for (int n : nums) {
            res ^= n;
        }

        return res;
    }
}
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

- The array is traversed exactly once.

**Space Complexity:** `O(1)`

- Only one extra variable is used.

---

## 🔒 Constraints

- `1 ≤ nums.length ≤ 3 × 10⁴`
- `-3 × 10⁴ ≤ nums[i] ≤ 3 × 10⁴`
- Every element appears twice except one.

---

## 🌟 Key Points

- Uses the XOR property to eliminate duplicate elements.
- Runs in linear time.
- Uses constant extra space.
- No sorting or HashMap is required.
- This is the optimal solution.

---

## ⚠️ Common Mistakes

- Using a HashMap, which increases space complexity to `O(n)`.
- Sorting the array, resulting in `O(n log n)` time.
- Forgetting that XOR of a number with itself is `0`.
- Initializing `res` with a value other than `0`.
