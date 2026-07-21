# 🔢 Remove Duplicates from Sorted Array

## 🔗 Problem Link

LeetCode 26: Remove Duplicates from Sorted Array

---

## 🏷️ Tags

- Array
- Two Pointers

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given an integer array `nums` sorted in **non-decreasing order**, remove the duplicates **in-place** such that each unique element appears only once.

Return the number of unique elements `k`, where the first `k` elements of `nums` contain the unique values in sorted order.

> **Note:** The remaining elements beyond index `k - 1` can contain any values and are not considered.

---

## ✨ Examples

### Example 1

**Input**

```text
nums = [1,1,2]
```

**Output**

```text
2, nums = [1,2,_]
```

**Explanation**

The function returns `2`, and the first two elements of the array are `1` and `2`.

---

### Example 2

**Input**

```text
nums = [0,0,1,1,1,2,2,3,3,4]
```

**Output**

```text
5, nums = [0,1,2,3,4,_,_,_,_,_]
```

**Explanation**

The function returns `5`, and the first five elements contain all unique values in sorted order.

---

## 🚀 Approach

Since the array is already sorted, duplicate elements are always adjacent.

1. Initialize a pointer `i` at index `0` to track the position of the last unique element.
2. Traverse the array using another pointer `j` starting from index `1`.
3. If `nums[j]` is different from `nums[i]`:
   - Increment `i`.
   - Copy `nums[j]` to `nums[i]`.
4. After traversal, the first `i + 1` elements contain all unique values.
5. Return `i + 1`.

This approach removes duplicates in-place without using extra space.

---

## 💻 Java Solution

```java
class Solution {
    public int removeDuplicates(int[] nums) {

        if (nums.length == 0)
            return 0;

        int i = 0;

        for (int j = 1; j < nums.length; j++) {

            if (nums[i] != nums[j]) {
                nums[++i] = nums[j];
            }

        }

        return i + 1;
    }
}
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

- The array is traversed exactly once.

**Space Complexity:** `O(1)`

- No extra space is used.

---

## 🔒 Constraints

- `1 ≤ nums.length ≤ 3 × 10⁴`
- `-100 ≤ nums[i] ≤ 100`
- `nums` is sorted in non-decreasing order.

---

## 🌟 Key Points

- Uses the **Two Pointer** technique.
- Takes advantage of the sorted property of the array.
- Performs the operation completely in-place.
- Maintains the relative order of unique elements.
- No additional data structures are required.

---

## ⚠️ Common Mistakes

- Forgetting that the array is already sorted.
- Returning `i` instead of `i + 1`.
- Using an extra array instead of modifying the original array.
- Incrementing the pointer before checking for duplicates.

---

