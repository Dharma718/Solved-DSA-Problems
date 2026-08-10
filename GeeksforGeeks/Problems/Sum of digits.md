# 🟩 Sum of Digits

## 📌 Problem Statement

Given a positive integer `n`, calculate and return the **sum of all its digits**.

For example, if:

```text
n = 1234
```

then:

```text
1 + 2 + 3 + 4 = 10
```

Therefore, the output is:

```text
10
```

---

# 💡 My Approach

My approach uses repeated **digit extraction** to calculate the sum.

For every iteration:

1. Extract the last digit using `% 10`.
2. Add that digit to `sum`.
3. Remove the last digit using `/ 10`.
4. Continue until the number becomes `0`.

The two important operations are:

```text
n % 10
```

and:

```text
n / 10
```

### Extracting the Last Digit

The expression:

```text
n % 10
```

returns the last digit of `n`.

For example:

```text
1234 % 10 = 4
```

### Removing the Last Digit

The expression:

```text
n / 10
```

removes the last digit when integer division is used.

For example:

```text
1234 / 10 = 123
```

This allows the number to be processed digit by digit.

---

# 🔍 Step-by-Step Explanation

First, initialize the sum:

```java id="b9f7m4"
int sum = 0;
```

This variable stores the sum of the digits processed so far.

Next, continue processing while the number is greater than `0`:

```java id="q8v2c6"
while (n > 0)
```

Inside the loop, extract the last digit:

```java id="m3x7k1"
int first = n % 10;
```

For example, if:

```text
n = 1234
```

then:

```text
first = 4
```

Add the extracted digit to the sum:

```java id="r5d8p2"
sum += first;
```

Then remove the last digit:

```java id="z6h4n9"
n = n / 10;
```

The process continues until all digits have been processed.

Finally, return the calculated sum:

```java id="w2k7s5"
return sum;
```

---

# 🧪 Dry Run

Consider:

```text id="k4p8x2"
n = 1234
```

Initially:

```text id="m7q3r9"
sum = 0
```

### Iteration 1

```text id="f3n8y1"
n = 1234
```

Extract last digit:

```text id="x5m2v7"
1234 % 10 = 4
```

Update sum:

```text id="c8j4q6"
sum = 0 + 4 = 4
```

Remove last digit:

```text id="p2w7k3"
1234 / 10 = 123
```

---

### Iteration 2

```text id="z4r8m1"
n = 123
```

Extract:

```text id="v7c3x5"
123 % 10 = 3
```

Update:

```text id="q9n2b6"
sum = 4 + 3 = 7
```

Remove:

```text id="h5k8p2"
123 / 10 = 12
```

---

### Iteration 3

```text id="a7m4x9"
n = 12
```

Extract:

```text id="j3q6v8"
12 % 10 = 2
```

Update:

```text id="p8r2c4"
sum = 7 + 2 = 9
```

Remove:

```text id="y6n1k5"
12 / 10 = 1
```

---

### Iteration 4

```text id="s4v8m2"
n = 1
```

Extract:

```text id="c7p3x9"
1 % 10 = 1
```

Update:

```text id="n5q2r8"
sum = 9 + 1 = 10
```

Remove:

```text id="k4m7v1"
1 / 10 = 0
```

The loop stops because:

```text id="x8p3c6"
n > 0
```

is now false.

### Final Result

```text id="r6y2m9"
sum = 10
```

Therefore:

```text id="b3k7x5"
Output = 10
```

---

# 💻 Solution

```java id="q8m4v2"
class Solution {
    static int sumOfDigits(int n) {
        int sum = 0;

        while (n > 0) {
            int first = n % 10;
            sum += first;
            n = n / 10;
        }

        return sum;
    }
}
```

---

# ⚙️ Complexity Analysis

Let `d` be the number of digits in `n`.

### Time Complexity

```text id="v5n8q2"
O(d)
```

The loop processes each digit exactly once.

Therefore, the time complexity is proportional to the number of digits in the number.

### Space Complexity

```text id="x3m7k9"
O(1)
```

Only a few variables are used, regardless of the number of digits.

Therefore, the solution uses constant extra space.

---

# ✅ Approach Evaluation

This is a **correct and efficient approach** for calculating the sum of digits.

The solution processes each digit exactly once and uses the standard arithmetic operations:

```text
% 10 → Extract the last digit
/ 10 → Remove the last digit
```

There is no unnecessary traversal or additional data structure.

For a number containing `d` digits:

```text
Time  → O(d)
Space → O(1)
```

This makes the approach efficient and straightforward.

---

# 📌 Key Takeaways

* `% 10` extracts the last digit.
* `/ 10` removes the last digit.
* A running variable `sum` stores the accumulated digit sum.
* Every digit is processed exactly once.
* No additional data structure is required.
* Time complexity is `O(d)`, where `d` is the number of digits.
* Space complexity is `O(1)`.

---

# 🔗 Problem Source

**Platform:** GeeksforGeeks

**Problem:** Sum of Digits

[**View Problem on GeeksforGeeks →**](https://www.geeksforgeeks.org/problems/sum-of-digits1742/1)

---

**Part of the [Solved DSA Problems](https://github.com/Dharma718/Solved-DSA-Problems) repository.**

