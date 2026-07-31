# Rearrange Array Elements by Sign (LeetCode 2149)

## Problem Statement

Given an array `nums` containing an **equal number of positive and negative integers**, rearrange the array such that:

- The first element is **positive**.
- Positive and negative numbers alternate.
- The **relative order** of positive and negative numbers remains the same.

---

## Example

### Input

```text
nums = [3,1,-2,-5,2,-4]
```

### Output

```text
[3,-2,1,-5,2,-4]
```

---

# Approach

Since the problem guarantees that:

- Number of positive elements = Number of negative elements

we can directly place

- Positive numbers at **even indices** (0,2,4,...)
- Negative numbers at **odd indices** (1,3,5,...)

No extra checking is required because both positive and negative indices will always remain within the array.

---

# Code

```cpp
class Solution {
public:
    vector<int> rearrangeArray(vector<int>& nums) {

        int n = nums.size();

        // Create answer array
        vector<int> ans(n,0);

        // Even index for positives
        int PositiveIndex = 0;

        // Odd index for negatives
        int NegativeIndex = 1;

        for(int i=0;i<n;i++){

            if(nums[i] < 0){

                ans[NegativeIndex] = nums[i];
                NegativeIndex += 2;

            }
            else{

                ans[PositiveIndex] = nums[i];
                PositiveIndex += 2;

            }
        }

        return ans;
    }
};
```

---

# Understanding the Idea

The answer array has two kinds of positions.

```
Index

0   1   2   3   4   5

P   N   P   N   P   N

Even Index  → Positive Number

Odd Index   → Negative Number
```

So whenever we find

- a positive number → put it at the next even index.
- a negative number → put it at the next odd index.

---

# Step 1

Input

```text
nums = [3,1,-2,-5,2,-4]
```

Create

```
ans = [0,0,0,0,0,0]
```

Initialize

```
PositiveIndex = 0

NegativeIndex = 1
```

---

# Step 2

Traverse the array

```
nums

+----+----+-----+-----+----+-----+
| 3  | 1  | -2  | -5  | 2  | -4  |
+----+----+-----+-----+----+-----+
```

---

## Iteration 1

Current Number

```
3
```

Positive

Store at

```
ans[0]
```

```
ans

+----+---+---+---+---+---+
| 3  | 0 | 0 | 0 | 0 | 0 |
+----+---+---+---+---+---+
```

Update

```
PositiveIndex = 2
```

---

## Iteration 2

Current Number

```
1
```

Positive

Store at

```
ans[2]
```

```
+----+---+----+---+---+---+
| 3  | 0 | 1  | 0 | 0 | 0 |
+----+---+----+---+---+---+
```

Update

```
PositiveIndex = 4
```

---

## Iteration 3

Current Number

```
-2
```

Negative

Store at

```
ans[1]
```

```
+----+-----+----+---+---+---+
| 3  | -2  | 1  | 0 | 0 | 0 |
+----+-----+----+---+---+---+
```

Update

```
NegativeIndex = 3
```

---

## Iteration 4

Current Number

```
-5
```

Store at

```
ans[3]
```

```
+----+-----+----+-----+---+---+
| 3  | -2  | 1  | -5  | 0 | 0 |
+----+-----+----+-----+---+---+
```

Update

```
NegativeIndex = 5
```

---

## Iteration 5

Current Number

```
2
```

Store at

```
ans[4]
```

```
+----+-----+----+-----+----+---+
| 3  | -2  | 1  | -5  | 2  | 0 |
+----+-----+----+-----+----+---+
```

Update

```
PositiveIndex = 6
```

---

## Iteration 6

Current Number

```
-4
```

Store at

```
ans[5]
```

```
+----+-----+----+-----+----+-----+
| 3  | -2  | 1  | -5  | 2  | -4  |
+----+-----+----+-----+----+-----+
```

Update

```
NegativeIndex = 7
```

---

# Final Output

```text
[3,-2,1,-5,2,-4]
```

---

# Dry Run

Input

```
3 1 -2 -5 2 -4
```

Initial

```
PositiveIndex = 0

NegativeIndex = 1
```

| Current Number | Position | Answer Array |
|---------------|----------|--------------|
| 3 | 0 | 3 _ _ _ _ _ |
| 1 | 2 | 3 _ 1 _ _ _ |
| -2 | 1 | 3 -2 1 _ _ _ |
| -5 | 3 | 3 -2 1 -5 _ _ |
| 2 | 4 | 3 -2 1 -5 2 _ |
| -4 | 5 | 3 -2 1 -5 2 -4 |

Final

```
3 -2 1 -5 2 -4
```

---

# Visualization

```
Original Array

3   1   -2   -5   2   -4
│   │     │    │    │    │
│   │     │    │    │    │
▼   ▼     ▼    ▼    ▼    ▼

Positive Indexes

0 → 2 → 4

Negative Indexes

1 → 3 → 5


Answer Array

+----+-----+----+-----+----+-----+
| 3  | -2  | 1  | -5  | 2  | -4  |
+----+-----+----+-----+----+-----+
```

---

# Flow Diagram

```
                Start
                   │
                   ▼
         Create Answer Array
                   │
                   ▼
     PositiveIndex = 0
     NegativeIndex = 1
                   │
                   ▼
          Traverse nums[]
                   │
          ┌────────┴────────┐
          │                 │
          ▼                 ▼
   Is nums[i] Positive?     No
          │                 │
         Yes                ▼
          │          Store at Odd Index
          ▼                 │
 Store at Even Index         │
          │                 │
          ▼                 ▼
 PositiveIndex +=2   NegativeIndex +=2
          │                 │
          └────────┬────────┘
                   ▼
          More Elements?
                   │
              Yes / No
                   │
                   ▼
             Return Answer
```

---

# Why Does This Work?

The problem guarantees:

- Equal number of positive and negative numbers.
- First element of the answer should be positive.

Therefore,

```
Even Index  → Positive

Odd Index   → Negative
```

Since positives and negatives are equal in count, we never run out of even or odd positions, and the indices always stay within bounds.

---

# Complexity Analysis

| Operation | Complexity |
|-----------|------------|
| Traverse Array | **O(N)** |
| Fill Answer Array | **O(N)** |
| Overall Time | **O(N)** |
| Extra Space | **O(N)** |

---

# Key Points

- ✅ Preserves the order of positive numbers.
- ✅ Preserves the order of negative numbers.
- ✅ Very simple implementation.
- ✅ No nested loops.
- ✅ Time Complexity: **O(N)**.
- ✅ Space Complexity: **O(N)**.
- ✅ Works because the number of positive and negative elements is guaranteed to be equal.
