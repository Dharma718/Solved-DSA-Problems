# 🟥 Binary Number Triangle

## 📌 Problem Statement

Given an integer `n`, print a **binary number triangle** containing `1`s and `0`s.

The pattern consists of `n` rows, where:

* Row `i` contains `i + 1` elements.
* Each position contains either `1` or `0`.
* The value is determined by the sum of the row index and column index.
* If `(i + j)` is even, print `1`.
* Otherwise, print `0`.

### Example

For:

```text
n = 5
```

the output is:

```text
1
0 1
1 0 1
0 1 0 1
1 0 1 0 1
```

---

# 💡 My Approach

My approach uses **two nested loops** to construct the triangle row by row.

For every row:

1. The outer loop determines the current row.
2. The inner loop prints the required number of elements for that row.
3. For every position, I check:

```text
(i + j) % 2 == 0
```

If the result is `0`, the position receives:

```text
1
```

Otherwise, it receives:

```text
0
```

This creates the alternating binary pattern automatically.

---

# 🧠 Key Observation

The main observation in my approach is that the value at each position can be determined using the **sum of its row and column indices**.

```text
(i + j) % 2 == 0 → 1
(i + j) % 2 != 0 → 0
```

For example:

```text
i = 0, j = 0
(0 + 0) % 2 = 0 → 1
```

and:

```text
i = 0, j = 1
(0 + 1) % 2 = 1 → 0
```

Therefore, the values naturally alternate between `1` and `0`.

---

# 🔍 Step-by-Step Explanation

The outer loop controls the rows:

```java
for (int i = 0; i < n; i++)
```

Since `i` starts from `0`, the first row has one element.

The second row has two elements, and so on.

Therefore, the inner loop runs from `0` through `i`:

```java
for (int j = 0; j <= i; j++)
```

This produces:

```text
i = 0 → 1 element
i = 1 → 2 elements
i = 2 → 3 elements
i = 3 → 4 elements
```

and so on.

---

## 🔢 Determining the Binary Value

For every position `(i, j)`, calculate:

```java
(i + j) % 2
```

If it is even:

```java
if ((i + j) % 2 == 0)
```

print:

```text
1
```

Otherwise, print:

```text
0
```

After finishing each row:

```java
System.out.println();
```

moves the output to the next line.

---

# 🧪 Dry Run

Consider:

```text
n = 5
```

Initially:

```text
i = 0
```

### Row 1

```text
j = 0

(i + j) % 2
= (0 + 0) % 2
= 0
```

Therefore:

```text
1
```

---

### Row 2

```text
i = 1
```

#### Position 1

```text
j = 0

(1 + 0) % 2
= 1
```

Therefore:

```text
0
```

#### Position 2

```text
j = 1

(1 + 1) % 2
= 0
```

Therefore:

```text
1
```

Row:

```text
0 1
```

---

### Row 3

```text
i = 2
```

#### `j = 0`

```text
(2 + 0) % 2 = 0
→ 1
```

#### `j = 1`

```text
(2 + 1) % 2 = 1
→ 0
```

#### `j = 2`

```text
(2 + 2) % 2 = 0
→ 1
```

Row:

```text
1 0 1
```

---

### Row 4

```text
i = 3
```

The values become:

```text
j = 0 → (3 + 0) % 2 = 1 → 0
j = 1 → (3 + 1) % 2 = 0 → 1
j = 2 → (3 + 2) % 2 = 1 → 0
j = 3 → (3 + 3) % 2 = 0 → 1
```

Row:

```text
0 1 0 1
```

---

### Row 5

```text
i = 4
```

The values become:

```text
j = 0 → 1
j = 1 → 0
j = 2 → 1
j = 3 → 0
j = 4 → 1
```

Row:

```text
1 0 1 0 1
```

### Final Output

```text
1
0 1
1 0 1
0 1 0 1
1 0 1 0 1
```

---

# 💻 Solution

```java
public class Solution {
    public static void nBinaryTriangle(int n) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j <= i; j++) {
                if ((i + j) % 2 == 0) {
                    System.out.print("1 ");
                } else {
                    System.out.print("0 ");
                }
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

For each row `i`, the inner loop runs `i + 1` times.

Therefore, the total number of positions printed grows quadratically with `n`.

```text
Time = O(n²)
```

### Space Complexity

```text
O(1)
```

The solution does not use any additional data structure whose size depends on `n`.

Only the loop variables and conditional check are used.

```text
Space = O(1)
```

---

# ✅ Approach Evaluation

This is a **correct and efficient approach** for the given pattern.

The important part of the solution is the observation:

```text
(i + j) % 2
```

Instead of separately tracking whether the next value should be `0` or `1`, the parity of the row and column indices directly determines the value.

This makes the implementation simple and avoids unnecessary variables or additional data structures.

For a pattern containing `n` rows:

```text
Time  → O(n²)
Space → O(1)
```

---

# 📌 Key Takeaways

* The outer loop controls the number of rows.
* The inner loop prints `i + 1` elements for row `i`.
* `(i + j) % 2` determines whether to print `1` or `0`.
* Even `(i + j)` produces `1`.
* Odd `(i + j)` produces `0`.
* The pattern naturally alternates between `1` and `0`.
* No additional data structure is required.
* Time complexity is `O(n²)`.
* Space complexity is `O(1)`.

---

# 🔗 Problem Source

**Platform:** Code360

**Problem:** Binary Number Triangle

[**View Problem on Code360 →**](https://www.naukri.com/code360/problems/binary-number-triangle_6581890)

---

**Part of the [Solved DSA Problems](https://github.com/Dharma718/Solved-DSA-Problems) repository.**
