# 🔄 Rotate String

## 🔗 Problem Link

<a href="https://leetcode.com/problems/rotate-string/" target="_blank">
LeetCode 796: Rotate String
</a>

---

## 🏷️ Tags

- String
- Simulation
- String Manipulation

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given two strings `s` and `goal`, return `true` if and only if `s` can become `goal` after some number of shifts on `s`.

A shift moves the **leftmost character** of `s` to the **rightmost position**.

For example:

```text
s = "abcde"

After one shift:
"bcdea"

After two shifts:
"cdeab"
```

---

## ✨ Examples

### Example 1

```text
Input:
s = "abcde"
goal = "cdeab"

Output:
true
```

Explanation:

```text
abcde
 ↓
bcdea
 ↓
cdeab
```

So `s` can become `goal`.

---

### Example 2

```text
Input:
s = "abcde"
goal = "abced"

Output:
false
```

Explanation:

No sequence of rotations of `s` can produce `goal`.

---

## 🚀 Approach

Use **Simulation**.

The idea is to repeatedly rotate the string and check whether it becomes `goal`.

### Step 1 — Check Lengths

If the lengths are different, they can never be rotations of each other.

```java
if (s.length() != goal.length()) {
    return false;
}
```

---

### Step 2 — Store the Current Rotation

Start with:

```java
String current = s;
```

---

### Step 3 — Try Every Rotation

A string of length `n` can have at most `n` unique rotations.

So loop:

```java
for (int i = 0; i < s.length(); i++)
```

At every iteration, first check:

```java
if (current.equals(goal)) {
    return true;
}
```

If they match, `goal` is a valid rotation.

---

### Step 4 — Perform One Left Rotation

A left rotation moves the first character to the end.

For example:

```text
abcde
```

becomes:

```text
bcdea
```

We can do this using:

```java
current.substring(1) + current.charAt(0)
```

So:

```java
current = current.substring(1) + current.charAt(0);
```

---

### Step 5 — No Match

If all rotations are checked and none matches:

```java
return false;
```

---

## 🧠 Dry Run

For:

```text
s = "abcde"
goal = "cdeab"
```

### Rotation 1

```text
current = "abcde"
```

Not equal.

Rotate:

```text
"bcdea"
```

### Rotation 2

```text
current = "bcdea"
```

Not equal.

Rotate:

```text
"cdeab"
```

### Rotation 3

```text
current = "cdeab"
```

Now:

```text
current.equals(goal)
```

is `true`.

Return:

```text
true
```

---

## 💻 Java Solution

```java
class Solution {
    public boolean rotateString(String s, String goal) {

        if (s.length() != goal.length()) {
            return false;
        }

        String current = s;

        for (int i = 0; i < s.length(); i++) {

            if (current.equals(goal)) {
                return true;
            }

            current = current.substring(1) + current.charAt(0);
        }

        return false;
    }
}
```

---

## ⏱️ Complexity Analysis

### Time Complexity

```text
O(n²)
```

There can be `n` rotations.

Each rotation creates a new string of length `n`.

Therefore:

```text
n × n = O(n²)
```

### Space Complexity

```text
O(n)
```

The rotated string requires `O(n)` space.

---

## 🔒 Constraints

- `1 <= s.length, goal.length <= 100`
- `s` and `goal` consist of lowercase English letters.

---

## 🌟 Key Points

- First check whether both strings have the same length.
- A string of length `n` has at most `n` rotations.
- Check the current string before rotating.
- One left rotation is:
  ```java
  current.substring(1) + current.charAt(0)
  ```
- If any rotation equals `goal`, return `true`.
- If no rotation matches, return `false`.

---

## ⚠️ Common Mistakes

- Forgetting to check the string before performing the rotation.
- Not checking whether the lengths are equal.
- Rotating in the wrong direction.
- Forgetting to move the first character to the end.
- Running more than `n` rotations unnecessarily.
- Comparing strings using `==` instead of `.equals()` in Java.

---

## 🎯 Interview Tip

> **Rotate String = Keep rotating left and check if it becomes the goal.**

```text
abcde
 ↓
bcdea
 ↓
cdeab
 ↓
deabc
 ↓
eabcd
```

At every step:

```text
current.equals(goal)
```

If yes → `true`  
After all rotations → `false`
