# 🔤 Longest Substring Without Repeating Characters

## 🔗 Problem Link

<a href="https://leetcode.com/problems/longest-substring-without-repeating-characters/" target="_blank">
LeetCode 3: Longest Substring Without Repeating Characters
</a>

---

## 🏷️ Tags

- String
- Sliding Window
- Two Pointers
- HashSet

---

## 📊 Difficulty

Medium

---

## Problem Statement

Given a string `s`, find the length of the **longest substring without repeating characters**.

A substring must contain characters that are **next to each other** in the original string.

---

## ✨ Examples

### Example 1

```text
Input:
s = "abcabcbb"

Output:
3
```

Explanation:

```text
"abc"
```

is the longest substring without repeating characters.

Length:

```text
3
```

---

### Example 2

```text
Input:
s = "bbbbb"

Output:
1
```

Explanation:

The longest substring is:

```text
"b"
```

Length:

```text
1
```

---

### Example 3

```text
Input:
s = "pwwkew"

Output:
3
```

Explanation:

The longest substring is:

```text
"wke"
```

Length:

```text
3
```

---

## 🚀 Approach

Use **Sliding Window + Two Pointers + HashSet**.

We maintain a window containing only **unique characters**.

```text
left → window → right
```

### Step 1 — Create a HashSet

The `HashSet` stores the characters currently present inside the window.

```java
Set<Character> present = new HashSet<>();
```

---

### Step 2 — Expand the Window

Use `right` to move through the string.

```java
for (int right = 0; right < s.length(); right++)
```

The current character is:

```java
char current = s.charAt(right);
```

---

### Step 3 — Handle Duplicate Characters

If the current character is already inside the window:

```java
while (present.contains(current))
```

remove characters from the left side.

```java
present.remove(s.charAt(left));
left++;
```

We keep doing this until the duplicate character is removed.

---

### Step 4 — Add the Current Character

Once there is no duplicate:

```java
present.add(current);
```

Now the current window contains only unique characters.

---

### Step 5 — Calculate Maximum Length

The current window is:

```text
[left ... right]
```

So its length is:

```text
right - left + 1
```

Update the maximum:

```java
maxLen = Math.max(maxLen, right - left + 1);
```

---

## 🧠 Dry Run

For:

```text
s = "abcabcbb"
```

Initially:

```text
left = 0
maxLen = 0
```

### `right = 0`

```text
current = 'a'
```

Window:

```text
"a"
```

Length:

```text
1
```

---

### `right = 1`

```text
current = 'b'
```

Window:

```text
"ab"
```

Length:

```text
2
```

---

### `right = 2`

```text
current = 'c'
```

Window:

```text
"abc"
```

Length:

```text
3
```

So:

```text
maxLen = 3
```

---

### `right = 3`

```text
current = 'a'
```

`a` already exists in the window.

Remove from the left:

```text
remove 'a'
left++
```

Now the window becomes:

```text
"bc"
```

Add `a`:

```text
"bca"
```

Length:

```text
3
```

---

The process continues until the complete string is checked.

Final answer:

```text
3
```

---

## 💻 Java Solution

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {

        Set<Character> present = new HashSet<>();

        int left = 0;
        int maxLen = 0;

        for (int right = 0; right < s.length(); right++) {

            char current = s.charAt(right);

            while (present.contains(current)) {
                present.remove(s.charAt(left));
                left++;
            }

            present.add(current);

            maxLen = Math.max(maxLen, right - left + 1);
        }

        return maxLen;
    }
}
```

---

## ⏱️ Complexity Analysis

### Time Complexity

```text
O(n)
```

The `right` pointer moves from left to right once.

The `left` pointer also moves forward only.

Therefore, each character is added and removed from the `HashSet` at most once.

---

### Space Complexity

```text
O(n)
```

The `HashSet` stores characters currently inside the window.

---

## 🔒 Constraints

```text
0 <= s.length <= 10⁵
```

`s` consists of English letters, digits, symbols and spaces.

---

## 🌟 Key Points

- Use **Sliding Window** for substring problems where we need the longest/shortest valid range.
- Use two pointers:
  ```text
  left
  right
  ```
- `right` expands the window.
- `left` shrinks the window when a duplicate is found.
- `HashSet` keeps track of characters inside the current window.
- The window always contains **unique characters**.
- Current window length:
  ```text
  right - left + 1
  ```
- Update `maxLen` after making the window valid.

---

## ⚠️ Common Mistakes

- Forgetting `+1` in:
  ```text
  right - left + 1
  ```
- Moving `left` without removing the character from the `HashSet`.
- Using `if` instead of `while` when removing duplicates.
- Confusing substring with subsequence.
- Updating `maxLen` before removing duplicates.
- Moving `left` backward.
- Forgetting to add the current character after the window becomes valid.

---

## 🎯 Interview Tip

> **Sliding Window = Expand with `right`, shrink with `left` when the window becomes invalid.**

```text
right →
[ unique characters ]

duplicate found
      ↓
move left →
      ↓
valid window
      ↓
update maxLen
```

### Pattern

```text
HashSet
   ↓
Right expands
   ↓
Duplicate?
   ↓ Yes
Left shrinks
   ↓
Add current
   ↓
Update maximum
```
