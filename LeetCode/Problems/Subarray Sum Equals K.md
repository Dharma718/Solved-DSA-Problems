# 🟨 Subarray Sum Equals K

## 📌 Problem Statement

Given an integer array `nums` and an integer `k`, return the total number of continuous subarrays whose elements add up to exactly `k`.

A subarray must contain **continuous elements** from the original array.

### Example

```text
Input:
nums = [1, 1, 1]
k = 2

Output:
2
```

The two subarrays whose sum is `2` are:

```text
[1, 1]
[1, 1]
```

Therefore, the answer is:

```text
2
```

---

# 💡 My Approach

My approach uses **two nested loops** to consider every possible starting and ending position of a subarray.

For every starting index `i`:

1. Initialize `sum` as `0`.
2. Start another loop from `i`.
3. Keep adding each element to `sum`.
4. Whenever `sum == k`, increment `count`.
5. Continue checking the remaining elements so that every possible subarray starting at `i` is considered.

The important part is that I do **not** calculate the sum of every subarray from scratch.

Instead, I maintain a running sum:

```text
sum += nums[j]
```

This allows the sum to be updated as the ending index moves forward.

---

# 🔍 Step-by-Step Explanation

First, store the length of the array:

```java id="2qj11v"
int n = nums.length;
```

Then create a variable to store the number of valid subarrays:

```java id="j3wx5k"
int count = 0;
```

Next, use the outer loop to choose the starting index:

```java id="w8h2q1"
for (int i = 0; i < n; i++)
```

For every new starting position, reset the running sum:

```java id="x3n7pk"
int sum = 0;
```

Then use the inner loop to extend the subarray from index `i`:

```java id="k7s5dm"
for (int j = i; j < n; j++)
```

Add the current element to the running sum:

```java id="p9h2rx"
sum += nums[j];
```

Whenever the current subarray has sum equal to `k`:

```java id="4m6r8c"
if (sum == k)
```

increment the answer:

```java id="n4c2yz"
count++;
```

After checking all possible subarrays, return `count`.

---

# 🧪 Dry Run

Consider:

```text id="q6v4py"
nums = [1, 2, 1]
k = 3
```

Initially:

```text id="g6d1z9"
count = 0
```

### Starting at index `0`

```text id="xq6n0w"
i = 0
sum = 0
```

#### `j = 0`

```text id="r4s2z8"
sum = 0 + 1 = 1
```

`sum != 3`

```text
count = 0
```

#### `j = 1`

```text id="j9t2v4"
sum = 1 + 2 = 3
```

Now:

```text id="m2z8q6"
sum == k
```

So:

```text id="v6k1r3"
count = 1
```

The subarray is:

```text
[1, 2]
```

#### `j = 2`

```text id="b8r5k1"
sum = 3 + 1 = 4
```

`sum != 3`

```text
count = 1
```

---

### Starting at index `1`

Reset:

```text id="t6n2x8"
sum = 0
```

#### `j = 1`

```text id="a4m7q2"
sum = 0 + 2 = 2
```

`sum != 3`

#### `j = 2`

```text id="e5p1y7"
sum = 2 + 1 = 3
```

Now:

```text id="s8d3k5"
sum == k
```

Therefore:

```text id="c2v9m4"
count = 2
```

The subarray is:

```text
[2, 1]
```

---

### Starting at index `2`

Reset:

```text id="r3w7n1"
sum = 0
```

#### `j = 2`

```text id="f8k2m6"
sum = 0 + 1 = 1
```

`sum != 3`

The final count is:

```text id="h7q4p9"
count = 2
```

### Final Output

```text
2
```

---

# 💻 Solution

```java id="a3m7k2"
class Solution {
    public int subarraySum(int[] nums, int k) {
        int n = nums.length;
        int count = 0;

        for (int i = 0; i < n; i++) {
            int sum = 0;

            for (int j = i; j < n; j++) {
                sum += nums[j];

                if (sum == k) {
                    count++;
                }
            }
        }

        return count;
    }
}
```

---

# ⚙️ Complexity Analysis

### Time Complexity

```text id="p5x8m2"
O(n²)
```

The outer loop runs `n` times, and for each starting index, the inner loop can also run up to `n` times.

Therefore, the overall time complexity is:

```text
O(n²)
```

### Space Complexity

```text id="k8r3v6"
O(1)
```

Only a constant number of variables are used:

* `n`
* `count`
* `i`
* `j`
* `sum`

No additional data structure is used.

Therefore:

```text
Space = O(1)
```

---

# 🧩 Approach Evaluation

This is a **correct brute-force approach**.

It systematically considers every possible continuous subarray and calculates its sum using a running sum.

### Strengths

* Simple and easy to understand
* Does not require an additional data structure
* Uses only constant extra space
* Correctly handles negative numbers
* Avoids recalculating the complete sum for every subarray

### Limitation

The main limitation is the quadratic time complexity:

```text
O(n²)
```

For large input sizes, this can become inefficient.

There is a more optimized approach using **Prefix Sum + HashMap**, which can reduce the time complexity to `O(n)`.

However, this file intentionally documents **my own submitted approach** rather than replacing it with a different solution.

---

# 📌 Key Takeaways

* Every possible starting index is considered.
* Every possible ending index is considered for each starting position.
* A running `sum` avoids recalculating each subarray sum from scratch.
* Whenever `sum == k`, the current subarray is counted.
* The approach uses constant extra space.
* The solution is correct but has `O(n²)` time complexity.
* A Prefix Sum + HashMap approach can solve the problem more efficiently in `O(n)` time.

---

# 🔗 Problem Source

**Platform:** LeetCode

**Problem:** Subarray Sum Equals K

[**View Problem on LeetCode →**](https://leetcode.com/problems/subarray-sum-equals-k/)

---

**Part of the [Solved DSA Problems](https://github.com/Dharma718/Solved-DSA-Problems) repository.**
