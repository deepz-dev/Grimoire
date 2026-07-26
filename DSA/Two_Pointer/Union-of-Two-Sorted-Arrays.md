# 🔢 Union of Two Sorted Arrays

## 🔗 Problem Link

GeeksforGeeks: Union of Two Sorted Arrays

---

## 🏷️ Tags

- Array
- Two Pointers

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given two **sorted arrays** `a[]` and `b[]`, where both arrays may contain duplicate elements, return the **union** of the two arrays in sorted order.

The union should contain only **distinct** elements.

---

## ✨ Examples

### Example 1

**Input**

```text
a = [1,2,3,4,5]
b = [1,2,3,6,7]
```

**Output**

```text
[1,2,3,4,5,6,7]
```

---

### Example 2

**Input**

```text
a = [2,2,3,4,5]
b = [1,1,2,3,4]
```

**Output**

```text
[1,2,3,4,5]
```

---

## 🚀 Approach

Since both arrays are sorted, we use the **Two Pointer (Merge) Technique**.

- Maintain two pointers:
  - `i` for array `a`
  - `j` for array `b`
- Compare the current elements.
- Add the smaller element to the answer.
- If both elements are equal, add only one copy and move both pointers.
- Before inserting, compare with the last inserted element to avoid duplicates.

---

# ✅ Solution 1 - Using ArrayList

```java
ArrayList<Integer> ans = new ArrayList<>();
```

This is the version commonly seen on **GeeksforGeeks** because the function signature itself returns an `ArrayList`.

### 💻 Java Code

```java
class Solution {

    public static ArrayList<Integer> findUnion(int[] a, int[] b) {

        ArrayList<Integer> ans = new ArrayList<>();

        int i = 0, j = 0;

        while (i < a.length && j < b.length) {

            if (a[i] < b[j]) {

                if (ans.isEmpty() || ans.get(ans.size() - 1) != a[i])
                    ans.add(a[i]);

                i++;

            } else if (a[i] > b[j]) {

                if (ans.isEmpty() || ans.get(ans.size() - 1) != b[j])
                    ans.add(b[j]);

                j++;

            } else {

                if (ans.isEmpty() || ans.get(ans.size() - 1) != a[i])
                    ans.add(a[i]);

                i++;
                j++;
            }
        }

        while (i < a.length) {

            if (ans.isEmpty() || ans.get(ans.size() - 1) != a[i])
                ans.add(a[i]);

            i++;
        }

        while (j < b.length) {

            if (ans.isEmpty() || ans.get(ans.size() - 1) != b[j])
                ans.add(b[j]);

            j++;
        }

        return ans;
    }
}
```

### 👍 Pros

- Matches GFG method signature.
- Beginner friendly.
- Common in DSA practice.

### 👎 Cons

- Variable is tightly coupled to the `ArrayList` implementation.

---

# ✅ Solution 2 - Using List (Recommended)

```java
List<Integer> ans = new ArrayList<>();
```

The algorithm is **exactly the same**.

Only the variable type changes.

### 💻 Java Code

```java
class Solution {

    public static List<Integer> findUnion(int[] a, int[] b) {

        List<Integer> ans = new ArrayList<>();

        int i = 0, j = 0;

        while (i < a.length && j < b.length) {

            if (a[i] < b[j]) {

                if (ans.isEmpty() || ans.get(ans.size() - 1) != a[i])
                    ans.add(a[i]);

                i++;

            } else if (a[i] > b[j]) {

                if (ans.isEmpty() || ans.get(ans.size() - 1) != b[j])
                    ans.add(b[j]);

                j++;

            } else {

                if (ans.isEmpty() || ans.get(ans.size() - 1) != a[i])
                    ans.add(a[i]);

                i++;
                j++;
            }
        }

        while (i < a.length) {

            if (ans.isEmpty() || ans.get(ans.size() - 1) != a[i])
                ans.add(a[i]);

            i++;
        }

        while (j < b.length) {

            if (ans.isEmpty() || ans.get(ans.size() - 1) != b[j])
                ans.add(b[j]);

            j++;
        }

        return ans;
    }
}
```

### 👍 Pros

- Follows Java best practices.
- Uses abstraction.
- Easier to switch implementations later.
- Preferred in interviews and production code.

### 👎 Cons

- Slightly harder for beginners to understand.

---

## ⭐ Which One Should I Use?

### ✅ DSA Platforms (LeetCode, GFG)

```java
ArrayList<Integer> ans = new ArrayList<>();
```

Reason:

- Matches the required return type on many platforms.
- Straightforward and beginner-friendly.

---

### ✅ Interviews & Production Code

```java
List<Integer> ans = new ArrayList<>();
```

Reason:

`List` is an **interface** and `ArrayList` is one of its **implementations**.

Programming to the interface makes the code more flexible.

If you later decide to use a `LinkedList`, only one line changes:

```java
List<Integer> ans = new LinkedList<>();
```

The rest of the code remains unchanged.

This follows the Java design principle:

> **Program to an Interface, not an Implementation.**

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n + m)`

- Each array is traversed exactly once.

**Space Complexity:** `O(n + m)`

- Space is used only for storing the union.

---

## 🌟 Key Points

- Uses the Two Pointer (Merge) technique.
- Requires both arrays to be sorted.
- Removes duplicates while traversing.
- No additional sorting is required.
- Both solutions have the same algorithm and complexity.

---

## ⚠️ Common Mistakes

- Using nested loops (`O(n × m)`).
- Forgetting to move both pointers when equal elements are found.
- Adding duplicate values.
- Forgetting to process the remaining elements after one array is exhausted.
- Comparing with the current element instead of the last inserted element.

---

## 💡 Final Takeaway

| Feature | `ArrayList<Integer>` | `List<Integer>` |
|---------|-----------------------|-----------------|
| Algorithm | ✅ Same | ✅ Same |
| Time Complexity | `O(n + m)` | `O(n + m)` |
| Space Complexity | `O(n + m)` | `O(n + m)` |
| Object Created | `ArrayList` | `ArrayList` |
| Variable Type | `ArrayList` | `List` |
| Best For | Coding Platforms | Interviews & Production |
| Flexibility | Low | High |

> **Remember:** The algorithm never changes. The only difference is the type of reference used to access the same `ArrayList` object.
