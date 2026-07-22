# 🔢 Palindrome Number

## 🔗 Problem Link

LeetCode 9: Palindrome Number

---

## 🏷️ Tags

- Math

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given an integer `x`, return `true` if `x` is a palindrome, and `false` otherwise.

A palindrome number reads the same from left to right and from right to left.

> **Note:** Solve the problem without converting the integer into a string.

---

## ✨ Examples

### Example 1

**Input**

```text
x = 121
```

**Output**

```text
true
```

**Explanation**

The number `121` reads the same forward and backward.

---

### Example 2

**Input**

```text
x = -121
```

**Output**

```text
false
```

**Explanation**

From left to right, it reads `-121`. From right to left, it becomes `121-`, so it is not a palindrome.

---

### Example 3

**Input**

```text
x = 10
```

**Output**

```text
false
```

**Explanation**

Reversing `10` gives `01`, which is not equal to `10`.

---

## 🚀 Approach

The idea is to reverse the given number and compare it with the original number.

1. Store the original number in a temporary variable.
2. Extract the last digit using `% 10`.
3. Build the reversed number by multiplying the current reverse by `10` and adding the extracted digit.
4. Remove the last digit from the original number using `/ 10`.
5. Repeat until the number becomes `0`.
6. Compare the reversed number with the original copy.
   - If both are equal, return `true`.
   - Otherwise, return `false`.

---

## 💻 Java Solution

```java
class Solution {
    public boolean isPalindrome(int x) {

        int reverse = 0;
        int copy = x;

        while (x > 0) {

            int ld = x % 10;
            reverse = (reverse * 10) + ld;
            x = x / 10;
        }

        return copy == reverse;
    }
}
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(log₁₀ n)`

- Each digit is processed exactly once.

**Space Complexity:** `O(1)`

- Only a few integer variables are used.

---

## 🔒 Constraints

- `-2³¹ ≤ x ≤ 2³¹ - 1`

---

## 🌟 Key Points

- Does not convert the number into a string.
- Reverses the number mathematically using modulo and division.
- Constant extra space.
- Efficient solution for checking numeric palindromes.

---

## ⚠️ Common Mistakes

- Forgetting that negative numbers are never palindromes.
- Ignoring integer overflow while reversing very large numbers.
- Converting the integer to a string when the follow-up asks not to.
- Not preserving the original number before modifying it.