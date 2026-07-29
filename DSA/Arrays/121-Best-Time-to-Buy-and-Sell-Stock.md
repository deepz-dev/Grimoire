# 🔢 Best Time to Buy and Sell Stock

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

You are given an array `prices` where `prices[i]` is the price of a stock on the `iᵗʰ` day.

You want to maximize your profit by choosing:

- One day to **buy** the stock.
- A later day to **sell** the stock.

Return the **maximum profit** you can achieve.

If no profit is possible, return `0`.

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

- Buy on day 2 at price `1`.
- Sell on day 5 at price `6`.

Profit:

```text
6 - 1 = 5
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

The stock price keeps decreasing.

No profit can be made.

---

## 🚀 Optimal Approach (Greedy)

Traverse the array only once.

Maintain two variables:

- `buy` → Lowest stock price seen so far.
- `profit` → Maximum profit obtained so far.

For every price:

- If the current price is smaller than `buy`, update `buy`.
- Otherwise, calculate the profit if we sell today.
- Update `profit` whenever a larger profit is found.

Since we always buy at the lowest price seen before the current day, every possible valid transaction is considered.

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

            } else if (prices[i] - buy > profit) {

                profit = prices[i] - buy;
            }
        }

        return profit;
    }
}
```

---

## ⏱️ Complexity Analysis

**Time Complexity:** `O(n)`

- The array is traversed exactly once.

**Space Complexity:** `O(1)`

- Only two extra variables are used.

---

## 🔒 Constraints

- `1 ≤ prices.length ≤ 10⁵`
- `0 ≤ prices[i] ≤ 10⁴`

---

## 🌟 Key Points

- Uses a Greedy approach.
- Maintains the minimum buying price seen so far.
- Updates the maximum profit while traversing.
- Traverses the array only once.
- Uses constant extra space.
- This is the optimal solution.

---

## ⭐ Alternative Solution (Brute Force)

Try every possible pair of buy and sell days.

For every day:

- Buy on day `i`.
- Sell on every later day `j`.
- Keep track of the maximum profit.

---

### 💻 Java Solution

```java
class Solution {

    public int maxProfit(int[] prices) {

        int profit = 0;

        for (int i = 0; i < prices.length; i++) {

            for (int j = i + 1; j < prices.length; j++) {

                profit = Math.max(profit, prices[j] - prices[i]);
            }
        }

        return profit;
    }
}
```

---

### ⏱️ Complexity Analysis

**Time Complexity:** `O(n²)`

- Every pair of buy and sell days is checked.

**Space Complexity:** `O(1)`

---

### 🌟 Key Points

- Easy to understand.
- Checks every possible transaction.
- Too slow for large inputs.
- Not suitable for interviews.

---

## 💡 Why Does the Greedy Approach Work?

The profit depends on two values:

```text
Selling Price - Buying Price
```

To maximize the profit:

- We should always buy at the **lowest price seen so far**.
- For every day, we check whether selling today gives a better profit than any previous transaction.

Example:

```text
prices = [7,1,5,3,6,4]
```

| Day | Price | Buy | Profit |
|-----|------:|----:|-------:|
|1|7|7|0|
|2|1|1|0|
|3|5|1|4|
|4|3|1|4|
|5|6|1|5|
|6|4|1|5|

Final Answer

```text
5
```

Since every price is compared with the minimum price before it, no profitable transaction is missed.

---

## ⚠️ Common Mistakes

- Updating the profit before updating the minimum buying price.
- Buying after selling (the buy day must come before the sell day).
- Returning a negative profit instead of `0`.
- Initializing `buy` with `0` instead of the first day's price.
- Using the brute-force solution (`O(n²)`) when an `O(n)` solution is expected.
