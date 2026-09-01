# 🔢 Subarray Sum Equals K

## 🔗 Problem Link

LeetCode 560: Subarray Sum Equals K

---

## 🏷️ Tags

- Array
- HashMap
- Prefix Sum

---

## 📊 Difficulty

Medium

---

## Problem Statement

Given an integer array `nums` and an integer `k`, return the **total number of subarrays** whose sum equals `k`.

A **subarray** is a contiguous non-empty sequence of elements within an array.

---

## ✨ Examples

### Example 1

**Input**

```text
nums = [1,1,1], k = 2
```

**Output**

```text
2
```

**Explanation**

The two subarrays with sum `2` are:

```text
[1,1]
[1,1]
```

---

### Example 2

**Input**

```text
nums = [1,2,3], k = 3
```

**Output**

```text
2
```

**Explanation**

The subarrays are:

```text
[1,2]
[3]
```

Both have sum `3`.

---

## 🚀 Approach

Use **Prefix Sum + HashMap**.

The main idea is:

> If the current prefix sum is `sum`, and we have previously seen `sum - k`, then the elements between that previous position and the current position have sum `k`.

### 🧠 Why?

Suppose:

```text
currentPrefixSum = sum
```

We need a previous prefix sum such that:

```text
sum - previousPrefixSum = k
```

Therefore:

```text
previousPrefixSum = sum - k
```

So for every element:

1. Add the current element to the running prefix sum.
2. Calculate:

```text
needed = sum - k
```

3. If `needed` exists in the HashMap, add its frequency to the answer.
4. Store the current prefix sum in the HashMap.
5. Continue until the array ends.

---

## 🔑 Important Initialization

Before traversing the array:

```java
map.put(0, 1);
```

This is very important.

It represents:

```text
Prefix sum 0 has occurred once before the array starts.
```

### Example

For:

```text
nums = [3]
k = 3
```

After processing `3`:

```text
sum = 3
needed = 3 - 3 = 0
```

Since `0` already exists in the map:

```text
map = {0=1}
```

we found one valid subarray:

```text
[3]
```

Without:

```java
map.put(0, 1);
```

we would miss subarrays starting from index `0`.

---

## 🧪 Dry Run

Consider:

```text
nums = [1,2,1]
k = 3
```

Initial:

```text
sum = 0
count = 0

map = {0=1}
```

### Step 1

Element:

```text
1
```

Prefix sum:

```text
sum = 1
```

Needed:

```text
1 - 3 = -2
```

`-2` is not present.

Store:

```text
map = {0=1, 1=1}
```

---

### Step 2

Element:

```text
2
```

Prefix sum:

```text
sum = 3
```

Needed:

```text
3 - 3 = 0
```

`0` exists with frequency `1`.

Therefore:

```text
count = 1
```

The subarray is:

```text
[1,2]
```

Store prefix sum `3`.

---

### Step 3

Element:

```text
1
```

Prefix sum:

```text
sum = 4
```

Needed:

```text
4 - 3 = 1
```

`1` exists with frequency `1`.

Therefore:

```text
count = 2
```

The subarray is:

```text
[2,1]
```

Final answer:

```text
2
```

---

## 💻 Java Solution

```java
class Solution {

    public int subarraySum(int[] nums, int k) {

        HashMap<Integer, Integer> map = new HashMap<>();

        int cnt = 0;
        int presum = 0;

        // Prefix sum 0 occurs once before the array starts
        map.put(0, 1);

        for (int i = 0; i < nums.length; i++) {

            presum += nums[i];

            int needed = presum - k;

            // If needed prefix sum exists,
            // its frequency represents valid subarrays
            if (map.containsKey(needed)) {
                cnt += map.get(needed);
            }

            // Store/update frequency of current prefix sum
            if (map.containsKey(presum)) {
                map.put(presum, map.get(presum) + 1);
            } else {
                map.put(presum, 1);
            }
        }

        return cnt;
    }
}
```

---

## 🧠 Why Store Frequency Instead of Just Index?

We are counting **all possible subarrays**, so the same prefix sum can occur multiple times.

For example:

```text
nums = [1,-1,1,-1]
```

Prefix sums can repeat:

```text
1, 0, 1, 0
```

If a prefix sum appears multiple times, each occurrence can create a different subarray.

Therefore, the HashMap stores:

```text
prefixSum → frequency
```

Example:

```text
map = {
    0 → 3,
    1 → 2
}
```

When:

```text
needed = 0
```

we add:

```text
map.get(0)
```

to the answer.

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

- The array is traversed once.
- HashMap operations take `O(1)` average time.

**Space Complexity:** `O(n)`

- In the worst case, the HashMap can contain `n` different prefix sums.

---

## 🔒 Constraints

- `1 ≤ nums.length ≤ 2 × 10⁴`
- `-1000 ≤ nums[i] ≤ 1000`
- `-10⁷ ≤ k ≤ 10⁷`

---

## 🌟 Key Points

- Use **Prefix Sum + HashMap**.
- Store:

```text
prefixSum → frequency
```

- For every prefix sum `sum`, search for:

```text
sum - k
```

- If found, add its frequency to the answer.
- Initialize the map with:

```java
map.put(0, 1);
```

- The frequency is important because the same prefix sum can occur multiple times.
- Works even when the array contains **negative numbers**.
- Optimal complexity:

```text
Time  → O(n)
Space → O(n)
```

---

## ⚠️ Common Mistakes

- Forgetting:

```java
map.put(0, 1);
```

- Checking for `sum + k` instead of:

```text
sum - k
```

- Storing only the first index instead of the frequency.
- Using a sliding window when negative numbers are allowed.
- Forgetting that the subarray must be **contiguous**.
- Incrementing the prefix-sum frequency before checking `sum - k`, which can cause incorrect counting in some cases.

---

## 🎯 Interview Tip

When you see:

> **Count the number of subarrays whose sum equals K**

Immediately think:

```text
Prefix Sum + HashMap
```

The key equation is:

```text
currentPrefixSum - previousPrefixSum = k
```

Therefore:

```text
previousPrefixSum = currentPrefixSum - k
```

### 🔑 One-line memory trick

```text
Count Subarrays with Sum K
        ↓
Prefix Sum
        ↓
Find (sum - k)
        ↓
HashMap Frequency
```
