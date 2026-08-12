# 🟨 Count Primes

## 📌 Problem Statement

Given an integer `n`, return the number of prime numbers that are **strictly less than `n`**.

A prime number is a natural number greater than `1` that has exactly two positive divisors:

* `1`
* Itself

### Example

For:

```text
n = 10
```

The prime numbers strictly less than `10` are:

```text
2, 3, 5, 7
```

Therefore:

```text
Output = 4
```

---

# 💡 My Approach

My approach uses the **Sieve of Eratosthenes**.

The main idea is to maintain a boolean array where:

```text
true  → potentially prime
false → not prime
```

I first mark every number from `2` to `n - 1` as `true`.

Then, for every number `i` starting from `2`, if it is still marked as prime, I mark all of its multiples as `false`.

The multiples start from:

```text
i * i
```

because smaller multiples would already have been marked by smaller prime numbers.

Finally, I traverse the array and count all positions that are still marked `true`.

---

# 🧠 Key Observation

The important observation is that if `i` is prime, then all multiples of `i` greater than or equal to `i²` cannot be prime.

For example, for:

```text
i = 2
```

we eliminate:

```text
4, 6, 8, 10, ...
```

For:

```text
i = 3
```

we eliminate:

```text
9, 12, 15, ...
```

For:

```text
i = 5
```

we start from:

```text
25
```

because smaller multiples of `5` have already been handled by smaller prime factors.

This is the core idea behind the Sieve of Eratosthenes.

---

# 🔍 Step-by-Step Explanation

## 1. Handle Small Values

```java
if (n <= 2) {
    return 0;
}
```

There are no prime numbers strictly less than `2`.

Therefore, when `n <= 2`, the answer is immediately `0`.

---

## 2. Create the Boolean Array

```java
boolean[] res = new boolean[n];
```

The array has indices:

```text
0 → n - 1
```

Each index represents the corresponding number.

For example, if:

```text
n = 10
```

then:

```text
res[2]
```

represents the number `2`.

---

## 3. Initially Mark Numbers as Prime

```java
for (int i = 2; i < n; i++) {
    res[i] = true;
}
```

Every number from `2` to `n - 1` is initially considered potentially prime.

At this point:

```text
2 → true
3 → true
4 → true
5 → true
...
9 → true
```

Composite numbers will be eliminated in the next step.

---

# 🔢 4. Eliminate Composite Numbers

The main sieve loop is:

```java
for (int i = 2; i * i <= n; i++) {
```

For each `i`, we check whether it is still marked as prime:

```java
if (res[i]) {
```

If it is prime, we mark its multiples as non-prime.

```java
for (int j = i * i; j < n; j += i) {
    res[j] = false;
}
```

---

# 🧠 Why Start from `i * i`?

Suppose:

```text
i = 5
```

Its multiples are:

```text
10, 15, 20, 25, 30, ...
```

But:

```text
10 = 2 × 5
15 = 3 × 5
20 = 4 × 5
```

These numbers have already been identified as composite when processing smaller numbers.

The first multiple that necessarily needs to be newly considered is:

```text
5 × 5 = 25
```

Therefore, starting from:

```text
i * i
```

avoids unnecessary repeated work.

---

# 🔢 Why `i * i <= n`?

The sieve only needs to process possible prime factors up to approximately the square root of `n`.

If a composite number has a factor larger than its square root, it must also have a corresponding factor smaller than its square root.

Therefore, once:

```text
i * i > n
```

there is no need to continue eliminating multiples.

---

# 🔢 5. Count the Remaining Prime Numbers

After all composite numbers have been marked:

```java
int count = 0;

for (int i = 2; i < n; i++) {
    if (res[i]) {
        count++;
    }
}
```

Every remaining `true` position represents a prime number.

The final count is returned:

```java
return count;
```

---

# 🧪 Dry Run

Consider:

```text
n = 10
```

Initially, numbers `2` through `9` are marked `true`:

```text
2  3  4  5  6  7  8  9
T  T  T  T  T  T  T  T
```

### Process `i = 2`

`2` is still marked as prime.

Start from:

```text
2 × 2 = 4
```

Mark multiples of `2` as false:

```text
4, 6, 8
```

Now:

```text
2  3  4  5  6  7  8  9
T  T  F  T  F  T  F  T
```

---

### Process `i = 3`

`3` is still marked as prime.

Start from:

```text
3 × 3 = 9
```

Mark:

```text
9 → false
```

Now:

```text
2  3  4  5  6  7  8  9
T  T  F  T  F  T  F  F
```

---

### Remaining `true` Values

The numbers still marked as `true` are:

```text
2, 3, 5, 7
```

Therefore:

```text
count = 4
```

### Final Answer

```text
4
```

---

# 💻 Solution

```java
class Solution {
    public int countPrimes(int n) {
        if (n <= 2) {
            return 0;
        }

        boolean[] res = new boolean[n];

        for (int i = 2; i < n; i++) {
            res[i] = true;
        }

        for (int i = 2; i * i <= n; i++) {
            if (res[i]) {
                for (int j = i * i; j < n; j += i) {
                    res[j] = false;
                }
            }
        }

        int count = 0;

        for (int i = 2; i < n; i++) {
            if (res[i]) {
                count++;
            }
        }

        return count;
    }
}
```

---

# ⚙️ Complexity Analysis

### Time Complexity

```text
O(n log log n)
```

The Sieve of Eratosthenes efficiently eliminates composite numbers by processing the multiples of prime numbers.

Therefore, the overall time complexity is:

```text
Time = O(n log log n)
```

### Space Complexity

```text
O(n)
```

The boolean array:

```java
boolean[] res = new boolean[n];
```

requires space proportional to `n`.

Therefore:

```text
Space = O(n)
```

---

# ✅ Approach Evaluation

This is a **correct and efficient approach** for the problem.

The main technique used is the **Sieve of Eratosthenes**, which is significantly more efficient for counting all primes below `n` than individually checking every number for primality.

The important ideas in the implementation are:

```text
Mark candidates as prime
        ↓
Find an unmarked prime
        ↓
Mark its multiples as composite
        ↓
Start marking from i²
        ↓
Count the remaining prime numbers
```

The boolean array provides a simple way to keep track of which numbers are still considered prime.

---

# 📌 Key Takeaways

* The problem asks for primes **strictly less than `n`**.
* A boolean array is used to track prime candidates.
* Numbers from `2` to `n - 1` are initially marked `true`.
* Composite numbers are eliminated using their prime factors.
* Multiples are marked starting from `i * i`.
* Only values up to the square-root range need to be used as sieve bases.
* Remaining `true` values represent prime numbers.
* Time complexity is `O(n log log n)`.
* Space complexity is `O(n)`.

---

# 🔗 Problem Source

**Platform:** LeetCode

**Problem:** Count Primes

[**View Problem on LeetCode →**](https://leetcode.com/problems/count-primes/)

---

**Part of the [Solved DSA Problems](https://github.com/Dharma718/Solved-DSA-Problems) repository.**

