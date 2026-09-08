# 🔢 Fibonacci Number

## 🔗 Problem Link

<a href="https://leetcode.com/problems/fibonacci-number/description/" target="_blank">
LeetCode 509: Fibonacci Number
</a>

---

## 🏷️ Tags

- Recursion
- Maths
- Dynamic Programming

---

## 📊 Difficulty

Easy

---

## Problem Statement

The **Fibonacci sequence** is a sequence where each number is the sum of the two preceding numbers.

The sequence starts with:

```text
F(0) = 0
F(1) = 1
```

For `n > 1`:

```text
F(n) = F(n - 1) + F(n - 2)
```

Given `n`, return `F(n)`.

---

## ✨ Examples

### Example 1

```text
Input:
n = 2

Output:
1
```

Explanation:

```text
F(2) = F(1) + F(0)
     = 1 + 0
     = 1
```

### Example 2

```text
Input:
n = 3

Output:
2
```

Explanation:

```text
F(3) = F(2) + F(1)
     = 1 + 1
     = 2
```

### Example 3

```text
Input:
n = 4

Output:
3
```

Explanation:

```text
F(4) = F(3) + F(2)
     = 2 + 1
     = 3
```

---

## 🚀 Approach

Use **Recursion**.

The Fibonacci definition itself gives the recursive relation:

```text
F(n) = F(n - 1) + F(n - 2)
```

### Step 1 — Base Case

If:

```text
n <= 1
```

return `n`.

```java
if (n <= 1) {
    return n;
}
```

This handles:

```text
F(0) = 0
F(1) = 1
```

### Step 2 — Calculate Previous Two Terms

For every `n > 1`, calculate:

```text
F(n - 1)
F(n - 2)
```

using recursion.

```java
int last = fib(n - 1);
int slast = fib(n - 2);
```

Here:

```text
last  → F(n - 1)
slast → F(n - 2)
```

### Step 3 — Add Them

Return:

```java
return last + slast;
```

Because:

```text
F(n) = F(n - 1) + F(n - 2)
```

---

## 🧠 Recursion Tree

For:

```text
fib(4)
```

the calls look like:

```text
                fib(4)
               /      \
          fib(3)      fib(2)
          /   \        /   \
      fib(2) fib(1) fib(1) fib(0)
      /   \
  fib(1) fib(0)
```

The same values are calculated multiple times.

For example:

```text
fib(2)
```

is calculated more than once.

This repeated calculation makes the recursive solution inefficient for larger `n`.

---

## 💻 Java Solution

```java
class Solution {
    public int fib(int n) {

        // Base case
        if (n <= 1) {
            return n;
        }

        // Calculate previous two terms
        int last = fib(n - 1);
        int slast = fib(n - 2);

        // Fibonacci relation
        return last + slast;
    }
}
```

---

## ⏱️ Complexity Analysis

### Time Complexity

```text
O(2^n)
```

Each recursive call creates two more recursive calls, causing repeated calculations.

### Space Complexity

```text
O(n)
```

The maximum depth of the recursion call stack is `n`.

---

## 🔒 Constraints

```text
0 <= n <= 30
```

---

## 🌟 Key Points

- Fibonacci starts with:
  ```text
  F(0) = 0
  F(1) = 1
  ```
- The recursive formula is:
  ```text
  F(n) = F(n - 1) + F(n - 2)
  ```
- `n <= 1` is the base case.
- Every recursive call calculates the previous two Fibonacci numbers.
- Simple recursive Fibonacci has **overlapping subproblems**.
- The same values are calculated repeatedly.
- This makes the recursive solution `O(2^n)`.

---

## ⚠️ Common Mistakes

- Forgetting the base case.
- Using the wrong base case:
  ```text
  F(0) = 0
  F(1) = 1
  ```
- Writing only `fib(n - 1)` and forgetting `fib(n - 2)`.
- Forgetting to return the sum.
- Confusing `n - 1` and `n - 2`.
- Not understanding that recursive calls create a tree of function calls.

---

## 🎯 Interview Tip

> **Fibonacci recursion = Base Case + Previous Two Terms + Add**

```text
fib(n)
   ↓
fib(n-1) + fib(n-2)
   ↓
repeat until n <= 1
```

For optimization:

```text
Recursive → O(2^n)
Memoization → O(n)
Tabulation → O(n)
Space Optimized → O(1)
```
