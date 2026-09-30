# 🔢 Count Primes

## 🔗 Problem Link

<a href="https://leetcode.com/problems/count-primes/" target="_blank">
LeetCode 204: Count Primes
</a>

---

## 🏷️ Tags

- Maths
- Prime Numbers
- Sieve of Eratosthenes
- Array

---

## 📊 Difficulty

Medium

---

## Problem Statement

Given an integer `n`, return the number of prime numbers that are **strictly less than `n`**.

For example:

```text
n = 10

Prime numbers less than 10:
2, 3, 5, 7

Answer = 4
```

---

## ✨ Examples

### Example 1

```text
Input:
n = 10

Output:
4
```

Explanation:

```text
2, 3, 5, 7
```

There are `4` prime numbers less than `10`.

---

### Example 2

```text
Input:
n = 0

Output:
0
```

---

### Example 3

```text
Input:
n = 1

Output:
0
```

---

## 🚀 Approach

Use the **Sieve of Eratosthenes**.

The main idea is:

> Start with all numbers as possible primes and eliminate the numbers that are definitely composite.

### Step 1 — Handle Small Values

If:

```text
n <= 2
```

there are no prime numbers less than `n`.

```java
if (n <= 2) return 0;
```

---

### Step 2 — Create a Marking Array

```java
byte[] s = new byte[n];
```

Each index represents a number.

```text
index → number
0     → 0
1     → 1
2     → 2
3     → 3
...
```

Initially every value is `0`.

We use:

```text
0 → not marked as composite
1 → composite
```

---

### Step 3 — Initially Count All Possible Primes

Numbers `2` to `n - 1` are initially considered possible primes.

So:

```java
int cnt = n - 2;
```

We start with `n - 2` numbers.

---

### Step 4 — Find Composite Numbers

Start from:

```java
i = 2
```

and continue while:

```java
i * i < n
```

If:

```java
s[i] == 0
```

then `i` has not been marked composite, so `i` is prime.

Now eliminate its multiples.

---

### Step 5 — Mark Multiples

Start from:

```java
i * i
```

and move by `i`:

```java
for (int j = i * i; j < n; j += i)
```

Why `i * i`?

Because smaller multiples have already been handled by smaller prime numbers.

Example for `i = 2`:

```text
4, 6, 8, 10, 12...
```

For `i = 3`:

```text
9, 12, 15, 18...
```

---

### Step 6 — Decrease the Count

When we find an unmarked number:

```java
if (s[j] == 0)
```

mark it:

```java
s[j] = 1;
```

and remove it from our prime count:

```java
cnt--;
```

This ensures every composite number is counted only once.

---

## 🧠 Example

For:

```text
n = 10
```

Initially:

```text
2 3 4 5 6 7 8 9
```

Count:

```text
8
```

### Start with 2

Mark multiples of `2`:

```text
4, 6, 8
```

Remaining possible primes:

```text
2 3 5 7 9
```

Count:

```text
5
```

### Next prime: 3

Mark:

```text
9
```

Remaining:

```text
2 3 5 7
```

Count:

```text
4
```

Answer:

```text
4
```

---

## 💻 Java Solution

```java
class Solution {
    public int countPrimes(int n) {
        if (n <= 2) return 0;

        int cnt = n - 2;
        byte[] s = new byte[n];

        for (int i = 2; i * i < n; i++) {

            if (s[i] == 0) {

                for (int j = i * i; j < n; j += i) {

                    if (s[j] == 0) {
                        s[j] = 1;
                        cnt--;
                    }
                }
            }
        }

        return cnt;
    }
}
```

---

## ⏱️ Complexity Analysis

### Time Complexity

```text
O(n log log n)
```

This is the standard complexity of the Sieve of Eratosthenes.

### Space Complexity

```text
O(n)
```

The `byte[]` array stores information for every number from `0` to `n - 1`.

---

## 🔒 Constraints

```text
0 <= n <= 5 * 10⁶
```

---

## 🌟 Key Points

- Use the **Sieve of Eratosthenes**.
- Start by assuming numbers `2` to `n - 1` are prime.
- Mark composite numbers as `1`.
- Start marking multiples from:
  ```text
  i * i
  ```
- Move through multiples using:
  ```text
  j += i
  ```
- Only process `i` when it is still unmarked.
- `cnt` starts with all numbers from `2` to `n - 1`.
- Every time a composite is marked for the first time, decrement `cnt`.

---

## ⚠️ Common Mistakes

- Starting the marking loop from `i` instead of `i * i`.
- Forgetting:
  ```text
  j += i
  ```
- Marking the prime number itself as composite.
- Counting numbers from `0` or `1` as primes.
- Forgetting the `n <= 2` case.
- Decreasing `cnt` multiple times for the same composite.
- Confusing:
  ```text
  i * i < n
  ```
  with:
  ```text
  i < n
  ```

---

## 🎯 Interview Tip

> **Sieve = Assume prime → Find prime → Mark all its multiples as composite.**

```text
2 → mark multiples
3 → mark multiples
5 → mark multiples
...
```

The key pattern to remember:

```text
Start = i * i
Step  = i
```
