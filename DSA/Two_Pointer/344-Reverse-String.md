# 🔄 Reverse String

## 🔗 Problem Link

<a href="https://leetcode.com/problems/reverse-string/" target="_blank">
LeetCode 344: Reverse String
</a>

---

## 🏷️ Tags

- String
- Two Pointers
- In-Place
- Array

---

## 📊 Difficulty

Easy

---

## Problem Statement

Write a function that reverses a string.

The input string is given as an array of characters `s`.

The string must be reversed **in-place** using:

```text
O(1)
```

extra memory.

---

## ✨ Examples

### Example 1

```text
Input:
s = ["h","e","l","l","o"]

Output:
["o","l","l","e","h"]
```

### Example 2

```text
Input:
s = ["H","a","n","n","a","h"]

Output:
["h","a","n","n","a","H"]
```

---

## 🚀 Approach

Use the **Two Pointer** approach.

We maintain two pointers:

```text
i → points to the beginning
j → points to the end
```

### Step 1 — Initialize Pointers

```java
int i = 0;
int j = s.length - 1;
```

---

### Step 2 — Swap Characters

While:

```text
i < j
```

swap the characters at `i` and `j`.

```java
char temp = s[i];
s[i] = s[j];
s[j] = temp;
```

---

### Step 3 — Move Pointers

After swapping:

```java
i++;
j--;
```

So both pointers move toward the center.

---

### 🧠 Example

For:

```text
["h", "e", "l", "l", "o"]
```

First:

```text
i = 0 → h
j = 4 → o
```

Swap:

```text
["o", "e", "l", "l", "h"]
```

Move:

```text
i++
j--
```

Next:

```text
e ↔ l
```

Continue until:

```text
i >= j
```

At that point, the string is completely reversed.

---

## 💻 Java Solution

```java
class Solution {
    public void reverseString(char[] s) {

        int i = 0;
        int j = s.length - 1;

        while (i < j) {

            char temp = s[i];
            s[i] = s[j];
            s[j] = temp;

            i++;
            j--;
        }
    }
}
```

---

## ⏱️ Complexity Analysis

### Time Complexity

```text
O(n)
```

Each character is processed at most once.

### Space Complexity

```text
O(1)
```

Only one temporary variable is used for swapping.

---

## 🔒 Constraints

- `1 <= s.length <= 10⁵`
- `s[i]` is a printable ASCII character.

---

## 🌟 Key Points

- Use **two pointers**.
- One pointer starts from the left.
- One pointer starts from the right.
- Swap the characters.
- Move both pointers toward the center.
- Stop when:
  ```text
  i >= j
  ```
- The array is modified **in-place**.
- No extra array is required.

---

## ⚠️ Common Mistakes

- Using `i <= j` instead of `i < j`.
- Forgetting to increment `i`.
- Forgetting to decrement `j`.
- Creating another array unnecessarily.
- Returning the array even though the method is `void`.
- Confusing `s.length` with `s.length - 1` for the last index.

---

## 🎯 Interview Tip

> **Reverse an array/string in-place → Two pointers + Swap.**

```text
i →        ← j

Swap
 ↓
i++       j--
 ↓
Repeat until i >= j
```
