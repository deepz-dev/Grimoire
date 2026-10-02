# 🔢 Perfect Number

## 🔗 Problem Link

<a href="https://leetcode.com/problems/perfect-number/" target="_blank">
LeetCode 507: Perfect Number
</a>

---

## 🏷️ Tags

- Maths
- Number Theory
- Divisors
- Basic Maths

---

## 📊 Difficulty

Easy

---

## Problem Statement

A **perfect number** is a positive integer that is equal to the sum of its positive divisors, excluding the number itself.

For example:

```text
28 = 1 + 2 + 4 + 7 + 14
```

Therefore, `28` is a perfect number.

---

## ✨ Examples

### Example 1

```text
Input:
num = 28

Output:
true
```

Explanation:

```text
1 + 2 + 4 + 7 + 14 = 28
```

---

### Example 2

```text
Input:
num = 7

Output:
false
```

Explanation:

The only positive divisor of `7` excluding `7` itself is:

```text
1
```

Since:

```text
1 != 7
```

`7` is not a perfect number.

---

## 🚀 Approach

Use **Divisor Pairing**.

Instead of checking every number from `1` to `num - 1`, we only check up to:

```text
√num
```

### Step 1 — Handle Small Numbers

If:

```text
num <= 1
```

return `false`.

```java
if (num <= 1) {
    return false;
}
```

---

### Step 2 — Start the Sum With 1

For every number greater than `1`, `1` is always a proper divisor.

So:

```java
int sum = 1;
```

---

### Step 3 — Find Divisor Pairs

Loop from:

```text
2 → √num
```

using:

```java
for (int i = 2; i * i <= num; i++)
```

If:

```java
num % i == 0
```

then `i` is a divisor.

But every divisor has a corresponding pair:

```text
i × (num / i) = num
```

So we can add both:

```java
i + (num / i)
```

---

### Step 4 — Handle Perfect Square

If:

```text
i * i == num
```

then:

```text
i == num / i
```

So we must add `i` only once.

```java
if (i * i == num) {
    sum += i;
}
```

Otherwise:

```java
sum += i + (num / i);
```

---

### Step 5 — Compare the Sum

Finally:

```java
return sum == num;
```

If the sum of all proper divisors equals the original number, it is a perfect number.

---

## 🧠 Dry Run

For:

```text
num = 28
```

Initially:

```text
sum = 1
```

Check divisors up to:

```text
√28 ≈ 5
```

### `i = 2`

```text
28 % 2 == 0
```

Divisor pair:

```text
2 × 14 = 28
```

Add:

```text
sum = 1 + 2 + 14
    = 17
```

### `i = 3`

```text
28 % 3 != 0
```

Nothing added.

### `i = 4`

```text
28 % 4 == 0
```

Divisor pair:

```text
4 × 7 = 28
```

Add:

```text
sum = 17 + 4 + 7
    = 28
```

Now:

```text
sum == num
28 == 28
```

Therefore:

```text
true
```

---

## 💻 Java Solution

```java
class Solution {
    public boolean checkPerfectNumber(int num) {

        // Numbers <= 1 cannot be perfect numbers
        if (num <= 1) {
            return false;
        }

        // 1 is always a proper divisor
        int sum = 1;

        // Check divisors only up to sqrt(num)
        for (int i = 2; i * i <= num; i++) {

            if (num % i == 0) {

                // Perfect square: add divisor only once
                if (i * i == num) {
                    sum += i;
                } else {
                    // Add both divisors in the pair
                    sum += i + (num / i);
                }
            }
        }

        return sum == num;
    }
}
```

---

## ⏱️ Complexity Analysis

### Time Complexity

```text
O(√n)
```

We only check possible divisors up to `√n`.

### Space Complexity

```text
O(1)
```

Only a few variables are used.

---

## 🔒 Constraints

```text
1 <= num <= 10⁸
```

---

## 🌟 Key Points

- A perfect number equals the sum of its **proper divisors**.
- `1` is always included as a proper divisor.
- Check divisors only up to:
  ```text
  √num
  ```
- Every divisor has a paired divisor:
  ```text
  i × (num / i) = num
  ```
- For perfect squares, don't add the square-root divisor twice.
- Final condition:
  ```text
  sum == num
  ```

---

## ⚠️ Common Mistakes

- Including `num` itself in the divisor sum.
- Checking all numbers from `1` to `num - 1`.
- Forgetting to add `1`.
- Adding the square-root divisor twice for perfect squares.
- Forgetting the `num <= 1` case.
- Confusing:
  ```text
  divisor pair → i and num / i
  ```

---

## 🎯 Interview Tip

> **Divisor found? Think in pairs. Check only till √n.**

```text
i divides num
      ↓
i × (num / i) = num
      ↓
add both divisors
```

For perfect square:

```text
i == num / i
```

so add it only once.
