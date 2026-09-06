# 🔢 Basic Hashing

## 🔗 Problem Link

Basic Hashing — DSA Fundamentals

---

## 🏷️ Tags

- Hashing
- Array Hashing
- Frequency Counting
- HashMap
- Map
- Character Hashing

---

## 📊 Difficulty

Easy

---

## Problem Statement

Hashing is a technique used to **store useful information about elements that have already been seen**, so that the information can be retrieved quickly later.

The main idea is:

> **Precompute information → store it → answer queries quickly.**

For example, given:

```text
arr = [1, 2, 1, 3, 2]
queries = [1, 3, 4, 2]
```

We need to find the frequency of each queried number.

The answers are:

```text
1 → 2
3 → 1
4 → 0
2 → 2
```

---

## ✨ Examples

### Example 1 — Frequency Counting

**Input**

```text
arr = [1, 2, 1, 3, 2]
```

**Query**

```text
1
```

**Output**

```text
2
```

---

### Example 2 — Element Not Present

**Input**

```text
arr = [1, 2, 1, 3, 2]
```

**Query**

```text
4
```

**Output**

```text
0
```

---

### Example 3 — Character Frequency

**Input**

```text
s = "abcdabefc"
```

**Queries**

```text
'a'
'c'
'z'
```

**Output**

```text
'a' → 2
'c' → 2
'z' → 0
```

---

## 🚀 Approach

### 1. Brute Force

For every query, traverse the entire array and count how many times the queried element occurs.

If:

```text
N = array size
Q = number of queries
```

Then:

```text
Time Complexity = O(N × Q)
```

For:

```text
N = 10⁵
Q = 10⁵
```

we get:

```text
10⁵ × 10⁵ = 10¹⁰ operations
```

which is too slow.

---

### 2. Hashing

Instead of repeatedly searching the array, calculate the required information **once** and store it.

Hashing has two main phases:

### Pre-storing

Traverse the array and store information about every element.

For frequency:

```text
hash[x] = frequency of x
```

Conceptually:

```text
for every x in arr:
    hash[x]++
```

### Fetching

When a query arrives:

```text
answer = hash[query]
```

There is no need to traverse the original array again.

---

## 🧠 Core Mental Model

Think:

```text
                 PROBLEM
                    ↓
       "I need information about
        things I've already seen"
                    ↓
                 HASHING
                    ↓
            What should I store?
                    ↓
                KEY → VALUE
                    ↓
        ┌───────────┴───────────┐
        ↓                       ↓
 Small bounded values     Large/arbitrary values
        ↓                       ↓
 Frequency Array          Map / HashMap
        ↓                       ↓
       O(1)                  O(1) avg
```

The most important idea is:

> **Store useful information about what you've already seen, so you don't repeatedly search for it.**

---

## 📦 Array Hashing

If the values are **small and bounded**, an array can directly act as a hash table.

Example:

```text
arr = [1, 3, 2, 1, 3]
```

Create:

```text
hash[0 ... 12]
```

Initially:

```text
0 0 0 0 0 0 0 0 0 0 0 0 0
```

For every element:

```text
hash[arr[i]]++
```

After processing:

```text
hash[1] = 2
hash[2] = 1
hash[3] = 2
hash[4] = 0
```

### Pattern to Recognize

Whenever you see:

> **"Find/count how many times each number occurs"**

and the value range is small:

```text
Think → Frequency Array / Array Hashing
```

---

## 🗺️ Map = Key → Value

A map stores information in the form:

```text
KEY → VALUE
```

Example:

```text
KEY        VALUE
----------------
12    →      1
3     →      2
2     →      2
1     →      2
```

### Key

The thing we are interested in.

Example:

```text
number = 12
```

### Value

The information associated with that key.

Example:

```text
frequency = 1
```

Therefore:

```text
number → frequency
```

is a common hashing pattern.

---

## 📊 Map for Frequency Counting

Given:

```text
arr = [1, 2, 3, 1, 3, 2, 12]
```

We build:

```text
map[1]  → 2
map[2]  → 2
map[3]  → 2
map[12] → 1
```

Conceptually:

```text
for every x in arr:
    map[x]++
```

Then:

```text
map[x]
```

gives the frequency of `x`.

If `x` does not exist:

```text
frequency = 0
```

---

## ⚖️ Array Hashing vs Map

| Situation | Think |
|---|---|
| Values are small and bounded | Array hashing |
| Values can be huge | Map / HashMap |
| Need key → information | Map |
| Need frequency | Frequency array / map |
| Need quick existence check | Hashing |

### Important Decision

Don't think:

> "I know HashMap, so I'll use HashMap."

Instead ask:

> **"What is the range of my values?"**

If the values are manageable:

```text
→ Array hashing
```

If the values are huge or arbitrary:

```text
→ Map / HashMap
```

---

## 🔤 Character Hashing

The same hashing idea works for characters.

Example:

```text
s = "abcdabefc"
```

We can pre-store the frequency of every character.

### Lowercase Letters

There are only 26 lowercase English letters:

```text
a → 0
b → 1
c → 2
...
z → 25
```

We can map a character using:

```text
character - 'a'
```

Example:

```text
'f' - 'a' = 5
```

Therefore:

```text
hash[s[i] - 'a']++
```

While fetching:

```text
hash[c - 'a']
```

Array size:

```text
26
```

### Pattern

If a problem says:

> **"String contains only lowercase English letters"**

immediately think:

```text
frequency[26]
```

---

## 🔠 Uppercase Letters

The same idea works for uppercase letters:

```text
A → 0
B → 1
...
Z → 25
```

Use:

```text
c - 'A'
```

Array size:

```text
26
```

---

## 🔡 Mixed Characters

If the input can contain general ASCII characters, use:

```text
hash[256]
```

Then:

```text
hash[s[i]]++
```

and:

```text
hash[c]
```

No subtraction is required.

### Quick Rule

```text
Only lowercase → 26
Only uppercase → 26
General ASCII → 256
```

---

## 💻 C++ / Java

### C++

```text
map<int, int>
```

or:

```text
unordered_map<int, int>
```

The basic idea remains:

```text
key → value
```

For frequency:

```text
number → frequency
```

### Java

```text
HashMap<Integer, Integer>
```

Again:

```text
key → value
```

---

## ⚡ `map` vs `unordered_map`

| Structure | Average | Worst Case |
|---|---:|---:|
| C++ `map` | O(log N) | O(log N) |
| C++ `unordered_map` | O(1) | O(N) |
| Java `HashMap` | O(1) average | Can degrade |

For typical DSA problem solving:

```text
unordered_map
```

is generally preferred when average `O(1)` lookup/insertion is useful.

If collision-related performance becomes problematic, a tree-based:

```text
map
```

provides:

```text
O(log N)
```

operations.

---

## 🔍 Why Is `unordered_map` O(1) Average?

Very roughly, hashing converts a key into a hash/index so that we can quickly find where its information should be stored.

Conceptually:

```text
key
 ↓
hash function
 ↓
bucket / index
 ↓
stored value
```

Instead of searching through every element:

```text
O(N)
```

hashing provides approximately:

```text
O(1) average lookup
```

---

## 🎯 Problem-Solving Questions

When you see a problem, ask these questions.

### Question 1

> **Am I repeatedly searching/counting something?**

If yes, ask:

> **Can I pre-store information?**

---

### Question 2

> **What information do I need to remember?**

It could be:

```text
frequency
existence
index
sum
count
```

---

### Question 3

> **What should be my key?**

Examples:

```text
number → frequency
character → frequency
number → index
```

---

### Question 4

> **Can I use an array or do I need a map?**

```text
Small bounded values → Array
Large/arbitrary values → Map
```

---

## 🔥 Pattern Triggers

When you see these phrases, your brain should react:

| Problem Wording | Pattern |
|---|---|
| "How many times..." | Frequency hashing |
| "Count occurrences" | Frequency array / map |
| "Does this exist?" | Hashing / Set |
| "Have I seen this before?" | Hashing |
| "Find its previous occurrence" | Hashing |
| "Store information about each number" | Map |
| Small value range | Array hashing |
| Huge values | Map |
| Repeated queries | **Pre-store → Fetch** |

---

## ⚠️ Common Mistakes

- Thinking **Hashing = HashMap**.
- Using a map when the value range is small enough for simple array hashing.
- Using an array when the values are extremely large or arbitrary.
- Repeatedly traversing the array for every query.
- Forgetting to distinguish between the **key** and the **value**.
- Memorizing syntax without understanding what information needs to be stored.
- Manually implementing collision handling when the problem only requires using `unordered_map` / `HashMap`.

---

## 🧩 Hashing Is an Idea, Not a Data Structure

Don't blindly think:

```text
Hashing = HashMap
```

Hashing is the **idea**.

That idea can be implemented using:

```text
Array
Map
unordered_map
HashMap
```

depending on the constraints and the information that needs to be stored.

---

## 🌟 Key Points

- **Pre-store → Fetch** is the fundamental hashing pattern.
- Hashing avoids repeatedly searching the original data.
- A map stores information as **Key → Value**.
- Frequency problems commonly use:
  ```text
  number → frequency
  ```
- Small bounded values can use **array hashing**.
- Large or arbitrary values can use a **map**.
- Lowercase English characters need only an array of size `26`.
- General ASCII character hashing can use an array of size `256`.
- `unordered_map` provides **O(1) average** lookup/insertion.
- Collisions can cause hashing performance to degrade.
- Collision handling is mainly important for understanding the theory; normal DSA problems usually provide the hashing data structure.
- The goal is to recognize **when hashing is the solution pattern**, not to memorize syntax.

---

## 🎯 What You Should Be Able to Explain

After learning basic hashing, you should be able to answer:

1. Why is brute-force frequency counting `O(N × Q)`?
2. What does pre-storing mean?
3. What does fetching mean?
4. When can I use an array for hashing?
5. Why do we need a map for huge values?
6. What is a key?
7. What is a value?
8. How does character hashing work?
9. Why is lowercase hashing size `26`?
10. Why is `unordered_map` generally `O(1)` average?
11. What is a collision?
12. Why can collisions make hashing slower?
13. Most importantly, **when should I recognize hashing as the solution pattern?**

---

## 🧠 One Sentence to Lock In

> **Hashing = store useful information about what you've already seen, so you don't repeatedly search for it.**
