# 🔢 Longest Consecutive Sequence

## 🔗 Problem Link

LeetCode 128: Longest Consecutive Sequence

---

## 🏷️ Tags

- Array
- HashSet
- Sorting
- Sequence

---

## 📊 Difficulty

Medium

---

## Problem Statement

Given an **unsorted** array of integers `nums`, return the length of the **longest consecutive elements sequence**.

The sequence does not need to appear in the same order as the original array.

The solution must run in:

```text
O(n)
```

time.

---

## ✨ Examples

### Example 1

**Input**

```text
nums = [100,4,200,1,3,2]
```

**Output**

```text
4
```

**Explanation**

The longest consecutive sequence is:

```text
[1, 2, 3, 4]
```

Therefore:

```text
length = 4
```

---

### Example 2

**Input**

```text
nums = [0,3,7,2,5,8,4,6,0,1]
```

**Output**

```text
9
```

**Explanation**

The longest sequence is:

```text
[0,1,2,3,4,5,6,7,8]
```

Therefore:

```text
length = 9
```

---

### Example 3

**Input**

```text
nums = [1,0,1,2]
```

**Output**

```text
3
```

**Explanation**

The sequence is:

```text
[0,1,2]
```

The duplicate `1` does not increase the sequence length.

---

# 🚀 Approach

The array is **unsorted**, so checking consecutive elements directly will not work.

Example:

```text
[100, 4, 200, 1, 3, 2]
```

The actual sequence:

```text
1 → 2 → 3 → 4
```

is scattered throughout the array.

We can use a **HashSet** to get `O(1)` average-time lookup.

---

## 🧠 Main Idea

Put every element into a `HashSet`.

```text
nums = [100,4,200,1,3,2]

Set = {
    100,
    4,
    200,
    1,
    3,
    2
}
```

Now we can quickly check whether:

```text
x + 1
```

exists.

---

## ⭐ Important Trick

We should only start building a sequence when `x` is the **beginning** of a sequence.

How do we know?

Check whether:

```text
x - 1
```

exists.

### If `x - 1` exists:

```text
x
```

is NOT the beginning.

Example:

```text
1, 2, 3, 4
```

For `2`:

```text
2 - 1 = 1
```

`1` exists.

Therefore, don't start from `2`.

---

### If `x - 1` does NOT exist:

`x` is the beginning of a sequence.

Example:

```text
1,2,3,4
```

For `1`:

```text
1 - 1 = 0
```

`0` does not exist.

Therefore:

```text
1 = start
```

Now check:

```text
2
3
4
5
```

until the sequence ends.

---

# 🔄 Algorithm

For every element `x`:

### Step 1

Check:

```text
if (!set.contains(x - 1))
```

This means `x` is the beginning of a sequence.

### Step 2

Start:

```text
current = x
count = 1
```

### Step 3

Keep checking:

```text
current + 1
```

If it exists:

```text
current++
count++
```

### Step 4

Update the maximum:

```text
longest = Math.max(longest, count)
```

---

## 🧪 Dry Run

```text
nums = [100,4,200,1,3,2]
```

Set:

```text
{100, 4, 200, 1, 3, 2}
```

### x = 100

Check:

```text
99
```

Not present.

So `100` is a sequence start.

```text
100 → 101
```

101 doesn't exist.

```text
count = 1
```

---

### x = 4

Check:

```text
3
```

3 exists.

So `4` is not a starting point.

Skip it.

---

### x = 200

Check:

```text
199
```

Not present.

Start sequence:

```text
200
```

No `201`.

```text
count = 1
```

---

### x = 1

Check:

```text
0
```

Not present.

Start:

```text
1
```

Check:

```text
2 ✓
3 ✓
4 ✓
5 ✗
```

Therefore:

```text
count = 4
```

Update:

```text
longest = 4
```

---

### Final Answer

```text
4
```

---

# 💻 Java Solution

```java
class Solution {

    public int longestConsecutive(int[] nums) {

        int n = nums.length;

        if (n == 0) {
            return 0;
        }

        int longest = 1;

        Set<Integer> st = new HashSet<>();

        // Store all elements in HashSet
        for (int i = 0; i < n; i++) {
            st.add(nums[i]);
        }

        // Find the beginning of every sequence
        for (int x : st) {

            // x is the start of a sequence
            if (!st.contains(x - 1)) {

                int cnt = 1;
                int current = x;

                // Build the consecutive sequence
                while (st.contains(current + 1)) {

                    current = current + 1;
                    cnt = cnt + 1;
                }

                longest = Math.max(longest, cnt);
            }
        }

        return longest;
    }
}
```

---

# 🆚 Another Approach — Sorting

A simpler approach is to sort the array first.

Example:

```text
[100,4,200,1,3,2]
```

After sorting:

```text
[1,2,3,4,100,200]
```

Now consecutive elements are next to each other.

We can traverse the sorted array and count consecutive values.

### Complexity

```text
Time  → O(n log n)
Space → O(1) / depends on sorting implementation
```

---

# 🏆 Which Approach Is Better?

| Approach | Time | Extra Space | Best For |
|---|---:|---:|---|
| Sorting | `O(n log n)` | `O(1)`* | Simpler solution |
| HashSet | `O(n)` average | `O(n)` | Optimal time |

### 🥇 Optimal → HashSet

The problem specifically asks for:

```text
O(n)
```

time.

Therefore, **HashSet is the preferred solution**.

The key idea is:

```text
Only start counting from numbers where x - 1 does not exist.
```

This prevents repeatedly scanning the same sequence.

---

# ⏱️ Complexity Analysis

## Time Complexity

```text
O(n)
```

### Why?

First:

```text
Insert n elements → O(n)
```

Then:

```text
Traverse the HashSet → O(n)
```

The consecutive sequence is only expanded from numbers that are **sequence starts**.

Therefore, the overall average complexity is:

```text
O(n)
```

---

## Space Complexity

```text
O(n)
```

The `HashSet` stores the elements.

---

## 🌟 Key Points

- Use a `HashSet` for fast lookup.
- Do **not** start a sequence from every element.
- A number `x` is a sequence start only when:

```text
x - 1 does not exist
```

- Then keep checking:

```text
x + 1
x + 2
x + 3
...
```

- Duplicate elements do not affect the result because `HashSet` stores unique values.
- This gives average `O(n)` time.
- This is the optimal approach for the required complexity.

---

## ⚠️ Common Mistakes

- Sorting when the interviewer specifically asks for `O(n)`.
- Starting a sequence from every number.
- Forgetting to check `x - 1`.
- Using the original array for repeated searches, which can lead to `O(n²)`.
- Forgetting to handle an empty array.
- Counting duplicate elements as part of the sequence.
- Assuming the array itself must be sorted.

---

## 🎯 Interview Tip

If the interviewer says:

> "The array is unsorted and I want O(n) time."

Immediately think:

```text
HashSet
```

Then remember the pattern:

```text
Is x - 1 present?
       ↓
   YES → skip
       ↓
   NO → sequence starts here
       ↓
Check x + 1, x + 2, x + 3...
```

### 🔑 One-line memory trick

```text
"Only start counting from the beginning of a sequence."
```
