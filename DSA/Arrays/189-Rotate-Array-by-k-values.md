# 🔢 Rotate Array

## 🔗 Problem Link

LeetCode 189: Rotate Array

---

## 🏷️ Tags

- Array
- Two Pointers

---

## 📊 Difficulty

Medium

---

## Problem Statement

Given an integer array `nums`, rotate the array to the **right** by `k` steps, where `k` is non-negative.

The rotation must be performed **in-place**.

---

## ✨ Examples

### Example 1

**Input**

```text
nums = [1,2,3,4,5,6,7], k = 3
```

**Output**

```text
[5,6,7,1,2,3,4]
```

**Explanation**

```
Rotate 1 step : [7,1,2,3,4,5,6]
Rotate 2 steps: [6,7,1,2,3,4,5]
Rotate 3 steps: [5,6,7,1,2,3,4]
```

---

### Example 2

**Input**

```text
nums = [-1,-100,3,99], k = 2
```

**Output**

```text
[3,99,-1,-100]
```

---

## 🚀 Approach

Use the **Reversal Algorithm** to rotate the array efficiently.

1. Compute `k = k % n` to handle cases where `k` is greater than the array length.
2. Reverse the entire array.
3. Reverse the first `k` elements.
4. Reverse the remaining `n - k` elements.

This rotates the array in-place without using extra space.

---

## 💻 Java Solution

```java
class Solution {

    public void rotate(int[] nums, int k) {

        int n = nums.length;
        k = k % n;

        reverse(nums, 0, n - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, n - 1);
    }

    private void reverse(int[] nums, int left, int right) {

        while (left < right) {

            int temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;

            left++;
            right--;
        }
    }
}
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

- The array is reversed three times, but each element is visited only once overall.

**Space Complexity:** `O(1)`

- The rotation is performed in-place using constant extra space.

---

## 🔒 Constraints

- `1 ≤ nums.length ≤ 10⁵`
- `-2³¹ ≤ nums[i] ≤ 2³¹ - 1`
- `0 ≤ k ≤ 10⁵`

---

## 🌟 Key Points

- Uses the efficient **Reversal Algorithm**.
- Performs the rotation in-place.
- Handles cases where `k > n` using modulo.
- Better than rotating one step at a time (`O(n × k)`).

---

## ⚠️ Common Mistakes

- Forgetting to calculate `k % n`.
- Reversing the segments in the wrong order.
- Not handling `k = 0`.
- Using an extra array when an in-place solution is required.