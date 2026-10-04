# 🔤 Longest Common Prefix

## 🔗 Problem Link

<a href="https://leetcode.com/problems/longest-common-prefix/" target="_blank">
LeetCode 14: Longest Common Prefix
</a>

---

## 🏷️ Tags

- String
- String Manipulation
- Prefix
- Iteration

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given an array of strings, find the **longest common prefix** string amongst them.

If there is no common prefix, return an empty string:

```text
""
```

A **prefix** is a sequence of characters that appears at the beginning of a string.

---

## ✨ Examples

### Example 1

```text
Input:
strs = ["flower", "flow", "flight"]

Output:
"fl"
```

Explanation:

```text
flower
flow
flight
```

The common prefix is:

```text
"fl"
```

---

### Example 2

```text
Input:
strs = ["dog", "racecar", "car"]

Output:
""
```

Explanation:

There is no common prefix among the strings.

---

## 🚀 Approach

Use **Prefix Reduction**.

The main idea is:

> Start with the first string as the prefix and keep reducing it until every string starts with that prefix.

### Step 1 — Take the First String as Prefix

```java
String prefix = strs[0];
```

Initially, assume the entire first string is the common prefix.

For:

```text
["flower", "flow", "flight"]
```

we start with:

```text
prefix = "flower"
```

---

### Step 2 — Compare With Every Other String

Loop through the remaining strings:

```java
for (int i = 1; i < strs.length; i++)
```

Check whether the current string starts with our prefix:

```java
strs[i].startsWith(prefix)
```

---

### Step 3 — Reduce the Prefix

If the current string does not start with the prefix:

```java
while (!strs[i].startsWith(prefix))
```

remove the last character:

```java
prefix = prefix.substring(0, prefix.length() - 1);
```

Example:

```text
flower
↓
flowe
↓
flow
```

Now `"flow"` is a prefix of `"flow"`.

---

### Step 4 — Check for Empty Prefix

If:

```java
prefix.isEmpty()
```

there is no common prefix.

So return:

```java
return "";
```

---

### Step 5 — Return the Final Prefix

After comparing all strings, return:

```java
return prefix;
```

---

## 🧠 Dry Run

For:

```text
strs = ["flower", "flow", "flight"]
```

### Initially

```text
prefix = "flower"
```

Compare with:

```text
"flow"
```

`"flow"` does not start with `"flower"`.

Reduce:

```text
"flower"
"flowe"
"flow"
```

Now:

```text
prefix = "flow"
```

---

Compare with:

```text
"flight"
```

`"flight"` does not start with `"flow"`.

Reduce:

```text
"flow"
"flo"
"fl"
```

Now:

```text
"flight".startsWith("fl") → true
```

Final answer:

```text
"fl"
```

---

## 💻 Java Solution

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {

        String prefix = strs[0];

        for (int i = 1; i < strs.length; i++) {

            while (!strs[i].startsWith(prefix)) {

                prefix = prefix.substring(0, prefix.length() - 1);

                if (prefix.isEmpty()) {
                    return "";
                }
            }
        }

        return prefix;
    }
}
```

---

## ⏱️ Complexity Analysis

### Time Complexity

```text
O(n × m)
```

Where:

- `n` = number of strings
- `m` = length of the prefix/string being checked

In the worst case, we may compare many characters across all strings.

### Space Complexity

```text
O(m)
```

Because the `prefix` string is repeatedly created using `substring()`.

---

## 🔒 Constraints

- `1 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` consists of lowercase English letters if non-empty.

---

## 🌟 Key Points

- Start with the first string as the prefix.
- Compare the prefix with every other string.
- If a string does not start with the prefix, reduce the prefix.
- Remove characters from the **end** of the prefix.
- Continue until the current string starts with the prefix.
- If the prefix becomes empty, return:
  ```text
  ""
  ```
- Finally return the remaining prefix.

---

## ⚠️ Common Mistakes

- Starting with an empty prefix.
- Comparing characters individually without understanding the prefix idea.
- Removing characters from the beginning instead of the end.
- Forgetting to check:
  ```java
  prefix.isEmpty()
  ```
- Using `contains()` instead of `startsWith()`.
- Forgetting that the prefix must start at index `0`.

---

## 🎯 Interview Tip

> **Start with the first string → compare → keep shrinking the prefix until it matches.**

```text
flower
   ↓
flow
   ↓
fl
   ↓
Answer
```

The important method:

```java
startsWith(prefix)
```

means:

> "Does this string begin with the current prefix?"
