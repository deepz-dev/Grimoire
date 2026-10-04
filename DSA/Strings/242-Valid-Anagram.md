# 🔤 Valid Anagram

## 🔗 Problem Link

<a href="https://leetcode.com/problems/valid-anagram/" target="_blank">
LeetCode 242: Valid Anagram
</a>

---

## 🏷️ Tags

- String
- Hashing
- Frequency Counting
- Array

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given two strings `s` and `t`, return `true` if `t` is an **anagram** of `s`, and `false` otherwise.

Two strings are anagrams if they contain the **same characters with the same frequencies**, but the order can be different.

---

## ✨ Examples

### Example 1

```text
Input:
s = "anagram"
t = "nagaram"

Output:
true
```

Explanation:

Both strings contain the same characters with the same frequencies.

---

### Example 2

```text
Input:
s = "rat"
t = "car"

Output:
false
```

Explanation:

The character frequencies are different.

---

## 🚀 Approach

Use **Frequency Counting with an Array**.

Since the problem contains only lowercase English letters, we can use an array of size `26`.

```java
int[] freq = new int[26];
```

Each index represents a character:

```text
a → 0
b → 1
c → 2
...
z → 25
```

### Step 1 — Check Length

Anagrams must have the same length.

```java
if (s.length() != t.length()) {
    return false;
}
```

---

### Step 2 — Count Characters of `s`

For every character in `s`:

```java
freq[ch - 'a']++;
```

Example:

```text
s = "anagram"
```

We increase the frequency of every character.

---

### Step 3 — Remove Characters of `t`

For every character in `t`:

```java
freq[ch - 'a']--;
```

If `s` and `t` contain exactly the same characters with the same frequency, every value in `freq` should become `0`.

---

### Step 4 — Check the Frequency Array

Traverse the array:

```java
for (int count : freq)
```

If any value is not `0`:

```java
return false;
```

Otherwise:

```java
return true;
```

---

## 🧠 Dry Run

For:

```text
s = "anagram"
t = "nagaram"
```

First count `s`:

```text
a → 3
n → 1
g → 1
r → 1
m → 1
```

Then subtract the frequencies of `t`.

Since `t` contains exactly the same characters:

```text
a → 0
n → 0
g → 0
r → 0
m → 0
```

All values become `0`.

Therefore:

```text
true
```

---

## 💻 Java Solution

```java
class Solution {
    public boolean isAnagram(String s, String t) {

        if (s.length() != t.length()) {
            return false;
        }

        int[] freq = new int[26];

        for (char ch : s.toCharArray()) {
            freq[ch - 'a']++;
        }

        for (char ch : t.toCharArray()) {
            freq[ch - 'a']--;
        }

        for (int count : freq) {
            if (count != 0) {
                return false;
            }
        }

        return true;
    }
}
```

---

## ⏱️ Complexity Analysis

### Time Complexity

```text
O(n)
```

We traverse both strings and then the fixed-size array of `26` characters.

### Space Complexity

```text
O(1)
```

The frequency array always contains only `26` elements.

---

## 🔒 Constraints

- `1 <= s.length, t.length <= 5 * 10⁴`
- `s` and `t` consist of lowercase English letters.

---

## 🌟 Key Points

- Anagrams must have the **same length**.
- Count the frequency of characters in `s`.
- Subtract the frequency of characters in `t`.
- If every frequency becomes `0`, they are anagrams.
- Since only lowercase English letters are given, an array of size `26` is enough.
- This is more efficient than using a `HashMap` because the character range is fixed.

---

## ⚠️ Common Mistakes

- Forgetting to check the string lengths.
- Using `freq[ch]` instead of:
  ```java
  freq[ch - 'a']
  ```
- Checking only whether the characters exist instead of checking their frequencies.
- Forgetting to decrease the frequency for the second string.
- Returning `true` without checking the complete frequency array.

---

## 🎯 Interview Tip

> **Anagram = Same characters + Same frequency.**

```text
s → + frequency
t → - frequency
        ↓
   all values 0?
      ↙     ↘
    Yes      No
     ↓        ↓
   true     false
```
