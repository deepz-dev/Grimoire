# 🔢 Sort Colors

## 🔗 Problem Link

LeetCode 75: Sort Colors

---

## 🏷️ Tags

- Array
- Two Pointers
- Dutch National Flag Algorithm

---

## 📊 Difficulty

Medium

---

## Problem Statement

Given an array `nums` containing only `0`, `1`, and `2`, sort the array **in-place** so that objects of the same color are adjacent.

The colors should appear in the following order:

```
0 → Red
1 → White
2 → Blue
```

You must solve the problem **without using the library's sort function**.

---

## ✨ Examples

### Example 1

**Input**

```text
nums = [2,0,2,1,1,0]
```

**Output**

```text
[0,0,1,1,2,2]
```

---

### Example 2

**Input**

```text
nums = [2,0,1]
```

**Output**

```text
[0,1,2]
```

---

## 🚀 Approach

Use the **Dutch National Flag Algorithm**.

Instead of sorting, divide the array into three regions using **three pointers**.

- `low` → Position where the next `0` should be placed.
- `mid` → Current element being processed.
- `high` → Position where the next `2` should be placed.

Traverse the array only once while maintaining these regions.

### Cases

### Case 1

```text
nums[mid] == 0
```

- Swap `nums[low]` and `nums[mid]`
- Increment both `low` and `mid`

---

### Case 2

```text
nums[mid] == 1
```

- `1` is already in the correct region.
- Simply move `mid`.

---

### Case 3

```text
nums[mid] == 2
```

- Swap `nums[mid]` and `nums[high]`
- Decrement `high`
- Do **NOT** increment `mid`

Reason:

The element swapped from the right side has not been processed yet.

---

## 🇳🇱 Dutch National Flag Algorithm

This algorithm was proposed by **Edsger W. Dijkstra**.

It is called the **Dutch National Flag Algorithm** because it partitions elements into three groups, just like the three colors of the Dutch national flag.

```
-------------------------------
|   0s   |   1s   |   Unknown   |   2s   |
-------------------------------
          ↑         ↑             ↑
         low       mid          high
```

During execution:

- Left side contains only `0`s.
- Middle contains only `1`s.
- Right side contains only `2`s.
- `mid` scans the unknown region.

The algorithm keeps shrinking the unknown region until the array becomes completely sorted.

---

## 💻 Java Solution

```java
class Solution {

    public void sortColors(int[] nums) {

        int low = 0;
        int mid = 0;
        int high = nums.length - 1;

        while (mid <= high) {

            if (nums[mid] == 0) {

                int temp = nums[low];
                nums[low] = nums[mid];
                nums[mid] = temp;

                low++;
                mid++;

            } else if (nums[mid] == 1) {

                mid++;

            } else {

                int temp = nums[high];
                nums[high] = nums[mid];
                nums[mid] = temp;

                high--;
            }
        }
    }
}
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

- Every element is processed at most once.

**Space Complexity:** `O(1)`

- Sorting is performed in-place using only three pointers.

---

## 🔒 Constraints

- `n == nums.length`
- `1 ≤ n ≤ 300`
- `nums[i]` is either `0`, `1`, or `2`

---

## 🌟 Key Points

- Uses the Dutch National Flag Algorithm.
- Maintains three partitions using `low`, `mid`, and `high`.
- Completes sorting in a single traversal.
- Uses constant extra space.
- No built-in sorting method is required.
- This is the optimal solution.

---

## ⚠️ Common Mistakes

- Incrementing `mid` after swapping with `high`.
  - The swapped element has not been processed yet.

- Using a sorting algorithm (`Arrays.sort()`), which violates the problem requirement.

- Using counting sort when the interviewer specifically asks for a one-pass solution.

- Incorrect loop condition.
  - Use:

```java
while (mid <= high)
```

not

```java
while (mid < high)
```

- Forgetting to increment both `low` and `mid` after placing a `0`.

---

## 💡 Why Don't We Increment `mid` After Swapping with `high`?

Consider:

```text
nums = [2,0,1]
```

Initially

```
low = 0
mid = 0
high = 2
```

Since

```
nums[mid] = 2
```

Swap with `high`

```
[1,0,2]
```

The new value at `mid` is `1`.

It has **never been processed**.

If we immediately increment `mid`, we might skip checking this new element.

Therefore,

After swapping with `high`:

```
high--
```

Only `high` moves.

`mid` stays at the same position to process the newly swapped element.

This is the most important part of the Dutch National Flag Algorithm.

---

## 🎯 Interview Tip

Whenever a problem contains exactly **three distinct values** that need to be grouped or partitioned efficiently, think of the **Dutch National Flag Algorithm**.

Common keywords:

- Three categories
- Three colors
- Partition into three groups
- One-pass sorting
- In-place sorting

These are strong hints that this algorithm may be applicable.
