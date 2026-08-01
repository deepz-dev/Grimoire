# ➖ Longest Subarray With Zero Sum

## 🔗 Problem Link

GeeksforGeeks: Largest Subarray with 0 Sum

---

## 🏷️ Tags

- Array
- Prefix Sum
- HashMap

---

## 📊 Difficulty

Medium

---

## Problem Statement

Given an integer array `A` of size `n`, find the **length of the longest subarray whose sum is equal to 0**.

Return the maximum possible length.

---

## ✨ Examples

### Example 1

**Input**

```text
A = [15,-2,2,-8,1,7,10,23]
```

**Output**

```text
5
```

**Explanation**

```text
Subarray = [-2,2,-8,1,7]

Sum = 0

Length = 5
```

---

### Example 2

**Input**

```text
A = [1,2,3]
```

**Output**

```text
0
```

---

### Example 3

**Input**

```text
A = [9,-3,3,-1,6,-5]
```

**Output**

```text
5
```

---

## 🚀 Optimal Approach (Prefix Sum + HashMap)

Maintain a running **prefix sum** while traversing the array.

If the same prefix sum occurs again, then the elements between those two indices must have a sum of **0**.

Why?

```text
Suppose

Prefix Sum at i = X

Prefix Sum at j = X

Then,

Sum(i+1...j)

= Prefix(j) - Prefix(i)

= X - X

= 0
```

Store the **first occurrence** of every prefix sum in a HashMap.

Whenever the same sum appears again, calculate the subarray length and update the answer.

---

## 🧠 Algorithm

1. Initialize:

```text
sum = 0

maxLen = 0

HashMap<PrefixSum, FirstIndex>
```

2. Traverse the array.

3. Update prefix sum.

4. If prefix sum becomes `0`

- Entire array from `0` to `i` has zero sum.

5. Else

- If prefix sum already exists

```text
Length = i - firstOccurrence
```

Update answer.

- Otherwise

Store the current prefix sum and its index.

6. Return `maxLen`.

---

## 💻 Java Solution

```java
import java.util.*;

class Solution {

    public int maxLen(int[] A, int n) {

        Map<Integer, Integer> mpp = new HashMap<>();

        int maxi = 0;
        int sum = 0;

        for (int i = 0; i < n; i++) {

            sum += A[i];

            if (sum == 0) {
                maxi = i + 1;
            }

            else {

                if (mpp.containsKey(sum)) {

                    maxi = Math.max(maxi, i - mpp.get(sum));
                }

                else {

                    mpp.put(sum, i);
                }
            }
        }

        return maxi;
    }
}
```

---

## 🧪 Dry Run

Input

```text
A = [9,-3,3,-1,6,-5]
```

Initially

```text
sum = 0

maxLen = 0

HashMap = {}
```

### i = 0

```text
sum = 9

Store

9 → 0
```

---

### i = 1

```text
sum = 6

Store

6 → 1
```

---

### i = 2

```text
sum = 9

Already exists

Length = 2 - 0 = 2

maxLen = 2
```

---

### i = 3

```text
sum = 8

Store

8 → 3
```

---

### i = 4

```text
sum = 14

Store

14 → 4
```

---

### i = 5

```text
sum = 9

Already exists

Length = 5 - 0 = 5

maxLen = 5
```

Traversal ends.

Answer

```text
5
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

- Each element is visited once.
- HashMap operations take `O(1)` on average.

**Space Complexity:** `O(n)`

- In the worst case, every prefix sum is unique.

---

## 💡 Why Prefix Sum Works?

Suppose

```text
Prefix Sum till index i = 20

Prefix Sum till index j = 20
```

Then

```text
Subarray(i+1...j)

= 20 - 20

= 0
```

Hence,

Whenever the same prefix sum repeats,

the elements between those indices always sum to zero.

That is the key idea behind this solution.

---

## 🌟 Key Points

- Uses Prefix Sum.
- Uses HashMap to store first occurrence of each prefix sum.
- Repeated prefix sum indicates a zero-sum subarray.
- Store only the first occurrence to maximize the subarray length.
- Works for positive, negative, and mixed arrays.
- This is the optimal solution.

---

## ⚠️ Common Mistakes

- Updating the index of an already existing prefix sum.
- Not handling the case when prefix sum becomes `0`.
- Using nested loops, resulting in `O(n²)` time.
- Forgetting that only the first occurrence of a prefix sum should be stored.

---

## 🎯 Interview Tip

Whenever you encounter:

```text
Longest Subarray
+
Target Sum
+
Array contains negative numbers
```

Think immediately of:

```text
Prefix Sum + HashMap
```

Sliding Window **does not work** with negative numbers because the window sum is no longer monotonic.

Prefix Sum is the optimal approach.
