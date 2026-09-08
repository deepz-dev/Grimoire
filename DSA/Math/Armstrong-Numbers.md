## 📂 File Name

```text
Armstrong-Numbers.md
```

---

## 📁 Topic

```text
Maths → Basic Maths → Armstrong Number
```

---

## 📄 README.md

```md
# 🔢 Armstrong Number

## 🔗 Problem Link

<a href="https://www.geeksforgeeks.org/problems/armstrong-numbers2727/1" target="_blank">
GeeksforGeeks: Armstrong Numbers
</a>

---

## 🏷️ Tags

- Maths
- Basic Maths
- Number Theory
- Digit Manipulation

---

## 📊 Difficulty

Easy

---

## Problem Statement

Given a **3-digit number `n`**, check whether it is an **Armstrong number** or not.

An Armstrong number of three digits is a number where the **sum of the cubes of its digits is equal to the number itself**.

For example:

```text
371 = 3³ + 7³ + 1³
    = 27 + 343 + 1
    = 371
```

Therefore, `371` is an Armstrong number.

---

## ✨ Examples

### Example 1

```text
Input:
n = 153

Output:
true
```

Explanation:

```text
1³ + 5³ + 3³
= 1 + 125 + 27
= 153
```

So, `153` is an Armstrong number.

---

### Example 2

```text
Input:
n = 372

Output:
false
```

Explanation:

```text
3³ + 7³ + 2³
= 27 + 343 + 8
= 378
```

Since:

```text
378 != 372
```

`372` is not an Armstrong number.

---

### Example 3

```text
Input:
n = 100

Output:
false
```

Explanation:

```text
1³ + 0³ + 0³
= 1
```

Since:

```text
1 != 100
```

`100` is not an Armstrong number.

---

## 🚀 Approach

Use **digit extraction** to process every digit of the number.

### Step 1 — Store the Original Number

We need the original number at the end for comparison.

```java
int temp = n;
```

Because `n` will be modified while extracting its digits.

---

### Step 2 — Create a Result Variable

Use a variable to store the sum of the cubes of all digits.

```java
int res = 0;
```

---

### Step 3 — Extract Each Digit

Use:

```text
n % 10
```

to get the last digit.

For example:

```text
n = 153

153 % 10 = 3
```

So:

```java
int digit = n % 10;
```

---

### Step 4 — Add the Cube of the Digit

For a 3-digit Armstrong number, calculate:

```text
digit³
```

and add it to `res`.

```java
res += Math.pow(digit, 3);
```

---

### Step 5 — Remove the Last Digit

Use:

```text
n / 10
```

to remove the last digit.

```java
n /= 10;
```

Example:

```text
153 → 15 → 1 → 0
```

---

### Step 6 — Compare With Original Number

After processing all digits:

```java
return res == temp;
```

If the sum of cubes is equal to the original number, it is an Armstrong number.

---

## 🧠 Dry Run

For:

```text
n = 153
```

Initially:

```text
temp = 153
res = 0
```

### Iteration 1

```text
digit = 153 % 10 = 3

res = 0 + 3³
    = 27

n = 153 / 10
  = 15
```

### Iteration 2

```text
digit = 15 % 10 = 5

res = 27 + 5³
    = 152

n = 15 / 10
  = 1
```

### Iteration 3

```text
digit = 1 % 10 = 1

res = 152 + 1³
    = 153

n = 1 / 10
  = 0
```

Now:

```text
res == temp

153 == 153
```

Therefore:

```text
true
```

---

## 💻 Java Solution

```java
class Solution {
    static boolean armstrongNumber(int n) {
        // Step 1: Store the original number to compare later
        int temp = n;

        // Step 2: Variable to store the sum of the cubes of the digits
        int res = 0;

        // Step 3: Loop to process each digit of the number
        while (n != 0) {

            // Step 4: Get the last digit of the number
            int digit = n % 10;

            // Step 5: Add the cube of the digit to the result
            res += Math.pow(digit, 3);

            // Step 6: Remove the last digit from the number
            n /= 10;
        }

        // Step 7: Check if the sum of cubes is equal to the original number
        return res == temp;
    }
}
```

---

## ⏱️ Complexity Analysis

### Time Complexity

```text
O(d)
```

Where `d` is the number of digits.

For a 3-digit number:

```text
O(3) = O(1)
```

Each digit is processed exactly once.

### Space Complexity

```text
O(1)
```

Only a few variables are used.

---

## 🔒 Constraints

```text
100 ≤ n < 1000
```

The input is a **3-digit number**.

---

## 🌟 Key Points

- Store the original number before modifying `n`.
- Use `% 10` to extract the last digit.
- Use `/= 10` to remove the last digit.
- For a 3-digit Armstrong number, calculate the **cube** of every digit.
- Add all cubes into `res`.
- Finally compare:
  ```text
  res == original number
  ```
- If equal → Armstrong number.
- Otherwise → Not an Armstrong number.

---

## ⚠️ Common Mistakes

- Forgetting to store the original number before changing `n`.
- Using `n / 10` without assigning it back to `n`.
- Forgetting to cube each digit.
- Comparing `res` with the modified `n` instead of the original number.
- Confusing `% 10` and `/ 10`:
  ```text
  % 10 → get last digit
  / 10 → remove last digit
  ```

---

## 🎯 Interview Tip

> **Remember: Extract → Cube → Add → Remove → Compare**

```text
n % 10  → Get digit
digit³  → Cube
res +=  → Add
n /= 10 → Remove digit
res == temp → Check
```
```

---

## 📝 Commit Message

```text
feat(maths): add Armstrong number solution
```
