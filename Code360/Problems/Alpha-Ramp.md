# 🟦 Alpha Ramp

## 📌 Problem Statement

Given an integer `n`, print an **Alpha Ramp** pattern using uppercase English alphabets.

The pattern contains `n` rows. For each row:

* The alphabet is determined by the row number.
* The same alphabet is printed repeatedly across that row.
* Row `1` prints `A` once.
* Row `2` prints `B` twice.
* Row `3` prints `C` three times.
* This continues for all `n` rows.

### Example

For:

```text
n = 5
```

the output is:

```text
A
B B
C C C
D D D D
E E E E E
```

---

# 💡 My Approach

My approach uses **two nested loops**.

The outer loop determines the current row:

```java
for (int i = 0; i < n; i++)
```

The row index `i` is also used to determine which alphabet character should be printed.

The inner loop runs from `0` to `i`, which means the character is printed exactly `i + 1` times.

For the alphabet, I use:

```text
(char)('A' + i)
```

This converts the row index into the corresponding uppercase alphabet.

For example:

```text
i = 0 → 'A' + 0 → A
i = 1 → 'A' + 1 → B
i = 2 → 'A' + 2 → C
i = 3 → 'A' + 3 → D
```

Therefore, each row automatically receives the correct alphabet.

---

# 🧠 Key Observation

The important observation is that the **row index determines both the character and the number of times it is printed**.

For row index `i`:

```text
Character → 'A' + i
Repetitions → i + 1
```

For example:

```text
i = 0 → A → 1 time
i = 1 → B → 2 times
i = 2 → C → 3 times
i = 3 → D → 4 times
```

This allows the entire pattern to be generated using only two loops.

---

# 🔍 Step-by-Step Explanation

The outer loop controls the rows:

```java
for (int i = 0; i < n; i++)
```

Since `i` starts from `0`, the first row corresponds to `A`.

The inner loop is:

```java
for (int j = 0; j <= i; j++)
```

This means:

```text
i = 0 → 1 iteration
i = 1 → 2 iterations
i = 2 → 3 iterations
i = 3 → 4 iterations
```

Therefore, each row contains one more character than the previous row.

---

## 🔤 Converting the Row Index to an Alphabet

The expression:

```java
(char)('A' + i)
```

uses the character value of `A` as the starting point.

For example:

```text
i = 0 → A
i = 1 → B
i = 2 → C
i = 3 → D
i = 4 → E
```

The cast to `char` converts the resulting value back into a character.

---

# 🧪 Dry Run

Consider:

```text
n = 4
```

Initially:

```text
i = 0
```

### Row 1

Character:

```text
'A' + 0 = A
```

Inner loop:

```text
j = 0
```

So `A` is printed once:

```text
A
```

---

### Row 2

```text
i = 1
```

Character:

```text
'A' + 1 = B
```

The inner loop runs twice:

```text
j = 0
j = 1
```

Therefore:

```text
B B
```

---

### Row 3

```text
i = 2
```

Character:

```text
'A' + 2 = C
```

The inner loop runs three times:

```text
j = 0
j = 1
j = 2
```

Therefore:

```text
C C C
```

---

### Row 4

```text
i = 3
```

Character:

```text
'A' + 3 = D
```

The inner loop runs four times.

Therefore:

```text
D D D D
```

### Final Output

```text
A
B B
C C C
D D D D
```

---

# 💻 Solution

```java
public class Solution {
    public static void alphaRamp(int n) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j <= i; j++) {
                System.out.print((char) ('A' + i) + " ");
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

The outer loop runs `n` times, while the inner loop prints:

```text
1 + 2 + 3 + ... + n
```

characters.

Therefore:

```text
Time = O(n²)
```

### Space Complexity

```text
O(1)
```

Only the loop variables are used. No additional data structure is created based on `n`.

Therefore:

```text
Space = O(1)
```

---

# ✅ Approach Evaluation

This is a **correct and efficient approach for the required pattern**.

The solution uses the row index directly to determine the alphabet:

```text
'A' + i
```

and the same row index determines how many times that character should be printed:

```text
i + 1
```

This makes the implementation simple, direct, and avoids unnecessary variables or additional data structures.

---

# 📌 Key Takeaways

* The outer loop controls the rows.
* The inner loop controls the number of characters in each row.
* `(char)('A' + i)` converts the row index into the required alphabet.
* The same alphabet is printed throughout each row.
* Row `i` contains `i + 1` copies of the character.
* No additional data structure is required.
* Time complexity is `O(n²)`.
* Space complexity is `O(1)`.

---

# 🔗 Problem Source

**Platform:** Code360

**Problem:** Alpha Ramp

[**View Problem on Code360 →**](https://www.naukri.com/code360/problems/alpha-ramp_6581888)

---

**Part of the [Solved DSA Problems](https://github.com/Dharma718/Solved-DSA-Problems) repository.**

