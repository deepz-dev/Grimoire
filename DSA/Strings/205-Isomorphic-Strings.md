# 🔄 Isomorphic Strings

## 🔗 Problem Link

<a href="https://leetcode.com/problems/isomorphic-strings/" target="_blank">
LeetCode 205: Isomorphic Strings
</a>

---

## 🏷️ Tags

- String
- Hashing
- Arrays
- Mapping

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given two strings `s` and `t`, determine if they are **isomorphic**.

Two strings are isomorphic if the characters in `s` can be replaced to get `t`.

The mapping must follow these rules:

- Every occurrence of a character must map to the same character.
- Two different characters cannot map to the same character.
- A character can map to itself.

---

## ✨ Examples

### Example 1

```text
Input:
s = "egg"
t = "add"

Output:
true
```

Explanation:

```text
e → a
g → d
```

So:

```text
egg
 ↓↓
add
```

The mapping is consistent.

---

### Example 2

```text
Input:
s = "foo"
t = "bar"

Output:
false
```

Explanation:

```text
f → b
o → a
```

But the second `o` would need to map to `r`.

So the mapping is not consistent.

---

### Example 3

```text
Input:
s = "paper"
t = "title"

Output:
true
```

The mapping is:

```text
p → t
a → i
p → t
e → l
r → e
```

The same characters always map to the same characters.

---

## 🚀 Approach

Use **Two-Way Mapping with Arrays**.

We need to make sure that the mapping works in **both directions**:

```text
s → t
t → s
```

This prevents two different characters from mapping to the same character.

---

### Step 1 — Create Two Arrays

```java
int[] mapST = new int[256];
int[] mapTS = new int[256];
```

`mapST` stores:

```text
s character → t character
```

`mapTS` stores:

```text
t character → s character
```

---

### Step 2 — Traverse Both Strings

For every position:

```java
char a = s.charAt(i);
char b = t.charAt(i);
```

Here:

```text
a → character from s
b → character from t
```

---

### Step 3 — Check Existing Mapping

```java
if (mapST[a] != mapTS[b]) {
    return false;
}
```

The arrays store `i + 1` instead of `i` because:

```text
0 = not mapped yet
```

So:

```java
mapST[a] = i + 1;
mapTS[b] = i + 1;
```

---

### 🧠 Why Two Arrays?

Suppose:

```text
s = "ab"
t = "cc"
```

If we only check:

```text
s → t
```

we might allow:

```text
a → c
b → c
```

But this is not valid because two different characters cannot map to the same character.

The reverse mapping:

```text
t → s
```

prevents this.

Therefore:

```text
s → t
AND
t → s
```

must both be consistent.

---

## 🧠 Dry Run

For:

```text
s = "egg"
t = "add"
```

### `i = 0`

```text
a = 'e'
b = 'a'
```

Both are not mapped.

Store:

```text
e → a
a → e
```

---

### `i = 1`

```text
a = 'g'
b = 'd'
```

Store:

```text
g → d
d → g
```

---

### `i = 2`

```text
a = 'g'
b = 'd'
```

The mapping already exists:

```text
g → d
d → g
```

It is consistent.

Therefore:

```text
true
```

---

## 💻 Java Solution

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {

        int[] mapST = new int[256];
        int[] mapTS = new int[256];

        for (int i = 0; i < s.length(); i++) {

            char a = s.charAt(i);
            char b = t.charAt(i);

            if (mapST[a] != mapTS[b]) {
                return false;
            }

            mapST[a] = i + 1;
            mapTS[b] = i + 1;
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

We traverse the strings only once.

### Space Complexity

```text
O(1)
```

The arrays always have a fixed size of `256`.

---

## 🔒 Constraints

- `1 <= s.length <= 5 * 10⁴`
- `t.length == s.length`
- `s` and `t` consist of valid ASCII characters.

---

## 🌟 Key Points

- Isomorphic strings require a **consistent one-to-one mapping**.
- Maintain two mappings:
  ```text
  s → t
  t → s
  ```
- Use arrays for fast lookup.
- `0` means the character has not been mapped yet.
- Store `i + 1` instead of `i` because index `0` is used as the "not mapped" value.
- If the mappings become inconsistent, return `false`.
- If all characters are processed successfully, return `true`.

---

## ⚠️ Common Mistakes

- Using only one mapping array.
- Allowing two characters from `s` to map to the same character in `t`.
- Forgetting the reverse mapping.
- Storing `i` instead of `i + 1`.
- Forgetting that repeated characters must always have the same mapping.

---

## 🎯 Interview Tip

> **Isomorphic = One-to-One Mapping.**

Remember:

```text
s → t
t → s
```

Both directions must be consistent.

```text
a → x
b → y     ✅

a → x
b → x     ❌
```
