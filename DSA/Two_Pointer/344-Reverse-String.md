# 🔄 Reverse String

## 🔗 Problem Link

<a href="https://leetcode.com/problems/reverse-string/" target="_blank">
LeetCode 344: Reverse String
</a>

---

## 🏷️ Tags

- String
- Two Pointers
- Recursion
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

# 🚀 Approach 1 — Two Pointers

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

### Step 3 — Move Pointers

After swapping:

```java
i++;
j--;
```

Both pointers move toward the center.

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

Continue until:

```text
i >= j
```

The string is completely reversed.

---

## 💻 Java Solution — Two Pointers

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

# 🚀 Approach 2 — Recursion

Use **Recursion + Two Pointers**.

The logic is almost the same as the two-pointer approach.

The difference is:

> Instead of using a `while` loop to move toward the center, we use recursive calls.

We pass:

```text
left  → beginning of the current range
right → end of the current range
```

### Step 1 — Create a Recursive Helper

```java
private void reverse(char[] s, int left, int right)
```

The helper function reverses the portion:

```text
left ... right
```

### Step 2 — Base Case

Stop when:

```java
left >= right
```

Why?

Because the pointers have met or crossed, meaning the remaining portion is already reversed.

```java
if (left >= right) {
    return;
}
```

### Step 3 — Swap

Swap the characters at `left` and `right`.

```java
char temp = s[left];
s[left] = s[right];
s[right] = temp;
```

### Step 4 — Recursive Call

Move both pointers toward the center:

```java
reverse(s, left + 1, right - 1);
```

This repeats the same process for the smaller inner portion.

### 🧠 Example

For:

```text
["h", "e", "l", "l", "o"]
```

First call:

```text
left = 0
right = 4
```

Swap:

```text
h ↔ o
```

Array:

```text
["o", "e", "l", "l", "h"]
```

Recursive call:

```text
reverse(s, 1, 3)
```

Swap:

```text
e ↔ l
```

Array:

```text
["o", "l", "l", "e", "h"]
```

Recursive call:

```text
reverse(s, 2, 2)
```

Now:

```text
left >= right
```

Stop.

Final:

```text
["o", "l", "l", "e", "h"]
```

---

## 💻 Java Solution — Recursion

```java
class Solution {
    public void reverseString(char[] s) {
        reverse(s, 0, s.length - 1);
    }

    private void reverse(char[] s, int left, int right) {

        if (left >= right) {
            return;
        }

        char temp = s[left];
        s[left] = s[right];
        s[right] = temp;

        reverse(s, left + 1, right - 1);
    }
}
```

---

## ⏱️ Complexity Analysis

### Two Pointer

**Time Complexity:**

```text
O(n)
```

Each character is processed at most once.

**Space Complexity:**

```text
O(1)
```

Only a temporary variable is used.

---

### Recursion

**Time Complexity:**

```text
O(n)
```

Each recursive call processes one pair of characters.

**Space Complexity:**

```text
O(n)
```

Because of the recursive call stack.

More precisely:

```text
O(n / 2) = O(n)
```

---

## 🔒 Constraints

- `1 <= s.length <= 10⁵`
- `s[i]` is a printable ASCII character.

---

## 🌟 Key Points

### Two Pointer

- Start `left` from `0`.
- Start `right` from `n - 1`.
- Swap both characters.
- Move:
  ```text
  left++
  right--
  ```
- Stop when:
  ```text
  left >= right
  ```

### Recursion

- Same swapping logic.
- Use a helper function.
- Base case:
  ```text
  left >= right
  ```
- Recursive step:
  ```text
  left + 1
  right - 1
  ```
- Recursion uses extra call-stack space.

---

## ⚠️ Common Mistakes

- Using `left > right` instead of `left >= right`.
- Forgetting to move both pointers.
- Forgetting the recursive call.
- Calling recursion with the same `left` and `right`.
- Forgetting that recursion uses stack space.
- Creating another array unnecessarily.

---

## 🎯 Interview Tip

> **Both approaches use the same core idea: Swap the outside characters and move toward the center.**

```text
Two Pointer:
while → swap → move

Recursion:
base case → swap → recursive call
```

### Easy Memory Trick

```text
Reverse = Swap Outside → Move Inside
```
