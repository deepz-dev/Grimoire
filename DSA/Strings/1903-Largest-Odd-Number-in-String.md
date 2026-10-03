# 🔢 Largest Odd Number in String

## 🔗 Problem Link

<a href="https://leetcode.com/problems/largest-odd-number-in-string/" target="_blank">
LeetCode 1903: Largest Odd Number in String
</a>

---

## 🏷️ Tags

- String
- Greedy
- Two Pointers
- Substring

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given a string `num` representing a large integer, return the **largest-valued odd integer** as a string that is a non-empty substring of `num`.

If no odd integer exists, return:

```text
""
```

A substring is a contiguous sequence of characters within a string.

---

## ✨ Examples

### Example 1

```text
Input:
num = "52"

Output:
"5"
```

Explanation:

The odd digit is `5`, so the largest odd substring is:

```text
"5"
```

---

### Example 2

```text
Input:
num = "4206"

Output:
""
```

Explanation:

There are no odd digits in the string.

---

### Example 3

```text
Input:
num = "35427"

Output:
"35427"
```

Explanation:

The number already ends with an odd digit, so the complete string is odd.

---

## 🚀 Approach

Use a **Greedy approach**.

### 🧠 Main Idea

For a number to be odd, its **last digit must be odd**.

So we only need to find the **rightmost odd digit**.

Why the rightmost?

Because we want the **largest-valued substring**.

A substring ending at a later position contains more digits, making it larger.

---

### Step 1 — Traverse From Right to Left

Start from the last digit:

```java
for (int i = num.length() - 1; i >= 0; i--)
```

We check digits from right to left.

---

### Step 2 — Convert Character to Digit

The string contains characters, so convert the current character into an integer:

```java
int digit = num.charAt(i) - '0';
```

For example:

```text
'7' - '0' = 7
```

---

### Step 3 — Find the Rightmost Odd Digit

Check:

```java
if (digit % 2 != 0)
```

If it is odd, return everything from the beginning up to this digit:

```java
return num.substring(0, i + 1);
```

---

### Step 4 — No Odd Digit

If the loop finishes without finding an odd digit:

```java
return "";
```

---

## 🧠 Dry Run

For:

```text
num = "35427"
```

Start from the right:

```text
7 → odd
```

So immediately return:

```text
"35427"
```

---

### Another Example

```text
num = "4206"
```

Check from right:

```text
6 → even
0 → even
2 → even
4 → even
```

No odd digit exists.

Return:

```text
""
```

---

## 💻 Java Solution

```java
class Solution {
    public String largestOddNumber(String num) {

        for (int i = num.length() - 1; i >= 0; i--) {

            int digit = num.charAt(i) - '0';

            if (digit % 2 != 0) {
                return num.substring(0, i + 1);
            }
        }

        return "";
    }
}
```

---

## ⏱️ Complexity Analysis

### Time Complexity

```text
O(n)
```

In the worst case, we scan the entire string.

### Space Complexity

```text
O(n)
```

The returned substring can contain up to `n` characters.

Apart from the returned result, the algorithm uses:

```text
O(1)
```

extra space.

---

## 🔒 Constraints

- `1 <= num.length <= 10⁵`
- `num` consists only of digits.
- `num` does not contain leading zeros.

---

## 🌟 Key Points

- An integer is odd if its **last digit is odd**.
- Start searching from the **right side**.
- Find the **rightmost odd digit**.
- Return the substring from index `0` to that digit.
- If there is no odd digit, return:
  ```text
  ""
  ```
- This is a **Greedy** approach because we immediately choose the rightmost possible ending position.

---

## ⚠️ Common Mistakes

- Searching from left to right.
- Returning only the odd digit instead of the complete substring.
- Forgetting `i + 1` in:
  ```java
  num.substring(0, i + 1)
  ```
- Checking whether the whole string is odd instead of finding the rightmost odd digit.
- Returning `"0"` when no odd digit exists.
- Forgetting that `num` is a string because the number can be very large.

---

## 🎯 Interview Tip

> **Largest odd substring → Find the rightmost odd digit and cut there.**

```text
Start ← ← ← ← Right

Find odd digit
      ↓
Return num[0 ... i]
```

The key condition:

```text
digit % 2 != 0
```
