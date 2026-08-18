# 🔤 Reverse Letter Triangle

## 📌 Problem Statement

Given an integer `n`, print a **reverse letter triangle** pattern using uppercase English alphabets.

The pattern starts with `n` letters in the first row. In every subsequent row, the number of letters decreases by one.

For each row, the letters start from `A` and continue sequentially.

### Example

For:

```text
n = 5
```

The pattern is:

```text
A B C D E
A B C D
A B C
A B
A
```

---

# 💡 My Approach

My approach uses **nested loops** to generate the required pattern.

The main idea is:

* The outer loop controls the rows.
* The inner loop controls the number of characters printed in each row.
* The number of characters decreases as the row number increases.
* The character is generated using:

```text
(char)('A' + j)
```

The important part of my implementation is:

```text
for(int i = 0; i < n; i++){
    for(int j = 0; j < n - i; j++){
        System.out.print((char)('A' + j) + " ");
    }
    System.out.println();
}
```

For every row, the inner loop starts again from `j = 0`, so every row begins with `A`.

---

# 🧠 Key Observation

The number of characters printed in each row follows this pattern:

```text
n
n - 1
n - 2
n - 3
...
1
```

For example, when:

```text
n = 5
```

the number of characters in each row is:

```text
Row 1 → 5
Row 2 → 4
Row 3 → 3
Row 4 → 2
Row 5 → 1
```

This can be represented as:

```text
n - i
```

where `i` starts from `0`.

Therefore, the inner loop runs while:

```text
j < n - i
```

---

# 🔍 Step-by-Step Explanation

## 1. Control the Rows

```text
for(int i = 0; i < n; i++)
```

The outer loop runs `n` times.

Each iteration represents one row of the pattern.

For:

```text
n = 5
```

the values of `i` are:

```text
0
1
2
3
4
```

---

## 2. Determine the Number of Letters

```text
for(int j = 0; j < n - i; j++)
```

The inner loop determines how many letters are printed in the current row.

Since the required number of letters decreases by one after every row, we use:

```text
n - i
```

For example:

```text
i = 0 → n - i = 5
i = 1 → n - i = 4
i = 2 → n - i = 3
i = 3 → n - i = 2
i = 4 → n - i = 1
```

Therefore, the pattern becomes:

```text
A B C D E
A B C D
A B C
A B
A
```

---

## 3. Generate the Letters

```text
(char)('A' + j)
```

The expression starts with `'A'` and moves forward according to the value of `j`.

The character progression is:

```text
j = 0 → 'A'
j = 1 → 'B'
j = 2 → 'C'
j = 3 → 'D'
j = 4 → 'E'
```

Therefore, the inner loop produces:

```text
A B C D E
```

for the first row.

Because `j` starts from `0` again for every new row, each row begins with `A`.

---

## 4. Print a Space After Each Letter

```text
System.out.print((char)('A' + j) + " ");
```

The generated character is printed followed by a space.

For example:

```text
A 
B 
C 
```

---

## 5. Move to the Next Row

```text
System.out.println();
```

After all characters for the current row have been printed, `println()` moves the output to the next line.

This creates the triangle structure.

---

# 🧪 Dry Run

Consider:

```text
n = 5
```

---

### Iteration 1

```text
i = 0
```

The inner loop runs while:

```text
j < 5
```

Characters printed:

```text
j = 0 → A
j = 1 → B
j = 2 → C
j = 3 → D
j = 4 → E
```

Output:

```text
A B C D E
```

---

### Iteration 2

```text
i = 1
```

Now:

```text
j < 5 - 1
j < 4
```

Characters printed:

```text
j = 0 → A
j = 1 → B
j = 2 → C
j = 3 → D
```

Output:

```text
A B C D
```

---

### Iteration 3

```text
i = 2
```

Now:

```text
j < 5 - 2
j < 3
```

Characters printed:

```text
j = 0 → A
j = 1 → B
j = 2 → C
```

Output:

```text
A B C
```

---

### Iteration 4

```text
i = 3
```

Now:

```text
j < 5 - 3
j < 2
```

Characters printed:

```text
j = 0 → A
j = 1 → B
```

Output:

```text
A B
```

---

### Iteration 5

```text
i = 4
```

Now:

```text
j < 5 - 4
j < 1
```

Only:

```text
j = 0 → A
```

is printed.

Output:

```text
A
```

---

# 📊 Pattern Progress

For:

```text
n = 5
```

the pattern develops as:

```text
Row 1:
A B C D E

Row 2:
A B C D

Row 3:
A B C

Row 4:
A B

Row 5:
A
```

The number of characters decreases by one after every row:

```text
5 → 4 → 3 → 2 → 1
```

while the starting character remains:

```text
A
```

for every row.

---

# 💻 Solution

```java
public class Solution {
    public static void nLetterTriangle(int n) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n - i; j++) {
                System.out.print((char)('A' + j) + " ");
            }
            System.out.println();
        }
    }
}
```

---

# ⚙️ Complexity Analysis

### Time Complexity

The number of characters printed is:

```text
n + (n - 1) + (n - 2) + ... + 1
```

This is:

```text
n(n + 1) / 2
```

Therefore, the time complexity is:

```text
O(n²)
```

---

### Space Complexity

The solution uses only the loop variables `i` and `j` and does not create any additional data structure.

Therefore:

```text
O(1)
```

---

# ✅ Approach Evaluation

This is a **correct and straightforward nested-loop approach** for generating the required pattern.

The solution identifies two independent parts of the pattern:

```text
Outer loop
    ↓
Controls the rows

Inner loop
    ↓
Controls the letters in each row
```

The key relationship is:

```text
Number of letters = n - i
```

while the character is determined by:

```text
'A' + j
```

Therefore, the complete pattern generation can be summarized as:

```text
Start Row
    ↓
Calculate number of letters
    ↓
Start from A
    ↓
Print consecutive letters
    ↓
Move to next row
    ↓
Reduce number of letters by 1
    ↓
Repeat
```

---

# 📌 Key Takeaways

* The solution uses nested loops to generate the pattern.
* The outer loop controls the number of rows.
* The inner loop controls the number of letters in each row.
* The number of letters decreases by one after every row.
* Every row starts from `A`.
* `(char)('A' + j)` generates consecutive uppercase letters.
* The pattern contains `n` rows.
* The total number of printed characters is proportional to `n²`.
* Time complexity is `O(n²)`.
* Space complexity is `O(1)`.

---

# 🔗 Problem Source

**Platform:** Code360

**Problem:** [Reverse Letter Triangle](https://www.naukri.com/code360/problems/reverse-letter-triangle_6581906)

---

**Part of the** [**Solved DSA Problems**](https://github.com/Dharma718/Solved-DSA-Problems) **repository.**

