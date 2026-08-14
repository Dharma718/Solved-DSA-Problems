# 🟧 Insertion Sort

## 📌 Problem Statement

Given an integer array `arr`, sort the array in **ascending order** using the Insertion Sort technique.

The sorting must be performed **in-place**, meaning the original array should be modified directly without creating another array for the sorted result.

### Example

```text
Input:
[5, 3, 4, 1, 2]

Output:
[1, 2, 3, 4, 5]
```

---

# 💡 My Approach

My approach uses **Insertion Sort**.

The main idea is to divide the array conceptually into two parts:

```text
Sorted portion | Unsorted portion
```

Initially, the first element is considered sorted.

For every next element:

1. Store the current element in `key`.
2. Compare `key` with the elements before it.
3. Shift every larger element one position to the right.
4. Insert `key` into its correct position.

The important part of my implementation is:

```java
int key = arr[i];
int j = i - 1;
```

Here:

* `key` stores the element that needs to be inserted.
* `j` starts at the element immediately before `key`.

---

# 🧠 Key Observation

At every iteration, the portion to the **left of `i` is already sorted**.

The current element is then inserted into that sorted portion.

For example:

```text
[5, 3, 4, 1, 2]
 ↑
Sorted portion
```

When `3` is selected:

```text
key = 3
```

Since `5 > 3`, `5` is shifted to the right:

```text
[5, 5, 4, 1, 2]
```

Then `3` is inserted:

```text
[3, 5, 4, 1, 2]
```

Now the first two elements are sorted.

This process continues until the entire array becomes sorted.

---

# 🔍 Step-by-Step Explanation

## 1. Get the Array Length

```java
int n = arr.length;
```

This stores the number of elements in the array.

---

## 2. Traverse the Array

```java
for (int i = 0; i < n; i++)
```

The outer loop selects each element that needs to be inserted into the sorted portion.

For example:

```text
i = 0 → first element
i = 1 → second element
i = 2 → third element
...
```

Starting from `0` is valid because the first element requires no shifting and naturally forms the initial sorted portion.

---

## 3. Store the Current Element

```java
int key = arr[i];
```

The current element is stored separately because elements may need to be shifted while searching for its correct position.

---

## 4. Start Comparing with the Previous Element

```java
int j = i - 1;
```

The sorted portion ends immediately before the current element.

Therefore, comparison starts from:

```text
arr[i - 1]
```

and moves toward the beginning of the array.

---

## 5. Shift Larger Elements

```java
while (j >= 0 && arr[j] > key) {
    arr[j + 1] = arr[j];
    j--;
}
```

As long as:

* `j` is within the array, and
* `arr[j]` is greater than `key`

the larger element is shifted one position to the right.

This creates an empty position where `key` can eventually be inserted.

---

## 6. Insert the Key

After the shifting is complete:

```java
arr[j + 1] = key;
```

At this point, `j + 1` is the correct position for `key`.

---

# 🧪 Dry Run

Consider:

```text
[5, 3, 4, 1, 2]
```

---

### Iteration 1

```text
i = 0
key = 5
```

There is nothing before `5`, so it remains:

```text
[5, 3, 4, 1, 2]
```

Sorted portion:

```text
[5]
```

---

### Iteration 2

```text
i = 1
key = 3
j = 0
```

Compare:

```text
5 > 3
```

Shift `5`:

```text
[5, 5, 4, 1, 2]
```

Move `j`:

```text
j = -1
```

Insert `3` at `j + 1`:

```text
[3, 5, 4, 1, 2]
```

Sorted portion:

```text
[3, 5]
```

---

### Iteration 3

```text
i = 2
key = 4
j = 1
```

Compare:

```text
5 > 4
```

Shift `5`:

```text
[3, 5, 5, 1, 2]
```

Move `j`:

```text
j = 0
```

Now:

```text
3 > 4
```

is false.

Insert `4`:

```text
[3, 4, 5, 1, 2]
```

Sorted portion:

```text
[3, 4, 5]
```

---

### Iteration 4

```text
i = 3
key = 1
j = 2
```

Compare with `5`:

```text
5 > 1
```

Shift:

```text
[3, 4, 5, 5, 2]
```

Compare with `4`:

```text
4 > 1
```

Shift:

```text
[3, 4, 4, 5, 2]
```

Compare with `3`:

```text
3 > 1
```

Shift:

```text
[3, 3, 4, 5, 2]
```

Insert `1`:

```text
[1, 3, 4, 5, 2]
```

Sorted portion:

```text
[1, 3, 4, 5]
```

---

### Iteration 5

```text
i = 4
key = 2
```

Compare with `5`:

```text
5 > 2
```

Shift.

Compare with `4`:

```text
4 > 2
```

Shift.

Compare with `3`:

```text
3 > 2
```

Shift.

Compare with `1`:

```text
1 > 2
```

False.

Insert `2`:

```text
[1, 2, 3, 4, 5]
```

The array is completely sorted.

---

# 📊 Array Progress

```text
Initial:
[5, 3, 4, 1, 2]

After inserting 3:
[3, 5, 4, 1, 2]

After inserting 4:
[3, 4, 5, 1, 2]

After inserting 1:
[1, 3, 4, 5, 2]

After inserting 2:
[1, 2, 3, 4, 5]
```

The important pattern is:

```text
Sorted portion grows →→→
```

---

# 💻 Solution

```java
class Solution {
    public void insertionSort(int arr[]) {
        int n = arr.length;

        for (int i = 0; i < n; i++) {
            int key = arr[i];
            int j = i - 1;

            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j--;
            }

            arr[j + 1] = key;
        }
    }
}
```

---

# ⚙️ Complexity Analysis

### Best Case

When the array is already sorted, each element requires only one comparison and no shifting.

```text
Time = O(n)
```

### Average Case

For a generally unsorted array, elements may need to be shifted through part of the sorted portion.

```text
Time = O(n²)
```

### Worst Case

The worst case occurs when the array is sorted in descending order.

Every new element needs to be shifted across the entire sorted portion.

```text
Time = O(n²)
```

### Space Complexity

The algorithm sorts the array in-place and uses only a fixed number of variables.

```text
Space = O(1)
```

---

# ✅ Approach Evaluation

This is the **standard Insertion Sort approach** and is a correct in-place implementation.

The strongest idea is maintaining the invariant:

> Before processing index `i`, the elements before `i` are already sorted.

Then `key = arr[i]` is inserted into that sorted portion by shifting larger elements to the right.

The overall process is:

```text
Choose key
    ↓
Compare with sorted portion
    ↓
Shift larger elements
    ↓
Find correct position
    ↓
Insert key
    ↓
Sorted portion grows
```

---

# 📌 Key Takeaways

* Insertion Sort builds the sorted array one element at a time.
* The left portion of the array remains sorted throughout the process.
* `key` stores the element currently being inserted.
* Larger elements are shifted rather than repeatedly swapped.
* The algorithm works **in-place**.
* Best-case time complexity is `O(n)`.
* Average-case time complexity is `O(n²)`.
* Worst-case time complexity is `O(n²)`.
* Space complexity is `O(1)`.

---

# 🔗 Problem Source

**Platform:** GeeksforGeeks

**Problem:** Insertion Sort

[**View Problem on GeeksforGeeks →**](https://www.geeksforgeeks.org/problems/insertion-sort/1)

---

**Part of the [Solved DSA Problems](https://github.com/Dharma718/Solved-DSA-Problems) repository.**

