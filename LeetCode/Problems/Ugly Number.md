

# 🟪 Ugly Number

## 📌 Problem Statement

An **Ugly Number** is a positive integer whose prime factors are limited to:

```text
2, 3, 5
```

Given an integer `n`, determine whether `n` is an Ugly Number.

Return `true` if `n` is an Ugly Number; otherwise, return `false`.

### Example 1

```text
Input:
6

Output:
true
```

Because:

```text
6 = 2 × 3
```

Its prime factors are only `2` and `3`.

### Example 2

```text
Input:
14

Output:
false
```

Because:

```text
14 = 2 × 7
```

The prime factor `7` is not allowed.

---

# 💡 My Approach

My approach repeatedly divides the given number by the allowed prime factors:

```text
2, 3, 5
```

The main idea is to completely remove every occurrence of these three factors from the number.

The process is:

```text
Remove all factors of 2
        ↓
Remove all factors of 3
        ↓
Remove all factors of 5
        ↓
Check the remaining value
```

If the remaining value becomes `1`, then the original number contains no prime factors other than `2`, `3`, and `5`.

Therefore, it is an Ugly Number.

The important part of my implementation is:

```text
while (n % 2 == 0)
while (n % 3 == 0)
while (n % 5 == 0)
```

Each loop continuously divides `n` by the corresponding allowed factor until that factor is completely removed.

---

# 🧠 Key Observation

An Ugly Number can be represented using only the prime factors:

```text
2, 3, 5
```

Therefore, if we repeatedly divide the number by `2`, `3`, and `5`, an Ugly Number should eventually become:

```text
1
```

For example:

```text
30
 ↓ /2
15
 ↓ /3
5
 ↓ /5
1
```

Therefore:

```text
30 → Ugly Number
```

Now consider:

```text
42
 ↓ /2
21
 ↓ /3
7
```

The remaining value is `7`.

Since `7` is not one of the allowed prime factors, it cannot be removed.

Therefore:

```text
42 → Not an Ugly Number
```

So the main observation is:

> **After removing all factors of `2`, `3`, and `5`, the remaining value must be `1` for the number to be an Ugly Number.**

---

# 🔍 Step-by-Step Explanation

## 1. Handle Non-Positive Numbers

```text
if (n <= 0) {
    return false;
}
```

An Ugly Number must be a **positive integer**.

Therefore, if `n` is `0` or negative, there is no need to perform any further calculations.

The answer is immediately:

```text
false
```

---

## 2. Remove Factors of 2

```text
while (n % 2 == 0) {
    n = n / 2;
}
```

The first loop checks whether `n` is divisible by `2`.

If it is divisible by `2`, we divide it by `2`.

This continues until `n` is no longer divisible by `2`.

For example:

```text
40
 ↓ /2
20
 ↓ /2
10
 ↓ /2
5
```

At this point, `5` is no longer divisible by `2`.

Therefore, all factors of `2` have been removed.

---

## 3. Remove Factors of 3

```text
while (n % 3 == 0) {
    n = n / 3;
}
```

After removing all factors of `2`, the next loop removes all factors of `3`.

For example:

```text
45
 ↓ /3
15
 ↓ /3
5
```

Now `5` is no longer divisible by `3`.

Therefore, all factors of `3` have been removed.

---

## 4. Remove Factors of 5

```text
while (n % 5 == 0) {
    n = n / 5;
}
```

Finally, the solution removes all factors of `5`.

For example:

```text
125
 ↓ /5
25
 ↓ /5
5
 ↓ /5
1
```

Now all possible factors of `5` have been removed.

---

## 5. Check the Remaining Value

After removing all possible factors of `2`, `3`, and `5`, the solution performs:

```text
return n == 1;
```

If:

```text
n == 1
```

then the original number contained only the allowed prime factors.

Therefore:

```text
true
```

If:

```text
n != 1
```

then some other factor remains.

Therefore:

```text
false
```

---

# 🧪 Dry Run

Consider:

```text
n = 60
```

Initially:

```text
n = 60
```

---

### Step 1 — Remove Factors of 2

Check:

```text
60 % 2 == 0
```

Divide:

```text
60 / 2 = 30
```

Again:

```text
30 % 2 == 0
```

Divide:

```text
30 / 2 = 15
```

Now:

```text
15 % 2 != 0
```

So the first loop stops.

Current value:

```text
n = 15
```

---

### Step 2 — Remove Factors of 3

Check:

```text
15 % 3 == 0
```

Divide:

```text
15 / 3 = 5
```

Now:

```text
5 % 3 != 0
```

So the second loop stops.

Current value:

```text
n = 5
```

---

### Step 3 — Remove Factors of 5

Check:

```text
5 % 5 == 0
```

Divide:

```text
5 / 5 = 1
```

Now:

```text
1 % 5 != 0
```

The third loop stops.

Current value:

```text
n = 1
```

---

### Step 4 — Final Check

The solution returns:

```text
n == 1
```

Since:

```text
1 == 1
```

the result is:

```text
true
```

Therefore:

```text
60 → Ugly Number
```

---

# 🧪 Another Example

Consider:

```text
n = 14
```

---

### Remove Factors of 2

```text
14 % 2 == 0
```

Divide:

```text
14 / 2 = 7
```

Now:

```text
n = 7
```

---

### Remove Factors of 3

```text
7 % 3 != 0
```

No division occurs.

---

### Remove Factors of 5

```text
7 % 5 != 0
```

No division occurs.

---

### Final Check

The remaining value is:

```text
n = 7
```

Therefore:

```text
n == 1
```

is false.

So:

```text
14 → Not an Ugly Number
```

---

# 📊 Value Progress

For:

```text
n = 60
```

the value changes as:

```text
60
 ↓ /2
30
 ↓ /2
15
 ↓ /3
5
 ↓ /5
1
```

For:

```text
n = 14
```

the value changes as:

```text
14
 ↓ /2
7
```

Since `7` remains, the number is not an Ugly Number.

---

# 💻 Solution

```java
class Solution {
    public boolean isUgly(int n) {
        if (n <= 0) {
            return false;
        }

        while (n % 2 == 0) {
            n = n / 2;
        }

        while (n % 3 == 0) {
            n = n / 3;
        }

        while (n % 5 == 0) {
            n = n / 5;
        }

        return n == 1;
    }
}
```

---

# ⚙️ Complexity Analysis

### Time Complexity

```text
O(log n)
```

Each division reduces the value of `n` by a constant factor.

Therefore, the number of divisions performed is logarithmic with respect to the original value of `n`.

```text
Time = O(log n)
```

---

### Space Complexity

The solution does not use any additional data structure.

Only a constant amount of memory is required for the variables used in the calculation.

```text
Space = O(1)
```

---

# ✅ Approach Evaluation

This is a **correct and efficient approach** for solving the problem.

The approach directly uses the definition of an Ugly Number instead of explicitly finding all prime factors.

The solution removes the only allowed prime factors:

```text
2, 3, 5
```

and then checks whether anything other than `1` remains.

The complete process is:

```text
Original Number
      ↓
Remove factors of 2
      ↓
Remove factors of 3
      ↓
Remove factors of 5
      ↓
Check remaining value
      ↓
     Is 1?
    ↙     ↘
  Yes      No
   ↓        ↓
 true     false
```

This is an efficient approach because it does not require storing the factors, generating prime numbers, or using any additional data structure.

---

# 📌 Key Takeaways

* An Ugly Number is a positive integer whose prime factors are only `2`, `3`, and `5`.
* Non-positive numbers are immediately rejected.
* All factors of `2` are removed first.
* All factors of `3` are then removed.
* All factors of `5` are finally removed.
* If the remaining value is `1`, the number is an Ugly Number.
* If another value remains, it contains an unwanted prime factor.
* The solution works directly on the given number.
* Time complexity is `O(log n)`.
* Space complexity is `O(1)`.
* The approach is correct and efficient.

---

# 🔗 Problem Source

**Platform:** LeetCode

**Problem:** [Ugly Number](https://leetcode.com/problems/ugly-number/description/)

---

**Part of the** [**Solved DSA Problems**](https://github.com/Dharma718/Solved-DSA-Problems) **repository.**

