# 🔢 Majority Element

## 🔗 Problem Link

LeetCode 169: Majority Element

---

## 🏷️ Tags

- Array
- Sorting

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given an integer array `nums` of size `n`, return the **majority element**.

The majority element is the element that appears **more than ⌊n / 2⌋ times**.

You may assume that the majority element always exists in the array.

---

## ✨ Examples

### Example 1

**Input**

```text
nums = [3,2,3]
```

**Output**

```text
3
```

---

### Example 2

**Input**

```text
nums = [2,2,1,1,1,2,2]
```

**Output**

```text
2
```

---

## 🚀 Approach

Since the majority element appears **more than half of the array size**, it will always occupy the middle position after sorting.

1. Sort the array.
2. Return the element at index `n / 2`.

Because the majority element occurs more than `⌊n/2⌋` times, it is guaranteed to be the middle element in the sorted array.

---

## 💻 Java Solution

```java
class Solution {

    public int majorityElement(int[] nums) {

        Arrays.sort(nums);

        return nums[nums.length / 2];
    }
}
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n log n)`

- Sorting the array takes `O(n log n)` time.

**Space Complexity:** `O(1)`

- No extra space is used (ignoring the internal space used by the sorting algorithm).

---

## 🔒 Constraints

- `1 ≤ nums.length ≤ 5 × 10⁴`
- `-10⁹ ≤ nums[i] ≤ 10⁹`
- The majority element always exists.

---

## 🌟 Key Points

- Uses sorting to identify the majority element.
- The majority element always occupies the middle index after sorting.
- Simple and easy to understand.
- No frequency counting is required.

---

## ⚠️ Common Mistakes

- Forgetting that this approach relies on the guarantee that a majority element always exists.
- Returning the first or last element after sorting instead of the middle element.
- Assuming this approach works for problems where no majority element is guaranteed.
