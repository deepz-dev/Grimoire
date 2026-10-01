# 🔤 First Unique Character in a String

## 🔗 Problem Link

<a href="https://leetcode.com/problems/first-unique-character-in-a-string/" target="_blank">
LeetCode 387: First Unique Character in a String
</a>

---

## 🏷️ Tags

- String
- Hashing
- Frequency Counting
- Brute Force

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given a string `s`, find the **first non-repeating character** in it and return its index.

If no unique character exists, return:

```text
-1
```

---

## ✨ Examples

### Example 1

```text
Input:
s = "leetcode"

Output:
0
```

Explanation:

```text
'l' occurs only once.

Index of 'l' = 0
```

So the answer is:

```text
0
```

---

### Example 2

```text
Input:
s = "loveleetcode"

Output:
2
```

Explanation:

```text
'l' → repeated
'o' → repeated
'v' → occurs once
```

The index of `'v'` is:

```text
2
```

---

### Example 3

```text
Input:
s = "aabb"

Output:
-1
```

Explanation:

```text
'a' → repeated
'b' → repeated
```

There is no unique character.

---

## 🚀 Approach

Use **Brute Force**.

The idea is to check every character and count how many times it appears in the string.

### Step 1 — Traverse Each Character

Use the outer loop:

```java
for (int i = 0; i < s.length(); i++)
```

This checks every character from left to right.

---

### Step 2 — Count Its Occurrences

For every character at index `i`, use another loop to compare it with every character in the string.

```java
int count = 0;

for (int j = 0; j < s.length(); j++) {
    if (s.charAt(i) == s.charAt(j)) {
        count++;
    }
}
```

If the characters are equal, increase the count.

---

### Step 3 — Check If It Is Unique

After counting:

```java
if (count == 1)
```

the character occurs only once.

Because we are traversing from left to right, the **first character with count `1`** is automatically the first unique character.

So return:

```java
return i;
```

---

### Step 4 — No Unique Character

If the complete string is checked and no character has a frequency of `1`:

```java
return -1;
```

---

## 🧠 Dry Run

For:

```text
s = "loveleetcode"
```

Start from index `0`:

```text
l → repeated
o → repeated
v → unique
```

When we reach:

```text
index = 2
character = 'v'
count = 1
```

we immediately return:

```text
2
```

---

## 💻 Java Solution

```java
class Solution {
    public int firstUniqChar(String s) {

        for (int i = 0; i < s.length(); i++) {

            int count = 0;

            for (int j = 0; j < s.length(); j++) {

                if (s.charAt(i) == s.charAt(j)) {
                    count++;
                }
            }

            if (count == 1) {
                return i;
            }
        }

        return -1;
    }
}
```

---

## ⏱️ Complexity Analysis

### Time Complexity

```text
O(n²)
```

For every character, we traverse the entire string to count its occurrences.

### Space Complexity

```text
O(1)
```

Only the `count` variable and loop variables are used.

---

## 🔒 Constraints

- `1 <= s.length <= 10⁵`
- `s` consists of only lowercase English letters.

---

## 🌟 Key Points

- Check every character from **left to right**.
- Count how many times the current character appears.
- If `count == 1`, return its index.
- Because we traverse left to right, the first unique character is automatically found first.
- If no character is unique, return `-1`.
- This solution uses **brute force** and takes `O(n²)` time.

---

## ⚠️ Common Mistakes

- Returning the character instead of its index.
- Returning the first character without checking its frequency.
- Forgetting to reset `count = 0` for every new character.
- Returning `-1` before checking the entire string.
- Using `count == 0` instead of `count == 1`.

---

## 🎯 Interview Tip

> **First unique = Traverse left to right + count occurrences + return the first count of 1.**

```text
Character
    ↓
Count occurrences
    ↓
count == 1 ?
   ↙     ↘
 Yes      No
  ↓        ↓
return i  next character
```
