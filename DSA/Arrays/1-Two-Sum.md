# 🔢 Two Sum

## 🔗 Problem Link

LeetCode 1: Two Sum

---

## 🏷️ Tags

- Array
- Hash Table

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given an array of integers `nums` and an integer `target`, return the **indices** of the two numbers such that they add up to `target`.

You may assume that each input has **exactly one solution**, and you may not use the same element twice.

You can return the answer in any order.

---

## ✨ Examples

### Example 1

**Input**

```text
nums = [2,7,11,15], target = 9
```

**Output**

```text
[0,1]
```

**Explanation**

`nums[0] + nums[1] = 2 + 7 = 9`

---

### Example 2

**Input**

```text
nums = [3,2,4], target = 6
```

**Output**

```text
[1,2]
```

---

### Example 3

**Input**

```text
nums = [3,3], target = 6
```

**Output**

```text
[0,1]
```

---

## 🚀 Approach

### Brute Force

1. Traverse the array using the first loop.
2. For every element, check all remaining elements.
3. If the sum equals the target, return their indices.
4. Since exactly one solution exists, the search stops once the pair is found.

Although simple, this approach checks every possible pair, resulting in quadratic time complexity.

---

## 💻 Java Solution

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {

        int[] ans = new int[2];

        for (int i = 0; i < nums.length; i++) {

            for (int j = i + 1; j < nums.length; j++) {

                if (nums[i] + nums[j] == target) {
                    ans[0] = i;
                    ans[1] = j;
                    return ans;
                }
            }
        }

        return ans;
    }
}
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n²)`

- Every pair of elements is checked.

**Space Complexity:** `O(1)`

- Only a constant amount of extra space is used.

---

## 🔒 Constraints

- `2 ≤ nums.length ≤ 10⁴`
- `-10⁹ ≤ nums[i] ≤ 10⁹`
- `-10⁹ ≤ target ≤ 10⁹`
- Exactly one valid answer exists.

---

## 🌟 Key Points

- Simple and easy-to-understand approach.
- Does not require any extra data structures.
- Suitable for learning before moving to the optimized solution.
- The optimal solution uses a **HashMap** and runs in **O(n)** time.

---

## ⚠️ Common Mistakes

- Starting the inner loop from `0` instead of `i + 1`.
- Using the same element twice.
- Forgetting to return immediately after finding the answer.
- Returning values instead of indices.