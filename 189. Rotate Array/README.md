# Rotate Array (LeetCode 189)

## Problem Statement

Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.

### Example

**Input**
```text
nums = [1,2,3,4,5,6,7]
k = 3
```

**Output**
```text
[5,6,7,1,2,3,4]
```

---

# Why do we write `k = k % n`?

Before rotating the array, we calculate:

```cpp
k = k % n;
```

where:

- `k` = Number of rotations
- `n` = Size of the array

This ensures that we never perform unnecessary rotations.

### Why?

If an array has `n` elements, then rotating it exactly `n` times brings it back to its original position.

For example, if `n = 7`:

```text
0 rotations  → Original array
1 rotation   → Rotate once
2 rotations  → Rotate twice
3 rotations  → Rotate three times
4 rotations  → Rotate four times
5 rotations  → Rotate five times
6 rotations  → Rotate six times
7 rotations  → Original array again
8 rotations  → Same as 1 rotation
9 rotations  → Same as 2 rotations
10 rotations → Same as 3 rotations
```

So, instead of rotating 10 times, we only need to rotate:

```text
10 % 7 = 3
```

### Example 1

```text
nums = [1,2,3,4,5,6,7]
n = 7
k = 10
```

```cpp
k = k % n;
```

```text
k = 10 % 7 = 3
```

Instead of rotating **10** times, we rotate only **3** times.

```text
Before
1 2 3 4 5 6 7

After
5 6 7 1 2 3 4
```

### Example 2

```text
nums = [1,2,3,4,5]
n = 5
k = 5
```

```cpp
k = 5 % 5 = 0;
```

The array remains unchanged because one complete rotation cycle returns it to the original order.

```text
Before
1 2 3 4 5

After
1 2 3 4 5
```

> **Memory Tip:** Think of the array as a **clock**. After one full circle (`n` rotations), you're back at the starting position. The modulo operation (`k % n`) tells you how many extra rotations are actually needed.

---

# Approach: Reverse Algorithm

Instead of moving elements one by one, we use **three reverse operations**.

### Steps

1. Reverse the entire array.
2. Reverse the first `k` elements.
3. Reverse the remaining `n-k` elements.

---

# Dry Run

### Input

```text
nums = [1,2,3,4,5,6,7]
k = 3
```

---

## Step 1: Reverse the Entire Array

```text
Original

+---+---+---+---+---+---+---+
| 1 | 2 | 3 | 4 | 5 | 6 | 7 |
+---+---+---+---+---+---+---+

↓

+---+---+---+---+---+---+---+
| 7 | 6 | 5 | 4 | 3 | 2 | 1 |
+---+---+---+---+---+---+---+
```

Code:

```cpp
reverse(nums.begin(), nums.end());
```

---

## Step 2: Reverse the First `k` Elements

Since `k = 3`, reverse the first three elements.

```text
Before

+---+---+---+---+---+---+---+
| 7 | 6 | 5 | 4 | 3 | 2 | 1 |
+---+---+---+---+---+---+---+

↓

+---+---+---+---+---+---+---+
| 5 | 6 | 7 | 4 | 3 | 2 | 1 |
+---+---+---+---+---+---+---+
```

Code:

```cpp
reverse(nums.begin(), nums.begin() + k);
```

---

## Step 3: Reverse the Remaining Elements

Reverse the last `n-k` elements.

```text
Before

+---+---+---+---+---+---+---+
| 5 | 6 | 7 | 4 | 3 | 2 | 1 |
+---+---+---+---+---+---+---+

↓

+---+---+---+---+---+---+---+
| 5 | 6 | 7 | 1 | 2 | 3 | 4 |
+---+---+---+---+---+---+---+
```

Code:

```cpp
reverse(nums.begin() + k, nums.end());
```

---

# Why Does the Reverse Algorithm Work?

Split the array into two parts:

```text
A = [1,2,3,4]
B = [5,6,7]
```

Original array:

```text
A A A A | B B B
1 2 3 4 | 5 6 7
```

We want:

```text
B B B | A A A A
5 6 7 | 1 2 3 4
```

The reverse algorithm transforms the array as follows:

```text
Original

A B

↓

Reverse Entire Array

reverse(B) reverse(A)

↓

Reverse First k Elements

B reverse(A)

↓

Reverse Remaining Elements

B A
```

This gives the required rotated array.

---

# Algorithm

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();

        if (n == 0) return;

        k %= n;

        if (k == 0) return;

        reverse(nums.begin(), nums.end());
        reverse(nums.begin(), nums.begin() + k);
        reverse(nums.begin() + k, nums.end());
    }
};
```

---

# Complexity Analysis

| Operation | Complexity |
|-----------|------------|
| Reverse entire array | O(n) |
| Reverse first `k` elements | O(k) |
| Reverse remaining elements | O(n-k) |

### Time Complexity

```
O(n)
```

### Space Complexity

```
O(1)
```

The algorithm rotates the array **in-place** without using any extra array.

---

# Key Takeaways

- Normalize rotations using `k %= n`.
- One full rotation cycle returns the array to its original state.
- Reverse the entire array.
- Reverse the first `k` elements.
- Reverse the remaining elements.
- Achieves **O(n)** time complexity and **O(1)** extra space.

---

# Memory Tricks

### For `k %= n`

> Think of the array as a **clock**. After one complete circle, you are back where you started. `k % n` gives the remaining rotations.

### For the Reverse Algorithm

> **Reverse Everything → Reverse First `k` → Reverse Remaining**
