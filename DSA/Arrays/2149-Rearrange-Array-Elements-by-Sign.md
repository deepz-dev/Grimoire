# 🔄 Rearrange Array Elements by Sign

## 🔗 Problem Link

LeetCode 2149: Rearrange Array Elements by Sign

---

## 🏷️ Tags

- Array
- Two Pointers
- Simulation

---

## 📊 Difficulty

Medium

---

## Problem Statement

Given an integer array `nums` of **even length** containing an equal number of positive and negative integers, rearrange the array such that:

- Every consecutive pair contains integers with opposite signs.
- The relative order of positive integers is preserved.
- The relative order of negative integers is preserved.
- The rearranged array starts with a positive integer.

Return the rearranged array.

---

## ✨ Examples

### Example 1

**Input**

```text
nums = [3,1,-2,-5,2,-4]
```

**Output**

```text
[3,-2,1,-5,2,-4]
```

**Explanation**

Positive numbers:

```text
[3,1,2]
```

Negative numbers:

```text
[-2,-5,-4]
```

Place positives at even indices and negatives at odd indices:

```text
Index:   0   1   2   3   4   5
Result: [3, -2,  1, -5,  2, -4]
```

---

### Example 2

**Input**

```text
nums = [-1,1]
```

**Output**

```text
[1,-1]
```

---

## 🚀 Optimal Approach (Two Pointers)

We know that:

- Positive numbers must occupy **even indices**.
- Negative numbers must occupy **odd indices**.

So we can directly place each element in its correct position.

Maintain two pointers:

```text
pos = 0
neg = 1
```

Here:

- `pos` points to the next position for a positive number.
- `neg` points to the next position for a negative number.

After placing an element, move the corresponding pointer by `2`.

---

## 🧠 Algorithm

1. Create a result array `ra` of the same size as `nums`.
2. Initialize:

```text
pos = 0
neg = 1
```

3. Traverse `nums`.
4. If the current number is positive:
   - Store it at `ra[pos]`.
   - Move `pos` by `2`.
5. If the current number is negative:
   - Store it at `ra[neg]`.
   - Move `neg` by `2`.
6. Return the result array.

---

## 💻 Java Solution

```java
class Solution {

    public int[] rearrangeArray(int[] nums) {

        int x = nums.length;

        int[] ra = new int[x];

        int pos = 0;
        int neg = 1;

        int i = 0;

        while (i < x) {

            if (nums[i] >= 0) {

                ra[pos] = nums[i];

                pos += 2;

            } else {

                ra[neg] = nums[i];

                neg += 2;
            }

            i++;
        }

        return ra;
    }
}
```

---

## 🔍 Why `pos = 0` and `neg = 1`?

The result must start with a positive number.

Therefore, positive numbers occupy:

```text
0, 2, 4, 6, ...
```

Negative numbers occupy:

```text
1, 3, 5, 7, ...
```

So we initialize:

```java
int pos = 0;
int neg = 1;
```

and move each pointer by:

```java
pos += 2;
neg += 2;
```

---

## 🧪 Dry Run

Consider:

```text
nums = [3,1,-2,-5,2,-4]
```

Initially:

```text
ra  = [_, _, _, _, _, _]

pos = 0
neg = 1
```

### `nums[0] = 3`

Positive:

```text
ra[0] = 3

ra = [3, _, _, _, _, _]

pos = 2
```

### `nums[1] = 1`

Positive:

```text
ra[2] = 1

ra = [3, _, 1, _, _, _]

pos = 4
```

### `nums[2] = -2`

Negative:

```text
ra[1] = -2

ra = [3, -2, 1, _, _, _]

neg = 3
```

### `nums[3] = -5`

Negative:

```text
ra[3] = -5

ra = [3, -2, 1, -5, _, _]

neg = 5
```

### `nums[4] = 2`

Positive:

```text
ra[4] = 2

ra = [3, -2, 1, -5, 2, _]
```

### `nums[5] = -4`

Negative:

```text
ra[5] = -4

ra = [3, -2, 1, -5, 2, -4]
```

Final result:

```text
[3,-2,1,-5,2,-4]
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

- Every element is visited exactly once.

**Space Complexity:** `O(n)`

- A new result array of size `n` is created.

---

## 💡 Why Does This Approach Work?

The problem guarantees that there are an equal number of positive and negative elements.

Therefore, if the array length is `n`:

```text
Positive elements = n / 2
Negative elements = n / 2
```

There are also exactly:

```text
n / 2 even indices
n / 2 odd indices
```

So we can directly place:

```text
Positive → Even indices
Negative → Odd indices
```

Since we traverse the original array from left to right, the relative order of both positive and negative numbers is automatically preserved.

---

## 🌟 Key Points

- Uses two index pointers.
- `pos` handles positive numbers.
- `neg` handles negative numbers.
- Positive numbers go to even indices.
- Negative numbers go to odd indices.
- Relative ordering is preserved.
- Requires only one traversal of the input.
- Runs in optimal `O(n)` time.

---

## ⚠️ Common Mistakes

- Starting both `pos` and `neg` from `0`.
- Incrementing the pointers by `1` instead of `2`.
- Putting negative numbers at even indices.
- Forgetting that the answer must start with a positive number.
- Rearranging the numbers in a way that changes their relative order.
- Trying to sort the array, which would destroy the required relative ordering.

---

## 🎯 Interview Idea

Whenever a problem gives a fixed pattern such as:

```text
Positive Negative Positive Negative ...
```

think about the **indices**.

Here the pattern directly tells us:

```text
Even index → Positive
Odd index  → Negative
```

That allows us to construct the answer directly in one traversal.
