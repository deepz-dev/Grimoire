# 🔄 Valid Palindrome

## 🔗 Problem Link

<a href="https://leetcode.com/problems/valid-palindrome/" target="_blank">
LeetCode 125: Valid Palindrome
</a>

---

## 🏷️ Tags

- String
- Recursion
- Two Pointers
- Palindrome

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given a string `s`, determine whether it is a **palindrome** after:

1. Converting uppercase letters to lowercase.
2. Removing all non-alphanumeric characters.

A palindrome reads the same forward and backward.

---

## ✨ Examples

### Example 1

```text
Input:
s = "A man, a plan, a canal: Panama"

Output:
true
```

After removing non-alphanumeric characters and converting to lowercase:

```text
amanaplanacanalpanama
```

It reads the same from both directions.

---

### Example 2

```text
Input:
s = "race a car"

Output:
false
```

After cleaning:

```text
raceacar
```

Forward and backward are different.

---

### Example 3

```text
Input:
s = " "

Output:
true
```

After removing non-alphanumeric characters:

```text
""
```

An empty string is a palindrome.

---

## 🚀 Approach

Use **String Cleaning + Recursion**.

### Step 1 — Clean the String

Remove all characters that are not:

```text
a-z
A-Z
0-9
```

Then convert the remaining characters to lowercase.

```java
s = s.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();
```

For example:

```text
"A man, a plan, a canal: Panama"
```

becomes:

```text
"amanaplanacanalpanama"
```

---

### Step 2 — Compare Characters Recursively

Start from the first character:

```text
i = 0
```

Compare:

```text
s.charAt(i)
```

with:

```text
s.charAt(s.length() - i - 1)
```

The second expression gives the character from the opposite end.

For example:

```text
s = "abcba"

i = 0

left  = s.charAt(0) → 'a'
right = s.charAt(4) → 'a'
```

They are equal, so continue.

---

### Step 3 — Base Case

We only need to compare characters until the middle.

```java
if (i >= s.length() / 2) {
    return true;
}
```

Once we reach the middle, all required pairs have already matched.

---

### Step 4 — Check for Mismatch

If:

```java
s.charAt(i) != s.charAt(s.length() - i - 1)
```

then the string cannot be a palindrome.

Return:

```java
return false;
```

---

### Step 5 — Move to the Next Character

If both characters match:

```java
return checkPalindrome(i + 1, s);
```

This moves the comparison toward the center.

---

## 🧠 Recursion Flow

For:

```text
s = "abcba"
```

The comparisons are:

```text
a ↔ a
b ↔ b
c
```

Once we reach the middle:

```text
i >= s.length() / 2
```

return:

```text
true
```

### Mental Model

```text
First ↔ Last
Second ↔ Second Last
Third ↔ Third Last
...
Middle
```

---

## 💻 Java Solution

```java
class Solution {

    public boolean isPalindrome(String s) {

        // Remove non-alphanumeric characters
        // and convert everything to lowercase
        s = s.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();

        return checkPalindrome(0, s);
    }

    private boolean checkPalindrome(int i, String s) {

        // Base case: reached the middle
        if (i >= s.length() / 2) {
            return true;
        }

        // If characters do not match
        if (s.charAt(i) != s.charAt(s.length() - i - 1)) {
            return false;
        }

        // Check the next pair
        return checkPalindrome(i + 1, s);
    }
}
```

---

## ⏱️ Complexity Analysis

### Time Complexity

```text
O(n)
```

Cleaning the string takes `O(n)` and the recursive comparison checks each character at most once.

### Space Complexity

```text
O(n)
```

The recursive call stack can go up to `n / 2`, which is `O(n)`.

Also, creating the cleaned string requires additional space.

---

## 🔒 Constraints

- `1 <= s.length <= 2 * 10⁵`
- `s` consists only of printable ASCII characters.

---

## 🌟 Key Points

- First clean the string.
- Convert everything to lowercase.
- Compare characters from both ends.
- Use:
  ```text
  s.length() - i - 1
  ```
  to access the character from the right side.
- Only compare until the middle.
- If any pair is different → `false`.
- If all pairs match → `true`.
- This is essentially a **two-pointer palindrome check implemented using recursion**.

---

## ⚠️ Common Mistakes

- Forgetting to convert uppercase characters to lowercase.
- Not removing spaces and special characters.
- Using:
  ```text
  s.length() - i
  ```
  instead of:
  ```text
  s.length() - i - 1
  ```
- Comparing the entire string instead of stopping at the middle.
- Forgetting the base case.
- Comparing the original string instead of the cleaned string.

---

## 🎯 Interview Tip

> **Palindrome = Compare both ends and move toward the middle.**

```text
Left → → → Middle ← ← ← Right

s[i] == s[n - i - 1]
```

For recursion:

```text
Check pair → Move i → Check next pair → ... → Middle
```
