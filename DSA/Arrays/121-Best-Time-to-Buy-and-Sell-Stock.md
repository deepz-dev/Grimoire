# 📈 Best Time to Buy and Sell Stock

## 🔗 Problem Link

LeetCode 121: Best Time to Buy and Sell Stock

---

## 🏷️ Tags

- Array
- Greedy

---

## 📊 Difficulty

Easy

---

## Problem Statement

You are given an array `prices` where `prices[i]` represents the stock price on the `iᵗʰ` day.

You may choose **one day to buy** one stock and **one later day to sell** that stock.

Return the **maximum profit** possible.

If no profit can be made, return `0`.

---

## ✨ Examples

### Example 1

**Input**

```text
prices = [7,1,5,3,6,4]
```

**Output**

```text
5
```

**Explanation**

```text
Buy at price = 1

Sell at price = 6

Profit = 6 - 1 = 5
```

---

### Example 2

**Input**

```text
prices = [7,6,4,3,1]
```

**Output**

```text
0
```

**Explanation**

```text
Prices keep decreasing.

No profitable transaction is possible.
```

---

# 🚀 Solution 1 — Track Minimum Price

## Idea

Traverse the array once.

Keep track of:

- Lowest buying price seen so far.
- Maximum profit obtained so far.

Whenever a smaller price is found,

update the buying price.

Otherwise,

calculate the profit if sold today.

Update the answer if it is larger.

---

## 💻 Java Solution

```java
class Solution {

    public int maxProfit(int[] prices) {

        int buy = prices[0];
        int profit = 0;

        for (int i = 1; i < prices.length; i++) {

            if (prices[i] < buy) {
                buy = prices[i];
            }

            else if (prices[i] - buy > profit) {
                profit = prices[i] - buy;
            }
        }

        return profit;
    }
}
```

---

## Dry Run

Input

```text
prices = [7,1,5,3,6,4]
```

| Day | Price | Buy | Profit |
|----:|------:|----:|-------:|
|1|7|7|0|
|2|1|1|0|
|3|5|1|4|
|4|3|1|4|
|5|6|1|5|
|6|4|1|5|

Answer

```text
5
```

---

# 🚀 Solution 2 — Math.min() and Math.max()

This is the same greedy algorithm written more compactly.

Instead of using `if-else`, use:

- `Math.min()` to update the minimum buying price.
- `Math.max()` to update the maximum profit.

---

## 💻 Java Solution

```java
class Solution {

    public int maxProfit(int[] prices) {

        int min = prices[0];
        int profit = 0;

        for (int i = 1; i < prices.length; i++) {

            int cost = prices[i] - min;

            profit = Math.max(profit, cost);

            min = Math.min(min, prices[i]);
        }

        return profit;
    }
}
```

---

# 🚀 Solution 3 — Enhanced Greedy (Most Compact)

Instead of initializing with the first element,

start with the largest possible buying price.

Whenever a smaller price appears,

update the buying price.

Otherwise,

directly compute the best profit.

---

## 💻 Java Solution

```java
class Solution {

    public int maxProfit(int[] prices) {

        int buy = Integer.MAX_VALUE;
        int profit = 0;

        for (int price : prices) {

            if (price < buy) {
                buy = price;
            }

            else {
                profit = Math.max(profit, price - buy);
            }
        }

        return profit;
    }
}
```

---

# ⭐ Optimal Solution

**Solution 3** is generally preferred.

Reason:

- No special handling for the first element.
- Cleaner initialization.
- Works directly using enhanced for-loop.
- Most concise implementation.
- Same greedy idea as the other two solutions.

All three solutions implement **exactly the same algorithm**.

Only the coding style is different.

---

## 🧠 Greedy Intuition

At every step,

we ask two questions.

```text
1. Is today's price the cheapest so far?

YES

→ Update buying price.
```

Otherwise,

```text
2. If I sell today,

will I earn more profit than before?

YES

→ Update maximum profit.
```

Repeat until the array ends.

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

- Traverse the array once.

**Space Complexity:** `O(1)`

- Only two variables are maintained.

---

## 🌟 Key Points

- Greedy Algorithm.
- Track the minimum buying price.
- Update profit whenever a better selling price is found.
- Only one traversal.
- No extra space.
- Optimal solution.

---

## ⚠️ Common Mistakes

- Selling before buying.
- Updating profit before updating the minimum price.
- Using nested loops (`O(n²)`).
- Forgetting to return `0` when no profit is possible.

---

## 🎯 Interview Tip

Whenever you see:

```text
Buy once

Sell once

Maximum Profit
```

Think immediately of:

```text
Greedy

Maintain Minimum Price

Maintain Maximum Profit
```

Never use nested loops.

The greedy approach solves it in linear time.
