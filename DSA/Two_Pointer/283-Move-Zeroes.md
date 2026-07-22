# 🔢 Move Zeroes

## 🔗 Problem Link

LeetCode 283: Move Zeroes

---

## 🏷️ Tags

- Array
- Two Pointers

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given an integer array `nums`, move all `0`s to the end while maintaining the relative order of the non-zero elements.

> **Note:** The operation must be performed **in-place** without making a copy of the array.

---

## ✨ Examples

### Example 1

**Input**

```text
nums = [0,1,0,3,12]
```

**Output**

```text
[1,3,12,0,0]
```

---

### Example 2

**Input**

```text
nums = [0]
```

**Output**

```text
[0]
```

---

## 🚀 Approach

Use the **Two Pointer** technique.

1. Find the index of the first zero.
2. Traverse the remaining array.
3. Whenever a non-zero element is found, swap it with the first zero.
4. Move the zero pointer forward after every swap.

This keeps all non-zero elements in their original order while pushing zeros to the end.

---

## 💻 Java Solution

```java
class Solution {
    public void moveZeroes(int[] nums) {

        int j = -1;

        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 0) {
                j = i;
                break;
            }
        }

        if (j == -1) return;

        for (int i = j + 1; i < nums.length; i++) {

            if (nums[i] != 0) {

                int temp = nums[i];
                nums[i] = nums[j];
                nums[j] = temp;

                j++;
            }
        }
    }
}
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

**Space Complexity:** `O(1)`

---

## 🔒 Constraints

- `1 ≤ nums.length ≤ 10⁴`
- `-2³¹ ≤ nums[i] ≤ 2³¹ - 1`

---

## 🌟 Key Points

- Uses the Two Pointer technique.
- Performs the operation in-place.
- Preserves the relative order of non-zero elements.
- No extra array is required.

---

## ⚠️ Common Mistakes

- Creating a new array instead of modifying the original.
- Forgetting to preserve the order of non-zero elements.
- Incrementing the zero pointer incorrectly after swapping.