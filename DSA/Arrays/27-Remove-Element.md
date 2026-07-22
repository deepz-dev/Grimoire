# 🔢 Remove Element

## 🔗 Problem Link

LeetCode 27: Remove Element

---

## 🏷️ Tags

- Array
- Two Pointers

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` **in-place**.

Return the number of elements in `nums` that are **not equal** to `val`.

> **Note:** The order of the remaining elements may be changed. The first `k` elements of `nums` should contain the elements that are not equal to `val`.

---

## ✨ Examples

### Example 1

**Input**

```text
nums = [3,2,2,3], val = 3
```

**Output**

```text
2, nums = [2,2,_,_]
```

**Explanation**

The function returns `2`, and the first two elements of `nums` are `2`.

---

### Example 2

**Input**

```text
nums = [0,1,2,2,3,0,4,2], val = 2
```

**Output**

```text
5, nums = [0,1,4,0,3,_,_,_]
```

**Explanation**

The function returns `5`, and the first five elements contain all values except `2`.

---

## 🚀 Approach

Use the **Two Pointer** technique.

1. Initialize a pointer `i = 0`.
2. Traverse the array using another pointer `j`.
3. If `nums[j]` is **not equal** to `val`:
   - Copy `nums[j]` to `nums[i]`.
   - Increment `i`.
4. After the traversal, `i` represents the number of elements that are not equal to `val`.
5. Return `i`.

This modifies the array in-place without using extra space.

---

## 💻 Java Solution

```java
class Solution {
    public int removeElement(int[] nums, int val) {

        int i = 0;

        for (int j = 0; j < nums.length; j++) {

            if (nums[j] != val) {
                nums[i] = nums[j];
                i++;
            }

        }

        return i;
    }
}
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

- Each element is visited exactly once.

**Space Complexity:** `O(1)`

- No extra space is used.

---

## 🔒 Constraints

- `0 ≤ nums.length ≤ 100`
- `0 ≤ nums[i] ≤ 50`
- `0 ≤ val ≤ 100`

---

## 🌟 Key Points

- Uses the **Two Pointer** technique.
- Performs the operation in-place.
- No extra array is required.
- The order of the remaining elements is not important.
- Returns the count of elements that are not equal to `val`.

---

## ⚠️ Common Mistakes

- Returning the modified array instead of the count.
- Using an extra array unnecessarily.
- Forgetting to increment the write pointer after copying.
- Comparing with the wrong condition (`==` instead of `!=`).