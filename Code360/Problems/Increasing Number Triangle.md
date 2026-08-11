# 🟦 Increasing Number Triangle

## 📌 Problem Statement

Given an integer `n`, print an **Increasing Number Triangle** pattern.

The pattern contains `n` rows, where:

* Row `1` contains `1` number.
* Row `2` contains `2` numbers.
* Row `3` contains `3` numbers.
* Each subsequent row contains one more number than the previous row.
* The numbers increase continuously from `1` without resetting at the beginning of each row.

### Example

For:

```text
n = 5
```

the output is:

```text
1
2 3
4 5 6
7 8 9 10
11 12 13 14 15
```

---

# 💡 My Approach

My approach uses:

* One outer loop to control the rows.
* One inner loop to control the numbers printed in each row.
* A `count` variable to keep track of the next number to print.

I initialize:

```java
int count = 1;
```

The important part is that `count` is declared **outside both loops**.

Therefore, it does not reset when a new row begins.

After printing each number, I increment `count`:

```java
count++;
```

This allows the numbers to continue sequentially from one row to the next.

---

# 🧠 Key Observation

The number of elements in each row increases by one.

For:

```text
n = 5
```

the number of elements per row is:

```text
Row 1 → 1
Row 2 → 2
Row 3 → 3
Row 4 → 4
Row 5 → 5
```

At the same time, `count` continuously increases:

```text
1 → 2 → 3 → 4 → 5 → ...
```

The `count` variable is therefore responsible for maintaining the continuous sequence across all rows.

---

# 🔍 Step-by-Step Explanation

First, initialize the counter:

```java
int count = 1;
```

This means the first number printed will be `1`.

---

## 1. Outer Loop

```java
for (int i = 1; i <= n; i++)
```

The outer loop controls the number of rows.

For example, if:

```text
n = 5
```

then:

```text
i = 1
i = 2
i = 3
i = 4
i = 5
```

Five rows are produced.

---

## 2. Inner Loop

```java
for (int j = 1; j <= i; j++)
```

The inner loop determines how many numbers are printed in the current row.

Therefore:

```text
i = 1 → 1 number
i = 2 → 2 numbers
i = 3 → 3 numbers
i = 4 → 4 numbers
i = 5 → 5 numbers
```

---

## 3. Print the Current Number

Inside the inner loop:

```java
System.out.print(count + " ");
```

The current value of `count` is printed.

Then:

```java
count++;
```

increments the counter so that the next position receives the next number.

---

# 🧪 Dry Run

Consider:

```text
n = 4
```

Initially:

```text
count = 1
```

### Row 1

```text
i = 1
```

The inner loop runs once.

Print:

```text
count = 1
```

Then increment:

```text
count = 2
```

Output:

```text
1
```

---

### Row 2

```text
i = 2
```

The inner loop runs twice.

First iteration:

```text
count = 2
```

Print `2`, then:

```text
count = 3
```

Second iteration:

```text
count = 3
```

Print `3`, then:

```text
count = 4
```

Output:

```text
2 3
```

---

### Row 3

```text
i = 3
```

The inner loop runs three times.

```text
count = 4 → print 4
count = 5 → print 5
count = 6 → print 6
```

After the row:

```text
count = 7
```

Output:

```text
4 5 6
```

---

### Row 4

```text
i = 4
```

The inner loop runs four times.

```text
count = 7  → print 7
count = 8  → print 8
count = 9  → print 9
count = 10 → print 10
```

Final:

```text
count = 11
```

Output:

```text
7 8 9 10
```

### Final Pattern

```text
1
2 3
4 5 6
7 8 9 10
```

---

# 💻 Solution

```java
public class Solution {
    public static void nNumberTriangle(int n) {
        int count = 1;

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= i; j++) {
                System.out.print(count + " ");
                count++;
            }

            System.out.println();
        }
    }
}
```

---

# ⚙️ Complexity Analysis

### Time Complexity

```text
O(n²)
```

The first row prints `1` number, the second prints `2`, the third prints `3`, and so on.

The total number of printed elements is:

```text
1 + 2 + 3 + ... + n
```

Therefore, the total work grows quadratically:

```text
Time = O(n²)
```

### Space Complexity

```text
O(1)
```

The solution only uses a few variables:

* `count`
* `i`
* `j`

No additional data structure is used.

Therefore:

```text
Space = O(1)
```

---

# ✅ Approach Evaluation

This is a **correct and efficient approach** for the required pattern.

The main strength of the solution is the use of a single `count` variable outside the loops.

Because `count` is not reset after each row, the sequence continues naturally:

```text
1
↓
2 3
↓
4 5 6
↓
7 8 9 10
```

The implementation directly matches the structure of the required pattern and does not require any additional data structures.

---

# 📌 Key Takeaways

* The outer loop controls the rows.
* The inner loop prints `i` numbers in row `i`.
* `count` starts from `1`.
* `count` is maintained across all rows.
* `count++` ensures every printed number is followed by the next number.
* The sequence never resets at the beginning of a new row.
* Time complexity is `O(n²)`.
* Space complexity is `O(1)`.

---

# 🔗 Problem Source

**Platform:** Code360

**Problem:** Increasing Number Triangle

[**View Problem on Code360 →**](https://www.naukri.com/code360/problems/increasing-number-triangle_6581893)

---

**Part of the [Solved DSA Problems](https://github.com/Dharma718/Solved-DSA-Problems) repository.**
