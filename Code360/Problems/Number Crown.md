# 🟥 Number Crown

## 📌 Problem Statement

Given an integer `n`, print a **Number Crown pattern** consisting of:

* An increasing sequence of numbers on the left
* A decreasing sequence of numbers on the right
* Spaces between the two sides
* The number of spaces decreasing as the row number increases

For each row `i`:

```text
1 2 3 ... i
```

is printed on the left, followed by the required spaces, and then:

```text
i ... 3 2 1
```

is printed on the right.

### Example

For:

```text
n = 4
```

the pattern is:

```text
1             1
1 2         2 1
1 2 3     3 2 1
1 2 3 4 4 3 2 1
```

---

# 💡 My Approach

My approach divides every row into **three parts**:

```text
Left Numbers → Spaces → Right Numbers
```

For every row `i`:

### 1. Print increasing numbers

The first loop prints numbers from `1` to `i`:

```text
1 2 3 ... i
```

### 2. Print the middle spaces

The second loop prints:

```text
2 * (n - i)
```

spaces.

As the row number increases, the number of spaces decreases.

### 3. Print decreasing numbers

The third loop prints numbers from `i` down to `1`:

```text
i ... 3 2 1
```

Finally, `System.out.println()` moves the output to the next row.

---

# 🔍 Step-by-Step Explanation

The outer loop controls the number of rows:

```java
for (int i = 1; i <= n; i++)
```

Since `i` starts from `1` and goes up to `n`, exactly `n` rows are printed.

---

## Part 1: Left Side

```java
for (int j = 1; j <= i; j++) {
    System.out.print(j + " ");
}
```

This prints numbers in increasing order.

For example:

```text
i = 1 → 1
i = 2 → 1 2
i = 3 → 1 2 3
i = 4 → 1 2 3 4
```

---

## Part 2: Middle Spaces

```java
for (int j = 1; j <= 2 * (n - i); j++) {
    System.out.print(" ");
}
```

The number of spaces depends on the current row.

For:

```text
n = 4
```

the calculation becomes:

```text
i = 1 → 2 * (4 - 1) = 6
i = 2 → 2 * (4 - 2) = 4
i = 3 → 2 * (4 - 3) = 2
i = 4 → 2 * (4 - 4) = 0
```

Therefore, the gap becomes smaller as we move downward.

---

## Part 3: Right Side

```java
for (int j = i; j >= 1; j--) {
    System.out.print(j + " ");
}
```

This prints the numbers in decreasing order.

For example:

```text
i = 1 → 1
i = 2 → 2 1
i = 3 → 3 2 1
i = 4 → 4 3 2 1
```

---

# 🧪 Dry Run

Consider:

```text
n = 4
```

### Row 1

```text
i = 1
```

Left side:

```text
1
```

Spaces:

```text
2 * (4 - 1) = 6
```

Right side:

```text
1
```

Result:

```text
1             1
```

---

### Row 2

```text
i = 2
```

Left side:

```text
1 2
```

Spaces:

```text
2 * (4 - 2) = 4
```

Right side:

```text
2 1
```

Result:

```text
1 2         2 1
```

---

### Row 3

```text
i = 3
```

Left side:

```text
1 2 3
```

Spaces:

```text
2 * (4 - 3) = 2
```

Right side:

```text
3 2 1
```

Result:

```text
1 2 3     3 2 1
```

---

### Row 4

```text
i = 4
```

Left side:

```text
1 2 3 4
```

Spaces:

```text
2 * (4 - 4) = 0
```

Right side:

```text
4 3 2 1
```

Result:

```text
1 2 3 4 4 3 2 1
```

---

# 💻 Solution

```java
public class Solution {
    public static void numberCrown(int n) {
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= i; j++) {
                System.out.print(j + " ");
            }

            for (int j = 1; j <= 2 * (n - i); j++) {
                System.out.print(" ");
            }

            for (int j = i; j >= 1; j--) {
                System.out.print(j + " ");
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

The outer loop runs `n` times.

For each row, the number of operations performed by the three inner loops is proportional to the row size and the required spacing.

Across all rows, the total work is quadratic.

Therefore:

```text
Time = O(n²)
```

### Space Complexity

```text
O(1)
```

The solution does not use any additional data structures that grow with `n`.

Only loop variables are used.

Therefore:

```text
Space = O(1)
```

---

# ✅ Approach Evaluation

This is a **correct and efficient approach for the pattern-printing problem**.

The solution cleanly divides each row into three logical sections:

```text
Increasing Numbers
        ↓
Middle Spaces
        ↓
Decreasing Numbers
```

The use of:

```text
2 * (n - i)
```

correctly reduces the gap between the two number sequences as the rows progress.

The approach is simple, readable, and directly follows the structure of the required pattern.

---

# 📌 Key Takeaways

* The outer loop controls the rows.
* The first inner loop prints increasing numbers.
* The second inner loop prints the decreasing middle gap.
* The third inner loop prints decreasing numbers.
* The spacing is controlled using `2 * (n - i)`.
* The pattern is constructed row by row.
* Time complexity is `O(n²)`.
* Space complexity is `O(1)`.

---

# 🔗 Problem Source

**Platform:** Code360

**Problem:** Number Crown

[**View Problem on Code360 →**](https://www.naukri.com/code360/problems/number-crown_6581894)

---

**Part of the [Solved DSA Problems](https://github.com/Dharma718/Solved-DSA-Problems) repository.**
