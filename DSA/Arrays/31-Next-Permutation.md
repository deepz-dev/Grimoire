# 🔄 Next Permutation

## 🔗 Problem Link

LeetCode 31: Next Permutation

---

## 🏷️ Tags

- Array
- Two Pointers

---

## 📊 Difficulty

Medium

---

## Problem Statement

A permutation of an array is an arrangement of its elements.

Given an integer array `nums`, rearrange it into the **next lexicographically greater permutation**.

If such an arrangement is not possible (the array is in descending order), rearrange it into the **lowest possible order (ascending order)**.

The modification must be done **in-place** using only constant extra space.

---

## ✨ Examples

### Example 1

**Input**

```text
nums = [1,2,3]
```

**Output**

```text
[1,3,2]
```

---

### Example 2

**Input**

```text
nums = [3,2,1]
```

**Output**

```text
[1,2,3]
```

---

### Example 3

**Input**

```text
nums = [1,1,5]
```

**Output**

```text
[1,5,1]
```

---

# 🚀 Optimal Approach

The next permutation is obtained in **three simple steps**.

### Step 1

Find the **pivot**.

Traverse from right to left and find the **first element smaller than its next element**.

```text
nums[i] < nums[i+1]
```

That index becomes the pivot.

---

### Step 2

Again traverse from the right and find the **first element greater than the pivot**.

Swap both elements.

---

### Step 3

Reverse everything after the pivot.

Since the suffix is already in descending order,

reversing it makes it the smallest possible arrangement.

---

## 🧠 Algorithm

1. Find the pivot from the end.

```text
nums[i] < nums[i+1]
```

2. If no pivot exists

```text
Reverse the entire array.
```

3. Otherwise

- Find the first larger element from the right.
- Swap with pivot.
- Reverse the suffix.

---

## 💻 Java Solution

```java
class Solution {

    public void nextPermutation(int[] nums) {

        int n = nums.length;

        int pivot = -1;

        // Find pivot
        for (int i = n - 2; i >= 0; i--) {

            if (nums[i] < nums[i + 1]) {
                pivot = i;
                break;
            }
        }

        // Already largest permutation
        if (pivot == -1) {

            reverse(nums, 0, n - 1);
            return;
        }

        // Find next greater element
        for (int i = n - 1; i > pivot; i--) {

            if (nums[i] > nums[pivot]) {

                swap(nums, i, pivot);
                break;
            }
        }

        // Reverse suffix
        reverse(nums, pivot + 1, n - 1);
    }

    void swap(int[] nums, int i, int j) {

        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }

    void reverse(int[] nums, int left, int right) {

        while (left < right) {

            swap(nums, left, right);
            left++;
            right--;
        }
    }
}
```

---

## 🧪 Dry Run

Input

```text
nums = [1,2,3]
```

### Step 1

Find pivot

```text
1 2 3
    ^
pivot = 2
```

---

### Step 2

Find next greater element

```text
Swap 2 and 3

1 3 2
```

---

### Step 3

Reverse suffix

```text
Suffix contains only one element

Answer

1 3 2
```

---

### Another Example

Input

```text
nums = [1,3,5,4,2]
```

Find pivot

```text
1 3 5 4 2
    ^
pivot = 3
```

Find next greater

```text
Swap 3 and 4

1 4 5 3 2
```

Reverse suffix

```text
5 3 2

↓

2 3 5
```

Final

```text
1 4 2 3 5
```

---

## 💡 Why Reverse the Suffix?

After finding the pivot,

everything to its right is already in **descending order**.

Example

```text
1 3 5 4 2

      5 4 2
```

This suffix is the **largest possible arrangement**.

After swapping,

we want the **smallest possible arrangement** after the pivot.

Reversing converts

```text
5 4 2

↓

2 4 5
```

which gives the immediate next permutation.

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

- One pass to find the pivot.
- One pass to find the next greater element.
- One pass to reverse the suffix.

Overall:

```text
O(n)
```

---

**Space Complexity:** `O(1)`

- No extra space is used.

---

## 🌟 Key Points

- Find the pivot from the right.
- Swap with the next greater element.
- Reverse the suffix.
- In-place algorithm.
- Constant extra space.
- Optimal solution.

---

## ⚠️ Common Mistakes

- Searching the pivot from the left.
- Swapping with the first greater element from the left instead of the right.
- Forgetting to reverse the suffix.
- Sorting the suffix instead of reversing it.
- Forgetting to reverse the whole array when no pivot exists.

---

## 🎯 Interview Tip

Remember the **3-Step Rule**:

```text
1. Find Pivot

↓

2. Find Next Greater Element

↓

3. Reverse the Suffix
```

If there is **no pivot**,

simply reverse the entire array.

This is the standard **optimal solution** used in interviews.
