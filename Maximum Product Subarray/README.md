# Maximum Product Subarray (Kadane's Variant)

## Problem Statement

Given an array of integers `arr[]`, find the **maximum product** of any contiguous subarray.

> A subarray is a contiguous part of the array.

---

## Example

### Input

```cpp
arr = {2, 3, -2, 4}
```

### Output

```cpp
6
```

### Explanation

The subarray

```text
[2, 3]
```

has the maximum product.

```
2 × 3 = 6
```

---

## Another Example

### Input

```cpp
arr = {-2, 3, -4}
```

### Output

```cpp
24
```

### Explanation

```text
(-2) × 3 × (-4)
= 24
```

---

# Optimized Solution (O(n))

```cpp
class Solution {
public:
    int maxProduct(vector<int> &arr) {

        int result = arr[0];
        int maxProduct = arr[0];
        int minProduct = arr[0];

        for (int i = 1; i < arr.size(); i++) {

            int current = arr[i];

            if (current < 0)
                swap(maxProduct, minProduct);

            maxProduct = max(current, maxProduct * current);
            minProduct = min(current, minProduct * current);

            result = max(result, maxProduct);
        }

        return result;
    }
};
```

---

# Intuition

Unlike the **Maximum Sum Subarray (Kadane's Algorithm)**, this problem involves multiplication.

A negative number can completely change the answer.

For example,

```text
-2 × -3 = 6
```

Two negatives become positive.

So while traversing the array, we keep track of:

- Maximum product ending at current index
- Minimum product ending at current index

Why minimum?

Because a negative minimum can become the next maximum after multiplying with another negative.

---

# Why Do We Need Both Maximum and Minimum?

Consider

```text
[-2, 3, -4]
```

---

Initially

```text
Maximum Product = -2
Minimum Product = -2
```

Next number

```text
3
```

Maximum becomes

```text
3
```

Minimum becomes

```text
-6
```

Now next number is

```text
-4
```

Current minimum is

```text
-6
```

Multiplying

```text
-6 × -4 = 24
```

The smallest product suddenly becomes the largest product.

That's why we always maintain both values.

---

# Why Swap?

Whenever the current number is negative,

```cpp
swap(maxProduct, minProduct);
```

Because

```text
Positive × Negative = Negative

Negative × Negative = Positive
```

So,

the previous maximum may become the new minimum,

and

the previous minimum may become the new maximum.

---

## Diagram

Suppose

```text
Current Maximum = 12
Current Minimum = -8
Current Number = -2
```

Before multiplication

```text
Maximum → 12
Minimum → -8
```

Multiply by **-2**

```text
12 × -2 = -24

-8 × -2 = 16
```

Notice

```text
Maximum becomes Minimum

Minimum becomes Maximum
```

Hence

```cpp
swap(maxProduct, minProduct);
```

---

# Dry Run

Input

```cpp
arr = {2, 3, -2, 4}
```

---

## Initial State

```text
result = 2

maxProduct = 2

minProduct = 2
```

---

## Step 1

Current = 3

No swap needed.

```
maxProduct = max(3, 2×3)
           = 6

minProduct = min(3, 2×3)
           = 3

result = max(2,6)
       = 6
```

Current State

```text
maxProduct = 6

minProduct = 3

result = 6
```

---

## Step 2

Current = -2

Negative number

Swap

```text
Before Swap

max = 6

min = 3
```

```text
After Swap

max = 3

min = 6
```

Now calculate

```
maxProduct = max(-2, 3×-2)
           = -2

minProduct = min(-2, 6×-2)
           = -12

result = max(6,-2)
       = 6
```

Current State

```text
maxProduct = -2

minProduct = -12

result = 6
```

---

## Step 3

Current = 4

```
maxProduct = max(4,-2×4)
           = 4

minProduct = min(4,-12×4)
           = -48

result = max(6,4)
       = 6
```

Final Answer

```text
6
```

---

# Another Dry Run

Input

```cpp
arr = {-2,3,-4}
```

---

Initial

```text
max = -2

min = -2

result = -2
```

---

Current = 3

```
max = 3

min = -6

result = 3
```

---

Current = -4

Negative number

Swap

```text
Before

max = 3

min = -6
```

```text
After

max = -6

min = 3
```

Now calculate

```
max = max(-4,-6×-4)
    = 24

min = min(-4,3×-4)
    = -12

result = 24
```

Final Answer

```text
24
```

---

# Visualization

```text
Current Number

          │
          ▼

Is Negative?

      │
 ┌────┴────┐
 │         │
Yes        No
 │          │
Swap        Continue
Max & Min
 │
 ▼

Update Maximum Product

maxProduct =
max(current,
current × maxProduct)

 │
 ▼

Update Minimum Product

minProduct =
min(current,
current × minProduct)

 │
 ▼

Update Answer

result =
max(result,
maxProduct)
```

---

# Complexity Analysis

### Time Complexity

```
O(n)
```

We traverse the array only once.

---

### Space Complexity

```
O(1)
```

Only three variables are used.

---

# Key Takeaways

- Keep track of **maximum** and **minimum** product ending at each index.
- A negative number can turn the smallest product into the largest product.
- Swap the maximum and minimum whenever the current element is negative.
- Update the answer after processing each element.
- This optimized approach solves the problem in **O(n)** time and **O(1)** space.
