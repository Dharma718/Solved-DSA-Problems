# 🟨 Daily Temperatures

## 📌 Problem Statement

Given an array `temperatures` where `temperatures[i]` represents the temperature on the `i`-th day, return an array `res` where `res[i]` represents the number of days you have to wait after the `i`-th day to get a warmer temperature.

If there is no future day with a warmer temperature, `res[i]` should be `0`.

### Example

```text
Input:
temperatures = [73, 74, 75, 71, 69, 72, 76, 73]

Output:
[1, 1, 4, 2, 1, 1, 0, 0]
```

For example:

* `73` → warmer temperature `74` after `1` day
* `74` → warmer temperature `75` after `1` day
* `75` → warmer temperature `76` after `4` days
* `71` → warmer temperature `72` after `2` days
* `69` → warmer temperature `72` after `1` day
* `72` → warmer temperature `76` after `1` day
* `76` → no warmer future temperature → `0`
* `73` → no warmer future temperature → `0`

---

# 💡 My Approach

My approach uses a **Stack** to keep track of the indices of temperatures for which a warmer temperature has not yet been found.

The important idea is that the stack stores indices whose temperatures are waiting for a future warmer temperature.

When processing the current temperature:

```text
temperatures[i]
```

I compare it with the temperature at the index stored at the top of the stack:

```text
temperatures[stack.peek()]
```

If the current temperature is warmer:

```text
temperatures[i] > temperatures[stack.peek()]
```

then the current day is the first warmer day for the temperature represented by that stack index.

I remove that index from the stack and calculate the number of days waited:

```text
i - prev
```

The process continues while the current temperature is warmer than the temperature represented by the top stack index.

After resolving all possible previous temperatures, I push the current index into the stack because it may need a warmer temperature in the future.

---

# 🧠 Key Observation

The stack stores **indices**, not temperatures.

This is important because we need to calculate the number of days between the current day and the previous day:

```text
i - prev
```

where:

* `i` = current day
* `prev` = previous day waiting for a warmer temperature

The stack maintains indices whose warmer temperature has not yet been found.

---

# 🔍 Step-by-Step Explanation

First, store the length of the input array:

```java
int n = temperatures.length;
```

Then create the result array:

```java
int[] res = new int[n];
```

By default, every element of `res` is `0`.

This is useful because if a day never gets a warmer temperature, its answer should remain `0`.

Next, create a stack:

```java
Stack<Integer> stack = new Stack<>();
```

The stack stores the indices of temperatures that are waiting for a warmer temperature.

---

## 🔄 Processing Each Temperature

We iterate through the temperatures:

```java
for (int i = 0; i < n; i++)
```

For every current index `i`, check whether the current temperature is warmer than the temperature represented by the top index of the stack:

```java
while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()])
```

If it is warmer, remove that previous index:

```java
int prev = stack.pop();
```

Then calculate how many days it took to find the warmer temperature:

```java
res[prev] = i - prev;
```

After all possible previous temperatures have been resolved, push the current index:

```java
stack.push(i);
```

---

# 🧪 Dry Run

Consider:

```text
temperatures = [73, 74, 75, 71, 69, 72, 76, 73]
```

Initially:

```text
res   = [0, 0, 0, 0, 0, 0, 0, 0]
stack = []
```

### Iteration 1

```text
i = 0
temperature = 73
```

The stack is empty, so push index `0`.

```text
stack = [0]
```

---

### Iteration 2

```text
i = 1
temperature = 74
```

Compare:

```text
74 > 73
```

So index `0` has found its warmer day.

```text
prev = 0
res[0] = 1 - 0 = 1
```

Then push index `1`.

```text
res   = [1, 0, 0, 0, 0, 0, 0, 0]
stack = [1]
```

---

### Iteration 3

```text
i = 2
temperature = 75
```

Compare:

```text
75 > 74
```

So:

```text
prev = 1
res[1] = 2 - 1 = 1
```

Push index `2`.

```text
res   = [1, 1, 0, 0, 0, 0, 0, 0]
stack = [2]
```

---

### Iteration 4

```text
i = 3
temperature = 71
```

Compare:

```text
71 > 75 → false
```

Push index `3`.

```text
stack = [2, 3]
```

---

### Iteration 5

```text
i = 4
temperature = 69
```

Compare:

```text
69 > 71 → false
```

Push index `4`.

```text
stack = [2, 3, 4]
```

---

### Iteration 6

```text
i = 5
temperature = 72
```

Compare with index `4`:

```text
72 > 69
```

So:

```text
prev = 4
res[4] = 5 - 4 = 1
```

Now compare with index `3`:

```text
72 > 71
```

So:

```text
prev = 3
res[3] = 5 - 3 = 2
```

Now compare with index `2`:

```text
72 > 75 → false
```

Push index `5`.

```text
res   = [1, 1, 0, 2, 1, 0, 0, 0]
stack = [2, 5]
```

---

### Iteration 7

```text
i = 6
temperature = 76
```

Compare with index `5`:

```text
76 > 72
```

So:

```text
prev = 5
res[5] = 6 - 5 = 1
```

Compare with index `2`:

```text
76 > 75
```

So:

```text
prev = 2
res[2] = 6 - 2 = 4
```

The stack is now empty.

Push index `6`.

```text
res   = [1, 1, 4, 2, 1, 1, 0, 0]
stack = [6]
```

---

### Iteration 8

```text
i = 7
temperature = 73
```

Compare:

```text
73 > 76 → false
```

Push index `7`.

```text
stack = [6, 7]
```

The remaining indices in the stack do not have a future warmer temperature, so their result values remain `0`.

### Final Result

```text
[1, 1, 4, 2, 1, 1, 0, 0]
```

---

# 💻 Solution

```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        int[] res = new int[n];
        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i < n; i++) {
            while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
                int prev = stack.pop();
                res[prev] = i - prev;
            }

            stack.push(i);
        }

        return res;
    }
}
```

---

# ⚙️ Complexity Analysis

### Time Complexity

```text
O(n)
```

Although there is a `while` loop inside the `for` loop, every index is:

* Pushed into the stack at most once
* Popped from the stack at most once

Therefore, the total number of stack operations is linear with respect to `n`.

```text
Time = O(n)
```

### Space Complexity

```text
O(n)
```

The stack can contain up to `n` indices in the worst case.

The result array also contains `n` elements.

Therefore, the auxiliary stack requires:

```text
O(n)
```

space.

---

# ✅ Approach Evaluation

This is a **correct and optimal approach** for this problem.

The solution uses a **monotonic decreasing stack of indices**.

The important efficiency comes from the fact that each index is pushed once and popped at most once.

Therefore, even though the code contains a nested `while` loop, the overall time complexity remains:

```text
O(n)
```

This is significantly more efficient than checking every future day for every temperature, which would result in a quadratic approach.

---

# 📌 Key Takeaways

* The stack stores **indices**, not temperature values.
* The stack represents days that are still waiting for a warmer temperature.
* When a warmer temperature is found, previously waiting indices are resolved.
* `i - prev` gives the number of days between the current day and the previous day.
* Each index is pushed once.
* Each index is popped at most once.
* The overall time complexity is `O(n)`.
* The approach is based on a **monotonic decreasing stack**.

---

# 🔗 Problem Source

**Platform:** LeetCode

**Problem:** Daily Temperatures

[**View Problem on LeetCode →**](https://leetcode.com/problems/daily-temperatures/description/)

---

**Part of the [Solved DSA Problems](https://github.com/Dharma718/Solved-DSA-Problems) repository.**
