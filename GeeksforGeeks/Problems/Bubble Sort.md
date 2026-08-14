# 🟩 Bubble Sort

## 📌 Problem Statement

Given an integer array `arr`, sort the array in **ascending order** using the required sorting approach.

For example:

```text
Input:
[5, 3, 8, 1, 2]

Output:
[1, 2, 3, 5, 8]
```

---

# 💡 My Approach

My approach uses two nested loops to compare each element with all elements that come after it.

For every index `i`, I compare:

```text
arr[i]
```

with:

```text
arr[i + 1], arr[i + 2], ..., arr[n - 1]
```

Whenever a smaller element is found, I immediately swap the two elements.

The comparison is:

```java
if (arr[i] > arr[j])
```

If `arr[i]` is greater than `arr[j]`, the values are swapped.

This gradually places the smallest available value at the current index.

---

# 🧠 Key Observation

The main idea of my approach is:

```text
Select the current position
        ↓
Compare it with every element to its right
        ↓
If a smaller value is found
        ↓
Swap immediately
        ↓
Continue comparing
```

After completing all comparisons for index `i`, the smallest value among the remaining unsorted elements will have moved toward position `i`.

For example:

```text
[5, 3, 8, 1, 2]
 ↑
i = 0
```

Compare `5` with the elements after it:

```text
5 > 3 → swap
5 > 8 → no swap
3 > 1 → swap
3 > 2 → swap
```

The first position eventually becomes:

```text
[1, 5, 8, 3, 2]
```

The process then continues from the next index.

---

# 🔍 Step-by-Step Explanation

## 1. Outer Loop

```java
for (int i = 0; i < arr.length; i++)
```

The outer loop determines the position currently being arranged.

For an array of length `5`:

```text
i = 0
i = 1
i = 2
i = 3
i = 4
```

---

## 2. Inner Loop

```java
for (int j = i + 1; j < arr.length; j++)
```

The inner loop compares the element at index `i` with every element to its right.

For example, when:

```text
i = 0
```

the comparisons are:

```text
arr[0] with arr[1]
arr[0] with arr[2]
arr[0] with arr[3]
...
```

When:

```text
i = 2
```

the comparisons start from:

```text
arr[2] with arr[3]
arr[2] with arr[4]
...
```

---

## 3. Compare the Values

```java
if (arr[i] > arr[j])
```

If the current value is greater than the value at `j`, they are in the wrong order.

Therefore, they are swapped.

---

## 4. Swap the Values

The swap is performed using a temporary variable:

```java
int temp = arr[i];
arr[i] = arr[j];
arr[j] = temp;
```

After the swap, the smaller value moves toward the current position.

---

# 🧪 Dry Run

Consider:

```text
arr = [5, 3, 8, 1, 2]
```

### Pass 1

```text
i = 0
arr[0] = 5
```

Compare with `3`:

```text
5 > 3
```

Swap:

```text
[3, 5, 8, 1, 2]
```

Compare the current `arr[0]` (`3`) with `8`:

```text
3 > 8 → false
```

Compare with `1`:

```text
3 > 1
```

Swap:

```text
[1, 5, 8, 3, 2]
```

Compare with `2`:

```text
1 > 2 → false
```

After the first outer-loop iteration:

```text
[1, 5, 8, 3, 2]
```

The smallest element is now at index `0`.

---

### Pass 2

```text
i = 1
arr[1] = 5
```

Compare with `8`:

```text
5 > 8 → false
```

Compare with `3`:

```text
5 > 3
```

Swap:

```text
[1, 3, 8, 5, 2]
```

Compare with `2`:

```text
3 > 2
```

Swap:

```text
[1, 2, 8, 5, 3]
```

---

### Pass 3

```text
i = 2
arr[2] = 8
```

Compare with `5`:

```text
8 > 5
```

Swap:

```text
[1, 2, 5, 8, 3]
```

Compare with `3`:

```text
5 > 3
```

Swap:

```text
[1, 2, 3, 8, 5]
```

---

### Pass 4

```text
i = 3
arr[3] = 8
```

Compare with `5`:

```text
8 > 5
```

Swap:

```text
[1, 2, 3, 5, 8]
```

The array is now sorted.

---

# 📊 Array Progress

```text
Initial:
[5, 3, 8, 1, 2]

After i = 0:
[1, 5, 8, 3, 2]

After i = 1:
[1, 2, 8, 5, 3]

After i = 2:
[1, 2, 3, 8, 5]

After i = 3:
[1, 2, 3, 5, 8]
```

---

# 💻 Solution

```java
class Solution {
    public void bubbleSort(int[] arr) {
        for (int i = 0; i < arr.length; i++) {
            for (int j = i + 1; j < arr.length; j++) {
                if (arr[i] > arr[j]) {
                    int temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
            }
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

The outer loop runs `n` times, and the inner loop performs comparisons with the elements to the right.

The total number of comparisons is proportional to:

```text
(n - 1) + (n - 2) + ... + 1
```

Therefore:

```text
Time = O(n²)
```

### Space Complexity

```text
O(1)
```

The algorithm sorts the array in place and only uses a temporary variable for swapping.

Therefore:

```text
Space = O(1)
```

---

# ⚠️ Approach Evaluation

Your solution **correctly sorts the array in ascending order**, but there is an important distinction worth documenting.

Although the Code360/GFG problem is named **Bubble Sort**, your implementation does **not use the traditional Bubble Sort mechanism**.

### Traditional Bubble Sort

Standard Bubble Sort repeatedly compares **adjacent elements**:

```text
arr[j] and arr[j + 1]
```

and swaps them when they are in the wrong order.

### Your Approach

Your implementation compares:

```text
arr[i] and arr[j]
```

where `j` moves through **all elements after `i`**.

Therefore, your implementation is closer to a **selection-style sorting approach with immediate swaps** than conventional Bubble Sort.

However, your implementation is still:

```text
Correct for ascending sorting
Time Complexity → O(n²)
Space Complexity → O(1)
```

For your repository, I would keep **your submitted solution exactly as it is** while making this distinction clear in the explanation.

---

# 📌 Key Takeaways

* The outer loop selects the current position.
* The inner loop compares it with every element to its right.
* A swap occurs whenever a smaller value is found.
* The smallest remaining value moves toward the current position.
* The array is sorted in place.
* Time complexity is `O(n²)`.
* Space complexity is `O(1)`.
* The implementation is not the traditional adjacent-swap Bubble Sort mechanism.

---

# 🔗 Problem Source

**Platform:** GeeksforGeeks

**Problem:** Bubble Sort

[**View Problem on GeeksforGeeks →**](https://www.geeksforgeeks.org/problems/bubble-sort/1)

---

**Part of the [Solved DSA Problems](https://github.com/Dharma718/Solved-DSA-Problems) repository.**

