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

Given two **sorted** arrays `a[]` and `b[]`, where each array may contain duplicate elements, return the **union** of the two arrays in sorted order.

The union should contain **only distinct elements** that are present in either of the arrays.

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

### Example 3

**Input**

```text
a = [1,1,1,1]
b = [2,2,2,2]
```

**Output**

```text
[1,2]
```

---

## 🚀 Approach

Since both arrays are already sorted, use the **Two Pointer** technique.

1. Initialize two pointers `i` and `j`.
2. Compare the current elements of both arrays.
3. Insert the smaller element into the answer if it is not already present.
4. If both elements are equal, insert only one copy and move both pointers.
5. After one array is exhausted, add the remaining elements from the other array while avoiding duplicates.

The last inserted element is checked before every insertion to ensure only distinct elements are added.

---

## 💻 Java Solution

```java
class Solution {
    public static ArrayList<Integer> findUnion(int a[], int b[]) {

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

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n + m)`

- Each array is traversed exactly once.

**Space Complexity:** `O(n + m)`

- Space is used only for storing the union of the two arrays.

---

## 🔒 Constraints

- `1 ≤ a.size(), b.size() ≤ 10⁵`
- `-10⁹ ≤ a[i], b[i] ≤ 10⁹`

---

## 🌟 Key Points

- Uses the optimal **Two Pointer** approach.
- Works because both arrays are sorted.
- Duplicate elements are skipped by comparing with the last inserted element.
- No sorting is required.
- Maintains the sorted order of the union.

---

## ⚠️ Common Mistakes

- Using `<=` instead of `<` in loop conditions, causing `ArrayIndexOutOfBoundsException`.
- Forgetting to move **both** pointers when equal elements are found.
- Adding duplicate elements from the same array.
- Forgetting to process the remaining elements after one array is exhausted.
- Comparing with the current element instead of the **last inserted** element when checking duplicates.
