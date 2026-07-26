# 🔢 Intersection of Two Sorted Arrays

## 🔗 Problem Link

TakeUForward: Intersection of Two Sorted Arrays

---

## 🏷️ Tags

- Array
- Two Pointers
- Merge Technique

---

## 📊 Difficulty

Easy

---

# 📖 Problem Statement

Given two **sorted arrays**, find all elements that are present in **both arrays**.

If an element appears multiple times in both arrays, include it in the answer the minimum number of times it appears in both.

---

## ✨ Example

### Example 1

**Input**

```text
A = [1,2,3,3,4,5,6]
B = [3,3,5]
```

**Output**

```text
[3,3,5]
```

---

### Example 2

**Input**

```text
A = [1,2,3,3,4,5,6]
B = [3,5]
```

**Output**

```text
[3,5]
```

---

# 🔍 Observation

Both arrays are already **sorted**.

Since they are sorted,

- smaller values always appear before larger values.
- there is no need to compare every element with every other element.

Instead, we can scan both arrays together using **two pointers**.

---

# 🚀 Optimal Approach (Two Pointers / Merge Technique)

Maintain two pointers:

- `i` → points to Array A
- `j` → points to Array B

Compare the current elements.

### Case 1

```text
A[i] < B[j]
```

The smaller element cannot appear later in B.

Move pointer `i`.

---

### Case 2

```text
A[i] > B[j]
```

The smaller element cannot appear later in A.

Move pointer `j`.

---

### Case 3

```text
A[i] == B[j]
```

Common element found.

- Add it to the answer.
- Move both pointers.

---

Continue until one array finishes.

---

# 💻 Java Code

```java
import java.util.*;

class Solution {

    public List<Integer> intersectionOfArrays(List<Integer> A, List<Integer> B) {

        List<Integer> ans = new ArrayList<>();

        int i = 0;
        int j = 0;

        while (i < A.size() && j < B.size()) {

            if (A.get(i) < B.get(j)) {

                i++;

            } else if (A.get(i) > B.get(j)) {

                j++;

            } else {

                ans.add(A.get(i));
                i++;
                j++;
            }
        }

        return ans;
    }
}
```

---

# 🧠 Dry Run

```
A = [1,2,3,3,4,5,6]
B = [3,3,5]
```

| i | j | A[i] | B[j] | Action | Answer |
|---|---|------|------|--------|--------|
|0|0|1|3|1 < 3 → i++|[]|
|1|0|2|3|2 < 3 → i++|[]|
|2|0|3|3|Equal → Add 3|[3]|
|3|1|3|3|Equal → Add 3|[3,3]|
|4|2|4|5|4 < 5 → i++|[3,3]|
|5|2|5|5|Equal → Add 5|[3,3,5]|

Final Answer

```
[3,3,5]
```

---

# ⏱️ Complexity Analysis

### Time Complexity

```
O(n + m)
```

Reason:

Each pointer moves only forward.

- `i` moves at most `n` times.
- `j` moves at most `m` times.

Total work:

```
O(n + m)
```

---

### Space Complexity

```
O(k)
```

where

```
k = size of the intersection
```

Only the answer list uses extra space.

---

# 🌟 Why Two Pointers Work?

Because both arrays are sorted.

Suppose

```
A[i] = 2
B[j] = 5
```

Since A is sorted,

everything before 5 in B has already been checked.

So,

```
2
```

can never match anything later in B.

Therefore,

move pointer `i`.

Likewise,

if

```
A[i] = 8
B[j] = 4
```

move pointer `j`.

This avoids unnecessary comparisons.

---

# 📝 Why is this called the Merge Technique?

This algorithm is identical to the **Merge step of Merge Sort**.

Instead of creating one merged array,

we compare elements from two sorted arrays simultaneously.

Difference:

**Merge Sort**

```
Take every element.
```

**Intersection**

```
Take only equal elements.
```

The traversal pattern is exactly the same.

---

# ⚠️ Common Mistakes

❌ Using nested loops.

```
O(n × m)
```

Very slow.

---

❌ Forgetting to move both pointers when equal.

Can cause an infinite loop.

---

❌ Moving the wrong pointer.

Always move the pointer pointing to the **smaller element**.

---

# 💡 Interview Takeaway

### Pattern Used

```
Two Pointers
        +
Merge Technique
```

### When should you think of this approach?

Whenever you see

- Two Sorted Arrays
- Merge Two Arrays
- Union
- Intersection
- Merge Intervals (variation)
- Merge Sorted Lists

---

# ⭐ Final Summary

✔ Arrays are already sorted.

✔ Maintain two pointers.

✔ Compare current elements.

✔ Move the pointer with the smaller value.

✔ When equal, add to answer and move both pointers.

✔ Time Complexity: `O(n + m)`

✔ Space Complexity: `O(k)`

This is the optimal solution because each element is visited at most once.
