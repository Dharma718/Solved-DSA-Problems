# 🟦 Nth Fibonacci Number

## 📌 Problem Statement

Given an integer `n`, find the **nth Fibonacci number**.

The Fibonacci sequence is defined as:

```text
F(0) = 0
F(1) = 1
```

For every `n > 1`:

```text
F(n) = F(n - 1) + F(n - 2)
```

### Example

```text
Input:
5

Output:
5
```

The Fibonacci sequence starts as:

```text
0, 1, 1, 2, 3, 5, 8, 13, ...
```

Therefore:

```text
F(5) = 5
```

---

# 💡 My Approach

My approach uses **recursion** to calculate the nth Fibonacci number.

The main idea is to directly follow the mathematical definition of the Fibonacci sequence:

```text
F(n) = F(n - 1) + F(n - 2)
```

For every value of `n` greater than `1`, I recursively calculate the previous two Fibonacci numbers and add them.

The important part of my implementation is:

```text
int first = fibanocci(n - 1);
int last = fibanocci(n - 2);

return first + last;
```

The recursive function keeps breaking the problem into two smaller Fibonacci problems until it reaches the base cases.

---

# 🧠 Key Observation

The Fibonacci sequence has two base cases:

```text
F(0) = 0
F(1) = 1
```

Therefore, when:

```text
n <= 1
```

the function can directly return `n`.

```text
if(n <= 1){
    return n;
}
```

For every other value:

```text
F(n) = F(n - 1) + F(n - 2)
```

For example, to calculate:

```text
F(5)
```

the function breaks it down as:

```text
F(5)
   ↓
F(4) + F(3)
   ↓
(F(3) + F(2)) + (F(2) + F(1))
   ↓
...
```

Eventually, every recursive call reaches either:

```text
F(0)
```

or:

```text
F(1)
```

and the results are combined while the recursive calls return.

---

# 🔍 Step-by-Step Explanation

## 1. Define the Recursive Function

```text
public static int fibanocci(int n)
```

The function takes `n` and returns the nth Fibonacci number.

---

## 2. Handle the Base Cases

```text
if(n <= 1){
    return n;
}
```

There are two base cases:

```text
n = 0 → return 0
n = 1 → return 1
```

These values stop the recursion.

For example:

```text
fibanocci(0) → 0
fibanocci(1) → 1
```

---

## 3. Calculate the First Previous Fibonacci Number

```text
int first = fibanocci(n - 1);
```

This recursively calculates:

```text
F(n - 1)
```

For example:

```text
fibanocci(5)
```

first calculates:

```text
fibanocci(4)
```

---

## 4. Calculate the Second Previous Fibonacci Number

```text
int last = fibanocci(n - 2);
```

This recursively calculates:

```text
F(n - 2)
```

For example:

```text
fibanocci(5)
```

also calculates:

```text
fibanocci(3)
```

---

## 5. Add the Two Results

```text
return first + last;
```

The two previous Fibonacci values are added according to the Fibonacci definition:

```text
F(n) = F(n - 1) + F(n - 2)
```

---

## 6. Read the Input

```text
Scanner sc = new Scanner(System.in);
int n = sc.nextInt();
```

The program reads the value of `n` from the input.

---

## 7. Print the Result

```text
System.out.print(fibanocci(n));
```

The recursive Fibonacci function is called with the given value of `n`, and the result is printed.

---

# 🧪 Dry Run

Consider:

```text
n = 5
```

The function starts with:

```text
fibanocci(5)
```

Since `5 > 1`, it calculates:

```text
fibanocci(4) + fibanocci(3)
```

Now:

```text
fibanocci(4)
```

becomes:

```text
fibanocci(3) + fibanocci(2)
```

And:

```text
fibanocci(3)
```

becomes:

```text
fibanocci(2) + fibanocci(1)
```

The recursive calls eventually reach the base cases.

The calculation can be represented as:

```text
F(5)
├── F(4)
│   ├── F(3)
│   │   ├── F(2)
│   │   │   ├── F(1) → 1
│   │   │   └── F(0) → 0
│   │   └── F(1) → 1
│   └── F(2)
│       ├── F(1) → 1
│       └── F(0) → 0
└── F(3)
    ├── F(2)
    │   ├── F(1) → 1
    │   └── F(0) → 0
    └── F(1) → 1
```

Now the results are combined:

```text
F(2) = 1 + 0 = 1

F(3) = 1 + 1 = 2

F(4) = 2 + 1 = 3

F(5) = 3 + 2 = 5
```

Therefore:

```text
Output:
5
```

---

# 📊 Recursive Flow

For `n = 5`, the recursive calculation follows:

```text
F(5)
 ↓
F(4) + F(3)
 ↓
(F(3) + F(2)) + (F(2) + F(1))
 ↓
Base cases
 ↓
Combine results
 ↓
F(5) = 5
```

The important pattern is:

```text
One problem
    ↓
Two smaller problems
    ↓
More smaller problems
    ↓
Base cases
    ↓
Combine results
```

---

# 💻 Solution

```java
import java.util.*;

public class Solution {

    public static int fibanocci(int n) {
        if (n <= 1) {
            return n;
        }

        int first = fibanocci(n - 1);
        int last = fibanocci(n - 2);

        return first + last;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        System.out.print(fibanocci(n));
    }
}
```

---

# ⚙️ Complexity Analysis

### Time Complexity

```text
O(2^n)
```

At every non-base recursive call, the function makes two additional recursive calls:

```text
fibanocci(n - 1)
fibanocci(n - 2)
```

This creates a recursive tree with exponentially many repeated calculations.

Therefore, the time complexity is:

```text
Time = O(2^n)
```

---

### Space Complexity

```text
O(n)
```

The maximum depth of the recursive call stack is `n`.

Therefore, the auxiliary space used by the recursion is:

```text
Space = O(n)
```

---

# ✅ Approach Evaluation

This is a **correct recursive approach** that directly follows the mathematical definition of the Fibonacci sequence.

The strongest part of the approach is its simplicity:

```text
F(n) = F(n - 1) + F(n - 2)
```

However, the same Fibonacci values are calculated repeatedly.

For example, while calculating:

```text
F(5)
```

`F(3)` and `F(2)` are calculated multiple times.

Therefore, although the approach is correct and easy to understand, it is **not the most time-efficient approach** for larger values of `n`.

The recursive structure is:

```text
F(n)
 ↓
F(n - 1) + F(n - 2)
 ↓
Repeated recursive calculations
 ↓
Base cases
 ↓
Combine results
```

This makes it a useful approach for understanding **recursion and the Fibonacci recurrence**, but it has exponential time complexity because of repeated calculations.

---

# 📌 Key Takeaways

* The Fibonacci sequence starts with `0` and `1`.
* Each Fibonacci number is the sum of the previous two numbers.
* The solution uses recursion to directly implement the Fibonacci recurrence.
* `n <= 1` acts as the base case.
* Every other value is calculated using `F(n - 1) + F(n - 2)`.
* The approach is simple and closely follows the mathematical definition.
* The same Fibonacci values are recalculated multiple times.
* Time complexity is `O(2^n)`.
* Space complexity is `O(n)` because of the recursive call stack.
* This approach demonstrates the basic recursive structure of the Fibonacci problem.

---

# 🔗 Problem Source

**Platform:** Code360

**Problem:** [Nth Fibonacci Number](https://www.naukri.com/code360/problems/nth-fibonacci-number_74156)

---

**Part of the** [**Solved DSA Problems**](https://github.com/Dharma718/Solved-DSA-Problems) **repository.**

