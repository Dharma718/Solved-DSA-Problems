# 🟦 Generate Fibonacci Numbers

## 📌 Problem Statement

Given an integer `n`, generate the first `n` Fibonacci numbers and return them in an array.

The Fibonacci sequence starts with:

```text
0, 1
```

Every subsequent Fibonacci number is calculated as:

```text
F(n) = F(n - 1) + F(n - 2)
```

### Example

```text
Input:
5

Output:
[0, 1, 1, 2, 3]
```

The first five Fibonacci numbers are:

```text
0, 1, 1, 2, 3
```

---

# 💡 My Approach

My approach uses an **iterative Dynamic Programming-style approach** by storing the Fibonacci numbers in an array.

Instead of calculating each Fibonacci number recursively, I build the sequence from left to right.

The main idea is:

```text
Create an array of size n
        ↓
Set the first value to 0
        ↓
Set the second value to 1
        ↓
Calculate every next value
        ↓
Return the array
```

For every index from `2` onward:

```text
arr[i] = arr[i - 1] + arr[i - 2]
```

This uses the two previously calculated Fibonacci numbers to generate the next one.

---

# 🧠 Key Observation

Every Fibonacci number depends only on the previous two numbers.

For example:

```text
F(0) = 0
F(1) = 1

F(2) = F(1) + F(0)
     = 1 + 0
     = 1

F(3) = F(2) + F(1)
     = 1 + 1
     = 2

F(4) = F(3) + F(2)
     = 2 + 1
     = 3
```

Therefore, once the first two values are available, the remaining values can be generated iteratively.

The important part of my implementation is:

```text
arr[i] = arr[i - 1] + arr[i - 2];
```

This directly follows the Fibonacci definition.

---

# 🔍 Step-by-Step Explanation

## 1. Create the Result Array

```text
int[] arr = new int[n];
```

An integer array of size `n` is created to store the first `n` Fibonacci numbers.

For example, if:

```text
n = 5
```

the array initially contains:

```text
[0, 0, 0, 0, 0]
```

---

## 2. Set the First Fibonacci Number

```text
if(n >= 1){
    arr[0] = 0;
}
```

The Fibonacci sequence starts with:

```text
F(0) = 0
```

Therefore, if at least one Fibonacci number is required, the first position is set to `0`.

The array becomes:

```text
[0, 0, 0, 0, 0]
```

---

## 3. Set the Second Fibonacci Number

```text
if(n >= 2){
    arr[1] = 1;
}
```

The second Fibonacci number is:

```text
F(1) = 1
```

Therefore, when at least two numbers are required, the second position is set to `1`.

The array becomes:

```text
[0, 1, 0, 0, 0]
```

---

## 4. Generate the Remaining Fibonacci Numbers

```text
for(int i = 2; i < n; i++){
    arr[i] = arr[i - 1] + arr[i - 2];
}
```

The loop starts from index `2` because the first two Fibonacci numbers have already been initialized.

For every position:

```text
arr[i]
```

is calculated using:

```text
arr[i - 1]
```

and:

```text
arr[i - 2]
```

For example:

```text
arr[2] = arr[1] + arr[0]
       = 1 + 0
       = 1
```

Then:

```text
arr[3] = arr[2] + arr[1]
       = 1 + 1
       = 2
```

And:

```text
arr[4] = arr[3] + arr[2]
       = 2 + 1
       = 3
```

---

## 5. Return the Fibonacci Array

```text
return arr;
```

After all values have been generated, the completed array is returned.

For:

```text
n = 5
```

the final array is:

```text
[0, 1, 1, 2, 3]
```

---

# 🧪 Dry Run

Consider:

```text
n = 6
```

We need to generate:

```text
[0, 1, 1, 2, 3, 5]
```

---

### Step 1 — Create Array

```text
arr = [0, 0, 0, 0, 0, 0]
```

---

### Step 2 — Set `arr[0]`

```text
arr[0] = 0
```

Array:

```text
[0, 0, 0, 0, 0, 0]
```

---

### Step 3 — Set `arr[1]`

```text
arr[1] = 1
```

Array:

```text
[0, 1, 0, 0, 0, 0]
```

---

### Step 4 — `i = 2`

Calculate:

```text
arr[2] = arr[1] + arr[0]
       = 1 + 0
       = 1
```

Array:

```text
[0, 1, 1, 0, 0, 0]
```

---

### Step 5 — `i = 3`

Calculate:

```text
arr[3] = arr[2] + arr[1]
       = 1 + 1
       = 2
```

Array:

```text
[0, 1, 1, 2, 0, 0]
```

---

### Step 6 — `i = 4`

Calculate:

```text
arr[4] = arr[3] + arr[2]
       = 2 + 1
       = 3
```

Array:

```text
[0, 1, 1, 2, 3, 0]
```

---

### Step 7 — `i = 5`

Calculate:

```text
arr[5] = arr[4] + arr[3]
       = 3 + 2
       = 5
```

Final array:

```text
[0, 1, 1, 2, 3, 5]
```

Therefore, the output is:

```text
[0, 1, 1, 2, 3, 5]
```

---

# 📊 Array Progress

For:

```text
n = 6
```

the array develops as:

```text
Initial:
[0, 0, 0, 0, 0, 0]

After setting first value:
[0, 0, 0, 0, 0, 0]

After setting second value:
[0, 1, 0, 0, 0, 0]

After i = 2:
[0, 1, 1, 0, 0, 0]

After i = 3:
[0, 1, 1, 2, 0, 0]

After i = 4:
[0, 1, 1, 2, 3, 0]

After i = 5:
[0, 1, 1, 2, 3, 5]
```

The important pattern is:

```text
Previously calculated values
          ↓
Use previous two values
          ↓
Calculate next Fibonacci number
          ↓
Store it in the array
          ↓
Repeat
```

---

# 💻 Solution

```java
public class Solution {
    public static int[] generateFibonacciNumbers(int n) {
        int[] arr = new int[n];

        if (n >= 1) {
            arr[0] = 0;
        }

        if (n >= 2) {
            arr[1] = 1;
        }

        for (int i = 2; i < n; i++) {
            arr[i] = arr[i - 1] + arr[i - 2];
        }

        return arr;
    }
}
```

---

# ⚙️ Complexity Analysis

### Time Complexity

```text
O(n)
```

The loop runs from index `2` to `n - 1`.

Each Fibonacci number is calculated exactly once.

Therefore:

```text
Time = O(n)
```

---

### Space Complexity

```text
O(n)
```

The solution creates an array of size `n` to store all the Fibonacci numbers.

Therefore:

```text
Space = O(n)
```

The returned array itself requires `O(n)` space.

---

# ✅ Approach Evaluation

This is a **correct and efficient iterative approach** for generating the first `n` Fibonacci numbers.

Compared with the recursive Fibonacci approach, this method avoids repeatedly calculating the same Fibonacci values.

For example, instead of recursively calculating:

```text
F(n - 1)
F(n - 2)
```

and repeatedly recalculating smaller values, the solution stores the previously calculated results in the array and directly reuses them.

The overall process is:

```text
Initialize array
      ↓
Store 0
      ↓
Store 1
      ↓
Use previous two values
      ↓
Generate next value
      ↓
Store it
      ↓
Continue until n values are generated
```

The approach is therefore much more efficient for generating the complete Fibonacci sequence because every required value is calculated only once.

---

# 📌 Key Takeaways

* The Fibonacci sequence starts with `0` and `1`.
* Every next value is the sum of the previous two values.
* The solution stores the Fibonacci sequence in an array.
* The first two values are initialized separately.
* The remaining values are generated iteratively.
* Each Fibonacci number is calculated only once.
* The approach avoids the repeated calculations of naive recursion.
* Time complexity is `O(n)`.
* Space complexity is `O(n)` because the complete sequence is stored in an array.
* The approach is simple, iterative, and efficient for generating the required sequence.

---

# 🔗 Problem Source

**Platform:** Code360

**Problem:** [Generate Fibonacci Numbers](https://www.naukri.com/code360/guided-paths/core-python-essentials/content/498185/offering/7421617)

---

**Part of the** [**Solved DSA Problems**](https://github.com/Dharma718/Solved-DSA-Problems) **repository.**

