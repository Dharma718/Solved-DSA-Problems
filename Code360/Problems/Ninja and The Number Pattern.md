# 🟪 Ninja and the Number Pattern I

## 📌 Problem Statement

Given an integer `n`, print a square number pattern of size:

```text
2 * n - 1
```

The pattern is formed using **concentric layers**.

The outermost layer contains `n`, the next inner layer contains `n - 1`, and this continues toward the center.

### Example

For:

```text
n = 4
```

the pattern is:

```text
4444444
4333334
4322234
4321234
4322234
4333334
4444444
```

The pattern is symmetric from:

* Top to bottom
* Left to right

---

# 💡 My Approach

My approach treats every position in the pattern as belonging to a particular **layer**.

First, I calculate the size of the square:

```java
int size = 2 * n - 1;
```

For every position `(i, j)`, I calculate its distance from all four boundaries:

```text
top
left
bottom
right
```

Then I find the minimum of these four distances:

```text
layer = minimum(top, bottom, left, right)
```

This tells me which concentric layer the current position belongs to.

Finally, the number printed at that position is:

```text
num = n - layer
```

So the outermost layer has value `n`, the next layer has `n - 1`, and so on until the center.

---

# 🧠 Key Observation

The most important observation in my approach is that the value of every cell depends on its **minimum distance from the four boundaries**.

For a position `(i, j)`:

```text
top    = i
left   = j
bottom = size - 1 - i
right  = size - 1 - j
```

Then:

```text
layer = min(top, bottom, left, right)
```

Finally:

```text
number = n - layer
```

This avoids separately handling the outer border, inner border, center, and so on.

The entire pattern can be generated using the same calculation for every cell.

---

# 🔍 Step-by-Step Explanation

## 1. Calculate the Pattern Size

The pattern has:

```text
2 * n - 1
```

rows and columns.

Therefore:

```java
int size = 2 * n - 1;
```

For example, when:

```text
n = 4
```

we get:

```text
size = 2 * 4 - 1
     = 7
```

So the pattern is a `7 × 7` square.

---

## 2. Traverse Every Cell

Two nested loops visit every position in the square:

```java
for (int i = 0; i < size; i++) {
    for (int j = 0; j < size; j++) {
```

Here:

* `i` represents the row.
* `j` represents the column.

---

## 3. Calculate Distance from the Top

```java
int top = i;
```

The row index directly represents the distance from the top boundary.

For example:

```text
i = 0 → top = 0
i = 1 → top = 1
i = 2 → top = 2
```

---

## 4. Calculate Distance from the Left

```java
int left = j;
```

The column index represents the distance from the left boundary.

```text
j = 0 → left = 0
j = 1 → left = 1
j = 2 → left = 2
```

---

## 5. Calculate Distance from the Bottom

```java
int bottom = size - 1 - i;
```

This calculates how far the current row is from the bottom boundary.

For `size = 7`:

```text
i = 0 → bottom = 6
i = 1 → bottom = 5
i = 2 → bottom = 4
...
i = 6 → bottom = 0
```

---

## 6. Calculate Distance from the Right

```java
int right = size - 1 - j;
```

Similarly, this calculates the distance from the right boundary.

For `size = 7`:

```text
j = 0 → right = 6
j = 1 → right = 5
...
j = 6 → right = 0
```

---

## 7. Determine the Layer

Now the minimum distance among the four boundaries is calculated:

```java
int layer = Math.min(
    Math.min(top, bottom),
    Math.min(left, right)
);
```

This determines the concentric layer containing the current position.

For example, if:

```text
top    = 2
bottom = 4
left   = 3
right  = 3
```

then:

```text
layer = 2
```

---

## 8. Calculate the Number

Once the layer is known:

```java
int num = n - layer;
```

For:

```text
n = 4
```

the layers become:

```text
layer = 0 → 4
layer = 1 → 3
layer = 2 → 2
layer = 3 → 1
```

Therefore, the center contains `1`.

---

# 🧪 Dry Run

Consider:

```text
n = 4
```

Then:

```text
size = 2 * 4 - 1
     = 7
```

So we have a `7 × 7` pattern.

---

### Position `(0, 0)`

```text
top    = 0
left   = 0
bottom = 6
right  = 6
```

Minimum:

```text
layer = 0
```

Therefore:

```text
num = 4 - 0 = 4
```

Output:

```text
4
```

---

### Position `(1, 1)`

```text
top    = 1
left   = 1
bottom = 5
right  = 5
```

Minimum:

```text
layer = 1
```

Therefore:

```text
num = 4 - 1 = 3
```

Output:

```text
3
```

---

### Position `(2, 2)`

```text
top    = 2
left   = 2
bottom = 4
right  = 4
```

Minimum:

```text
layer = 2
```

Therefore:

```text
num = 4 - 2 = 2
```

Output:

```text
2
```

---

### Center Position `(3, 3)`

```text
top    = 3
left   = 3
bottom = 3
right  = 3
```

Therefore:

```text
layer = 3
```

and:

```text
num = 4 - 3
    = 1
```

So the center contains:

```text
1
```

---

# 📊 Layer Representation

For `n = 4`, the pattern can be understood as layers:

```text
Layer 0 → 4
Layer 1 → 3
Layer 2 → 2
Layer 3 → 1
```

Visually:

```text
4444444
4333334
4322234
4321234
4322234
4333334
4444444
```

The same layer value appears symmetrically around the center.

---

# 💻 Solution

```java
public class Solution {
    public static void getNumberPattern(int n) {
        int size = 2 * n - 1;

        for (int i = 0; i < size; i++) {
            for (int j = 0; j < size; j++) {
                int top = i;
                int left = j;
                int bottom = size - 1 - i;
                int right = size - 1 - j;

                int layer = Math.min(
                    Math.min(top, bottom),
                    Math.min(left, right)
                );

                int num = n - layer;

                System.out.print(num);
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

The pattern has:

```text
(2n - 1) × (2n - 1)
```

positions.

Every position is visited exactly once, and only a constant amount of work is performed for each position.

Therefore:

```text
Time = O(n²)
```

### Space Complexity

```text
O(1)
```

Only a fixed number of variables are used for each position:

* `top`
* `left`
* `bottom`
* `right`
* `layer`
* `num`

No additional data structure is created based on `n`.

Therefore:

```text
Space = O(1)
```

---

# ✅ Approach Evaluation

This is a **correct and efficient approach** for the required pattern.

The strongest part of the solution is the **layer-based observation**.

Instead of separately constructing each border, the solution determines the layer of every position using its minimum distance from the four boundaries:

```text
layer = min(top, bottom, left, right)
```

Then the corresponding value is simply:

```text
number = n - layer
```

This gives a clean way to generate the entire symmetric pattern using one consistent rule.

---

# 📌 Key Takeaways

* The pattern is a square of size `2 * n - 1`.
* Every position belongs to a concentric layer.
* The layer is determined by the minimum distance from the four boundaries.
* `n - layer` gives the number to print.
* The approach naturally produces the required symmetry.
* No additional data structure is required.
* Time complexity is `O(n²)`.
* Space complexity is `O(1)`.

---

# 🔗 Problem Source

**Platform:** Code360

**Problem:** Ninja and the Number Pattern I

[**View Problem on Code360 →**](https://www.naukri.com/code360/problems/ninja-and-the-number-pattern-i_6581959)

---

**Part of the [Solved DSA Problems](https://github.com/Dharma718/Solved-DSA-Problems) repository.**

