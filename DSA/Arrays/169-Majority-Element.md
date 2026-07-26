# 🔢 Majority Element

## 🔗 Problem Link

LeetCode 169: Majority Element

---

## 🏷️ Tags

- Array
- Boyer-Moore Voting Algorithm

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

## 🚀 Optimal Approach (Boyer-Moore Voting Algorithm)

Use the **Boyer-Moore Voting Algorithm**.

### Intuition

Since the majority element appears **more than half of the time**, every occurrence of a different element can cancel out one occurrence of the majority element.

Eventually, only the majority element remains as the candidate.

### Steps

1. Initialize:
   - `candidate = nums[0]`
   - `count = 0`
2. Traverse the array.
3. If `count == 0`, choose the current element as the new candidate.
4. If the current element equals the candidate, increment `count`.
5. Otherwise, decrement `count`.
6. After one traversal, the candidate is the majority element.

Since the problem guarantees that a majority element always exists, no second verification pass is required.

---

## 💻 Java Solution

```java
class Solution {

    public int majorityElement(int[] nums) {

        int candidate = nums[0];
        int count = 0;

        for (int num : nums) {

            if (count == 0) {
                candidate = num;
            }

            if (num == candidate) {
                count++;
            } else {
                count--;
            }
        }

        return candidate;
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

- `1 ≤ nums.length ≤ 5 × 10⁴`
- `-10⁹ ≤ nums[i] ≤ 10⁹`
- The majority element always exists.

---

## 🌟 Key Points

- Uses the Boyer-Moore Voting Algorithm.
- Completes in a single traversal.
- Uses constant extra space.
- Does not require sorting or a HashMap.
- This is the optimal solution.

---

## ⭐ Alternative Solution (Sorting)

Another simple approach is sorting.

### Idea

Since the majority element appears more than `⌊n/2⌋` times, it will always occupy the middle position after sorting.

### Steps

1. Sort the array.
2. Return `nums[n / 2]`.

---

### 💻 Java Solution

```java
class Solution {

    public int majorityElement(int[] nums) {

        Arrays.sort(nums);

        return nums[nums.length / 2];
    }
}
```

---

### ⏱️ Complexity Analysis

**Time Complexity:** `O(n log n)`

- Sorting the array takes `O(n log n)` time.

**Space Complexity:** `O(1)`

- No extra space is used (ignoring the internal space used by the sorting algorithm).

---

### 🌟 Key Points

- Very easy to understand.
- Relies on sorting.
- Does not satisfy the optimal time complexity.
- Good for beginners, but not preferred in interviews.

---

## ⚠️ Common Mistakes

- Forgetting to reset the candidate when `count` becomes `0`.
- Incrementing and decrementing `count` incorrectly.
- Assuming Boyer-Moore works when a majority element is **not guaranteed**.
  - In such cases, a second verification pass is required.
- Using sorting (`O(n log n)`) when the interviewer expects the optimal `O(n)` solution.

---

## 💡 Why Does Boyer-Moore Work?

Think of the majority element as having extra "votes."

Every time we encounter a different element, it cancels one vote of the current candidate.

Since the majority element appears **more than half of the array**, it can never be completely canceled out.

Therefore, after all cancellations, the remaining candidate must be the majority element.
