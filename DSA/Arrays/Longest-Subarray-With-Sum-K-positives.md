# 📏 Longest Subarray With Sum K

## 🔗 Problem Link

Striver A2Z DSA Sheet: Longest Subarray With Sum K

---

## 🏷️ Tags

- Array
- Sliding Window
- Two Pointers

---

## 📊 Difficulty

Medium

---

## Problem Statement

Given an array `nums` consisting of **positive integers** and an integer `k`, return the length of the **longest subarray** whose sum is exactly `k`.

If no such subarray exists, return `0`.

> **Note:** This Sliding Window approach works **only when all elements are non-negative (positive or zero).**

---

## ✨ Examples

### Example 1

**Input**

```text
nums = [10,5,2,7,1,9]
k = 15
```

**Output**

```text
4
```

**Explanation**

```text
Subarray = [5,2,7,1]
Sum = 15
Length = 4
```

---

### Example 2

**Input**

```text
nums = [-3,2,1]
k = 6
```

**Output**

```text
0
```

---

## 🚀 Optimal Approach (Sliding Window)

Since all elements are positive:

- Expanding the window always increases the sum.
- Shrinking the window always decreases the sum.

Maintain a window using two pointers:

```text
left
right
```

Keep track of the current window sum.

- If `sum > k`, shrink the window.
- If `sum == k`, update the answer.
- Expand the window by moving `right`.

---

## 🧠 Algorithm

1. Initialize:

```text
left = 0
right = 0
sum = nums[0]
maxLen = 0
```

2. While `right < n`

- If `sum > k`
    - Remove elements from the left until `sum <= k`.
- If `sum == k`
    - Update maximum length.
- Move `right`.
- Add the new element to the window.

3. Return `maxLen`.

---

## 💻 Java Solution

```java
class Solution {

    public int longestSubarray(int[] nums, int k) {

        int n = nums.length;

        int maxLen = 0;

        int left = 0;
        int right = 0;

        int sum = nums[0];

        while (right < n) {

            while (left <= right && sum > k) {
                sum -= nums[left];
                left++;
            }

            if (sum == k) {
                maxLen = Math.max(maxLen, right - left + 1);
            }

            right++;

            if (right < n) {
                sum += nums[right];
            }
        }

        return maxLen;
    }
}
```

---

## 🧪 Dry Run

Input

```text
nums = [10,5,2,7,1,9]
k = 15
```

Initially

```text
left = 0
right = 0
sum = 10
maxLen = 0
```

### Window

```text
[10]
sum = 10
```

Expand

```text
right = 1

Window = [10,5]

sum = 15
```

Answer found

```text
Length = 2
maxLen = 2
```

Expand

```text
Window = [10,5,2]

sum = 17
```

Too large

```text
Remove 10

Window = [5,2]

sum = 7
```

Expand

```text
Window = [5,2,7]

sum = 14
```

Expand

```text
Window = [5,2,7,1]

sum = 15
```

Answer found

```text
Length = 4

maxLen = 4
```

Expand

```text
Window = [5,2,7,1,9]

sum = 24
```

Shrink

```text
Remove 5

sum = 19

Remove 2

sum = 17

Remove 7

sum = 10
```

Traversal ends.

Final answer

```text
4
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

- Every element is added once.
- Every element is removed once.

**Space Complexity:** `O(1)`

- Only a few variables are used.

---

## 💡 Why Does This Approach Work?

Because every number is positive:

```text
Adding elements → Sum increases

Removing elements → Sum decreases
```

This monotonic behavior allows us to maintain a valid sliding window in linear time.

If negative numbers were present:

```text
Adding a number could decrease the sum.

Removing a number could increase the sum.
```

Sliding Window would fail.

For arrays containing negative numbers, use the **Prefix Sum + HashMap** approach.

---

## 🌟 Key Points

- Uses Sliding Window (Two Pointers).
- Maintains a running window sum.
- Shrinks only when the sum exceeds `k`.
- Updates the answer whenever `sum == k`.
- Optimal for arrays with non-negative numbers.
- Runs in linear time.

---

## ⚠️ Common Mistakes

- Applying Sliding Window to arrays containing negative numbers.
- Forgetting to shrink the window while `sum > k`.
- Accessing `nums[right]` after incrementing `right` without checking bounds.
- Initializing `sum` incorrectly.
- Forgetting to update `maxLen` when `sum == k`.

---

## 🎯 Interview Tip

Whenever you see:

```text
Longest / Smallest Subarray
+
Positive numbers only
+
Target Sum
```

Immediately think:

```text
Sliding Window (Two Pointers)
```

If the array contains **negative numbers**, Sliding Window is **not applicable**. Use:

```text
Prefix Sum + HashMap
```

instead.
