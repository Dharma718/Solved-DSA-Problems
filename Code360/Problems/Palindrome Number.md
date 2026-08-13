# 🟦 Palindrome Number

## 📌 Problem Statement

Given an integer `n`, determine whether the number is a **palindrome**.

A palindrome number reads the same from left to right and right to left.

### Example 1

```text
n = 121
```

Reversed:

```text
121
```

Therefore:

```text
true
```

### Example 2

```text
n = 123
```

Reversed:

```text
321
```

Therefore:

```text
false
```

---

# 💡 My Approach

My approach reverses the digits of the given number and then compares the reversed number with the original number.

First, I store the original value:

```java
int original = n;
```

This is necessary because `n` will be modified while extracting its digits.

Then I construct the reverse using:

```text
digit = n % 10
reverse = reverse * 10 + digit
n = n / 10
```

After all digits have been processed, I compare:

```text
reverse == original
```

If both values are equal, the number is a palindrome.

---

# 🧠 Key Observation

The main observation is that the last digit of a number can be obtained using:

```text
n % 10
```

and the last digit can be removed using:

```text
n / 10
```

For example, consider:

```text
n = 121
```

The digits are extracted from right to left:

```text
121 → 1
12  → 2
1   → 1
```

These digits are then used to construct:

```text
121
```

which is the reverse of the original number.

---

# 🔍 Step-by-Step Explanation

## 1. Store the Original Number

```java
int original = n;
```

The variable `n` will be changed during the reversal process, so the original value must be preserved.

---

## 2. Initialize the Reverse

```java
int reverse = 0;
```

This variable stores the reversed number as the digits are extracted.

---

## 3. Extract the Last Digit

```java
int digit = n % 10;
```

The modulo operator gives the last digit.

For example:

```text
121 % 10 = 1
```

---

## 4. Add the Digit to the Reverse

```java
reverse = reverse * 10 + digit;
```

Multiplying the current reverse by `10` shifts its digits to the left, allowing the newly extracted digit to be added at the end.

---

## 5. Remove the Last Digit

```java
n /= 10;
```

Integer division by `10` removes the last digit.

For example:

```text
121 → 12
12  → 1
1   → 0
```

The process continues until `n` becomes `0`.

---

# 🧪 Dry Run

Consider:

```text
n = 121
```

Initially:

```text
original = 121
reverse = 0
```

### Iteration 1

```text
n = 121
digit = 121 % 10 = 1

reverse = 0 * 10 + 1
        = 1

n = 121 / 10
  = 12
```

State:

```text
original = 121
n        = 12
reverse  = 1
```

---

### Iteration 2

```text
n = 12
digit = 12 % 10 = 2

reverse = 1 * 10 + 2
        = 12

n = 12 / 10
  = 1
```

State:

```text
original = 121
n        = 1
reverse  = 12
```

---

### Iteration 3

```text
n = 1
digit = 1 % 10 = 1

reverse = 12 * 10 + 1
        = 121

n = 1 / 10
  = 0
```

The loop ends.

Now compare:

```text
reverse = 121
original = 121
```

Since:

```text
121 == 121
```

the result is:

```text
true
```

---

# 💻 Solution

```java
public class Solution {
    public static boolean palindromeNumber(int n) {
        int original = n;
        int reverse = 0;

        while (n > 0) {
            int digit = n % 10;
            reverse = reverse * 10 + digit;
            n /= 10;
        }

        return reverse == original;
    }
}
```

---

# ⚙️ Complexity Analysis

### Time Complexity

```text
O(log n)
```

The number of iterations depends on the number of digits in `n`.

If `n` contains `d` digits, the loop runs `d` times.

Since the number of digits is proportional to `log n`:

```text
Time = O(log n)
```

### Space Complexity

```text
O(1)
```

Only a fixed number of variables are used:

* `original`
* `reverse`
* `digit`

No additional data structure is required.

```text
Space = O(1)
```

---

# ✅ Approach Evaluation

This is a **correct and efficient approach** for checking a palindrome number.

The solution does not convert the number into a string or use an additional data structure. Instead, it performs the reversal directly using arithmetic operations.

The core process is:

```text
Extract last digit
        ↓
Add digit to reverse
        ↓
Remove last digit
        ↓
Repeat
        ↓
Compare reverse with original
```

This provides an efficient constant-space solution.

---

# 📌 Key Takeaways

* Store the original number before modifying `n`.
* `% 10` extracts the last digit.
* `/ 10` removes the last digit.
* `reverse * 10 + digit` builds the reversed number.
* Compare the reversed number with the original.
* Equal values indicate a palindrome.
* Time complexity is `O(log n)`.
* Space complexity is `O(1)`.

---

# 🔗 Problem Source

**Platform:** Code360

**Problem:** Palindrome Number

[**View Problem on Code360 →**](https://www.naukri.com/code360/problems/palindrome-number_624662)

---

**Part of the [Solved DSA Problems](https://github.com/Dharma718/Solved-DSA-Problems) repository.**

