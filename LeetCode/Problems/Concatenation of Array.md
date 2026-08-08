# 🟨 Concatenation of Array

## 📌 Problem Statement

Given an integer array `nums` of length `n`, create an array `ans` of length `2n` such that:

```text
ans[i] = nums[i]
ans[i + n] = nums[i]
```

for every valid index `i`.

In other words, `ans` should be the concatenation of `nums` with itself:

```text
ans = nums + nums
```

### Example

```text
Input:
nums = [1, 2, 1]

Output:
[1, 2, 1, 1, 2, 1]
```

The original array is:

```text
[1, 2, 1]
```

Concatenating it with itself gives:

```text
[1, 2, 1] + [1, 2, 1]
= [1, 2, 1, 1, 2, 1]
```

---

# 💡 My Approach

My approach is to create a new array of size `2 * n` and fill both halves using a single loop.

For every element at index `i` in `nums`:

```text
ans[i] = nums[i]
ans[i + n] = nums[i]
```

This places the same element in:

* The first half of `ans`
* The corresponding position in the second half of `ans`

### Example

For:

```text
nums = [1, 2, 1]
n = 3
```

The answer array has size:

```text
2 * n = 6
```

During the loop:

```text
i = 0
ans[0] = nums[0] = 1
ans[3] = nums[0] = 1

i = 1
ans[1] = nums[1] = 2
ans[4] = nums[1] = 2

i = 2
ans[2] = nums[2] = 1
ans[5] = nums[2] = 1
```

Therefore:

```text
ans = [1, 2, 1, 1, 2, 1]
```

---

# 🔍 Step-by-Step Explanation

First, find the length of the input array:

```java
int n = nums.length;
```

If:

```text
nums = [1, 2, 1]
```

then:

```text
n = 3
```

Next, create the result array with twice the size of `nums`:

```java
int[] ans = new int[2 * n];
```

So:

```text
ans = [0, 0, 0, 0, 0, 0]
```

Now iterate through the original array:

```java
for(int i = 0; i < n; i++)
```

For each element, place it in two positions:

```java
ans[i] = nums[i];
ans[i + n] = nums[i];
```

This means the first copy occupies:

```text
ans[0] → nums[0]
ans[1] → nums[1]
ans[2] → nums[2]
```

and the second copy occupies:

```text
ans[3] → nums[0]
ans[4] → nums[1]
ans[5] → nums[2]
```

Finally, return the constructed array.

---

# 🧪 Dry Run

### Input

```text
nums = [1, 2, 1]
```

### Initial State

```text
n = 3

ans = [0, 0, 0, 0, 0, 0]
```

### Iteration 1

```text
i = 0

ans[0] = nums[0] = 1
ans[3] = nums[0] = 1
```

```text
ans = [1, 0, 0, 1, 0, 0]
```

### Iteration 2

```text
i = 1

ans[1] = nums[1] = 2
ans[4] = nums[1] = 2
```

```text
ans = [1, 2, 0, 1, 2, 0]
```

### Iteration 3

```text
i = 2

ans[2] = nums[2] = 1
ans[5] = nums[2] = 1
```

```text
ans = [1, 2, 1, 1, 2, 1]
```

### Final Output

```text
[1, 2, 1, 1, 2, 1]
```

---

# 💻 Solution

```java
class Solution {
    public int[] getConcatenation(int[] nums) {
        int n = nums.length;
        int[] ans = new int[2 * n];

        for (int i = 0; i < n; i++) {
            ans[i] = nums[i];
            ans[i + n] = nums[i];
        }

        return ans;
    }
}
```

---

# ⚙️ Complexity Analysis

### Time Complexity

```text
O(n)
```

The loop runs exactly `n` times, and each iteration performs constant-time operations.

Therefore:

```text
Time = O(n)
```

### Space Complexity

```text
O(n)
```

A new array of size `2n` is created to store the result.

The output itself requires `2n` space, so this is optimal for constructing the required result array.

---

# ✅ Approach Evaluation

This is a **correct and optimal approach** for the problem.

It is not a brute-force solution.

### Why?

The solution:

* Traverses the input array only once
* Places each element directly into its required positions
* Avoids unnecessary nested loops
* Does not perform unnecessary copying operations
* Uses the required output array efficiently

The time complexity is:

```text
O(n)
```

and the required result itself contains `2n` elements, making the `O(n)` output space necessary.

Therefore, this approach is both **efficient and straightforward**.

---

# 📌 Key Takeaways

* The result array must contain two copies of the input array.
* The result size is `2 * n`.
* The first copy is placed at index `i`.
* The second copy is placed at index `i + n`.
* A single loop is sufficient.
* The approach runs in `O(n)` time.
* The output requires `O(n)` space.

---

# 🔗 Problem Source

**Platform:** LeetCode

**Problem:** Concatenation of Array

**[View Problem on LeetCode →](https://leetcode.com/problems/concatenation-of-array/description/)**

---

**Part of the [Solved DSA Problems](https://github.com/Dharma718/Solved-DSA-Problems) repository.**
