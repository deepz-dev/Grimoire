# 🔢 Maximum Subarray

## 🔗 Problem Link

LeetCode 53: Maximum Subarray

---

## 🏷️ Tags

- Array
- Dynamic Programming
- Kadane's Algorithm

---

## 📊 Difficulty

Medium

---

## Problem Statement

Given an integer array `nums`, find the **contiguous subarray** that has the largest sum and return its sum.

A **subarray** is a contiguous (continuous) part of an array.

---

## ✨ Examples

### Example 1

**Input**

```text
nums = [-2,1,-3,4,-1,2,1,-5,4]
```

**Output**

```text
6
```

**Explanation**

The subarray `[4,-1,2,1]` has the largest sum.

---

### Example 2

**Input**

```text
nums = [1]
```

**Output**

```text
1
```

---

### Example 3

**Input**

```text
nums = [5,4,-1,7,8]
```

**Output**

```text
23
```

---

## 🚀 Optimal Approach (Kadane's Algorithm)

Use **Kadane's Algorithm**.

### Intuition

While traversing the array, keep track of the current subarray sum.

- If adding the current element increases the sum, continue the current subarray.
- If the current sum becomes negative, discard it and start a new subarray from the next element.

A negative running sum can never help in obtaining a larger future sum.

### Steps

1. Initialize:
   - `sum = 0`
   - `max = Integer.MIN_VALUE`
2. Traverse the array.
3. Add the current element to `sum`.
4. Update `max` if `sum` is greater.
5. If `sum` becomes negative, reset it to `0`.
6. Return `max`.

---

## 💻 Java Solution

```java
class Solution {

    public int maxSubArray(int[] nums) {

        int sum = 0;
        int max = Integer.MIN_VALUE;

        for (int i = 0; i < nums.length; i++) {

            sum += nums[i];

            if (sum > max) {
                max = sum;
            }

            if (sum < 0) {
                sum = 0;
            }
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

- Only two extra variables are used.

---

## 🔒 Constraints

- `1 ≤ nums.length ≤ 10⁵`
- `-10⁴ ≤ nums[i] ≤ 10⁴`

---

## 🌟 Key Points

- Uses Kadane's Algorithm.
- Finds the maximum sum contiguous subarray.
- Traverses the array only once.
- Uses constant extra space.
- This is the optimal solution.

---

## ⭐ Alternative Solution (Brute Force)

Generate every possible subarray and calculate its sum.

Return the maximum sum obtained.

### 💻 Java Solution

```java
class Solution {

    public int maxSubArray(int[] nums) {

        int max = Integer.MIN_VALUE;

        for (int i = 0; i < nums.length; i++) {

            int sum = 0;

            for (int j = i; j < nums.length; j++) {

                sum += nums[j];

                max = Math.max(max, sum);
            }
        }

        return max;
    }
}
```

---

### ⏱️ Complexity Analysis

**Time Complexity:** `O(n²)`

- Generate every possible subarray.

**Space Complexity:** `O(1)`

---

### 🌟 Key Points

- Very easy to understand.
- Checks every possible subarray.
- Too slow for large inputs.
- Not preferred in interviews.

---

## 💡 Why Does Kadane's Algorithm Work?

Suppose the running sum becomes negative.

Example:

```text
Current Sum = -8
Next Element = 10
```

Two choices:

Continue:

```text
-8 + 10 = 2
```

Start a new subarray:

```text
10
```

Clearly,

```
10 > 2
```

A negative running sum only decreases future sums.

Therefore, whenever the running sum becomes negative, it is better to discard it and start a new subarray.

This greedy decision guarantees the maximum possible subarray sum.

---

## ⚠️ Common Mistakes

- Initializing `max` as `0`.
  - Fails when all elements are negative.

- Resetting the sum before updating `max`.

- Confusing a **subarray** with a **subsequence**.

- Forgetting that the subarray must be contiguous.

- Using the brute-force solution (`O(n²)`) when the interviewer expects Kadane's Algorithm.
